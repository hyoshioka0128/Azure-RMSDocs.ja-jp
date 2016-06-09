---
# required metadata

title: AD RMS サーバー |Azure RMS
description: Rights Management サービス (RMS) のサーバー コンポーネントは、Microsoft インターネット インフォメーション サービスで実行される一連の Web サービスによって実装されます。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 17B05780-B0EF-4805-8304-52DCDEB3AADB
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** この SDK コンテンツは最新のものではありません。 しばらくの間、[最新版](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx)の文書は MSDN でご覧ください。 **

# AD RMS サーバー
このトピックでは、RMS サーバーの目的と機能について説明します。

Rights Management サービス (RMS) のサーバー コンポーネントは、[Microsoft インターネット インフォメーション サービス](http://www.iis.net/overview) (IIS) で実行される一連の Web サービスによって実装されます。 Azure の RMS を使用してクラウド ベースの実装を使用することもできます。 Azure Rights Management サービス使用の詳細については、「[クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)」を参照してください。

オンプレミス サーバーでは、Windows Server 2008 以降、RMS サービスをロールとして追加することで、そのインストールと構成ができます。 以前のオペレーティング システムにサービスをインストールするには、Microsoft ダウンロード センターから [Microsoft Windows Rights Management サービス Service Pack 2](http://www.microsoft.com/download/en/details.aspx?id=4909) をダウンロードします。

インストールされる多くの Web サービスの中でも、アプリケーション開発にとっては次のサービスが重要です。

**管理** - RMS を管理することができる管理 Web サイトをホストします。 このサービスは、ルート証明サーバーとライセンス サーバーで動作します。 [Active Directory Rights Management サービス スクリプト API](https://msdn.microsoft.com/library/Bb968797) を使用して管理スクリプトを記述できます。

**アカウント証明** - RMS 証明書階層内のコンピューターを識別するコンピューター証明書と、ユーザーを特定のコンピューターに関連付ける Rights Account Certificate を作成します。 詳細については、「[Activating a User (ユーザーのアクティブ化)](https://msdn.microsoft.com/library/Cc530378)」を参照してください。

このサービスは、ルート証明サーバーで動作します。

**ライセンス** -保護されたコンテンツをエンド ユーザーが使用できるようにするエンド ユーザー ライセンスを発行します。 このサービスは、ルート証明サーバーとライセンス サーバーで動作します。

**公開** - [発行ライセンス](https://msdn.microsoft.com/library/Aa362355)を作成します。 このサービスは、ルート証明サーバーとライセンス サーバーで動作します。

**事前証明** - サーバーがユーザーに代わって Rights Account Certificate (RAC) を要求できるようにします。 RAC は、RMS アクティブ化からコンピューター証明書を使用して、ユーザー アカウントを特定のコンピューターまたはコンピューターのグループにバインドします。また、保護されたコンテンツをコンシューマーが使用できるようにするために使用されます。 このサービスは、ルート証明サーバーとライセンス サーバーで動作します。

**サービス ロケーター** - アカウント証明サービス、ライセンス サービス、および公開サービスの URL を Active Directory に提供し、RMS クライアントがこれらのサービスを検出できるようにします。 このサービスは、ルート証明サーバーとライセンス サーバーで動作します。

 

## 関連項目 ##
* [概要](ad-rms-overview.md)
* [Microsoft インターネット インフォメーション サービス](http://www.iis.net/overview)
* [クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)
* [Microsoft Windows Rights Management サービス Service Pack 2](http://www.microsoft.com/download/en/details.aspx?id=4909)
* [Active Directory Rights Management Services Scripting API (Active Directory Rights Management Services スクリプト API)](https://msdn.microsoft.com/library/Bb968797)
* [Activating a Computer (コンピューターのアクティブ化)](https://msdn.microsoft.com/library/Cc530377)
* [Activating a User (ユーザーのアクティブ化)](https://msdn.microsoft.com/library/Cc530378)
* [Creating an Issuance License (発行ライセンスの作成)](https://msdn.microsoft.com/library/Aa362355)

 

 


<!--HONumber=Jun16_HO1-->


