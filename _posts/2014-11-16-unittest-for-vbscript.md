---
layout: post
title:  "VBS で UnitTest"
date:   2014-11-16 21:11:00 +0900
tags:   VBScript
categories:
---

![image](https://lh3.googleusercontent.com/Dc89QhYRyaFQ5G1cO-zH9W4nalN-RyrOwyUTCH60uYYYNLco0IpI_RW3kC4-s_O7vAhFSrOneDrCvR-ToKcdNdbkRR4HwdDx4o0FtTScaGcaKP599Potibea0nLBuImrdf66Vdy8bFrFT4nMMAXiOyccXbUQHkVQj29aO81sM3bDBN9qNlG8rAGg2tNe2qDBiRr8gl2lH30PCHknxCuI_XLlDXXtKtnpwNt0lnSSlzdlpG3-YmbtXzUo74Jp2nSUyUm-Gf7195cE9R62oBBKatd7niST0Vv3klPdERm8R-FuReaKQkbzuRyqkZfQVDBhuSZjxTyiDtnfBNI8fbuX43RunkbXYDNt0GECTI0iW9smJZSDGw7a4htGs7vSikUUgfU9ADkIJF3TuOZvGFk5moxAmain1aarcSOpUzwoMlPYlIoPWi_V2oxDdExEr0Cugq_pt3nTFiyPHMyBvXPm2x_fUzQcISubj1v3TDqKKkt2CM8nwyrnZh-hE34bnLfN2nrfD38rPOa4U_Wp19FJ0X2a04iHrQjFph6dSR_0E0DNdghW5iBZF5thYdcTZZG7F496nQ=w751-h501-no)

VBScritpを最近好きでよく書いてます。
テストはあまり好きじゃないのでおざなりにやってたら、思いがけないようなバグが出たりとかもしばしば。
もうちょっとテストを効率的にやりたいなぁなどと思い UnitTest が出来ないか検討。

どうせ無いだろうなぁと思ってたら意外にも発見。

１つ目は [ScriptUnit](http://xt1.org/scriptunit)。GUIのツールが付いてて、テストコードも書きやすそうな雰囲気。

 
２つ目は [VBSTester](http://vbstester.jp.brothersoft.com/)。VBScript製でテスト結果はメールで自分に送る使い方を想定しているみたい。あまりきちんと見てないけどテストコードが書きにくそうな雰囲気。

３つ目は [こちらのブログ](http://d.hatena.ne.jp/y10k/20090307) で作者の方が自作したと思われるVBScript製のツール。自作したライブラリと一緒に [公開](https://code.google.com/p/vbslib/) されていました。

グッと来たのは３つ目。
シンプルですがよく考えて作られているのが伝わってきます。
自分の使い方にも合ってそうなのでしばらく使ってみるつもりです。

