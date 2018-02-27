---
title: "Azure RMS カスタム テンプレート用の PowerShell - AIP"
description: "Azure Portal で権限管理テンプレートを作成し、管理するためにできることはすべて、PowerShell を使用してコマンド ラインからも実行できます。 また、テンプレートをエクスポートおよびインポートして、テナント間でテンプレートをコピーしたり、テンプレート内の複雑なプロパティ (多言語の名前や説明など) を一括編集したりできます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d8e31eb4f573a149ae39c32c89607775de61bfce
ms.sourcegitcommit: 31c79d948ec3089a4dc65639f1842c07c7aecba6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2018
---
# <a name="powershell-reference-for-custom-templates"></a>カスタム テンプレート用の PowerShell リファレンス

>*適用対象: Azure Information Protection、Office 365*

Azure Portal でテンプレートを作成し、管理するためにできることはすべて、PowerShell を使用してコマンド ラインからも実行できます。 また、テンプレートをエクスポートおよびインポートして、テナント間でテンプレートをコピーしたり、テンプレート内の複雑なプロパティ (多言語の名前や説明など) を一括編集したりできます。

エクスポートとインポートを使用して、カスタム テンプレートをバックアップおよび復元することもできます。ベスト プラクティスとして、意図しない変更を行った場合に以前のバージョンに簡単に戻すことができるように、カスタム テンプレートを定期的にバックアップします。

> [!IMPORTANT]
> PowerShell を使用して Azure Rights Management テンプレートを作成および管理するには、[Azure RMS 用の Windows PowerShell モジュール](https://go.microsoft.com/fwlink/?LinkId=257721)のバージョン 2.0.0.0 以降が必要です。
> 
> 既にこの PowerShell モジュールがインストールされている場合は、PowerShell ウィンドウで次のコマンドを実行してバージョン番号を確認してください。`(Get-Module aadrm -ListAvailable).Version`

インストール手順については、「[AADRM PowerShell モジュールのインストール](install-powershell.md)」を参照してください。

テンプレートの作成および管理をサポートするコマンドレットは次のとおりです。

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

[!INCLUDE[Commenting house rules](../includes/houserules.md)]