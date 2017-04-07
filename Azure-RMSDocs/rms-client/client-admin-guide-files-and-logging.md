---
title: "Azure Information Protection クライアント ファイルと使用状況ログ"
description: "Windows 用 Azure Information Protection クライアントのクライアント ファイルと使用状況ログについて説明します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5a34ab85-773f-4782-ba09-c321cddf5bc0
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 78c355acd1bc87347ef2d4b02ffbb24f2c08bc70
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="azure-information-protection-client-files-and-client-usage-logging"></a>Azure Information Protection クライアントのファイルとクライアント使用状況ログ

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*

Azure Information Protection クライアントをインストールした後、どこにファイルがあるかを知り、クライアントがどのように使われているのかを監視することが必要になる場合があります。

## <a name="file-locations-for-the-azure-information-protection-client"></a>Azure Information Protection クライアントのファイルの場所

クライアント ファイル:    

- 64 ビット オペレーティング システムの場合: **\ProgramFiles (x86)\Microsoft Azure Information Protection**

- 32 ビット オペレーティング システムの場合: **\Program Files\Microsoft Azure Information Protection**

クライアント ログ ファイルと現在インストールされているポリシー ファイル:

- 64 ビットおよび 32 ビット オペレーティング システムの場合: **%localappdata%\Microsoft\MSIP**

## <a name="usage-logging-for-the-azure-information-protection-client"></a>Azure Information Protection クライアントの使用状況ログ

クライアントは、ユーザー アクティビティをローカル Windows イベント ログの **[アプリケーションとサービス]** の **[Azure Information Protection]** に記録します。 イベントには次の情報が含まれます。

- 日付、クライアントのバージョン、ポリシー ID

- サインインしたユーザー名、コンピューター名

- ファイル名と場所

- 操作:

    - ラベルの設定: 情報 ID 101
    
    - ラベルの設定 (下位): 情報 ID 102
    
    - ラベルの設定 (上位): 情報 ID 103
    
    - ラベルの削除: 情報 ID 104
   
    - 推奨されるヒント: 情報 ID 105
    
    - カスタム保護の適用: 情報 ID 201
    
    - カスタム保護の削除: 情報 ID 202
    
    - サインイン (操作): 情報 ID 902
    
    - ポリシーのダウンロード (操作): 情報 ID 901
    
- 操作ソース:
    
    - 手動 
    
    - 推奨
    
    - 自動  
    
    - システム (サインインおよびダウンロードポリシー用)
    
- 操作前後のラベル 
    
- 操作前後の保護
    
- ユーザーの理由 (該当する場合)
    

Azure Rights Management サービスの使用状況ログについては、「[Azure Rights Management サービスの使用状況をログに記録して分析する](../deploy-use/log-analyze-usage.md)」をご覧ください。



## <a name="next-steps"></a>次のステップ
Azure Information Protection クライアントに関連付けられているすべてのログ ファイルがわかったので、このクライアントのサポートに必要な追加情報を以下の記事でご覧ください。


- [ドキュメント追跡](client-admin-guide-document-tracking.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
