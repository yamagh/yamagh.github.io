---
layout: post
title:  "Day One の Command Line Tool"
date:   2014-12-07 20:05:16 +0900
tags:   DayOne
categories:
---
Day One のレビュー欄を見ているとコマンドラインツールがあるというコメントを発見。
早速公式サイトで探してみると確かにある。

[CLI MAN - Day One](http://dayoneapp.com/tools/cli-man/)

コマンドラインから操作が出来ると色々と便利な使い方ができるみたい。  
例えば、

1. コマンドラインから日記を検索したり，読んだり、書いたりできる。
2. TwitterとかInstagramとかWebサービスのアクティビティをDayOneにまとめる。
3. 別の日記アプリからのインポートできる。 ([Flava](https://www.takeflava.com), [OhLife](http://ohlife.com/shutdown))

Webサービスの活動から日記を作れるのがなかなか面白そう。
連携できるサービスをズラッと書いてみると結構色々ある。

- Github
- Flickr
- Last.fm
- Blog (WordPress ...)
- RSS
- Twitter
- Instapaper
- Foursquare
- PinBoard
- Pocket
- GoodReads
- App.net
- OmniFocus
- GetGlue
- Google Analytics
- Gist
- SoundCloud
- Strava
- untappd
- Wunderlist
- Jawbone UP

面白そうなのでいくつか試しに設定してみる。

# The Day One CLI (Command Line Interface) のインストール

まずはこのページの中ほどにあるリンクから `dayone-cli.pkg` をダウンロード。

[Day One Tools – Support](http://help.dayoneapp.com/day-one-tools/)

![image](https://lh3.googleusercontent.com/qVAeCEMFjS29j6oMOl5MV0Yn68D__VIWoq8hF7G2_3ml3GU7Mj_3nrSm_KbL4Dh5eAxgua78Xf32K6u3tGT1RemH_-n6quepgPSK-RgGiSqwxjSKMlsF7Qj_FeLPY1LkegXCFI2757dnriXaybm9yzNrzlc-69b537eBWOn0f9wcZm3Zrb--Q3INlxov2vscl4QimZ9XI58Q_zi3827Yk2KGlF1nP3AE9VYdV8MBASUqx0tf61IPquAht1feC9wIA26q-xMeqnldTSH83IWlmBORi348QehVLeCGAMWNTT36tFLieYvZ4FrnCBcX390I_2KnrXlTsHjIlyo0nSR9I9zwPbaOPVtDLDUF_KnkQuWDQR9slEoy2Of8qPSqe-uNjLDz9C2IXy-wyYdqLeygB16tBigjorY8LjUM0aqYkH2Fd_oZv-2BUtftAqa2OTWUo7bYlqFJovjTcmlGMaYpFKC7HwgHLfrPZZ9xKfUtoLMMCVipSNbdo4IIn6FfqsJQAlZoktXXXDRfefNi5VptCTct9AVnNJJcZLf4yhr8yvnHkDMQg1jfrv6-FBqukqHWycQwqQ=w790-h182-no)

インストーラーの指示に従ってインストール。

![image](https://lh3.googleusercontent.com/9fy4K1obiNWM5LbncJ_uLS7-d63IIXVvBCqGELZ5FHdNV1A1UP9JARGMf6mL-JRElpy3S9nqvbjh4bwn6IpG3T_UJXif6Bdu0zQsvbuVyGL3H7VJWuZDH9BeQPOqHcViOMmnP36Rz9ktptgrmFhIIVDg26zkSjcTg-8CCq1kgMYtzS9175OD3wtqHECncEnHSJVjjb0HUr1XqG5-uMgfZyN2i7Ip0q1m-E9MoLbgvPOS5LIZVkjFb9A1SPTA1zwv6gA-8K1QhH_SECxeKHmiZBAi-cwBU8IBnyfpQgk9nq6SFUjiFgmfGAzMwzxSs2CZH_hTPJ0OT0PZo6wikLZblRE0RefxK8IQLbdVmBef1lD0wF33_20HI3YYh6l6caZRz1uNzF7-rluF-ImrR3w8fxp76CEvMCfVC029ARKQfIz_BtGuYkT2-WDsiy0yVg4llG1XLWEYqd4MQ49pi5ApAL8CyiyUDXg4vjFc553fLATacipZfPUOfLk9IrgWj4lohMi2SFJf8HdSTsa59z0g0G_xmcFpd99eIuqFnerfnSeCeRLMYMbrY_NKu73Ecn24zy11Eg=w620-h438-no)

インストールが終わったらちゃんと入っているか確認。

![image](https://lh3.googleusercontent.com/MzwpWbew2MlDHNK8Bu5lFmG0jRw6WsGdo8aF3vnnPTFYcZC_dVFh380nYI41SHEjdwW-gLb6yUHSZNNfiTut0HjNJxcWZbI1V9fqo4wR2JUZC-eQOhDt2pdVk-NOAwtDnaOIPo-mBhDW27ur3w7-B9W1_aBnFBZIAFMvChYulVws1kAtdLtLxcMSgUSbLV60YD8489mHhJbONJo13PqlX1TuGBwZ2ZSbZlDwORffWNWGm7ckENb2sogspHQFeHEbPoxmtt6XIWonWn_RW8m-7Nc9IbCvUd73yb_G9B7ddY216JbPcsOrdGQ637LMhLimZV9_uxfhI4B57m29MiQdXn25JQgNnj_ph1dmi8mEraEPlIFA28zjOHPik76SUkFD6jEKJBSra3akmOOJPAtNzv5_I0__Qu60EKwqEUSahoN_y8mZnm4X6KMrJccQbkNWBouuNC-nKAv5h8zyy-TWAKJ5ZA7dGHuGdHUUdd6QxMrhrM3eox4ahNhwqxa2GswoNlCegdDFQkDnlCO5vojSuHXE7iPbsQ1MklObP3gtTd3ClRROWjXTMxZLIqvyB-KX9tx_lQ=w717-h381-no)

うむうむ入っている。  
しかし、用意されているコマンドは `new` で日記の新規作成だけみたい。

試しに日記を書いてみる。

```bash
➜  ~  dayone -s=true new
Enter text for journal entry. Type ^D on a newline when finished.
--------------------------------------------------------------------
コマンドラインから日記を書いてみる。
果たしてこれは便利なのだろうか ？    
New entry : ~/Library/Mobile Documents/5U8NS4GX82~com~dayoneapp~dayone/Documents/Journal_dayone/entries/B6F887A9A5A14190954C28E7D1E8BDB8.doentry
```

![image](https://lh3.googleusercontent.com/Iax_--8V6Q5AYIClMRc8IxbmNWAoh9wIJT98NlvSzqDD9D-MRhb5MKYd63kTVIIMrmAAMYUL2FdcGk8RoGBl57adY88UogDOaq-3yBo4e5vf0rb9JuiMGwHkdR0QlH5M7uvxWVqRaLlXtpnoJ5dDQFa58YIREV1yISBNfyFBWqepTxCC05Tk51tLuYR13LJPynFQoDU6lnGSvEKwl2gEPTIEZcezbKeyi6gY-3L7KQvCDTmRSZUzpzBmaNQrSqq79qKbK5iSuM3-SUYMWODbYNqpEazvAUwflUCmCMEoLOJrtgxf7gcHU9aGkY-qBGPosOCO-tgOyDdMBrGqvoQDrOclaiXx-CAY9kEh68IOr1_Z7pmmU7g0HNyV_-v2opW6FzdTIJSMWzninhWm0TxBAejtbiOgSvwgcFxImw1ekYvAzYM8EjID4_rPGr3xkdNr_R6iNDvXPsUgQxGzibWBGhVLTWTb8Ia9_fR4CzqfvQKJP6rf2hYgMR56oy94kwA2nqO-580JNSFRvuyp_NHKwwj3cmKOPd8AhXWKBDTSJQv3sqC8NRNNWIdYZGPsK0vJQBQd1Q=w720-h442-no)

おお、ちゃんと登録できている。  
しかし、一度書いた行を書き直したり出来ないのはかなり不便だし、ネストしたリストを書くときに自動でインデントしてくれないのも不便。

続いて Jawbone UP と連携を設定してみたいが長くなりそうなので別エントリに分ける。

