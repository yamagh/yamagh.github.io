---
layout: post
title:  "[Ruby] 基数変換"
date:   2016-08-11 18:27:34 +0900
tags:   ruby
categories:
---

基数変換をしようとするといつも忘れてしまっているのでメモ。

```ruby
# 10進数 から 2進数
p 80.to_s(2)  #=> "1010000"
p "%b" % 80   #=> "1010000"

# 2進数 から 10進数
p "1010000".to_i(2)  #=> 80
p "%d" % 0b1010000   #=> "80"
```

