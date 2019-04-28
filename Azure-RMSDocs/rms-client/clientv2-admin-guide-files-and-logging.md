---
title: Azure Information Protection の統合のラベル付けクライアント ファイルと使用状況ログ
description: クライアント ファイルと、Azure Information Protection の使用状況ログについては、Windows 用のラベル付けのクライアントを統合します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: f49495ae79dbd61e85406957c0fb7864be7116ac
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60181295"
---
# <a name="admin-guide-azure-information-protection-unified-labeling-client-files-and-client-usage-logging"></a>管理者ガイド: Azure Information Protection の統合のラベル付けクライアント ファイルとクライアント使用状況ログ

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*
>
> "*手順:[Azure Information Protection unified Windows 用のラベル付けのクライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection の統合されたラベル付けクライアントをインストールした後、ファイルの場所を把握し、クライアントの使用方法を監視する必要があります。

## <a name="file-locations-for-the-azure-information-protection-client"></a>Azure Information Protection クライアントのファイルの場所

クライアント ファイル:   

- 64 ビット オペレーティング システムの場合: **\ProgramFiles (x86)\Microsoft Azure Information Protection**

- 32 ビット オペレーティング システムの場合: **\Program Files\Microsoft Azure Information Protection**

クライアントのログ ファイル。

- 64 ビットおよび 32 ビット オペレーティング システムの場合: **%localappdata%\Microsoft\MSIP**


## <a name="next-steps"></a>次の手順
Azure Information Protection の統合されたラベル付けクライアントに関連付けられたすべてのログ ファイルを特定したら、これでは、このクライアントをサポートする必要があります追加については、次を参照してください。

- [カスタマイズ](clientv2-admin-guide-customizations.md)

- [サポートされるファイルの種類](clientv2-admin-guide-file-types.md)

- [PowerShell コマンド](clientv2-admin-guide-powershell.md)

