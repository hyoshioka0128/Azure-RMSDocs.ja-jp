---
title: AD RMS サーバー |Azure RMS
description: Rights Management サービス (RMS) のサーバー コンポーネントは、Microsoft インターネット インフォメーション サービスで実行される一連の Web サービスによって実装されます。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 17B05780-B0EF-4805-8304-52DCDEB3AADB
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 6843d2298adcc6edee6cf0ddf35a8d8b32101083
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60179716"
---
# <a name="server"></a>サーバー

このトピックでは、Azure と Windows Server を対象に、RMS サーバーの目的と機能について説明します。

**Azure RMS** - Azure Rights Management サービス使用の詳細については、「[クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)」を参照してください。

> [!IMPORTANT] 
> Azure RMS を介してアプリケーションを開発し、テストすることをお勧めします。

**Windows Server** - RMS オンプレミス サーバーでは、Windows Server 2008 以降、RMS サービスをロールとして追加することで、そのインストールと構成ができます。 以前のオペレーティング システムにサービスをインストールするには、Microsoft ダウンロード センターから [Microsoft Windows Rights Management サービス Service Pack 2](https://www.microsoft.com/download/details.aspx?id=4909) をダウンロードします。

インストールされる多くの Web サービスの中でも、Windows Server の RMS サーバーの場合、アプリケーション開発にとっては次のサービスが重要です。

| サービス | 説明 |
|---------|-------------|
| Administration | RMS を管理することができる管理 Web サイトをホストします。 このサービスは、ルート証明サーバーとライセンス サーバーで動作します。 Active Directory Rights Management サービス スクリプト API を使用して管理スクリプトを記述できます。|
| アカウント証明書 |RMS 証明書階層内のコンピューターを識別するコンピューター証明書と、ユーザーを特定のコンピューターに関連付ける Rights Account Certificate を作成します。 詳細については、「Activating a Computer (コンピューターのアクティブ化)」と「Activating a User (ユーザーのアクティブ化)」を参照してください。<p><p>このサービスは、ルート証明サーバーで動作します。 |
|ライセンス | *使用許諾*を発行します。 このサービスは、ルート証明サーバーとライセンス サーバーで動作します。|
|発行 | *発行ライセンス*を作成します。発行ライセンスにより定義されるポリシーが使用許諾に列挙されます。 詳細については、「[Creating an Issuance License (発行ライセンスの作成)](https://msdn.microsoft.com/library/Aa362355)」を参照してください。<p><p>このサービスは、ルート証明サーバーとライセンス サーバーで動作します。|
|事前証明 | サーバーがユーザーに代わって *Rights Account Certificate* を要求できるようにします。 このサービスは、ルート証明サーバーとライセンス サーバーで動作します。|
|サービス ロケーター | アカウント証明サービス、ライセンス サービス、および発行サービスの URL を Active Directory に提供し、RMS クライアントがこれらのサービスを検出できるようにします。 このサービスは、ルート証明サーバーとライセンス サーバーで動作します。|

## <a name="related-topics"></a>関連トピック ##
* [概要](ad-rms-overview.md)
* [Microsoft インターネット インフォメーション サービス](https://www.iis.net/overview)
* [クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)
* [Microsoft Windows Rights Management サービス Service Pack 2](https://www.microsoft.com/download/details.aspx?id=4909)
* [Active Directory Rights Management Services Scripting API (Active Directory Rights Management Services スクリプト API)](https://msdn.microsoft.com/library/Bb968797)
* [Activating a Computer (コンピューターのアクティブ化)](https://msdn.microsoft.com/library/Cc530377)
* [Activating a User (ユーザーのアクティブ化)](https://msdn.microsoft.com/library/Cc530378)
* [Creating an Issuance License (発行ライセンスの作成)](https://msdn.microsoft.com/library/Aa362355)
