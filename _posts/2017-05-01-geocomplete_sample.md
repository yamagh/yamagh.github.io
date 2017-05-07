---
layout: post
title:  "[js] Geocomplete を使ってみた"
date:   2017-05-01 09:11:27 +0900
tags:   geocomplete js GoogleMap rails
categories:
---

[Geocomplete](http://ubilabs.github.io/geocomplete/) という jQuery プラグインを使ってみたので、その使い方を色々メモ。  

## 動作イメージ

このプラグインの動作イメージはこんな感じ。  
テキストボックスに住所とか名称を入力すると候補が表示されて、候補を選択すると座標とか電話番号とかがフォームに自動で設定できる。

[http://ubilabs.github.io/geocomplete/examples/form.html](http://ubilabs.github.io/geocomplete/examples/form.html)
![img](https://lh3.googleusercontent.com/f61dJ3Jw8UvZDIGSCQ2EIZkn3c9wCCdgkvXGflN6FRaV9ZzbAs8CSMcN10AaSZnLcc511H9iz7cUm9khOnq3HAX7N50sRUTc6h4U5y53GOqAiIFkmI912bi-e8utww6guU5llctTi3n-wND1qmGZyqEql_ZJwR6RY1oTc9K4eERp8WSBc3zDx5KUC4gcr1pllTEKxxpucvciLYo0DuXxBsdk5HaUn5jtuKn55m6UG93e1IwNAHwmH7wuyBgPzLhxNmCMclR5nCBegKOD_LwILra-FK8hX8hysjsH2HUvfKs6lqLNe6Gtqfub4SjkCt2kd_z8qFi8J_yvYckqvHC4Ve1FmvDvR2mONPRTtFKhY-HjPA4R2z1xcMbeJelT9MmyKCpf9U4nETg2n68ryQ9t4h8YdZmQbvXzbOk2yVGEQuXQsZYPUTZ_fQmEsM1sZ3lFFXlNE3ZsKF5BAIGOphe7vSrU_d6m9uLP5uAWhT_7epk_SGlXLlaHFSwiqVVieeVMzyCRf_D_o0nWjPVmh16jXILJe0_BBBCP4H7h3mzIZNcDr92Pzvy2ZAgXS3qoCrHlMmNAH178Qf4w3Cwh8FS10S0C8VV45ey_ySKCJS0mepJ4ygUqiK3crMUxL2zdGH7JpeYsD8dkcRI1jJEH-fdmKGnnCobIl-FNzVOTxhFaaF8=w996-h824-no) 

## Geocomplete の機能

- Google Maps API のジオコーディングサービスを使える  
  (ジオコーディングとは、住所（たとえば「東京都港区六本木 6-10-1」）を地理的座標（たとえば、緯度 35.6604282、経度 139.7269877）に変換すること)
- Google Places のオートコンプリートを使える

## Rails で使ってみる

このプラグインを Rails アプリで使ったときの手順とかをメモ。

大まかな手順はこんな感じ。HTML の記述部分は [Slim](http://slim-lang.com/) で書いてます。

1. `Google Places API Web Service` で `API_KEY` を取得する
2. Gemfile に追記して bundle install

    ```ruby
    gem 'geocomplete_rails'
    ```

3. application.js に追記

    ```js
    //= require geocomplete
    ```

4. application.slim に次の記述をを追加する (`API_KEY` には手順1で取得した `API_KEY` を設定する)

    ```slim
    javascript_include_tag "http://maps.googleapis.com/maps/api/js?key=`API_KEY`&libraries=places"
    ```

5. オートコンプリートを行わせたいテキストボックスに `geocomplete` という id を付ける  
   (id は何でも良いがとりあえずコレにして以降の手順を書く)

    ```slim
    = search_field :find, :query, {id: 'geocomplete'}
    ```

6. オートコンプリートで候補を選択した時にマップを表示させる要素として `.map_canvas` を用意する
7. オートコンプリートで候補を選択した時に名前とか座標の値を設定したい要素に `'data-geo' => 'name'` といった属性を付ける  

    ```slim
    = f.text_field :name, {'data-geo' => 'name'}
    ```

   `name` 以外にも以下の項目等があるが詳細は [Google Maps JavaScript API](https://developers.google.com/maps/documentation/javascript/places#place_details_responses) の `プレイス詳細の結果` を参照

   - `name` : プレイスの名前
   - `address_components` : プレイスの場所の住所コンポーネントの集合
   - `formatted_address` : プレイスの完全アドレス
   - `rating` : ユーザーの口コミ集計に基づくプレイスの評価 (0.0~5.0)
   - `street_address`
   - `route`
   - `intersection`
   - `political`
   - `country`
   - `administrative_area_level_1`
   - `administrative_area_level_2`
   - `administrative_area_level_3`
   - `colloquial_area`
   - `locality`
   - `sublocality`
   - `neighborhood`
   - `premise`
   - `subpremise`
   - `postal_code`
   - `natural_feature`
   - `airport`
   - `park`
   - `point_of_interest`
   - `post_box`
   - `street_number`
   - `floor`
   - `room`
   - `lat`
   - `lng`
   - `viewport`
   - `location`
   - `formatted_address`
   - `location_type`
   - `bounds`

8. jQuery でオートコンプリートが動くように設定する  
   オートコンプリートを動かす画面の coffee スクリプトにこんな感じに記述

    ```coffee
    $(document).on 'turbolinks:load', ->
      $("#geocomplete").geocomplete {        # 手順5 で指定したテキストボックスでオートコンプリートが動くように設定
        map: ".map_canvas"                   # 手順6 で用意した要素と紐付け
        details: "form"                      # オートコンプリートの結果を入れる親要素を指定
        detailsAttribute: "data-geo"         # 手順7 で使用した属性の指定
        types: ["geocode", "establishment"]  # Google から返ってくるオートコンプリート候補の種類の指定
        location: [35.710067, 139.8085117]   # `map` にデフォルトで表示する座標
      }
    ```

## 細かい手順

以上の手順を踏まえた詳細な手順を書こうと思ったけど、めんどくさくなったので終了。  
気が向いたらキチンと書いて Qiita とかに投稿するかも。

## まとめ

Google Places の情報が割と簡単に使えて便利。  
API_KEY の取得とか coffee スクリプトの書き方とかそんなところで時間を使ってしまったけど、慣れたサクッと使えそうなので積極的に使っていきたい。

