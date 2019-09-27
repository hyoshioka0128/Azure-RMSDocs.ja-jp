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
ms.openlocfilehash: 63991bd4528e5f28397aab837793ea3d167513a1
ms.sourcegitcommit: a091cabd5ad24b4534b5f69f029843037c7872d3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71314172"
---
# <a name="admin-guide-azure-information-protection-unified-labeling-client-files-and-client-usage-logging"></a>管理者ガイド: クライアントファイルとクライアントの使用状況ログの統合を Azure Information Protection する

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、WINDOWS 7 SP1、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012、windows Server 2008 r2*
>
> *手順:[Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection の統一されたラベル付けクライアントをインストールしたら、ファイルの場所を確認し、クライアントがどのように使用されているかを監視する必要があります。

## <a name="file-locations-for-the-azure-information-protection-client"></a>Azure Information Protection クライアントのファイルの場所

クライアント ファイル:   

- 64 ビット オペレーティング システムの場合: **\ProgramFiles (x86)\Microsoft Azure Information Protection**

- 32 ビット オペレーティング システムの場合: **\Program Files\Microsoft Azure Information Protection**

クライアントログファイル:

- 64ビットおよび32ビットのオペレーティングシステムの場合: **%localappdata%\Microsoft\MSIP\Logs**


## <a name="next-steps"></a>次の手順
Azure Information Protection 統合されたラベル付けクライアントに関連付けられているすべてのログファイルを確認したので、このクライアントのサポートに必要な追加情報については、次を参照してください。

- [カスタマイズ](clientv2-admin-guide-customizations.md)

- [サポートされるファイルの種類](clientv2-admin-guide-file-types.md)

- [PowerShell コマンド](clientv2-admin-guide-powershell.md)

