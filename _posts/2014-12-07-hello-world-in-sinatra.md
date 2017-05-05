---
layout: post
title:  "Sinatra で Hello World"
date:   2014-12-07 11:33:24 +0900
tags:   Ruby Sinatra
categories:
---

こんな感じでものすごく簡単に動かせた。

<script src="https://gist.github.com/yamagh/1b5db81204ec41fb9794.js"></script>

これを実行するとWebサーバーが起動。

```
$ ruby lib/hello.rb
➜  sandbox  ruby lib/hello.rb 
[2014-12-07 11:20:55] INFO  WEBrick 1.3.1
[2014-12-07 11:20:55] INFO  ruby 2.0.0 (2014-05-08) [universal.x86_64-darwin14]
== Sinatra/1.4.5 has taken the stage on 4567 for development with backup from WEBrick
[2014-12-07 11:20:55] INFO  WEBrick::HTTPServer#start: pid=25693 port=4567
```

![image](https://lh3.googleusercontent.com/aIbYXI1T9Dr3Ip6pu8_yIR_LJo0h8ysc9u2QbvuHE0YJ7ZTL2EcMjlSXYH2KhAIYUyUGoY9NNMTCjULRQEZTa3U5kTbeLjDRcD-z5gF2SGB5AFKDZpA5OFOojRdv0wZsQmewL4Sn5XfEBAR4pY9I6mckKb943EhyV0EO6frQpKOL3vPHZd7zOEyqdvTBhSOsEhls8xMqCuXUtYOfXNSIh0qC_TUFnQEr7pyQXrVS567Mj89GIJuYv7gmO7kaVXo1CvWjR_f7I2Qe9-utLM6CQnjHNGORYc3_n7uDeAD7LSS0KAxKCwTwIAAAtXuxNjlnY_8kLKH10C5W-rX-eUJuOopb0RVWvd2PM1_OCSM5b2LeQPlGvQrEpWsue4OPybqZHt9_-aDUEqhb0kU658QvHavz_b8W5MF36ll1A_CCNKc5229W8bQ9MvHoWmxSL9eGbboRBHgd6It75lyUlKT3soQNFqcM9ZMfTtVjB6buZBpFLgj7NjSOAJyWvgtt_GDIJv3Z-1qcQq9X0LWysYWZMCgC-QmN8mFWwDosXRq2whMzSPRUCHjE59GygvSHRPXlldDehg=w504-h234-no)

手軽さがApacheとは大違いですね。  
もちろん性能も大違いだとは思いますが。  
何かサクッと作りたいときに便利そうな感じ。

公式サイトはこちら  
[Sinatra: README (Japanese)](http://www.sinatrarb.com/intro-ja.html)

