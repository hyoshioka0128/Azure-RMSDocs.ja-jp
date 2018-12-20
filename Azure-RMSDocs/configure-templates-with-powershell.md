---
title: 保護テンプレート用の PowerShell - Azure Information Protection
description: Azure Portal で保護テンプレートを作成し、管理するためにできることはすべて、PowerShell を使用してコマンド ラインからも実行できます。 また、テンプレートをエクスポートおよびインポートして、テナント間でテンプレートをコピーしたり、テンプレート内の複雑なプロパティ (多言語の名前や説明など) を一括編集したりできます。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/12/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ee40d0c742695d449fd807f364e87d9c30f6079f
ms.sourcegitcommit: 1d2912b4f0f6e8d7596cbf31e2143a783158ab11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2018
ms.locfileid: "53304963"
---
# <a name="powershell-reference-for-protection-templates"></a>保護テンプレート用の PowerShell リファレンス

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection の保護設定は、保護テンプレートに保存されます。 Azure Portal で保護設定を作成し、管理するためにできることはすべて、PowerShell を使用してコマンド ラインからも実行できます。 

さらに、保護テンプレートのエクスポートとインポートもできます。 これら 2 つの操作により、テナント間で保護テンプレートをコピーしたり、多言語の名前や説明などの複雑なプロパティを一括編集したりできるようになります。

エクスポートとインポートを使用して保護テンプレートをバックアップして復元することもできます。 テンプレートは定期的にバックアップすることをお勧めします。 これで、意図しない保護設定を変更してしまった場合でも、前のバージョンに簡単に戻すことができます。

インストール手順については、「[AADRM PowerShell モジュールのインストール](install-powershell.md)」を参照してください。

保護テンプレートの作成および管理をサポートするコマンドレットは次のとおりです。

- [Add-AadrmTemplate](/powershell/module/aadrm/add-aadrmtemplate)

- [Export-AadrmTemplate](/powershell/module/aadrm/export-aadrmtemplate)

- [Get-AadrmTemplate](/powershell/module/aadrm/get-aadrmtemplate)

- [Get-AadrmTemplateProperty](/powershell/module/aadrm/get-aadrmtemplateproperty)

- [Import-AadrmTemplate](/powershell/module/aadrm/import-aadrmtemplate)

- [New-AadrmRightsDefinition](/powershell/module/aadrm/new-aadrmrightsdefinition)

- [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate)

- [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty)



## <a name="see-also"></a>参照
[Azure Information Protection のテンプレートを構成して管理する](configure-policy-templates.md)

