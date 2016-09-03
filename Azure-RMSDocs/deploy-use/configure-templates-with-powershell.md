---
title: "カスタム テンプレート用の PowerShell リファレンス |Azure RMS"
description: "Azure クラシック ポータルでテンプレートを作成および管理するためにできることはすべて、PowerShell を使用してコマンド ラインからも実行できます。 また、テンプレートをエクスポートおよびインポートして、テナント間でテンプレートをコピーしたり、テンプレート内の複雑なプロパティ (多言語の名前や説明など) を一括編集したりできます。"
author: cabailey
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 30ee2f77-ce16-4113-bcda-6089131849ec
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: 4874e6061bb9b8781fc2ad02c80dba38084f4747


---



# カスタム テンプレート用の PowerShell リファレンス

>*適用対象: Azure Rights Management、Office 365*

Azure クラシック ポータルでテンプレートを作成および管理するためにできることはすべて、PowerShell を使用してコマンド ラインからも実行できます。 また、テンプレートをエクスポートおよびインポートして、テナント間でテンプレートをコピーしたり、テンプレート内の複雑なプロパティ (多言語の名前や説明など) を一括編集したりできます。

エクスポートとインポートを使用して、カスタム テンプレートをバックアップおよび復元することもできます。ベスト プラクティスとして、意図しない変更を行った場合に以前のバージョンに簡単に戻すことができるように、カスタム テンプレートを定期的にバックアップします。

> [!IMPORTANT]
> Windows PowerShell を使用して Azure RMS 権限ポリシー テンプレートを作成および管理するには、 [Azure RMS 用の Windows PowerShell モジュール](http://go.microsoft.com/fwlink/?LinkId=257721)のバージョン 2.0.0.0 以降が必要です。
> 
> 既にこの PowerShell モジュールがインストールされている場合は、PowerShell ウィンドウで次のコマンドを実行してバージョン番号を確認してください。 `(Get-Module aadrm -ListAvailable).Version`

インストール手順については、「[Azure Rights Management 用 Windows PowerShell をインストールする](install-powershell.md)」を参照してください。

テンプレートの作成および管理をサポートするコマンドレットは次のとおりです。

-   [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx)

-   [Expまたはt-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx)

-   [Get-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727079.aspx)

-   [Get-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727081.aspx)

-   [Impまたはt-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx)

-   [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx)

-   [Remove-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727082.aspx)

-   [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx)



## 関連項目
[Azure Rights Management のカスタム テンプレートを構成する](configure-custom-templates.md)


<!--HONumber=Aug16_HO4-->


