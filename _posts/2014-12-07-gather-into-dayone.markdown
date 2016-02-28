---
layout: post
title:  "いろんなWebサービスのアクティビティをDayOneにまとめる"
date:   2014-12-07 20:06:27 +0900
categories: DayOne Twitter Pocket Last.fm
---
前回のエントリに引き続き設定をしてみる。

まずこちらのGihubのリポジトリからファイルを入手。

[ttscoff/Slogger: Social logging script for Day One](https://github.com/ttscoff/Slogger:embed)

入手したファイルの直下に移動して次のコマンドを実行。 

```
$ sudo gem install bundler
$ bundle install 
```

gemのインストールが一通り終わったら次は、 `Plugins` と `Plugins_disabled` というディレクトリがあるので、使いたいプラグインを `Plugins` へ、使いたくないプラグインは `Plugins_disabled` に移す。プラグインのOn/Offはこのディレクトリに入っているか/いないかで切り替わるみたい。

続いて、設定ファイルを生成。

```
$ ./slogger --update-config
```

これを実行すると `slogger_config` というファイルが作られるので、中を開いてユーザー名やパスワードなどを設定する。  
終わったら `./slogger` を実行。

```
.$ /slogger
```

Twitterを使う場合とかは認証画面が表示されるので画面の注意書きに従って認証する。
終わったあとDayOneを開いてみると...  
おお、Last.fmとPocketとTwitterから日記が作られてる。

<p><span itemscope itemtype="http://schema.org/Photograph"><img src="http://cdn-ak.f.st-hatena.com/images/fotolife/y/yamagh/20141207/20141207195314.png" alt="f:id:yamagh:20141207195314p:plain" title="f:id:yamagh:20141207195314p:plain" class="hatena-fotolife" itemprop="image"></span></p>

なかなかステキです。  
あとは毎日自動で実行すれば完璧！

