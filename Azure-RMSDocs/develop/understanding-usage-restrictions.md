---
# required metadata

title: 使用制限について | Azure RMS
description:
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 361bbc29-821f-4577-ace6-0aec799039a9

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿# 使用制限について

すべての RMS 対応アプリケーションは、使用制限を適用する必要があります。 使用制限とは、ユーザーが操作 (例: ドキュメントの印刷) を実行しようとしたが、 その操作を実行するための権限 (例: 印刷権限) がドキュメントの RMS ポリシーによって付与されていない 状態です。

ドキュメントに対するユーザーのアクセス許可は、[**IpcAccessCheck**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcaccesscheck) 機能を使用して照会できます。

## 使用制限について

-   標準の RMS 権限について理解する

    アプリケーションに適用できるすべての RMS 権限については、「[Usage restriction reference (使用制限のリファレンス)](usage-restriction-reference.md)」を参照してください。

    アプリケーションで定義される権限は状況に固有のもので、それを超える場合は標準の RMS 権限が作成されることがあります。

-   使用制限の強制ポイントを特定する

    *使用制限の強制ポイント*とは、アプリケーションの制御フロー内で使用制限を強制する必要がある場所です。 「[Usage restriction reference (使用制限のリファレンス)](usage-restriction-reference.md)」のトピックに、一般的な強制ポイントの例がいくつか紹介されています。

    独自のアプリケーションを評価して、どの使用制限の強制ポイントを適用するかを判断します。

    「[Usage restriction reference (使用制限のリファレンス)](usage-restriction-reference.md)」で説明されているすべての強制ポイントが必要なわけではありません。 たとえば、アプリケーションがコンテンツの印刷をユーザーに許可していない場合は、**IPC\_GENERIC\_PRINT** 権限についてチェックする必要はありません。

-   各強制ポイントでアクセス権のチェックを実行するように、コードを更新します。

    特定の権限の適用方法については、「[Usage restriction reference (使用制限のリファレンス)](usage-restriction-reference.md)」を参照してください。

### 関連項目

* [開発者の概念](ad-rms-concepts-nav.md)
* [**IpcAccessCheck**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcaccesscheck)
* [使用制限のリファレンス](usage-restriction-reference.md)
 

 





<!--HONumber=Apr16_HO3-->


