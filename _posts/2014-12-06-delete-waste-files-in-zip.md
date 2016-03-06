---
layout: post
title:  "Zipの中の `.DS_Store` や `__MACOSX` を削除"
date:   2014-12-06 17:22:45 +0900
categories: Mac
---

 こんな感じで `.DS_Store` やら `__MACOSX` が入っているzipから取り除く方法。

![image](https://lh3.googleusercontent.com/4G2WEDW5FgGAw0w1-dvPgZApQVh-T7eq0p4mBcPDMF63tz2pjD2ND2PcEBdrVE9yng1kaZqqDQVMtaL40QEUJEhdd0IJOnVVfyuQBijPnU3FDcaMWPcG27GifNYsQ_ZVx3GTOswy-IiHsTf91c-KE8xlfMdjCcIWwD_PBOcMq_udc839VB8ApkWhus0k0WWpdAp4KodotIbMj-dAKKM7-FQBYtPGpXTwrDhz8InPlrdmUiFXO_JSnwv6Q2rnh38WK6dClzBseuH84p6zhVkk3NfARz-DpZyicFxG9lsRa66vUTxaxnjMSlL2EZKWZ-2CCOlZK41fFHZ0Dh3kfn-9NRjxNRGaFLeEpCA0WPTSag9S4tIwE5lnIdcXoC2w7owS0wXMBXdva8Hp3E0VcoJC8ejLVJrASYroSbx3nsYVPcnnRm_teQ4D74BKRaYsF7MHQ4md-DtyEnqn8UOqISLLH6X2CccFGYZLI8oaUwfyyFELZeoefFptnffXZ0i8lXBXwhs962PF8pyQ-wQexKPY1B86yFf0ycCE_pc2A-yi0n7Q6EuUru9xDfqRpIJxBG_7zkB4kQ=w441-h276-no)

次のコマンドで消せる。

```bash
$ zip --delete picture.zip "*.DS_Store"
$ zip --delete picture.zip "*__MACOSX*"
```

複数のファイルからまとめて消すならこんな感じ。

```bash
$ find . -name "*.zip" -exec zip --delete {} "*.DS_Store" \;
$ find . -name "*.zip" -exec zip --delete {} "*__MACOSX*" \;
```

zipにそもそも入らないようにするのはこの記事が参考になった。

[Mac OSXでWin対応の圧縮ファイルを作るには - IVY HOUSE CLUB](http://www.ivyhc.com/?p=356)

