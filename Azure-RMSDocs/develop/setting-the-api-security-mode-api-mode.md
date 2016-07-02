---
title: "API セキュリティ モードを設定する方法 | Azure RMS"
description: "File API アプリケーションをどのセキュリティ モードで実行するかを選択します。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 11b998addd14fdde0592ed948b956ddb2ed6e570
ms.openlocfilehash: 2be40c9caf33f391f8be9fe116d3473ce995613b


---

# 方法: API セキュリティ モードの設定

[**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) 関数を使用して、File API アプリケーションをどのセキュリティ モードで実行するかを選択できます。

*サーバー モード*で実行するためにアプリケーションを初期化するには、[**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) 関数を呼び出し、セキュリティ モードを [**IPC\_API\_MODE\_SERVER**](/rights-management/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER) に設定します。 既定では、アプリケーションは*クライアント モード* (**IPC\_API\_MODE\_CLIENT**) で実行されます。

*サーバー モード*の詳細については、「[Application types (アプリケーションの種類)](application-types.md)」を参照してください。

**重要**: セキュリティ モードは、他の Rights Management サービス SDK 2.1 関数を呼び出す前に設定する必要があります。 セキュリティ モードは、設定後に現在のプロセスに対して変更することはできません。

## 関連項目

* [アプリケーションの種類](application-types.md)
* [**API mode values (API のモード値)**](/rights-management/sdk/2.1/api/win/api%20mode%20values#msipc_api_mode_values_IPC_API_MODE_SERVER)
* [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)
 

 



<!--HONumber=Jun16_HO4-->


