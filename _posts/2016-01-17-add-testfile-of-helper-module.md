---
layout: post
title:  "Helper モジュールのテスト追加"
date:   2016-01-17 13:03:40 +0900
tags:   rails test
categories:
---

`rails generate` でなぜかテストファイルが作られなかったので、手で追加する場合のメモ。

```bash
$ rails generate helper hoge
Running via Spring preloader in process 4787
      create  app/helpers/hoge_helper.rb
      invoke  test_unit
```
↑`test/helpers/hoge_helpers_test.rb` を作って欲しいが作ってくれない...

次のようなファイル (`test/helpers/hoge_helpers_test.rb`) を作ればOK  

```ruby
require 'test_helper'

class HogeHelperTest < ActionView::TestCase
  test "should work" do
    assert_equal "result", your_helper_method
  end
end
```

`app/helpers/hoge_helper.rb` と  
`test/helpers/hoge_helpers_test.rb` と  
`class HogeHelperTest` の名前は揃えること！

