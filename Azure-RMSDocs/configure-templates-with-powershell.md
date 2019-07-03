---
title: 保護テンプレート用の PowerShell - Azure Information Protection
description: Azure Portal で保護テンプレートを作成し、管理するためにできることはすべて、PowerShell を使用してコマンド ラインからも実行できます。 さらに、テナント間でテンプレートをコピーしたり、多言語の名前や説明などのテンプレートで複雑なプロパティの一括編集を実行できます。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 1e1e033ee900890431ed35faed5cca0171f86e38
ms.sourcegitcommit: a5f595f8a453f220756fdc11fd5d466c71d51963
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520996"
---
# <a name="powershell-reference-for-protection-templates"></a>保護テンプレート用の PowerShell リファレンス

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection の保護設定は、保護テンプレートに保存されます。 Azure Portal で保護設定を作成し、管理するためにできることはすべて、PowerShell を使用してコマンド ラインからも実行できます。 

さらに、保護テンプレートのエクスポートとインポートもできます。 これら 2 つの操作により、テナント間で保護テンプレートをコピーしたり、多言語の名前や説明などの複雑なプロパティを一括編集したりできるようになります。

エクスポートとインポートを使用して保護テンプレートをバックアップして復元することもできます。 テンプレートは定期的にバックアップすることをお勧めします。 これで、意図しない保護設定を変更してしまった場合でも、前のバージョンに簡単に戻すことができます。

インストール手順については、次を参照してください。 [AIPService PowerShell モジュールをインストールする](install-powershell.md)します。

保護テンプレートの作成および管理をサポートするコマンドレットは次のとおりです。

- [Add-AipServiceTemplate](/powershell/module/aipservice/add-aipservicetemplate)

- [Export-AipServiceTemplate](/powershell/module/aipservice/export-aipservicetemplate)

- [Get-AipServiceTemplate](/powershell/module/aipservice/get-aipservicetemplate)

- [Get-AipServiceTemplateProperty](/powershell/module/aipservice/get-aipservicetemplateproperty)

- [Import-AipServiceTemplate](/powershell/module/aipservice/import-aipservicetpd)

- [New-AipServiceRightsDefinition](/powershell/module/aipservice/new-aipservicerightsdefinition)

- [Remove-AipServiceTemplate](/powershell/module/aipservice/remove-aipservicetemplate)

- [セット AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty)



## <a name="see-also"></a>関連項目
[Azure Information Protection のテンプレートを構成して管理する](configure-policy-templates.md)

