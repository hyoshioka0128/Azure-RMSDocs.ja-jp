---
title: RMS SDK 4.2 の非推奨の通知
description: RMS SDK 4.2 の非推奨の通知
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
ms.date: 03/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 6742a2405471b75a70579e9fbf00a792335537d3
ms.sourcegitcommit: 4815ab96e4596303af297ae4c13fb6d7083b21e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "95570846"
---
# <a name="rms-sdk-42-deprecation-notice"></a>RMS SDK 4.2 の非推奨の通知 

*2020年3月より前のすべての RMS SDK 4.2 バージョンリリースに適用可能*

2020年3月3日、Android、iOS、OSX 用の RMS SDK 4.2 の更新プログラムは、Microsoft ダウンロードセンターでリリースされました。 現時点では、これらの RMS SDK プラットフォームを使用するすべてのアプリケーションに対して、この更新プログラムは必須です。  

2020年12月1日より、2020年3月より前にリリースされた RMS SDK のバージョンは、Azure Rights Management サービスエンドポイントへの接続に失敗します。 RMS SDK 4.2 を使用するアプリケーションは、この日付より前に更新する必要があります。 

## <a name="reason-for-change"></a>変更の理由 

以前のバージョンの RMS SDK は、証明書のピン留めを使用して、RMS 対応クライアントが RMS サービスと通信し、特定の予想されるルート CA にチェーンされている証明書を受信していることを確認します。  

最新のブラウザーでは、証明書の透過性ログを使用して、証明書が正当なドメイン所有者に発行されていること、および信頼されたルート証明機関によって証明書が発行されたことを確認  

最新のブラウザーをより適切にサポートするために、Microsoft は、2020年12月1日に、発行された証明書を、 `https://api.aadrm.com` 最新のブラウザーによって信頼されている証明書の透明性のログに報告する、グローバルに信頼されたルート CA によって発行された新しい証明書をに更新 この変更が完了すると、予期したルート証明書に対して証明書の固定を実行しようとする RMS SDK のレガシバージョンは、その証明書を見つけることができず、接続に失敗します。  

## <a name="client-impact"></a>クライアントへの影響 

次の Microsoft アプリケーションでは、現時点で RMS Sdk を使用しています。 これらのプラットフォームで更新プログラムが利用可能になりました。デバイスは、12月の期限前に更新する必要があります。 

- Office Pro Plus/2019 for Mac バージョン16.40 以降。
- Office 2016 for Mac バージョン16.16.27 以降。
- Word、Excel、PowerPoint for iOS バージョン2.40.20071600 以降。
- Word、Excel、および PowerPoint for Android バージョン16.0.12827.20140 以降。

リソース 

- Android: https://www.microsoft.com/download/details.aspx?id=43673
- iOS: https://www.microsoft.com/download/details.aspx?id=43674 
- macOS: https://www.microsoft.com/download/details.aspx?id=43675 
- Linux: https://azuread.github.io/rms-sdk-for-cpp/annotated.html
