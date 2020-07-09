---
title: FCI を使用する Windows ファイルサーバーのサポート Azure RMS-AIP
description: Office ドキュメントを自動的に保護する RMS コネクタを配置するときに、Windows Server ファイル分類インフラストラクチャがどのように Azure RMS で使用されるかについて説明します。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8fdad425-5daf-4ce1-822f-9d2fb0b87df1
ms.subservice: fci
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 7e0a586490b54c9fcb798f3d1a8776262ff6847c
ms.sourcegitcommit: 551e3f5b8956da49383495561043167597a230d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86136321"
---
# <a name="how-windows-file-servers-that-use-fci-support-azure-rights-management"></a>FCI を使用する Windows ファイルサーバーで Azure Rights Management をサポートする方法

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


ファイル分類インフラストラクチャを使用するように Windows Server を構成すると、このファイル サーバー リソース マネージャーの機能でローカル ファイルをスキャンし、機密データが含まれているかどうかを判断することができます。 この条件を満たすファイルには、管理者が定義する分類プロパティのタグが付けられます。 その後で、ファイル分類インフラストラクチャが分類に従って自動操作を実行できます。 これらのアクションの1つには、Azure Rights Management を使用した情報保護の適用と、Rights Management コネクタ (RMS コネクタとも呼ばれます) のデプロイが含まれます。 これにより Office ファイルは Azure RMS によって自動的に保護されます。

すべてのファイルの種類を保護する目的で、RMS コネクタを使用せずに、代わりに、[Azure Information Protection モジュール](./rms-client/client-admin-guide-powershell.md)でコマンドレットを使用する Windows PowerShell スクリプトを実行できます。

この分類ポリシーは、完全に構成可能で拡張性が高いので、承認されていないユーザーおよび承認されたユーザーからの潜在的なデータの漏えいを防止できます。 管理者がファイルにアクセスする必要がないようなポリシーを構成できるので、ネットワーク管理者からのデータ漏えいのリスクも減らすことができます。

Office ファイル用 RMS コネクタをデプロイして構成する手順については、「 [Azure Rights Management コネクタのデプロイ](deploy-rms-connector.md)」を参照してください。

すべてのファイルの種類に Windows PowerShell スクリプトを使用する方法については、「 [Windows Server ファイル分類インフラストラクチャでの RMS 保護 &#40;FCI&#41;](./rms-client/configure-fci.md)」を参照してください。



## <a name="next-steps"></a>次の手順
アプリケーションとサービスが Azure RMS をサポートする方法を理解したら、Rights Management のオンプレミス バージョンである Active Directory Rights Management サービス (AD RMS) と Azure RMS を比較してみることをお勧めします。 機能、要件、およびセキュリティ制御の比較については、「 [Azure Rights Management と AD RMS の比較](compare-on-premise.md)」を参照してください。


