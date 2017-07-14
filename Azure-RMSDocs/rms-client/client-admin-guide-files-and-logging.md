---
title: "Azure Information Protection クライアント ファイルと使用状況ログ"
description: "Windows 用 Azure Information Protection クライアントのクライアント ファイルと使用状況ログについて説明します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5a34ab85-773f-4782-ba09-c321cddf5bc0
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: bf695772d545daca602903e156903da2aadaae7a
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2017
---
# Azure Information Protection クライアントのファイルとクライアント使用状況ログ
<a id="azure-information-protection-client-files-and-client-usage-logging" class="xliff"></a>

>*適用対象: Active Directory Rights Management Services、Azure Information Protection、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012*

Azure Information Protection クライアントをインストールした後、どこにファイルがあるかを知り、クライアントがどのように使われているのかを監視することが必要になる場合があります。

## Azure Information Protection クライアントのファイルの場所
<a id="file-locations-for-the-azure-information-protection-client" class="xliff"></a>

クライアント ファイル:   

- 64 ビット オペレーティング システムの場合: **\ProgramFiles (x86)\Microsoft Azure Information Protection**

- 32 ビット オペレーティング システムの場合: **\Program Files\Microsoft Azure Information Protection**

クライアント ログ ファイルと現在インストールされているポリシー ファイル:

- 64 ビットおよび 32 ビット オペレーティング システムの場合: **%localappdata%\Microsoft\MSIP**

## Azure Information Protection クライアントの使用状況ログ
<a id="usage-logging-for-the-azure-information-protection-client" class="xliff"></a>

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



## 次のステップ
<a id="next-steps" class="xliff"></a>
Azure Information Protection クライアントに関連付けられているすべてのログ ファイルがわかったので、このクライアントのサポートに必要な追加情報を以下の記事でご覧ください。

- [カスタマイズ](client-admin-guide-customizations.md)

- [ドキュメント追跡](client-admin-guide-document-tracking.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
