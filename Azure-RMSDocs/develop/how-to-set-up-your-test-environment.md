---
# required metadata

title: テスト環境のセットアップ | Azure RMS
description: 権限保護対応アプリケーションは、さまざまなサーバー オプションを指定してテストできます。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: E480D8D6-F070-43D1-B2B0-6921459C3437
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# テスト環境のセットアップ

権限保護対応アプリケーションは、さまざまなサーバー オプションを指定してテストできます。

**重要** ベスト プラクティスとして、はじめに AD RMS サーバーに対して AD RMS 運用前環境で Rights Management サービス SDK 2.1 アプリケーションをテストすることをお勧めします。 その後で、顧客に Azure RMS サービスでのアプリケーションの使用を勧める場合は、その環境でのテストに移行します。 詳細については、「[クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)」を参照してください。

 

### 必要条件

-   [SDK のインストール](create-your-first-rights-aware-application.md)

手順

### 手順 1: テスト環境をセットアップする

権限保護対応アプリケーションをテストするには、運用前として構成した RMS サーバーに対してそのアプリケーションを実行する必要があります。 運用前 RMS サーバーでは、運用前/ISV 証明書階層を使用してファイルを暗号化および解読します。

AD RMS 証明書階層の詳細については、「[Understanding certificate chains (証明書チェーンについて)](understanding-certificate-chains.md)」を参照してください。

RMS サーバーに対してアプリケーションをテストする場合、2 つのオプションがあります。

-   **1-box AD RMS ISV 環境でアプリケーションを実行する**。 Windows Server 2012、Windows Server 2008 R2、または Windows Server 2008 を実行し、Hyper-V がインストールされている場合は、AD RMS 1-box VHD を使用して仮想マシンを作成することにより、1-box AD RMS ISV 環境をデプロイできます。 1-box AD RMS ISV 環境の RMS サーバーは運用前として構成されています。この環境には Active Directory Rights Management サービス クライアント 2.1 もインストールされています。 RMS サーバーとクライアントのレジストリ設定が既に構成されています。 アプリケーションをテストするには、1-box 環境が展開されている仮想マシンで実行します。
-   **運用前として構成され、ネットワークに展開されている RMS サーバーに対してアプリケーションを実行する**。 この場合は、アプリケーションを実行するコンピューターに AD RMS Client 2.1 をインストールして構成する必要もあります。 この方法については、「[Configure client (クライアントの構成)](how-to-configure-the-ad-rms-client-2-0.md)」を参照してください。 RMS サーバーをデプロイし、運用前として構成する方法については、「[サーバーのインストールと構成](how-to-install-and-configure-an-rms-server.md)」を参照してください。

## 関連項目

* [How-to use (使用方法)](how-to-use-msipc.md)
* [AD RMS SDK ウェビナーに関するダウンロード ページ](https://connect.microsoft.com/site1170/Downloads/DownloadDetails.aspx?DownloadID=42440)
* [Configure client (クライアントの構成)](how-to-configure-the-ad-rms-client-2-0.md)
* [SDK のインストール](create-your-first-rights-aware-application.md)
* [サーバーのインストールと構成](how-to-install-and-configure-an-rms-server.md)
* [Understanding certificate chains (証明書チェーンについて)](understanding-certificate-chains.md)
 

 





<!--HONumber=Apr16_HO4-->


