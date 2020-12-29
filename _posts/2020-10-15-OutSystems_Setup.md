---
layout:     post
title:      "OutSystems Setup"
date:       2020-10-15 23:36:08 +0900
tags:       OutSystems Setup
categories: 
published: true
---

OutSystems の事を詳しく知ろうと思うと、自由にサワれる環境が欲しくなってくるものですが、環境構築の手順に関する情報があまりないので自分の試してみた結果について書いてみたいと思います。今回は開発者がお試し用として使える環境を１から作ることを前提として Windows Server のインストールからやってみます。開発者がローカルで動かせるだけの環境を作るので細かい設定は特に行いません。

## 目次

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [目次](#目次)
- [今回つくる環境](#今回つくる環境)
- [作業の流れ](#作業の流れ)
- [手順](#手順)
  - [1. VirtualBox のインストール](#1-virtualbox-のインストール)
  - [2. Windows Server 2019 のインストール](#2-windows-server-2019-のインストール)
    - [2-1. Windows Server 2019 無料試用版 をダウンロード](#2-1-windows-server-2019-無料試用版-をダウンロード)
    - [2-2 マシンの作成](#2-2-マシンの作成)
    - [2-3 Windows Server 2019 のインストール](#2-3-windows-server-2019-のインストール)
    - [2-4 VirtualBox Guest Additions インストール](#2-4-virtualbox-guest-additions-インストール)
  - [3. Microsoft SQL Server 2017 のインストール](#3-microsoft-sql-server-2017-のインストール)
    - [3-1. インストーラーのダウンロード](#3-1-インストーラーのダウンロード)
    - [3-2. インストール](#3-2-インストール)
    - [3-3. SQL Server の TCP/IP プロトコルの有効化](#3-3-sql-server-の-tcpip-プロトコルの有効化)
    - [3-4. （任意）Microsoft SQL Server Management Studio (SSMS) のインストール](#3-4-任意microsoft-sql-server-management-studio-ssms-のインストール)
  - [4. Platform Server のインストール](#4-platform-server-のインストール)
    - [4-1. インストーラーのダウンロード](#4-1-インストーラーのダウンロード)
    - [4-2. Platform Server のインストール](#4-2-platform-server-のインストール)
    - [4-3. Configuration Tool で環境の設定](#4-3-configuration-tool-で環境の設定)
  - [5. SSL 証明書インストール](#5-ssl-証明書インストール)
  - [6. Service Center の設定](#6-service-center-の設定)
    - [6-1. ライセンスのアップロード](#6-1-ライセンスのアップロード)
    - [6-2. Service Center の設定](#6-2-service-center-の設定)
  - [7. 標準のコンポーネントをインストール](#7-標準のコンポーネントをインストール)
  - [8. 動作確認](#8-動作確認)
- [感想](#感想)

<!-- /code_chunk_output -->

## 今回つくる環境

次の構成の環境を VirtualBox の中に作ります。

- Windows Server 2019 (64bit)
- SQL Server 2017
- OutSystems Platform v11.9.1
  - デプロイメントコントローラ
  - サーバ
  - データベース
- スタンドアロン構成

## 作業の流れ

OutSystems の次のドキュメントを参考に作業していきます。

- [インストール手順 - OutSystemsを設定する](https://success.outsystems.com/ja-jp/Documentation/11/Setting_Up_OutSystems#_8)
- [Installation Checklist JP - Platform Server - 11.9.1](https://www.outsystems.com/downloads/ScreenDetails.aspx?MajorVersion=11&ReleaseId=19511&ComponentName=Platform+Server)

作業の概要を箇条書するとこのような感じです。

1. VirtualBox のインストール
2. Windows Server 2019 インストール
3. SQL Server インストール
   - Mixed mode - SQL Server and Windows Authentication
   - Case-sensitive
   - SQL Server TCP/IPプロトコル 有効化
4. Platform Server インストール
5. SSL 証明書インストール
6. Service Center の設定
7. 標準のコンポーネントをインストール
8. 動作確認

## 手順

### 1. [VirtualBox](https://www.virtualbox.org/) のインストール

homebrew でインストールします。詳細は割愛。

```sh
brew cask install virtualbox
```

### 2. Windows Server 2019 のインストール

#### 2-1. [Windows Server 2019 無料試用版](https://www.microsoft.com/ja-jp/windows-server/trial) をダウンロード

次のページに詳しくまとまっているため詳細は割愛しますが、今回の手順では ISO ファイルをダウンロードします。

[Windows Server 2019 180日評価版、Windows 10 Enterprise 90日評価版ダウンロード手順](https://qiita.com/bitterrich/items/d22d1a0fe02d08b1faed)

#### 2-2 マシンの作成

次のような設定でマシンを作成。  
[OutSystems のシステム要件](https://success.outsystems.com/Documentation/11/Setting_Up_OutSystems/OutSystems_system_requirements)としてはメモリが最低 4GB 必要となっています（2020年11月時点）。ただ個人的には 4GB では少なすぎる感じがするので最低でも 8GB は欲しいところです。

![img](/img/2020/10/15/2-2-1.webp)
![img](/img/2020/10/15/2-2-2.webp)

ホストのマシンのブラウザからもアクセスできるようにしたいので、ポートフォワーディングの設定も入れておく。

![img](/img/2020/10/15/2-2-3.webp)

#### 2-3 Windows Server 2019 のインストール

手順2−1でダウンロードした Windows Server 2019 の ISO ファイルをディスクドライブに設定。

![img](/img/2020/10/15/2-3-1.webp)

マシンを起動してインストール開始。

![img](/img/2020/10/15/2-3-2.webp)
![img](/img/2020/10/15/2-3-3.webp)
![img](/img/2020/10/15/2-3-4.webp)
![img](/img/2020/10/15/2-3-5.webp)
![img](/img/2020/10/15/2-3-6.webp)
![img](/img/2020/10/15/2-3-7.webp)
![img](/img/2020/10/15/2-3-8.webp)
![img](/img/2020/10/15/2-3-9.webp)
![img](/img/2020/10/15/2-3-10.webp)
![img](/img/2020/10/15/2-3-11.webp)

#### 2-4 VirtualBox Guest Additions インストール

入れておくと作業しやすいのでインストールしておく。

![img](/img/2020/10/15/2-4-1.webp)
![img](/img/2020/10/15/2-4-2.webp)

### 3. Microsoft SQL Server 2017 のインストール

#### 3-1. インストーラーのダウンロード

[OutSystems のシステム要件](https://success.outsystems.com/Documentation/11/Setting_Up_OutSystems/OutSystems_system_requirements)で一番新しいバージョンの SQL Server は 2017 のため（2020年11月時点）、SQL Server 2017 をインストールしていきます。評価版のインストーラーは次の URL からダウンロードできます。

[SQL Server 評価版ソフトウェア](https://www.microsoft.com/ja-jp/evalcenter/evaluate-sql-server-2019)

#### 3-2. インストール

インストーラーを起動してインストールしていきます。  
`SQL Server の新規スタンドアロン インストール` をクリックします。

![img](/img/2020/10/15/3-2-1.webp)

無償のエディションを指定する

![img](/img/2020/10/15/3-2-2.webp)

ライセンス条項に同意しますにチェックして次へ

![img](/img/2020/10/15/3-2-3.webp)

次へ

![img](/img/2020/10/15/3-2-4.webp)

次へ

![img](/img/2020/10/15/3-2-5.webp)

データベース エンジン サービス にチェックを入れて次へ

![img](/img/2020/10/15/3-2-6.webp)

次へ

![img](/img/2020/10/15/3-2-7.webp)

`SQL Server データベース エンジン` のスタートアップの種類が `自動`  になっていることを確認。`照合順序` のタブのスクリーンショットを取り忘れましたがこちらも設定する。

![img](/img/2020/10/15/3-2-8.webp)

`混合モード` を選択してパスワードを入力

![img](/img/2020/10/15/3-2-9.webp)

インストール

![img](/img/2020/10/15/3-2-10.webp)
![img](/img/2020/10/15/3-2-11.webp)
![img](/img/2020/10/15/3-2-12.webp)

#### 3-3. SQL Server の TCP/IP プロトコルの有効化

次の画像の通り有効に設定。

![img](/img/2020/10/15/3-3-1.webp)

設定完了後はサービスを再起動する。

![img](/img/2020/10/15/3-3-2.webp)

#### 3-4. （任意）Microsoft SQL Server Management Studio (SSMS) のインストール

DB に関する作業をするときにあると便利なので、ここで入れておくのもいいと思う。ここでは詳細は割愛。

### 4. Platform Server のインストール

#### 4-1. インストーラーのダウンロード

次のページから Platform Server のインストーラーをダウンロードします。今回は [11.9.1](https://www.outsystems.com/downloads/ScreenDetails.aspx?MajorVersion=11&ReleaseId=19511&ComponentName=Platform+Server) を使うことにします。

[Software Downloads Search](https://www.outsystems.com/Downloads/search/Platform-Server/11/)

#### 4-2. Platform Server のインストール

インストーラーを起動して次へ、次へと進めば完了。

![img](/img/2020/10/15/4-2-1.webp)
![img](/img/2020/10/15/4-2-2.webp)
![img](/img/2020/10/15/4-2-3.webp)

`Install Prerequisites` にチェックがついていることを確認

![img](/img/2020/10/15/4-2-4.webp)
![img](/img/2020/10/15/4-2-5.webp)
![img](/img/2020/10/15/4-2-6.webp)
![img](/img/2020/10/15/4-2-7.webp)
![img](/img/2020/10/15/4-2-8.webp)

#### 4-3. Configuration Tool で環境の設定

特に設定の変更は不要で各タブ設定していけば良い。

管理者のパスワードを入力して `Grant Permission` と `Create/Upgrade Databse` をクリック。

![img](/img/2020/10/15/4-3-1.webp)
![img](/img/2020/10/15/4-3-2.webp)
![img](/img/2020/10/15/4-3-3.webp)
![img](/img/2020/10/15/4-3-4.webp)
![img](/img/2020/10/15/4-3-5.webp)
![img](/img/2020/10/15/4-3-6.webp)
![img](/img/2020/10/15/4-3-7.webp)
![img](/img/2020/10/15/4-3-8.webp)
![img](/img/2020/10/15/4-3-9.webp)
![img](/img/2020/10/15/4-3-10.webp)
![img](/img/2020/10/15/4-3-11.webp)

Platform の管理者（ServiceCenter や Users にログインするユーザ) のパスワードを設定

![img](/img/2020/10/15/4-3-12.webp)
![img](/img/2020/10/15/4-3-13.webp)
![img](/img/2020/10/15/4-3-14.webp)

Scheduler のタブは特に設定変更せず、 `Apply and Exit`。

![img](/img/2020/10/15/4-3-15.webp)
![img](/img/2020/10/15/4-3-16.webp)
![img](/img/2020/10/15/4-3-17.webp)
![img](/img/2020/10/15/4-3-18.webp)
![img](/img/2020/10/15/4-3-19.webp)

### 5. SSL 証明書インストール

IIS のサービスマネージャーから `サーバー証明書` を選択。

![img](/img/2020/10/15/5-1-1.webp)

今回は試しに作る環境なので、自己署名証明書を使用します。  
右のペインから `自己署名入り証明書の作成...` を選択。

![img](/img/2020/10/15/5-1-2.webp)

適当な名前を設定。

![img](/img/2020/10/15/5-1-3.webp)
![img](/img/2020/10/15/5-1-4.webp)

右のペインから `バインド` を選択。  
開いたダイアログの下部にある `SSL 証明書` のコンボボックスから先程、先ほど作成した証明書を選択。

![img](/img/2020/10/15/5-1-5.webp)
![img](/img/2020/10/15/5-1-6.webp)

### 6. Service Center の設定

#### 6-1. ライセンスのアップロード

ライセンスファイルをアップロードします。

![img](/img/2020/10/15/6-1-1.webp)

#### 6-2. Service Center の設定

`Hostname` を設定。 `localhost` としました。

![img](/img/2020/10/15/6-2-1.webp)

`Deployment Zone Address` を設定。 `localhost` としました。

![img](/img/2020/10/15/6-2-2.webp)

Users アプリの管理者のパスワードを設定。 `Configure Administrator User` ボタンから設定。

![img](/img/2020/10/15/6-2-3.webp)
![img](/img/2020/10/15/6-2-4.webp)

### 7. 標準のコンポーネントをインストール

次の標準のコンポーネントをインストールしていきます。必須ではないものもありますが一通り実施します。すべて Service Center から実施。

1. Charts Web
2. OutSystems Charts
3. OutSystems UI Web
4. OutSystems UI
5. OutSystems Sample Data
6. OutSystems Screen Templates Web
7. OutSystems Templates Mobile
8. OutSystems Templates Reactive Web
9. OutSystems Now

![img](/img/2020/10/15/7-1-1.webp)
![img](/img/2020/10/15/7-1-2.webp)

### 8. 動作確認

![img](/img/2020/10/15/8-1-1.webp)
![img](/img/2020/10/15/8-1-2.webp)
![img](/img/2020/10/15/8-1-3.webp)
![img](/img/2020/10/15/8-1-4.webp)
![img](/img/2020/10/15/8-1-5.webp)
![img](/img/2020/10/15/8-1-6.webp)

## 感想

たくさん画像をキャプチャして疲れました。今回から画像を webp に変換するようにしたので、77枚の画像でたった 2.6MB ですみました（素晴らしい！）。

手順の中で詳しくは書きませんでしたがライセンスはトライアルのものを利用しています。このライセンスファイルは OutSystems がインターネット上の見えるところに公開しているものですが、公の場に書くのは [グレーな気がして](https://www.outsystems.com/forums/discussion/21392/free-trial-for-on-premise-outsystems/) 詳細は伏せました。ただ、開発者には自由に学べる環境や機会があることが重要だと思うため、今後は開発者用のライセンスも公開してもらいたいものです。
