---
title: Microsoft Information Protection の保護された PDF Reader
description: 分類と保護に対するラベルが付けられた PDF ドキュメントの詳細についてと、これらを表示する方法を学習します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aab59e02-930b-4a17-8442-2d5d081fe1a6
ms.reviewer: kartikka
ms.suite: ems
search.appverid:
- MET150
ms.openlocfilehash: 9a1deef0cc63861560e528aa06cd44857ab86515
ms.sourcegitcommit: 47182b6a65bfae3561cb34be3d6a6852a1edccb9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68446854"
---
# <a name="supported-pdf-readers-for-microsoft-information-protection"></a>Microsoft Information Protection のサポートされる PDF Reader

以下の情報を使って、分類と保護に対するラベルが付けられた PDF ドキュメントの詳細についてと、これらのドキュメントを表示する方法を学習します。

Microsoft と Adobe のコラボレーションによって、分類され、必要に応じて保護されている PDF ドキュメントにより簡単で一貫した操作を提供します。 このコラボレーションでは、[Azure Information Protection](../what-is-information-protection.md) など、Microsoft Information Protection ソリューションとの Adobe Acrobat のネイティブ統合がサポートされます。 

このネイティブ統合には次の利点があります。

- 機密情報が含まれるために保護されている PDF ドキュメントを表示できます。

- ドキュメントに適用されている組織のラベルに対する分類の値を表示できます。

- PDF の暗号化における ISO 標準をサポートします。
    
    この機能が[管理者によって無効](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)にされていない限り、最新バージョンの Azure Information Protection クライアントではこの保護された PDF ファイル形式が既定で有効化されるようになりました。

詳細については、ブログ記事「[Starting October, use Adobe Acrobat Reader for PDFs protected by Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Starting-October-use-Adobe-Acrobat-Reader-for-PDFs-protected-by/ba-p/262738)」 (10 月以降、Microsoft Information Protection で保護されている PDF に Adobe Acrobat Reader を使用する) を参照してください。

## <a name="supported-pdf-readers"></a>サポートされる PDF Reader

次の PDF Reader では、PDF の暗号化における ISO 標準に従う、保護された PDF ファイルを開くことができます。

|オペレーティング システム|サポートされるリーダーとダウンロード リンク|
|----------------|-----------------------------------|
|Windows 10 と以前のバージョン<br />から Windows 7 Service Pack 1|Adobe Acrobat Reader (推奨):<br />-  1. [Adobe の一般使用条件を参照する](https://www.adobe.com/legal/terms.html) <br />- 2. Adobe Reader for Windows を[adobe サイト](https://www.adobe.com/)からインストールする<br />- 3. Windows 用[Adobe プラグイン](https://go.microsoft.com/fwlink/?linkid=2050049)をインストールする <br />- 4. メッセージが表示されたら、管理者に[プラグインの承認](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-integration-with/ba-p/298396)を依頼してください。 <br /><br /> Azure Information Protection ビューアー: [ダウンロード](https://go.microsoft.com/fwlink/?linkid=838993)<br /><br />Foxit Reader: [ダウンロード](https://www.foxitsoftware.com/pdf-reader/)|
|macOS バージョン 10.12-10.14 |Adobe Acrobat Reader:<br />-  1. [Adobe の一般使用条件を参照する](https://www.adobe.com/legal/terms.html) <br />- 2. Adobe Reader for Mac を[adobe サイト](https://www.adobe.com/)からインストールする<br />- 3. Mac 用[Adobe プラグイン](https://go.microsoft.com/fwlink/?linkid=2050049)をインストールする <br />- 4. メッセージが表示されたら、管理者に[プラグインの承認](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-integration-with/ba-p/298396)を依頼してください。|
|Android|Azure Information Protection アプリ: [ダウンロード](https://go.microsoft.com/fwlink/?LinkId=325340)|
|iOS|Azure Information Protection アプリ: [ダウンロード](https://go.microsoft.com/fwlink/?LinkId=325338)|

### <a name="support-for-previous-formats"></a>以前の形式のサポート

次の表の PDF Reader では、.ppdf ファイル名拡張子を持つ保護された PDF ドキュメントと、.pdf ファイル名拡張子を持つ古い形式がサポートされています。

現在、SharePoint Online とオンプレミスの SharePoint では、IRM で保護されたライブラリで PDF ドキュメントの古い形式を使用します。


|オペレーティング システム|サポートされるリーダー|
|----------------|-----------------------------------|
|Windows 10 と以前のバージョン<br />から Windows 7 Service Pack 1|Azure Information Protection ビューアー<br /><br />Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br /> Nuance Power PDF<br /><br />RMS 共有アプリ|
|Android|Azure Information Protection アプリ<br /><br />RMS を使用する Foxit MobilePDF<br /><br />GigaTrust App for Android|
|iOS|Azure Information Protection アプリ<br /><br />RMS を使用する Foxit MobilePDF<br /><br />TITUS Docs|
