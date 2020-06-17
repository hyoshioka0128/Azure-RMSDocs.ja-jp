---
title: クライアントファイルと使用状況ログの統合されたラベル付け Azure Information Protection
description: Windows 用のクライアントファイルに関する情報と、Azure Information Protection 統合されたラベル付けクライアントの使用状況ログ。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/13/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 46152c8f004f05a1c1ae317c0710e98be4a98121
ms.sourcegitcommit: 9277d126f67179264c54fe2bce8463fef9e0b422
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84802782"
---
# <a name="admin-guide-azure-information-protection-unified-labeling-client-files-and-client-usage-logging"></a>管理者ガイド: Azure Information Protection クライアントファイルとクライアント使用状況ログの統合

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012*
>
> **Windows 7 と Office 2010 向けに拡張された Microsoft サポートをご利用のお客様は、これらのバージョンの Azure Information Protection サポートを受けることもできます。詳細については、サポート担当者にお問い合わせください。*
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

