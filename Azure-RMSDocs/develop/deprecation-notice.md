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
ms.openlocfilehash: 14ea411732b38883d278d4df22700b8503224be0
ms.sourcegitcommit: 307258ff0a8a7a3f607c8f47f38a9801d0e06ba1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2020
ms.locfileid: "85126647"
---
# <a name="rms-sdk-42-deprecation-notice"></a>RMS SDK 4.2 の非推奨の通知 

*2020年3月より前のすべての RMS SDK 4.2 バージョンリリースに適用可能*

2020年3月3日、Android、iOS、OSX 用の RMS SDK 4.2 の更新プログラムは、Microsoft ダウンロードセンターでリリースされました。 現時点では、これらの RMS SDK プラットフォームを使用するすべてのアプリケーションに対して、この更新プログラムは必須です。  

2020年9月15日2020より前にリリースされたバージョンの RMS SDK は、Azure Rights Management サービスエンドポイントへの接続に失敗します。 RMS SDK 4.2 を使用するアプリケーションは、この日付より前に更新する必要があります。 

## <a name="reason-for-change"></a>変更の理由 

以前のバージョンの RMS SDK は、証明書のピン留めを使用して、RMS 対応クライアントが RMS サービスと通信し、特定の予想されるルート CA にチェーンされている証明書を受信していることを確認します。  

最新のブラウザーでは、証明書の透過性ログを使用して、証明書が正当なドメイン所有者に発行されていること、および信頼されたルート証明機関によって証明書が発行されたことを確認  

最新のブラウザーをより適切にサポートするため、2020年9月15日より、Microsoft は、の証明書を、発行された証明書を `https://api.aadrm.com` 最新のブラウザーによって信頼されている証明書の透過性ログに報告する、グローバルに信頼されたルート CA によって発行された新しい証明書に この変更が完了すると、予期したルート証明書に対して証明書の固定を実行しようとする RMS SDK のレガシバージョンは、その証明書を見つけることができず、接続に失敗します。  

## <a name="client-impact"></a>クライアントへの影響 

次の Microsoft アプリケーションでは、現時点で RMS Sdk を使用しています。 これらのプラットフォームで更新プログラムが利用可能になり、9月の期限前にデバイスを更新する必要があります。 

- Office 2019 for Mac 
- Office 2016 for Mac 
- Word、Excel、および iOS 用 PowerPoint 
- Word、Excel、および Android 用 PowerPoint 

リソース 

- Android: https://www.microsoft.com/download/details.aspx?id=43673
- iOS: https://www.microsoft.com/download/details.aspx?id=43674 
- macOS: https://www.microsoft.com/download/details.aspx?id=43675 
- Linux: https://azuread.github.io/rms-sdk-for-cpp/annotated.html