---
title: 保護テンプレート用の PowerShell - Azure Information Protection
description: PowerShell コマンドレットを使用して、Azure Information Protection の保護テンプレートを追加、取得、エクスポート、インポート、削除、および構成します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 0188b757dc1f09fb3d153fe3430d9da6185e6836
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382906"
---
# <a name="powershell-reference-for-protection-templates"></a>保護テンプレート用の PowerShell リファレンス

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連**: [Windows 用のクラシッククライアント Azure Information Protection](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)ます。 統一されたラベル付けクライアントについては、Microsoft 365 のドキュメントの「 [秘密度ラベルについて](/microsoft-365/compliance/sensitivity-labels) 」を参照してください。 *

> [!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。
>

Azure Information Protection の保護設定は、保護テンプレートに保存されます。 Azure Portal で保護設定を作成し、管理するためにできることはすべて、PowerShell を使用してコマンド ラインからも実行できます。 

さらに、保護テンプレートのエクスポートとインポートもできます。 これら 2 つの操作により、テナント間で保護テンプレートをコピーしたり、多言語の名前や説明などの複雑なプロパティを一括編集したりできるようになります。

エクスポートとインポートを使用して保護テンプレートをバックアップして復元することもできます。 テンプレートは定期的にバックアップすることをお勧めします。 これで、意図しない保護設定を変更してしまった場合でも、前のバージョンに簡単に戻すことができます。

インストール手順については、「 [AIPService PowerShell モジュールのインストール](install-powershell.md)」を参照してください。

保護テンプレートの作成および管理をサポートするコマンドレットは次のとおりです。

- [AipServiceTemplate を追加します。](/powershell/module/aipservice/add-aipservicetemplate)

- [Export-AipServiceTemplate](/powershell/module/aipservice/export-aipservicetemplate)

- [Get-AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate)

- [Get-AipServiceTemplateProperty](/powershell/module/aipservice/get-aipservicetemplateproperty)

- [インポート-AipServiceTemplate](/powershell/module/aipservice/import-aipservicetpd)

- [AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition)

- [-AipServiceTemplate を削除します。](/powershell/module/aipservice/remove-aipservicetemplate)

- [Set-AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty)

## <a name="see-also"></a>参照
[Azure Information Protection のテンプレートを構成して管理する](configure-policy-templates.md)

