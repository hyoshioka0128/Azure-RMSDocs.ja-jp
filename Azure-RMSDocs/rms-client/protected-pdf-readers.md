---
title: Microsoft Information Protection の保護された PDF Reader
description: 分類と保護のラベルが付けられた PDF ドキュメント用のリーダーをインストールする
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 10/29/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: aab59e02-930b-4a17-8442-2d5d081fe1a6
ms.reviewer: kartikka
ms.suite: ems
ms.custom: user
search.appverid:
- MET150
ms.openlocfilehash: f6ebddb276cdf77c977acc516cf1b6c3d2bbc7b4
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97385116"
---
# <a name="which-pdf-readers-are-supported-for-protected-pdfs"></a>保護された Pdf ではどの PDF リーダーがサポートされていますか。

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***関連**: [AIP のラベル付けクライアントと従来のクライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

分類済みまたは保護された pdf の PDF リーダーを使用すると、機密情報を含む暗号化された Pdf を開くことができます。

[Azure Information Protection (AIP)](../what-is-information-protection.md)を使用して pdf を暗号化すると、承認されていないユーザーがファイルの内容を読み取ることができなくなります。

Azure Information Protection をサポートする保護された PDF リーダーは、ドキュメントを開くためのアクセス許可が付与されていることを確認し、コンテンツの暗号化を解除します。

たとえば、次の図は、Adobe Acrobat Reader で開かれた暗号化されたドキュメントを示しています。 上部のバーは、ドキュメントが Microsoft Information Protection ソリューションによって保護されていることを示します。

:::image type="content" source="../media/protected-pdf-in-adobe-reader.png" alt-text="Adobe Acrobat Reader で開かれている保護された PDF":::

手順については、次のセクションを参照してください。

- [Windows または Mac での Microsoft Edge での保護された Pdf の表示](#viewing-protected-pdfs-in-microsoft-edge-on-windows-or-mac)

- [Windows または Mac 用の保護された PDF リーダーのインストール](#installing-a-protected-pdf-reader-for-windows-or-mac)

- [モバイル用の保護された PDF リーダーのインストール (iOS/Android)](#installing-a-protected-pdf-reader-for-mobile-iosandroid)

> [!TIP]
> 推奨されるリーダーをインストールした後にドキュメントが開かない場合は、ドキュメントが古い形式で保護されている可能性があります。 
>
> この場合は、以前の形式でサポートされているリーダーのいずれかを試してみてください。 詳細については、「 [以前の形式のサポート](#support-for-previous-formats)」を参照してください。
> 
### <a name="iso-standards-for-pdf-encryption"></a>PDF 暗号化の ISO 標準

このページで参照されている PDF リーダーは、PDF 暗号化の ISO 標準に準拠するすべての保護されたドキュメントを開くことができます。 

この標準は、既定で AIP クライアントによって使用されます。

> [!NOTE]
> **従来のクライアントのみ**: AIP クラシッククライアントを使用している場合は、 [管理者によって無効](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)にされている可能性があります。
> 

### <a name="viewing-protected-pdfs-in-adobe-acrobat-reader"></a>Adobe Acrobat Reader での保護された Pdf の表示

Adobe Acrobat Reader は、 [Azure Information Protection](../what-is-information-protection.md) などの Microsoft Information Protection ソリューションと統合して、分類された、または保護された pdf について、シンプルで一貫したエクスペリエンスをユーザーに提供します。

Microsoft Information Protection 統合を使用した Adobe Acrobat Reader は、 [Windows](#installing-a-protected-pdf-reader-for-windows-or-mac) および [macOS](#installing-a-protected-pdf-reader-for-windows-or-mac)でサポートされています。

詳細については、次のブログ投稿を参照してください。 

- [Adobe Acrobat Reader と Microsoft Information Protection との統合の一般提供](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-Integration-with/ba-p/298396)

- [Adobe reader と Microsoft Information Protection 統合に関してよく寄せられる質問](https://techcommunity.microsoft.com/t5/Microsoft-Information-Protection/Adobe-reader-and-Microsoft-Information-Protection-integration/ba-p/482219)

## <a name="viewing-protected-pdfs-in-microsoft-edge-on-windows-or-mac"></a>Windows または Mac での Microsoft Edge での保護された Pdf の表示

Microsoft Edge には、分類および保護されている PDF ファイルを表示するための組み込みサポートが用意されています。 Microsoft Edge を使用することにより、ユーザーは追加の設定やソフトウェアをインストールまたは構成しなくても、保護された PDF ファイルをシームレスに開くことができます。

サポートされているバージョンは次のとおりです。

- **Windows: windows** 10 以前のバージョン。 
    
    以前のバージョンの詳細については、「 [以前の形式のサポート](#support-for-previous-formats)」を参照してください。

- **Mac**: macOS バージョン10.12 以降 


**手順**: 

1. システムにインストールされている [Microsoft Edge のバージョン](https://support.microsoft.com/help/4027011/microsoft-edge-find-out-which-version-you-have) を確認します。 
1. Microsoft Edge のバージョンが83.0.478.37 以上の場合は、Microsoft edge ブラウザーで直接保護されたファイルを開くことができます。 

1. SharePoint で PDF ファイルを開くには、[ブラウザーで **開く] をクリックし**  >  ます。 

    :::image type="content" source="../media/edge_open_browser.png" alt-text="ブラウザーで [ブラウザーで開く] オプションを使用して、Microsoft Edge を使用して保護された PDF を開きます。":::
 
## <a name="installing-a-protected-pdf-reader-for-windows-or-mac"></a>Windows または Mac 用の保護された PDF リーダーのインストール

保護された PDF ドキュメントをデスクトップコンピューターで開くには、オペレーティングシステム用に、 [acrobat および Acrobat Reader 用の関連する Microsoft Information Protection (MIP) プラグイン](https://go.microsoft.com/fwlink/?linkid=2050049) をインストールすることをお勧めします。

**手順**:

1. Adobe Reader がまだインストールされていない場合は、 [adobe サイト](https://www.adobe.com/)からインストールします。

    [Adobe の一般的な使用条件](https://www.adobe.com/legal/terms.html)を読んで同意してください。

1. オペレーティングシステム用に、 [acrobat と Acrobat Reader 用の MIP プラグイン](https://go.microsoft.com/fwlink/?linkid=2050049) をインストールします。  

    ダウンロード: [ ![Acrobat および acrobat Reader 用の MIP プラグインをダウンロードする](../media/download.png "Acrobat および Acrobat Reader 用 MIP プラグインをダウンロードする")](https://go.microsoft.com/fwlink/?linkid=2050049)

    サポートされているバージョンは次のとおりです。

    - **Windows: windows** 10 以前のバージョン。 
    
        以前のバージョンの詳細については、「 [以前の形式のサポート](#support-for-previous-formats)」を参照してください。

    - **Mac**: macOS バージョン 10.12-10.14 

1. 管理者の承認を求めるメッセージが表示された場合は、管理者にプラグインの承認を依頼してください。

    次に例を示します。
    
    :::image type="content" source="../media/admin-approval-for-mip-in-adobe-reader.png" alt-text="Acrobat および Acrobat Reader 用 MIP プラグインをインストールするために管理者の承認が必要":::
    
> [!NOTE]
> 詳細については、 [Microsoft Information Protection と Adobe release の発表](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-integration-with/ba-p/298396)を参照してください。
> 

### <a name="alternative-protected-pdf-readers-for-windows"></a>Windows 用の保護された別の PDF リーダー

または、ISO standard for PDF の暗号化に準拠している次のいずれかの Windows の PDF リーダーを使用します。

- Azure Information Protection ビューアー [ ![AIP ビューアーをダウンロードする](../media/download.png "AIP ビューアーをダウンロードする")](https://go.microsoft.com/fwlink/?linkid=838993) 

- Foxit Reader [![は Foxit reader ビューアーをダウンロードする](../media/download.png "Foxit Reader ビューアーのダウンロード")](https://www.foxitsoftware.com/pdf-reader/)

## <a name="installing-a-protected-pdf-reader-for-mobile-iosandroid"></a>モバイル用の保護された PDF リーダーのインストール (iOS/Android)

IOS または Android デバイスで保護された PDF を開くには、オペレーティングシステム用のアプリをダウンロードしてインストールします。

- Ios 用アプリの Azure Information Protection [ ![ios 用 Azure Information Protection アプリをダウンロードする](../media/download.png "IOS 用アプリの Azure Information Protection")  ](https://go.microsoft.com/fwlink/?LinkId=325338)

- Android 用アプリの Azure Information Protection [ ![android 用 Azure Information Protection アプリをダウンロード](../media/download.png "Android 用アプリの Azure Information Protection")する](https://go.microsoft.com/fwlink/?LinkId=325340)

詳細については、「 [iOS または Android 用の Azure Information Protection アプリとは](mobile-app-faq.md)」を参照してください。

## <a name="support-for-previous-formats"></a>以前の形式のサポート

次の PDF リーダーは、拡張子が **ppdf** の保護された pdf と、 **.pdf** 拡張子を持つ古い形式の両方をサポートしています。

推奨される閲覧者を使用して保護された PDF を開くことができない場合、ドキュメントは以前の形式で保護されている可能性があります。 たとえば、現在、Microsoft SharePoint では、IRM で保護されたライブラリ内の PDF ドキュメントに古い形式が使用されています。

- **Windows 7 Service Pack 1 を使用した windows 10 以前のバージョン**

    - [Azure Information Protection ビューアー](https://go.microsoft.com/fwlink/?linkid=838993)
    - Gaaiho Doc
    - GigaTrust Desktop PDF Client for Adobe
    - Foxit Reader
    - Nitro PDF Reader
    - Nuance Power PDF
    - Edge Chromium

- **Android**:

    - [Azure Information Protection アプリ](mobile-app-faq.md)
    - RMS を使用する Foxit MobilePDF
    - GigaTrust App for Android

- **iOS**:

    - [Azure Information Protection アプリ](mobile-app-faq.md)
    - RMS を使用する Foxit MobilePDF
    - TITUS Docs

- **MacOS catalina.properties**: Edge Chromium

## <a name="next-steps"></a>次のステップ

をインストールした後でさらにヘルプが必要な場合は、各リーダーの指示とドキュメントを参照してください。 たとえば、次の記事を参照してください。

- [ユーザーガイド: Azure Information Protection 統合ラベルクライアントを使用して保護されたファイルを表示する](clientv2-view-use-files.md)
- [IOS または Android 用の Azure Information Protection アプリとは](mobile-app-faq.md)