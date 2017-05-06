---
layout: post
title:  "Github pages は独自のプラグインをサポートしていない"
date:   2017-05-06 16:07:28 +0900
tags:   Jekyll blog
categories: GithubPages Jekyll blog
published: true
---

ひさびさにブログのデザインを変更しました。

今度は一から手作りで SASS なんかも初めて触ってみたりしつつ気合を入れてゴールデンウィークの一日を使って作りました。  
...が、色々とハマったとこなんかもあったのでメモ。

---

### Youtube のプラグインを試す

Youtube の動画を埋め込んだときにウインドウの幅によって縦横の比率が変わってしまう問題があって、その問題を解決するプラグインを見つけました。

[jekyll-youtube](https://github.com/dommmel/jekyll-youtube)

で、これを入れようと思って色々試行錯誤をしてしみたけれど、うまくいかない・・・

ローカルではうまく動くけれど Github にプッシュした時にビルドに失敗している模様。ビルドに失敗したと Github からはこんなメールが届いた。

> The page build failed for the `master` branch with the following error:
> 
> The tag `youtube` on line 1 in `_posts/2011-09-07-test-post-of-youtube.md` is not a recognized Liquid tag. For more information, see https://help.github.com/articles/page-build-failed-unknown-tag-error/.
> 
> For information on troubleshooting Jekyll see:
> 
>   https://help.github.com/articles/troubleshooting-jekyll-builds
> 
> If you have any questions you can contact us by replying to this email.

### Github Pages は独自のプラグインをサポートしていない

Github Pages は以下のページのプラグインはサポートしているけれど

[Dependency versions | GitHub Pages](https://pages.github.com/versions/)

これら以外の独自のプラグインをサポートしていないとのこと。  
詳しくはこちらのページに書いてありました。

[Adding Jekyll plugins to a GitHub Pages site - User Documentation](https://help.github.com/articles/adding-jekyll-plugins-to-a-github-pages-site/)

### ではどうするか

ではどうするかって話ですが、選択肢は２つのようです。

1. あきらめる
2. ローカルでビルドしてそれをデプロイする

今回はすっぱり諦めました。  
個人的には Jekyll でブログは楽ちんなのが一番のポイントなので、めんどくさいことは今回はパスすることにしました。が、気が向いたらトライするかも。

