---
title: FCI を使用する Windows ファイルサーバーのサポート Azure RMS-AIP
description: Office ドキュメントを自動的に保護する RMS コネクタを配置するときに、Windows Server ファイル分類インフラストラクチャがどのように Azure RMS で使用されるかについて説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8fdad425-5daf-4ce1-822f-9d2fb0b87df1
ms.subservice: fci
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 4e3c194be533adce625d1a15ad3fdfcd863da279
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97384334"
---
# <a name="how-windows-file-servers-that-use-fci-support-azure-rights-management"></a>FCI を使用する Windows ファイルサーバーで Azure Rights Management をサポートする方法

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連**: [Azure Information Protection Classic client for Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

ファイル分類インフラストラクチャを使用するように Windows Server を構成すると、このファイル サーバー リソース マネージャーの機能でローカル ファイルをスキャンし、機密データが含まれているかどうかを判断することができます。 

この条件を満たすファイルには、管理者が定義する分類プロパティのタグが付けられます。 その後で、ファイル分類インフラストラクチャが分類に従って自動操作を実行できます。 

これらのアクションの1つには、Azure Rights Management を使用した情報保護の適用と、Rights Management コネクタ (RMS コネクタとも呼ばれます) のデプロイが含まれます。 これにより Office ファイルは Azure RMS によって自動的に保護されます。

> [!TIP]
> すべてのファイルの種類を保護する目的で、RMS コネクタを使用せずに、代わりに、[Azure Information Protection モジュール](./rms-client/client-admin-guide-powershell.md)でコマンドレットを使用する Windows PowerShell スクリプトを実行できます。
> 

この分類ポリシーは、完全に構成可能で拡張性が高いので、承認されていないユーザーおよび承認されたユーザーからの潜在的なデータの漏えいを防止できます。 管理者がファイルにアクセスする必要がないようなポリシーを構成できるので、ネットワーク管理者からのデータ漏えいのリスクも減らすことができます。

Office ファイル用 RMS コネクタをデプロイして構成する手順については、「 [Azure Rights Management コネクタのデプロイ](deploy-rms-connector.md)」を参照してください。

すべてのファイルの種類に Windows PowerShell スクリプトを使用する方法については、「」を参照してください。 

- [Windows Server ファイル分類インフラストラクチャ &#40;FCI&#41;での RMS の保護 ](./rms-client/configure-fci.md)
- [ファイルサーバーリソースマネージャー FCI を使用した Azure RMS 保護用の Windows PowerShell スクリプト](rms-client/fci-script.md)


## <a name="next-steps"></a>次のステップ

アプリケーションとサービスが Azure RMS をサポートする方法を理解したら、Rights Management のオンプレミス バージョンである Active Directory Rights Management サービス (AD RMS) と Azure RMS を比較してみることをお勧めします。 機能、要件、およびセキュリティ制御の比較については、「 [Azure Rights Management と AD RMS の比較](compare-on-premise.md)」を参照してください。


