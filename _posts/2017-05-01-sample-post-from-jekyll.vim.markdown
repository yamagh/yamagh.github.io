---
layout: post
title: "sample-post-from-jekyll.vim"
date:   2017-05-01 14:21:47 +0900
categories: [foo]
published: true
---

vim から簡単にブログのポストが書けないかなぁ・・・と思って探してたら [jekyll.vim](https://github.com/csexton/jekyll.vim) というプラグインを発見。  
合わせて [tpope/vim-fugitive](https://github.com/tpope/vim-fugitive) という git のラッパープラグインも入れれば

1. `:JekyllPost` で記事の雛形を作成
2. `:Gwrite` で `git add` して
3. `:Gcommit` で `git commit`
4. `:Git push` で Github にコミット

という4ステップでブログが書けてめちゃくちゃ楽ちん。こりゃいいわ。

