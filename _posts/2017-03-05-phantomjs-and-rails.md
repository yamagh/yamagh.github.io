---
layout: post
title:  "Heroku と Rails と PhantomJS"
date:   2017-03-05 22:12:09 +0900
tags:   heroku rails phantomjs
categories:
---

Heroku で PhantomJs を使おうとしたら次のエラーが発生したので対処方法をメモ。

    Cliver::Dependency::NotFound (Could not find an executable ["phantomjs"] on your path.):   

次のコマンドで解決した。

    heroku buildpacks:add --index 1 https://github.com/stomita/heroku-buildpack-phantomjs

参考URL
- [Heroku, Ruby on Rails and PhantomJS](https://gist.github.com/edelpero/9257311)
- [HerokuでRuby on RailsとPhantomJSの両方を使う方法 - gaharaプロデューサーの学習ラボ](http://engineer.gahara.me/entry/heroku-ruby-phantomjs)

