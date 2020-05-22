---
title: Microsoft Information Protection の保護された PDF Reader
description: 分類と保護のラベルが付けられた PDF ドキュメント用のリーダーをインストールする
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 12/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aab59e02-930b-4a17-8442-2d5d081fe1a6
ms.reviewer: kartikka
ms.suite: ems
ms.custom: user
search.appverid:
- MET150
ms.openlocfilehash: c3501f151d8c894abc92408192a7ef86d28ad8df
ms.sourcegitcommit: 8499602fba94fbfa28d7682da2027eeed6583c61
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83746946"
---
# <a name="pdf-readers-that-support-microsoft-information-protection"></a>Microsoft Information Protection をサポートする PDF リーダー

Microsoft Information Protection によって保護されている PDF ドキュメントを開く必要がある場合は、次のリンクと情報を参照してください。

保護されている PDF ドキュメントには、機密情報が含まれている可能性があります。 セキュリティを強化するために、ドキュメントは暗号化されているため、承認されていない人物が読み取ることはできません。 このドキュメントを開くには、ドキュメントを開くためのアクセス許可が付与されていることを確認してから、暗号化を解除するリーダー (ビューアーと呼ばれることもあります) が必要です。

## <a name="install-pdf-readers-for-your-device"></a>デバイスの PDF リーダーをインストールする

保護された PDF ドキュメントを開くことができる PDF リーダーのインストールに使用しているデバイスを選択します。 これらのすべての閲覧者は、ISO 標準の PDF 暗号化に準拠した保護されたドキュメントを開くことができます。

- **コンピューター**: [Windows](protected-pdf-readers-windows.md)  |  [MacOS](protected-pdf-readers-mac.md)

- **モバイルデバイス**: [Android](protected-pdf-readers-android.md)  |  [iOS](protected-pdf-readers-ios.md)

### <a name="support-for-previous-formats"></a>以前の形式のサポート

次の表の PDF リーダーは、ファイル名拡張子が ppdf である保護された PDF ドキュメントと、.pdf ファイル名拡張子を持つ古い形式をサポートしています。 

現在、Microsoft SharePoint では、IRM で保護されたライブラリ内の PDF ドキュメントに古い形式が使用されています。


|オペレーティング システム|サポートされるリーダー|
|----------------|-----------------------------------|
|Windows 10 と以前のバージョン<br />から Windows 7 Service Pack 1|Azure Information Protection ビューアー<br /><br />Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br /> Nuance Power PDF|
|Android|Azure Information Protection アプリ<br /><br />RMS を使用する Foxit MobilePDF<br /><br />GigaTrust App for Android|
|iOS|Azure Information Protection アプリ<br /><br />RMS を使用する Foxit MobilePDF<br /><br />TITUS Docs|

## <a name="using-adobe-acrobat-reader-with-the-adobe-plug-in"></a>Adobe Acrobat Reader と Adobe プラグインの使用

Microsoft と Adobe の連携により、分類され、必要に応じて保護されている PDF ドキュメントに対して、よりシンプルで一貫性のあるエクスペリエンスを提供します。 このコラボレーションでは、[Azure Information Protection](../what-is-information-protection.md) など、Microsoft Information Protection ソリューションとの Adobe Acrobat のネイティブ統合がサポートされます。 

このネイティブ統合には次の利点があります。

- 機密情報が含まれるために保護されている PDF ドキュメントを表示できます。

- ドキュメントに適用されている組織のラベルに対する分類の値を表示できます。

- PDF の暗号化における ISO 標準をサポートします。
    
    この機能が[管理者によって無効](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)にされていない限り、この保護された PDF ファイル形式は Azure Information Protection クライアント (クラシック) に対して既定で有効になり、Azure Information Protection の統合されたラベル付けクライアントで常に使用されます。

[Windows](protected-pdf-readers-windows.md)および[MacOS](protected-pdf-readers-mac.md)で Adobe プラグを使用することができます。

詳細については、次のブログ投稿を参照してください。 

- [Adobe Acrobat Reader と Microsoft Information Protection との統合の一般提供](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-Integration-with/ba-p/298396)

- [Adobe reader と Microsoft Information Protection 統合に関してよく寄せられる質問](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Adobe-reader-and-Microsoft-Information-Protection-integration/ba-p/482219)

## <a name="next-steps"></a>次のステップ

このページのリンクを使用して PDF リーダーをインストールすると、保護された PDF ドキュメントを開くことができます。

インストール後にリーダーを使用するためのヘルプが必要な場合は、そのリーダーに付属の指示とドキュメントを参照してください。 たとえば、Windows 用の Azure Information Protection ビューアーについては、「[ユーザーガイド: Azure Information Protection ユニファイドラベルクライアントを使用して保護されたファイルを表示](clientv2-view-use-files.md)する」を参照してください。
