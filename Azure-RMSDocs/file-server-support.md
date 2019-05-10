---
title: Windows ファイルの Azure RMS の AIP の FCI サポートを使用するサーバー
description: Office ドキュメントを自動的に保護する RMS コネクタを配置するときに、Windows Server ファイル分類インフラストラクチャがどのように Azure RMS で使用されるかについて説明します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 12/12/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8fdad425-5daf-4ce1-822f-9d2fb0b87df1
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 474080f712e49baf1fc4952495eee8f3da475666
ms.sourcegitcommit: f9077101a974459a4252e763b5fafe51ff15a16f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64767623"
---
# <a name="how-windows-file-servers-that-use-fci-support-azure-rights-management"></a>Windows ファイルの FCI サポート Azure Rights Management を使用するサーバー

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


ファイル分類インフラストラクチャを使用するように Windows Server を構成すると、このファイル サーバー リソース マネージャーの機能でローカル ファイルをスキャンし、機密データが含まれているかどうかを判断することができます。 この条件を満たすファイルには、管理者が定義する分類プロパティのタグが付けられます。 その後で、ファイル分類インフラストラクチャが分類に従って自動操作を実行できます。 これらの操作には、Azure Rights Management を使用した情報保護の適用や Rights Management コネクタ (RMS コネクタとも呼びます) のデプロイなどがあります。 これにより Office ファイルは Azure RMS によって自動的に保護されます。

すべてのファイルの種類を保護する目的で、RMS コネクタを使用せずに、代わりに、[Azure Information Protection モジュール](./rms-client/client-admin-guide-powershell.md)でコマンドレットを使用する Windows PowerShell スクリプトを実行できます。

この分類ポリシーは、完全に構成可能で拡張性が高いので、承認されていないユーザーおよび承認されたユーザーからの潜在的なデータの漏えいを防止できます。 管理者がファイルにアクセスする必要がないようなポリシーを構成できるので、ネットワーク管理者からのデータ漏えいのリスクも減らすことができます。

Office ファイル用 RMS コネクタをデプロイおよび構成する方法については、「[Azure Rights Management コネクタをデプロイする](deploy-rms-connector.md)」を参照してください。

すべてのファイルの種類に Windows PowerShell スクリプトを使用する方法については、「[Windows Server ファイル分類インフラストラクチャ &#40;FCI&#41; での RMS の保護](./rms-client/configure-fci.md)」を参照してください。



## <a name="next-steps"></a>次の手順
アプリケーションとサービスが Azure RMS をサポートする方法を理解したら、Rights Management のオンプレミス バージョンである Active Directory Rights Management サービス (AD RMS) と Azure RMS を比較してみることをお勧めします。 機能、要件、およびセキュリティ制御の比較については、「[Azure Rights Management と AD RMS を比較する](compare-on-premise.md)」を参照してください。


