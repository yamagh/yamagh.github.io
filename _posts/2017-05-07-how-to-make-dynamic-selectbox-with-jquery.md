---
layout:     post
title:      "jQuery を使った動的なセレクトボックスの作り方"
date:       2017-05-07 20:44:29 +0900
tags:       rails jquery
categories: 
published:  false
---

動的にアイテムが変わるセレクトボックスの作り方が分からず色々しらべたのでやり方をメモ。

---

## やりたいこと


## やりかた


## やりかたを詳しく

  1. サンプルアプリを作る

    rails new sample --skip-bundle

  2. モデルを２つ作る (カテゴリーとサブカテゴリーというモデル)

    bin/rails g scaffold Category name 
    bin/rails g scaffold SubCategory name 

  3. 初期データを用意する


  4. データベースを初期化する

## 感想

Gem とかでもっとサクッと出来たらいいのに。

