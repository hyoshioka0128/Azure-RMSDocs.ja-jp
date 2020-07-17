---
title: Microsoft Information Protection の保護された PDF Reader
description: 分類と保護のラベルが付けられた PDF ドキュメント用のリーダーをインストールする
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/17/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aab59e02-930b-4a17-8442-2d5d081fe1a6
ms.reviewer: kartikka
ms.suite: ems
ms.custom: user
search.appverid:
- MET150
ms.openlocfilehash: 25bc9d18badcb6bb79e17795f7f86912968a44ee
ms.sourcegitcommit: c5772e8c4bdcd1840f2d855264f023ff12f6fc07
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2020
ms.locfileid: "86437778"
---
# <a name="pdf-readers-that-support-microsoft-information-protection"></a>Microsoft Information Protection をサポートする PDF リーダー

Microsoft Information Protection によって保護されている PDF ドキュメントを開く必要がある場合は、次のリンクと情報を参照してください。

保護されている PDF ドキュメントには、機密情報が含まれている可能性があります。 セキュリティを強化するために、ドキュメントは暗号化されており、承認されていない人物がドキュメントを閲覧することはできません。また、ドキュメントを表示している画面やスクリーンショットを共有することもできません 

このドキュメントを開くには、ドキュメントを開くためのアクセス許可が付与されていることを確認してから、暗号化を解除するリーダー (ビューアーと呼ばれることもあります) が必要です。

## <a name="install-pdf-readers-for-your-device"></a>デバイスの PDF リーダーをインストールする

保護された PDF ドキュメントを開くことができる PDF リーダーのインストールに使用しているデバイスを選択します。 これらのすべての閲覧者は、ISO 標準の PDF 暗号化に準拠した保護されたドキュメントを開くことができます。

- **コンピューター**: [Windows](protected-pdf-readers-windows.md)  |  [MacOS](protected-pdf-readers-mac.md)

- **モバイルデバイス**: [Android](protected-pdf-readers-android.md)  |  [iOS](protected-pdf-readers-ios.md)

### <a name="support-for-previous-formats"></a>以前の形式のサポート

次の表の PDF リーダーは、ファイル名拡張子が ppdf である保護された PDF ドキュメントと、.pdf ファイル名拡張子を持つ古い形式をサポートしています。 

現在、Microsoft SharePoint では、IRM で保護されたライブラリ内の PDF ドキュメントに古い形式が使用されています。


|オペレーティング システム|サポートされるリーダー|
|----------------|-----------------------------------|
|Windows 10 と以前のバージョン<br />から Windows 7 Service Pack 1|Microsoft Edge<br /><br />Azure Information Protection ビューアー<br /><br />Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br /> Nuance Power PDF|
|Android|Azure Information Protection アプリ<br /><br />RMS を使用する Foxit MobilePDF<br /><br />GigaTrust App for Android|
|iOS|Azure Information Protection アプリ<br /><br />RMS を使用する Foxit MobilePDF<br /><br />TITUS Docs|

## <a name="using-microsoft-edge-to-view-protected-pdf-files"></a>Microsoft Edge を使用して保護された PDF ファイルを表示する

Microsoft Edge では、分類および保護されている PDF ファイルを表示するネイティブサポートを提供しています。 Microsoft Edge を使用することにより、ユーザーは追加の設定やソフトウェアをインストールまたは構成しなくても、保護された PDF ファイルをシームレスに開くことができます。  設定をグループ化します。

Microsoft Edge では、ローカルに保存されている保護された PDF ファイルをユーザーが検出すると、ブラウザーで直接ファイルを表示できます。 ファイルが SharePoint で使用可能な場合、ユーザーは **、[**  >  Microsoft Edge から**ブラウザーで**開く] をクリックするだけでファイルを表示できます。 

:::image type="content" source="../media/edge_open_browser.png" alt-text="ブラウザーで [ブラウザーで開く] オプションを使用して、Microsoft Edge を使用して保護された PDF を開きます。":::

保護されたファイルは、 [Windows](./protected-pdf-readers-windows.md)と[MacOS](./protected-pdf-readers-mac.md)の両方で開くことができます。

## <a name="using-adobe-acrobat-reader-with-adobe-plug-in"></a>Adobe Acrobat Reader と Adobe プラグインの使用

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
