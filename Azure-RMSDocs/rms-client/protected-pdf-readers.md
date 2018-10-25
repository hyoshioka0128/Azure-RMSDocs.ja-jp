---
title: Microsoft Information Protection の保護された PDF Reader
description: ''
keywords: ''
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/13/2018
ms.topic: article
ms.prod: azure
ms.service: information-protection
ms.assetid: aab59e02-930b-4a17-8442-2d5d081fe1a6
ms.reviewer: kartikka
ms.suite: ems
ms.openlocfilehash: ab3d141394a9a042a8a3e15e35d1daffab20ad98
ms.sourcegitcommit: 1e6394044d646278ae582c7713cac8ffb9bf4c1e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2018
ms.locfileid: "49170249"
---
# <a name="supported-pdf-readers-for-microsoft-information-protection"></a>Microsoft Information Protection のサポートされる PDF Reader

以下の情報を使って、分類と保護に対するラベルが付けられた PDF ドキュメントの詳細についてと、これらのドキュメントを表示する方法を学習します。

Microsoft と Adobe のコラボレーションによって、分類され、必要に応じて保護されている PDF ドキュメントにより簡単で一貫した操作を提供します。 このコラボレーションでは、[Azure Information Protection](../what-is-information-protection.md) など、Microsoft Information Protection ソリューションとの Adobe Acrobat のネイティブ統合がサポートされます。 

このネイティブ統合には次の利点があります。

- 機密情報が含まれるために保護されている PDF ドキュメントを表示できます。

- ドキュメントに適用されている組織のラベルに対する分類の値を表示できます。

- PDF の暗号化における ISO 標準をサポートします。
    
    この保護された PDF ファイル形式は、[管理者によって有効にされる](client-admin-guide-customizations.md#protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)必要があります。 この構成が行われると、ファイル名拡張子は .pdf のまま保持され、.ppdf に変更されません。

詳細については、「[Starting October, use Adobe Acrobat Reader for PDFs protected by Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Starting-October-use-Adobe-Acrobat-Reader-for-PDFs-protected-by/ba-p/262738)」 (10 月以降、Microsoft Information Protection で保護されている PDF に Adobe Acrobat Reader を使用する) のブログ記事を参照してください

## <a name="supported-pdf-readers"></a>サポートされる PDF Reader

次の PDF Reader では、PDF の暗号化における ISO 標準に従う、保護された PDF ファイルを開くことができます。

|オペレーティング システム|サポートされるリーダーとダウンロード リンク|
|----------------|-----------------------------------|
|Windows 10 と以前のバージョン<br />から Windows 7 Service Pack 1|Adobe Acrobat Reader (推奨):<br />-  [Adobe の一般使用条件を参照する](https://www.adobe.com/legal/terms.html) <br />- [プレビューをダウンロードする](https://ardownload2.adobe.com/pub/adobe/reader/win/AcrobatDC/misc/MIP_Preview/1900820120/Adobe_MIP_Preview_1900820120.zip) <br /><br /> Azure Information Protection ビューアー: [ダウンロード](https://go.microsoft.com/fwlink/?linkid=838993)<br /><br />Foxit Reader: [ダウンロード](https://www.foxitsoftware.com/pdf-reader/)|
|Android|Azure Information Protection アプリ: [ダウンロード](https://go.microsoft.com/fwlink/?LinkId=325340)|
|iOS|Azure Information Protection アプリ: [ダウンロード](https://go.microsoft.com/fwlink/?LinkId=325338)|

### <a name="support-for-previous-formats"></a>以前の形式のサポート

次の表の PDF Reader は、.ppdf ファイル名拡張子および古い形式の .pdf ファイル名拡張子の保護された PDF ドキュメントをサポートします。

現在、SharePoint Online とオンプレミスの SharePoint では、IRM で保護されたライブラリで PDF ドキュメントの古い形式を使用します。


|オペレーティング システム|サポートされるリーダー|
|----------------|-----------------------------------|
|Windows 10 と以前のバージョン<br />から Windows 7 Service Pack 1|Azure Information Protection ビューアー<br /><br />Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br />RMS 共有アプリ|
|Android|Azure Information Protection アプリ<br /><br />RMS を使用する Foxit MobilePDF<br /><br />GigaTrust App for Android|
|iOS|Azure Information Protection アプリ<br /><br />RMS を使用する Foxit MobilePDF<br /><br />TITUS Docs|
