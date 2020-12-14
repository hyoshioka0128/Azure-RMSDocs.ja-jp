---
title: クラシッククライアントファイルと使用状況ログの Azure Information Protection
description: クラシッククライアントファイルと、Windows 用の Azure Information Protection クラシッククライアントの使用状況ログについて説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/29/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5a34ab85-773f-4782-ba09-c321cddf5bc0
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 3188392475a9da39f4187c30014ecc189248fd28
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97386119"
---
# <a name="admin-guide-azure-information-protection-classic-client-files-and-client-usage-logging"></a>管理者ガイド: Azure Information Protection 従来のクライアントファイルとクライアントの使用状況ログ

>***適用対象**: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8、Windows Server 2019、Windows Server 2016、windows Server 2012 R2、windows server 2012 *
>
>***関連**: [Azure Information Protection Classic client for Windows](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

> [!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Azure Information Protection クラシッククライアントをインストールしたら、ファイルの場所を確認し、クライアントがどのように使用されているかを監視する必要があります。

## <a name="file-locations-for-the-azure-information-protection-client"></a>Azure Information Protection クライアントのファイルの場所

クライアント ファイル:    

- 64 ビット オペレーティング システムの場合: **\ProgramFiles (x86)\Microsoft Azure Information Protection**

- 32 ビット オペレーティング システムの場合: **\Program Files\Microsoft Azure Information Protection**

クライアント ログ ファイルと現在インストールされているポリシー ファイル:

- 64 ビットおよび 32 ビット オペレーティング システムの場合: **%localappdata%\Microsoft\MSIP**

## <a name="usage-logging-for-the-azure-information-protection-classic-client"></a>Azure Information Protection クラシッククライアントの使用状況ログ

クライアントは、ローカルの Windows イベントログの **[アプリケーションとサービスログ**] Azure Information Protection にユーザーアクティビティを記録し  >  ます。 イベントには次の情報が含まれます。

- クライアントのバージョン、ポリシー ID

- サインインしたユーザーの IP アドレス

- ファイル名と場所

- アクション:

    - ラベルの設定: 情報 ID 101
    
    - ラベルの設定 (下): 情報 ID 102
    
    - ラベルの設定 (上位): 情報 ID 103
    
    - ラベルの削除: 情報 ID 104
    
    - 推奨ラベルのヒント: 情報105
    
    - カスタム保護の適用: 情報 ID 201
    
    - カスタム保護の削除: 情報 ID 202
    
    - Outlook の警告メッセージ: 情報 ID 301
    
    - Outlook でメッセージを表示する: 情報 ID 302
    
    - Outlook ブロックメッセージ: 情報 ID 303
    
    - サインイン (操作): 情報 ID 902
    
    - ポリシーのダウンロード (操作): 情報 ID 901
    
- 操作ソース:
    
    - 手動 
    
    - 推奨
    
    - 自動  
    
    - システム (サインインおよびダウンロードポリシー用)
    
    - Default
    
- 操作前後のラベル 
    
- 操作前後の保護
    
- ユーザーの理由 (該当する場合)

- 指定したユーザー、グループ、または組織の[エンコーディング名に基づく使用権限](../configure-usage-rights.md#usage-rights-and-descriptions)が含まれるカスタム アクセス許可 (該当する場合)

Outlook の警告、ブロック、およびブロックメッセージのイベントには、高度なクライアント設定が必要です。 詳細については、「[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](client-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)」を参照してください。


## <a name="next-steps"></a>次のステップ
Azure Information Protection クライアントに関連付けられているすべてのログ ファイルがわかったので、このクライアントのサポートに必要な追加情報を以下の記事でご覧ください。

- [カスタマイズ](client-admin-guide-customizations.md)

- [ドキュメント追跡](client-admin-guide-document-tracking.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)

