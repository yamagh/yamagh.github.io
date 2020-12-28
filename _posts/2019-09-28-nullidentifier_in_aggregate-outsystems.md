---
layout:     post
title:      "Aggregate で NullIdentifier() を使うときの注意点"
date:       2019-09-28 22:56:47 +0900
tags:       OutSystems11
categories: OutSystems
published:  true
---

OutSystems の Aggregate の Filters に条件式を書くとき、同一の評価結果となるべき条件式を If の中に書くか、外に書くかで実行結果が変わる、という問題に遭遇したのでメモ。

## tl;dr

- Aggregate の中で NullIdentifier() = 0 と思って使わない。
- NullIdentifier() と比較する時、データ型が本当に Identifier 型であることをよく確認する。

## 問題の事象

まずは、Aggregate の２つの実行結果をご覧ください。  

１つ目  
![img](https://lh3.googleusercontent.com/lQLRgKD7nq52mkKoCqNjSaLh-ET6hmB3GgJCC3GENPX8WO0bxXN3FwxuuhnkiO9YoY8yf5KI5e8K3_FQ38HqWQKVe6QE2QLseKu15joPVxrIj7lRpWhqlCGHeyhNwEX_RkcrTG2XH-o=w559-h294-no)

２つ目  
![img](https://lh3.googleusercontent.com/4K6AC9y5WPDaEssYHdGa5Za4D77JdpBRzUK2aGIp7qMU8Im4FSYTv9swpHdJbElV25F-5dQtedHYHwV1y8viSoLKiKZ9koJzCyVAPRta8gg3xAsL0V7n9rg4pwedja2WmZe7xOYbVmc=w559-h294-no)

どちらも `UserId = NullIdentifier()` が評価されるため、同じ実行結果となる事を期待しますが、そうはなっていません。１つ目の実行結果は２件のレコードが返ってきていますが、２つ目は０件です。この２つの実装の違いは評価式が If の外にあるか中にあるか、のみです。  

ちなみに UserId は LongInteger で値は変数の初期値のままです（つまり `0` です）。  
[OutSystems の NullIdentifier() Function のドキュメント](https://success.outsystems.com/Documentation/11/Reference/OutSystems_Language/Logic/Built-in_Functions/Data_Conversion#NullIdentifier)を見ると、 `NullIdentifier() = 0` と記載があることから、`UserId = NullIdentifier()` は `0 = 0` で true となるべきのため、レコードが返ってこない２つ目の結果は期待する動作と異なることになります。

## 原因と考察

### ポイント１: 条件式を If の中に書くか外に書くか

問題の事象が起きた時の SQL を比べてみると次のようになっていました。

<script src="https://gist.github.com/yamagh/cc365d508ed9dc4b37265ae69bf242d7.js"></script>

If の外に評価式を書いた場合は、その評価式が SQL に含まれていない事がわかります。  

なぜ SQL に含まれていないかというと、恐らくこれは OutSystems による SQL の最適化によるものです。`UserId = NullIdentifier()` の UserId は単なる変数なので DBMS へ SQL を投げずとも事前に評価可能なため、評価して結果が true であれば SQL に含めないという事だろうと思います。  

実際、評価式を `UserId <> NullIdentifier()` として必ず false となるようにして実行してみると、問題の事象の１つ目の画像にはなかった WHERE 句の条件が、次のように追加されました。

```sql
SELECT TOP (32) ENFoo.[ID] o0, ENFoo.[USERID] o1, ENFoo.[BAR] o2, ENFoo.[DATE] o3, ENFoo.[TIME] o4, ENFoo.[LONGINT] o5
FROM [JJUEOP012].DBO.[OSUSR_BYG_FOO] ENFoo
WHERE (@UserId IS NOT NULL)
```

まとめるとこのような感じです。

| If の | 事前の評価結果 | SQL          |
|:------|:---------------|:-------------|
| 外    | true           | 出力されない |
| 外    | false          | 出力される   |
| 中    | true           | 出力される   |
| 中    | false          | 出力される   |

ここで重要な点は、事前に評価可能な条件式の場合、If の中に書く時と外に書く時で実行される SQL が変わるという事です。

---

## 追記

ここまで書いてから次の条件式で実行してみました。If を使っておらず、DBMS へ SQL を発行する前に評価可能なため、WHERE句には何も出力されないことを想像しましたが、実際は異なっていました。

```sql
UserId = NullIdentifier() and 1=1
```

実行結果  
![img](https://lh3.googleusercontent.com/AQQd2ldpiGsi66i16RUF8GGSGjln4HfqF_KY2-9PN7spX8qVm579U8pcPrjJ21yefFR5zR2Kn4rBFq9v1UsqzNZgGeY62_ZrflCmzbXc4QeHFvRwPTGPrLKsHBmtcw0TFIskF69fgok=w800-h335-no)

WHERE句に次のように出力されていますね...  

```sql
WHERE ((@UserId = 0)
  AND (1 = 1))
```

ということなので、If の中/外に限らず、SQL が変わる場合があるとだけ頭の隅おいておけば良いと思います。

### ポイント２: Aggregate の中の NullIdentifier()

[OutSystems の NullIdentifier() Function のドキュメント](https://success.outsystems.com/Documentation/11/Reference/OutSystems_Language/Logic/Built-in_Functions/Data_Conversion#NullIdentifier) を見ると `NullIdentifier() = 0` ですが、いつ何時でもそうとは限らないようです。  

上で `UserId <> NullIdentifier()` とした時の SQL が次のようになっていましたが、

```sql
WHERE (@UserId IS NOT NULL)
```

UserId の変数の型を LongInteger から User Identifier 型に変更すると次のように変わります。

```sql
WHERE (@UserId <> 0)
```

この SQL はまさしく期待する SQL のため、同じデータ型同士で比較するべきだ、という結論が頭をよりぎますが、問題点はそこではありません。  

Aggregate の中で NullIdentifier() を使うと、比較するデータ型に応じて `NULL` として扱われたり、`0` として扱われたりと一貫性がない事です。ポイント１で挙げたように DBMS に SQL を発行する前は true と評価されていたものが DBMS 側では False と評価されていることが、今回の問題事象の原因です。Aggregate 以外で使う場合、NullIdentifier() は一貫して 0 として扱われるため、Aggregate の場合だけ動作が異なるように見えます。  

そのため、数値型と比較する場合は次のように 0 を Null として扱かってもいいように思います。

```sql
WHERE (@UserId IS NOT NULL or @UserId <> 0)
```

実際のところ、外部データベースを使わず、OutSystems のデフォルトのデータベースに Create/Update するだけならば、[Null 値が入ることはないため](https://success.outsystems.com/Documentation/11/Reference/OutSystems_Language/Data/Database_Reference/Default_Values_on_Database)、こちらの方が自然な動作のようにも感じます。  

とはいえ開発者としては、この動作を変えることはできないため、受け入れて、Aggregate の中では NullIdentifier は 0 になったり NULL になったりする場合がある、と覚えておいたほうが良いでしょう。

## 対処方法・まとめ

1. ポイント１で確認したように、Filters に書いた条件式がどこで（OutSystems 側／DBMS側のどちらか）で実行されているかは、時と場合によるため、うまく動かない時は Executed SQL をみて、意図した通りの SQL になっているか確認するのがベター。
2. Aggregate の中で NullIdentifier() = 0 と思って使わない。
3. NullIdentifier() と比較する時、データ型が本当に Identifier 型であることをよく確認する。
