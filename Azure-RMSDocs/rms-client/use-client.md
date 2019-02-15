---
title: Azure Information Protection クライアント
description: Microsoft Azure Information Protection は、組織のデータを保護するクライアント/サーバー型のソリューションです。 クライアント (Azure Information Protection クライアントまたは Rights Management クライアント) は、コンピューターおよびモバイル デバイスで実行するアプリケーションに統合されます。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/19/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a6fa85be-f92a-4e00-9efc-9dbfd4dfbfcb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 878d00d941a85f62982d9e23db36da8c5ad70078
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2019
ms.locfileid: "56251842"
---
# <a name="the-client-side-of-azure-information-protection"></a>クライアント側での Azure Information Protection

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*

Azure Information Protection は、組織の文書や電子メールを保護するクライアント/サーバー型のソリューションです。

- クライアントは、Azure Information Protection クライアントまたは Rights Management クライアントで、コンピューターやモバイル デバイスで実行するアプリケーションと統合されます。 

- サービスはクラウド (データの保護に Azure Rights Management サービスを使用する Azure Information Protection) または、オンプレミス (Active Directory Rights Management サービス) にあります。 

Azure Information Protection クライアントは、保護に加え、分類およびラベル付けも行います。 このクライアントは Office アプリケーションと統合できますが、別にインストールする必要があります。

Rights Management (RMS) クライアントは、Office アプリケーション、Azure Information Protection クライアント、ソフトウェア ベンダー製の RMS 対応アプリケーションなど、一部のアプリケーションと共に自動的にインストールされます。 ただし、開発者が Rights Management 保護を基幹業務アプリケーションに統合する場合などは単体インストールを実行できます。

組織のデータを保護する Azure Information Protection および Active Directory Rights Management サービスと一緒に使用する、これらのクライアントのデプロイ方法と使用方法の詳細については、次のドキュメントを参照してください。

- [Azure Information Protection クライアント](AIP-client.md)

- [RMS クライアントのデプロイに関する注意事項](client-deployment-notes.md)

- [Windows Server ファイル分類インフラストラクチャ (FCI) での RMS の保護](configure-fci.md)


## <a name="see-also"></a>関連項目
[Azure Information Protection と AD RMS の比較](../compare-on-premise.md)
