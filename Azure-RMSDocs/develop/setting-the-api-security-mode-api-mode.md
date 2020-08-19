---
title: API セキュリティ モードを設定する方法 | Azure RMS
description: IpcSetGlobalProperty 関数を使用して、ファイル API アプリケーションを実行するセキュリティモードを選択することによって、API セキュリティモードを設定する方法について説明します。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 942192690e06422246fa0ed7a4fb2d1d3ccf6cd6
ms.sourcegitcommit: dc50f9a6c2f66544893278a7fd16dff38eef88c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/18/2020
ms.locfileid: "88563602"
---
# <a name="how-to-set-the-api-security-mode"></a>方法: API セキュリティ モードの設定

[IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) 関数を使用して、File API アプリケーションをどのセキュリティ モードで実行するかを選択できます。

*サーバー モード*で実行するためにアプリケーションを初期化するには、[IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) 関数を呼び出し、セキュリティ モードを [IPC\_API\_MODE\_SERVER](https://msdn.microsoft.com/library/hh535236.aspx) に設定します。 既定では、アプリケーションは*クライアント モード* (**IPC\_API\_MODE\_CLIENT**) で実行されます。

*サーバー モード*の詳細については、「[Application types (アプリケーションの種類)](application-types.md)」を参照してください。

**重要**   他の Rights Management Services SDK 2.1 関数が呼び出される前に、セキュリティモードを設定する必要があります。 セキュリティ モードは、設定後に現在のプロセスに対して変更することはできません。

## <a name="related-topics"></a>関連トピック

* [アプリケーションの種類](application-types.md)
* [API mode values (API のモード値)](https://msdn.microsoft.com/library/hh535236.aspx)
* [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)
