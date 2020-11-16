---
layout:     post
title:      "OutSystems Setup"
date:       2020-10-15 23:36:08 +0900
tags:       OutSystems Setup
categories: 
published: true
---

OutSystems の事を詳しく知ろうと思うと、自由にサワれる環境が欲しくなってくるものですが、環境構築手順に関する情報があまりないので書いてみたいと思います。今回は開発者がお試し用として使える環境を１から作ることを前提として Windows Server のインストールからやってみます。開発者がローカルで動かせるだけの環境を作るので細かい設定は特に行いません。

## 目次

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [目次](#目次)
- [今回つくる環境](#今回つくる環境)
- [OutSystems インストールの前提条件のセットアップ](#outsystems-インストールの前提条件のセットアップ)
  - [1. VirtualBox のインストール](#1-virtualbox-のインストール)
  - [2. Windows Server 2019 のインストール](#2-windows-server-2019-のインストール)
    - [2-1. Windows Server 2019 無料試用版 をダウンロード](#2-1-windows-server-2019-無料試用版-をダウンロード)
    - [2-2 Windows Server 2019 のインストール](#2-2-windows-server-2019-のインストール)
  - [3. Microsoft SQL Server 2017 のインストール](#3-microsoft-sql-server-2017-のインストール)
  - [4. （たぶん任意）Microsoft SQL Server Management Studio (SSMS) のインストール](#4-たぶん任意microsoft-sql-server-management-studio-ssms-のインストール)
- [Platform Server のインストール](#platform-server-のインストール)
  - [1. インストーラーのダウンロード](#1-インストーラーのダウンロード)
  - [2. Platform Server のインストール](#2-platform-server-のインストール)
  - [3. Configuration Tool で環境の設定](#3-configuration-tool-で環境の設定)
- [参考URL](#参考url)

<!-- /code_chunk_output -->

## 今回つくる環境

- Windows Server 2019
- OutSystems Platform v11.9.1

## OutSystems インストールの前提条件のセットアップ

まず OutSystems をインストールするための前提となるサーバーのセットあアップを行います。公式のドキュメントの[ココ](https://success.outsystems.com/ja-jp/Documentation/11/Setting_Up_OutSystems#_7)の作業です。

### 1. [VirtualBox](https://www.virtualbox.org/) のインストール

今回は VirtualBox の中にセットアップしていきます。詳細は割愛。

```sh
brew cask install virtualbox
```

### 2. Windows Server 2019 のインストール

#### 2-1. [Windows Server 2019 無料試用版](https://www.microsoft.com/ja-jp/windows-server/trial) をダウンロード

次のページに詳しくまとまっているため詳細は割愛しますが、今回の手順では ISO ファイルをダウンロードします。

[Windows Server 2019 180日評価版、Windows 10 Enterprise 90日評価版ダウンロード手順](https://qiita.com/bitterrich/items/d22d1a0fe02d08b1faed)

#### 2-2 Windows Server 2019 のインストール

次のような設定でマシンを作成。  
[OutSystems のシステム要件](https://success.outsystems.com/Documentation/11/Setting_Up_OutSystems/OutSystems_system_requirements)としてはメモリが最低 4GB 必要となっています（2020年11月時点）。ただ個人的には 4GB では少なすぎる感じがするので最低でも 8GB は欲しいところです。

![img](../../../assets/2020-10-15-001-1024.webp)
![img](../../../assets/2020-10-15-002-1024.webp)

手順2−1でダウンロードした Windows Server 2019 の ISO ファイルをディスクドライブに設定。

![img](../../../assets/2020-10-15-003-1024.webp)

マシンを起動してインストール開始。

![img](../../../assets/2020-10-15-005-1024.webp)

`Windows Server 2019 Sandard evaluation (デスクトップ エクスペリエンス)` を選択。

![img](../../../assets/2020-10-15-006-1024.webp)

その他は次へ、次へでインストール実行。

![img](../../../assets/2020-10-15-007-1024.webp)

数分待てばインストールは完了。

![img](../../../assets/2020-10-15-008-1024.webp)

### 3. Microsoft SQL Server 2017 のインストール

[OutSystems のシステム要件](https://success.outsystems.com/Documentation/11/Setting_Up_OutSystems/OutSystems_system_requirements)で一番新しいバージョンの SQL Server は 2017 のため（2020年11月時点）、SQL Server 2017 をインストールしていきます。評価版のインストーラーは次の URL からダウンロードできます。

[SQL Server 評価版ソフトウェア](https://www.microsoft.com/ja-jp/evalcenter/evaluate-sql-server-2019)

インストーラーを起動して `基本` を選択。

![img](../../../assets/2020-10-15-009-1024.webp)

あとは次へ進むだけでインストールは完了。

![img](../../../assets/2020-10-15-010-1024.webp)
![img](../../../assets/2020-10-15-011-1024.webp)
![img](../../../assets/2020-10-15-012-1024.webp)
![img](../../../assets/2020-10-15-013-1024.webp)

### 4. （たぶん任意）Microsoft SQL Server Management Studio (SSMS) のインストール

SQL Server のインストールに引き続いて SSMS のインストールを行います。おそらくこのインストールは任意で OK です。

`SSMS のインストール` をクリックするとダウンロード先のページが開くのでインストーラーをダウンロードして実行。特に選択肢もなく完了します。

![img](../../../assets/2020-10-15-014-1024.webp)
![img](../../../assets/2020-10-15-015-1024.webp)
![img](../../../assets/2020-10-15-016-1024.webp)
![img](../../../assets/2020-10-15-017-1024.webp)
![img](../../../assets/2020-10-15-018-1024.webp)

## Platform Server のインストール

### 1. インストーラーのダウンロード

次のページから Platform Server のインストーラーをダウンロードします。今回は [11.9.1](https://www.outsystems.com/downloads/ScreenDetails.aspx?MajorVersion=11&ReleaseId=19511&ComponentName=Platform+Server) を使うことにします。

[Software Downloads Search](https://www.outsystems.com/Downloads/search/Platform-Server/11/)

### 2. Platform Server のインストール

インストーラーを起動して次へ、次へと進むめば完了。

![img](../../../assets/2020-10-15-019-1024.webp)
![img](../../../assets/2020-10-15-020-1024.webp)
![img](../../../assets/2020-10-15-021-1024.webp)
![img](../../../assets/2020-10-15-022-1024.webp)
![img](../../../assets/2020-10-15-023-1024.webp)
![img](../../../assets/2020-10-15-024-1024.webp)
![img](../../../assets/2020-10-15-025-1024.webp)
![img](../../../assets/2020-10-15-026-1024.webp)

### 3. Configuration Tool で環境の設定

![img](../../../assets/2020-10-15-027-1024.webp)

管理者のパスワードを入力して `Grant Permission` をクリック。

![img](../../../assets/2020-10-15-028-1024.webp)
![img](../../../assets/2020-10-15-029-1024.webp)
![img](../../../assets/2020-10-15-030-1024.webp)

続いて、 `Create/Upgrade Databse` をクリック。  
次のようにエラーが表示された場合は、

![img](../../../assets/2020-10-15-031-1024.webp)

SSMS を開いてサーバーのプロパティ設定のセキュリティ設定を開いて、サーバ認証の `SQL Server 認証モードと Windows 認証モード` を選択。

![img](../../../assets/2020-10-15-032-1024.webp)

その後、再度 `Create/Upgrade Databse` をクリックすればエラーは解消するはず。

![img](../../../assets/2020-10-15-033-1024.webp)
![img](../../../assets/2020-10-15-034-1024.webp)

Log データベースも同様に作成。

![img](../../../assets/2020-10-15-035-1024.webp)
![img](../../../assets/2020-10-15-036-1024.webp)
![img](../../../assets/2020-10-15-037-1024.webp)
![img](../../../assets/2020-10-15-038-1024.webp)
![img](../../../assets/2020-10-15-039-1024.webp)

Session データベースも同様に作成。

![img](../../../assets/2020-10-15-040-1024.webp)
![img](../../../assets/2020-10-15-041-1024.webp)
![img](../../../assets/2020-10-15-042-1024.webp)
![img](../../../assets/2020-10-15-043-1024.webp)

Platform の管理者（ServiceCenter や Users にログインするユーザのパスワードを設定）

![img](../../../assets/2020-10-15-044-1024.webp)

Cashe サービスの設定。パスワードの設定を入力して `Create/Upgrade Service`。

![img](../../../assets/2020-10-15-045-1024.webp)
![img](../../../assets/2020-10-15-046-1024.webp)
![img](../../../assets/2020-10-15-047-1024.webp)

Scheduler のタブは特に設定変更せず、 `Apply and Exit`。

![img](../../../assets/2020-10-15-048-1024.webp)
![img](../../../assets/2020-10-15-049-1024.webp)
![img](../../../assets/2020-10-15-050-1024.webp)

Platform Server のインストール完了。

![img](../../../assets/2020-10-15-051-1024.webp)

http://localhost/ServiceCenter が開ければ OK。

![img](../../../assets/2020-10-15-052-1024.webp)

ただし、ライセンスが未登録のためまだ開発には使えない。

![img](../../../assets/2020-10-15-053-1024.webp)

OutSystems がインターネット上の見える場所にトライアルのライセンスを[公開しているため](https://myfilerepo.blob.core.windows.net/sources/license.lic) そのライセンスファイルをダウンロード。

![img](../../../assets/2020-10-15-054-1024.webp)
![img](../../../assets/2020-10-15-055-1024.webp)

ダウンロードしたライセンスファイルをアップロードしてエラーが解消すれば環境のセットアップは完了。

![img](../../../assets/2020-10-15-056-1024.webp)

## 参考URL

- [公式の手順](https://success.outsystems.com/ja-jp/Documentation/11/Setting_Up_OutSystems#install-the-platform-server)