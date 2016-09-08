---
title: "アプリケーションのテスト | Azure RMS"
description: "アプリケーションのテストを設定する方法"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: E480D8D6-F070-43D1-B2B0-6921459C3437
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: 9cc96c7f4d75969ec75b1372a4a49499709b0d32


---

# アプリケーションのテスト

このトピックでは、アプリケーション テストを設定する方法について説明します。

## 手順

### 手順 1: テストの設定

Windows Server で実行されている Azure RMS または RMS サーバーをテストできます。Azure RMS のテストから始めることをお勧めします。その後、デプロイに必要であれば、RMS サーバーをテストしてください。

1. Azure RMS でテストする方法については、「[方法: ADAL 認証の使用](how-to-use-adal-authentication.md)」を参照してください。
2. RMS サーバーでテストする方法については、「[方法: RMS サーバーをインストールし、構成する](how-to-install-and-configure-an-rms-server.md)」を参照してください。
3. 以下では、開発者向けランタイムのインストール方法について説明しています。

   Rights Management Service Client 2.1 がアプリケーションのテストを実行するコンピューターにインストールされている必要があります。
   - 開発コンピューター以外のコンピューターでアプリケーションをテストする場合は、[AD RMS クライアント ダウンロード ページ](http://www.microsoft.com/en-us/download/details.aspx?id=38396)からそのコンピューターに RMS クライアント 2.1 をインストールできます。
   - 開発コンピューターでアプリケーションをテストする場合は、Rights Management サービス SDK 2.1 を既にインストールしています。 この時点で、RMS クライアント 2.1 がサイレント インストールされています。

    RMS SDK 2.1 のインストール方法については、「[SDK のインストール](install-the-rms-sdk.md)」を参照してください。

## 解説

このトピックのガイダンスは包括的なものではありません。 RMS クライアント 2.1 の構成方法について詳しくは、「[RMS Client 2.1 Deployment Notes](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx)」 (RMS クライアント 2.1 のデプロイに関する注意事項) をご覧ください。

### 関連項目

* [RMS サーバーをインストールし、構成する方法](how-to-install-and-configure-an-rms-server.md)
* [方法: ADAL 認証の使用](how-to-use-adal-authentication.md)
* [SDK のインストール](install-the-rms-sdk.md)
* [RMS クライアント 2.1 のデプロイに関する注意事項](https://technet.microsoft.com/en-us/library/jj159267(WS.10).aspx)
 

 



<!--HONumber=Aug16_HO4-->


