---
title: "Azure RMS カスタム テンプレート用の PowerShell - AIP"
description: "Azure クラシック ポータルで権限管理テンプレートを作成および管理するためにできることはすべて、PowerShell を使用してコマンド ラインからも実行できます。 また、テンプレートをエクスポートおよびインポートして、テナント間でテンプレートをコピーしたり、テンプレート内の複雑なプロパティ (多言語の名前や説明など) を一括編集したりできます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 8da24d00f6b6cb62bc745404e68e691b5afc2cb8
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2017
---
# <a name="powershell-reference-for-custom-templates"></a>カスタム テンプレート用の PowerShell リファレンス

>*適用対象: Azure Information Protection、Office 365*

Azure クラシック ポータルで権限管理テンプレートを作成および管理するためにできることはすべて、PowerShell を使用してコマンド ラインからも実行できます。 また、テンプレートをエクスポートおよびインポートして、テナント間でテンプレートをコピーしたり、テンプレート内の複雑なプロパティ (多言語の名前や説明など) を一括編集したりできます。

エクスポートとインポートを使用して、カスタム テンプレートをバックアップおよび復元することもできます。ベスト プラクティスとして、意図しない変更を行った場合に以前のバージョンに簡単に戻すことができるように、カスタム テンプレートを定期的にバックアップします。

> [!IMPORTANT]
> PowerShell を使用して Azure Rights Management テンプレートを作成および管理するには、[Azure RMS 用の Windows PowerShell モジュール](https://go.microsoft.com/fwlink/?LinkId=257721)のバージョン 2.0.0.0 以降が必要です。
> 
> 既にこの PowerShell モジュールがインストールされている場合は、PowerShell ウィンドウで次のコマンドを実行してバージョン番号を確認してください。`(Get-Module aadrm -ListAvailable).Version`

インストール手順については、「[Azure Rights Management 用 Windows PowerShell をインストールする](install-powershell.md)」を参照してください。

テンプレートの作成および管理をサポートするコマンドレットは次のとおりです。

- [Add-AadrmTemplate](/powershell/module/aadrm/add-aadrmtemplate)

- [Export-AadrmTemplate](/powershell/module/aadrm/export-aadrmtemplate)

- [Get-AadrmTemplate](/powershell/module/aadrm/get-aadrmtemplate)

- [Get-AadrmTemplateProperty](/powershell/module/aadrm/get-aadrmtemplateproperty)

- [Import-AadrmTemplate](/powershell/module/aadrm/import-aadrmtemplate)

- [New-AadrmRightsDefinition](/powershell/module/aadrm/new-aadrmrightsdefinition)

- [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate)

- [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty)



## <a name="see-also"></a>関連項目
[Azure Rights Management のカスタム テンプレートを構成する](configure-custom-templates.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]