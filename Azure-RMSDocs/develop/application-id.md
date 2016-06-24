---
# required metadata

title: 方法&#58; Azure アプリケーション ID を取得する | Azure RMS
description: Microsoft Rights Management SDK 4.2 を使って RMS 対応アプリを作成するには、RMS チームとの契約を作成する必要があります。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0fe9dc-bc91-4018-b28d-2db293a3eaa2
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 方法: Azure アプリケーション ID を取得する

Microsoft Rights Management SDK 4.2 を使って RMS 対応アプリを作成するには、RMS チームとの契約を作成する必要があります。

## 概要

MS RMS SDK 4.2 を使って RMS 対応アプリを作成し、リリースするには、RMS チームとの間でサービスの使用に関する契約を作成することも必要になります。 Rights Management License Agreement (RMLA) とも呼ばれるこの契約に同意することは、アプリの動作 (ビジネス ルールへの準拠) によってユーザーまたはコンテンツ所有者に代わって遵守されるコンテンツ保護のための契約に同意することになります。 RMS 対応アプリケーションの作成者と RMS チームとの契約は、この契約を表し、アプリが Azure AD 認証サービスに接続できるようにする "Azure アプリケーション ID" の存在に基づいて実効性を持つことになります。

## 処理

アプリ ID を作成し、使用に関する RMS チームとの契約に署名するには、次の手順を使用します。

-   [Azure でアプリ ID を作成する方法](https://msdn.microsoft.com/en-us/library/azure/dn132599.aspx)に関するページのガイダンスに従ってアプリ ID を作成します。
-   "アプリ ID" を <askipteam@microsoft.com> に送信して、RMLA プロセスを開始することを RMS チームに連絡します。.
-   RMLA に署名し、RMS チームに返送します。
-   RMLA に署名したら、*clientID* パラメーターを介して認証ライブラリを呼び出すときにアプリケーション ID を渡します。

    「[iOS/OS X のコード例](ios-os-x-code-examples.md)」トピックから抜粋した認証呼び出しを次に示します。


    // Retrieve token using ADAL
        [context acquireTokenWithResource:authenticationParameters.resource
                                 clientId:appClientId
                              redirectUri:redirectURI
                                   userId:authenticationParameters.userId
                          completionBlock:^(ADAuthenticationResult *result)



**注**: RMS チームが署名済みの RMLA を 60 日以内に受け取らなかった場合、Azure 認証システムに対するアプリの認証はブロックされます。

 

 

 


<!--HONumber=Apr16_HO4-->


