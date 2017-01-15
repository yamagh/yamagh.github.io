---
layout: post
title:  "Keras で CIFAR-10"
date:   2017-01-15 22:40:23 +0900
categories: [keras deeplearning]
---

先週、[TensorFlow](https://www.tensorflow.org/) のラッパーで [Keras](https://keras.io/ja/) なる便利なツールがあることを知って、今週末ちょっと触ってみた。

ためしに触ってみたのは [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html)。  
CIFAR-10とは飛行機とか、自動車とか、鳥やネコの画像を識別するAIを作るチュートリアルのようなもの。  
AI や人工知能について何も知らないと難しそうに思えるけれど、深層学習の分野ではこれがなかなかちょうどいい難易度の課題なのだとか。  

実際やってみた結果、わりと簡単に出来た。  
CIFAR-10 の公式ページにおいてあるデータセットの写真6万枚を使って学習と学習結果を評価するのだけど、学習用のデータではほぼ100%、評価用のデータでは約70%の認識率となった。  

下の画像はその結果。見にくいけれど画像の上に `ok` と表示されている画像は正しく認識できたことを表している。

![cifar10](https://lh3.googleusercontent.com/XsSE85-gMB2DyGEW5r7-5xi8LGDYLOn_jriuYQ5nhSlsj4cyUpsp8DJSFEKDDVpPcaqx6M2OwbmOUiDpUVcvR2XaHV9Qu_bT6fwAHfSfaq3_Q-OMkDU_3XYEiq32spIEzZXzkRDjrJVjS_zIUPnJJknd9Oq_bwrsaPOEhl8dmeEMs0K9n2Ff5MUoouyqkA5PkmU2mV-wbM1nne_1aE5QBsxS4tPDlx3zN4qk-E0-Z1crTSH1N1OtY-sTzPP7br5LDZ_rEym0taUY1XHqHG1yDX5_4witAcZXhB1vVl1eTfEC4jgIiDhcjB9rsRtK02WtEKUD86lp9byOEbwKxWbxnDuBf8LB0mW2WLCul-r1zo2UIUa-p8toD5EvsH16rQGOX-m_Hn2QJ-OT8tGNwvgD5jO9xnNW0y20DMwBR3EJa3WqFBI3qrqK6EP9ZGSOj3DRgyibxdgzna3aJt8alTBtok2VB5a_HfEx1NxMqQTfzh416CcdH6XBlG4rQAV7VbF_IIzgL3xodvclh0H_l6SRY5J5p1zCKyLbwM1EIJyerIyXoVj_Nr-PyBAPUZfGgUoB-bPwBnCkYLFwfUqlPZFlq2XyQp1qH6ueWXbppv2kbeMb1aFSjY03iw=w1317-h798-no)

初めて触って、週末ちょっとやってみたにしては思ったより簡単に出来て拍子抜けだった。  
Keras すごく便利。

ちなみに書いたソースコードは今感じ。
どこかのブログの内容を参考に書いたもので、ほとんどコピペみたいなものだけど、一応理解して何も見ずに書いた。  
CNN の層をもっと増やせば認識率上がったかも、とか思うが、活性化関数とか、損失関数とか、畳込みとかその辺のキーワードを何となく理解するのが目的だったので良しとする。

しばらく Keras で遊んでみよう。

<script src="https://gist.github.com/yamagh/4f23feb62ffe11081df61b0890b17d1b.js"></script>

ちなみに Github の Keras のリポジトリに入っている CIFAR-10 のサンプルコードは[こちら](https://github.com/fchollet/keras/blob/master/examples/cifar10_cnn.py)。

見ると何やっているか何となく分かるのだから、Keras のニューラルネットワークのモデルの可読性がいかに高いかがよく分かる。こんなものが誰だって使えるんだから、すごい時代だな―。

