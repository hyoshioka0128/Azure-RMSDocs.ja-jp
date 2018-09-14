---
title: API セキュリティ モードを設定する方法 | Azure RMS
description: File API アプリケーションをどのセキュリティ モードで実行するかを選択します。
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: d88656d966bc551fb5513a9e67d02b6a5c2d9fb2
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2018
ms.locfileid: "44151318"
---
# <a name="how-to-set-the-api-security-mode"></a>方法: API セキュリティ モードの設定

[IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) 関数を使用して、File API アプリケーションをどのセキュリティ モードで実行するかを選択できます。

*サーバー モード*で実行するためにアプリケーションを初期化するには、[IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) 関数を呼び出し、セキュリティ モードを [IPC\_API\_MODE\_SERVER](https://msdn.microsoft.com/library/hh535236.aspx) に設定します。 既定では、アプリケーションは*クライアント モード* (**IPC\_API\_MODE\_CLIENT**) で実行されます。

*サーバー モード*の詳細については、「[Application types (アプリケーションの種類)](application-types.md)」を参照してください。

**重要**: セキュリティ モードは、他の Rights Management サービス SDK 2.1 関数を呼び出す前に設定する必要があります。 セキュリティ モードは、設定後に現在のプロセスに対して変更することはできません。

## <a name="related-topics"></a>関連項目

* [アプリケーションの種類](application-types.md)
* [API mode values (API のモード値)](https://msdn.microsoft.com/library/hh535236.aspx)
* [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)
