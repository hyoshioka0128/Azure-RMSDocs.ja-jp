---
title: クライアントファイルと使用状況ログの統合されたラベル付け Azure Information Protection
description: Windows 用のクライアントファイルに関する情報と、Azure Information Protection 統合されたラベル付けクライアントの使用状況ログ。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/26/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 8e2b6d0b3e0436800cd73959107bd544dae348b0
ms.sourcegitcommit: 47d5765e1b76309a81aaf5e660256f2fb30eb2b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72805585"
---
# <a name="admin-guide-azure-information-protection-unified-labeling-client-files-and-client-usage-logging"></a>管理者ガイド: Azure Information Protection クライアントファイルとクライアント使用状況ログの統合

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、WINDOWS 7 SP1、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012、windows Server 2008 r2*
>
> *手順: [Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection の統一されたラベル付けクライアントをインストールしたら、ファイルの場所を確認し、クライアントがどのように使用されているかを監視する必要があります。

## <a name="file-locations-for-the-azure-information-protection-unified-labeling-client"></a>Azure Information Protection 統合ラベル付けクライアントのファイルの場所

クライアント ファイル:   

- 64 ビット オペレーティング システムの場合: **\ProgramFiles (x86)\Microsoft Azure Information Protection**

- 32 ビット オペレーティング システムの場合: **\Program Files\Microsoft Azure Information Protection**

クライアントログファイルと現在インストールされているポリシーファイル:

- 64 ビットおよび 32 ビット オペレーティング システムの場合: **%localappdata%\Microsoft\MSIP**


## <a name="usage-logging-for-the-azure-information-protection-unified-labeling-client"></a>Azure Information Protection 統合ラベル付けクライアントの使用状況ログ

統一されたラベル付けクライアントは、ユーザーアクティビティをローカルの Windows イベントログに記録しません。 代わりに、Azure Information Protection の[中央レポート](../reports-aip.md)機能を使用します。 


## <a name="next-steps"></a>次のステップ
Azure Information Protection 統合されたラベル付けクライアントに関連付けられているすべてのログファイルを確認したので、このクライアントのサポートに必要な追加情報については、次を参照してください。

- [カスタマイズ](clientv2-admin-guide-customizations.md)

- [サポートされるファイルの種類](clientv2-admin-guide-file-types.md)

- [PowerShell コマンド](clientv2-admin-guide-powershell.md)

