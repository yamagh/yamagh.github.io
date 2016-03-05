---
layout: post
title:  "undefined method `describe' for main:Object (NoMethodError)`"
date:   2014-12-07 00:53:25 +0900
categories: Ruby, RSpec
---

RSpecを始めてみようと思って[ここ](http://qiita.com/yusabana/items/db44b81bdddf6ed0e9f5)の記事を参考にサンプルを書いてみたらエラーが出て少し困った。

```bash
➜  sandbox  bundle exec rspec     
/Users/yamagh/GoogleDrive/dev/ruby/sandbox/spec/hello_spec.rb:3:in `<top (required)>': undefined method `describe' for main:Object (NoMethodError)
from /Library/Ruby/Gems/2.0.0/gems/rspec-core-3.1.7/lib/rspec/core/configuration.rb:1105:in `load'
from /Library/Ruby/Gems/2.0.0/gems/rspec-core-3.1.7/lib/rspec/core/configuration.rb:1105:in `block in load_spec_files'
from /Library/Ruby/Gems/2.0.0/gems/rspec-core-3.1.7/lib/rspec/core/configuration.rb:1105:in `each'
from /Library/Ruby/Gems/2.0.0/gems/rspec-core-3.1.7/lib/rspec/core/configuration.rb:1105:in `load_spec_files'
from /Library/Ruby/Gems/2.0.0/gems/rspec-core-3.1.7/lib/rspec/core/runner.rb:96:in `setup'
from /Library/Ruby/Gems/2.0.0/gems/rspec-core-3.1.7/lib/rspec/core/runner.rb:84:in `run'
from /Library/Ruby/Gems/2.0.0/gems/rspec-core-3.1.7/lib/rspec/core/runner.rb:69:in `run'
from /Library/Ruby/Gems/2.0.0/gems/rspec-core-3.1.7/lib/rspec/core/runner.rb:37:in `invoke'
from /Library/Ruby/Gems/2.0.0/gems/rspec-core-3.1.7/exe/rspec:4:in `<top (required)>'
from /usr/bin/rspec:23:in `load'
from /usr/bin/rspec:23:in `<main>'
```

記事の通りやってるしなんでだろーと思ったけど、とりあえず解決方法が分かったのでメモ。

```
[spec/spec_helper.rb]

51   # Limits the available syntax to the non-monkey patched syntax that is recommended.
52   # For more details, see:
53   #   - http://myronmars.to/n/dev-blog/2012/06/rspecs-new-expectation-syntax
54   #   - http://teaisaweso.me/blog/2013/05/27/rspecs-new-message-expectation-syntax/
55   #   - http://myronmars.to/n/dev-blog/2014/05/notable-changes-in-rspec-3#new__config_option_to_disable_rspeccore_monkey_patching
56   config.disable_monkey_patching!
57 
```

`rspec --init` で生成される `spec/spec_helper.rb` の56行目あたりにある `config.disable_monkey_patching!` をコメントにするとエラー解消。

```
➜  sandbox  bundle exec rspec
Run options: include {:focus=>true}

All examples were filtered out; ignoring {:focus=>true}

Hello
  message return hello

Finished in 0.00165 seconds (files took 0.13068 seconds to load)
1 example, 0 failures

Top 1 slowest examples (0.00089 seconds, 54.3% of total time):
  Hello message return hello
      0.00089 seconds ./spec/hello_spec.rb:4

Randomized with seed 5838
```

エラーなく動くようになりましたとさ。  
原因は気が向いたら調べてみるかも。
