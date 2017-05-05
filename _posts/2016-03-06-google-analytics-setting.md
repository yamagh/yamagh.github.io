---
layout: post
title:  "Jekyll で Google Analytics の設定"
date:   2016-03-06 17:16:12 +0900
tags:   Jekyll GoogleAnalytics
categories:
---
はてブから Jekyll にお引越しをしてみたらなんと５年間で３０記事くらいしか書いて
なくてあまりの少なさにもっと書かなきゃなぁと反省中。  

引越しも大体終わったので、Google Analytics の設定をしてみた。
途中思ったように設定ができなかったのでメモ。

[Blog Configuration - ruhoh universal static blog generator](http://jekyllbootstrap.com/usage/blog-configuration.html)

このページによると `./_config.yml` に次のように書くらしい。

```ruby
# Settings for analytics helper
# Set 'provider' to the analytics provider you want to use.
# Set 'provider' to false to turn analytics off globally.
#        
analytics :
  provider : google
  google : 
      tracking_id : 'UA-123-12'
  getclicky :
    site_id :
```

で実際に同じように書いてみたけれどうまくいかず。

どうするのが正しいのかとググってみたら次のページに参考になる方法が書いてた。

[How I Created a Beautiful and Minimal Blog Using Jekyll, Github Pages, and poole · Joshua Lande](http://joshualande.com/jekyll-github-pages-poole/)

１. `./_includes/google_analytics.html` を作成

```html
<script>
  (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
    (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
    m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
    })(window,document,'script','//www.google-analytics.com/analytics.js','ga');

  ga('create', 'UA-51327309-5', 'auto');
    ga('send', 'pageview');

</script>
```

２. `./_layouts/default.html` で `./_includes/google_analytics.html` を読み込む

```html
    {％ include google_analytics.html ％}
```

とりあえず設定できたのでよしとする。

