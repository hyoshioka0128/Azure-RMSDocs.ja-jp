---
title: "API セキュリティ モードを設定する方法 | Azure RMS"
description: "File API アプリケーションをどのセキュリティ モードで実行するかを選択します。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 77e2dfe7f2afb1e70de658850f83f86e9224aea6
ms.openlocfilehash: 9235fa1c194162689b854493ea31e76c08c40ce7


---

# 方法: API セキュリティ モードの設定

[IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) 関数を使用して、File API アプリケーションをどのセキュリティ モードで実行するかを選択できます。

*サーバー モード*で実行するためにアプリケーションを初期化するには、[IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) 関数を呼び出し、セキュリティ モードを [IPC\_API\_MODE\_SERVER](https://msdn.microsoft.com/library/hh535236.aspx) に設定します。 既定では、アプリケーションは*クライアント モード* (**IPC\_API\_MODE\_CLIENT**) で実行されます。

*サーバー モード*の詳細については、「[Application types (アプリケーションの種類)](application-types.md)」を参照してください。

**重要**: セキュリティ モードは、他の Rights Management サービス SDK 2.1 関数を呼び出す前に設定する必要があります。 セキュリティ モードは、設定後に現在のプロセスに対して変更することはできません。

## 関連項目

* [アプリケーションの種類](application-types.md)
* [API mode values (API のモード値)](https://msdn.microsoft.com/library/hh535236.aspx)
* [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)
 

 



<!--HONumber=Oct16_HO3-->


