---
title: RMS 共有アプリケーションの技術概要 - AIP
description: Windows 用 RMS 共有アプリケーションのデプロイを担当するエンタープライズ ネットワークの管理者向けの技術的な詳細です。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/02/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: f7b13fa4-4f8e-489a-ba46-713d7a79f901
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ec0c231e2036dc66b941be7f764bb5e5fd5c518a
ms.sourcegitcommit: d06594550e7ff94b4098a2aa379ef2b19bc6123d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2018
ms.locfileid: "53023804"
---
# <a name="technical-overview-and-protection-details-for-the-microsoft-rights-management-sharing-application"></a>Microsoft Rights Management 共有アプリケーションの技術的概要と保護の詳細

>*適用対象: Active Directory Rights Management サービス[、Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*


Microsoft Rights Management 共有アプリケーションは、Microsoft Windows およびその他のプラットフォーム用のオプションのダウンロード可能なアプリケーションであり、次の機能を備えています。

-   1 つのファイルの保護、または複数のファイルや選択したフォルダー内のすべてのファイルの一括保護。

-   任意の種類のファイルの保護の完全なサポートと、一般的に使用されるテキストとイメージ ファイルの種類用の組み込みビューアー。

-   RMS 保護をサポートしていないファイルの一般的な保護。

-   Office Information Rights Management (IRM) を使用して保護されたファイルとの完全な相互運用。

-   ファイル分類インフラストラクチャ (FCI) およびサポートされている PDF 作成ツールを使用して保護された PDF ファイルとの完全な相互運用。

Microsoft Rights Management 共有アプリケーションでは、[AD RMS Client 2.1 ランタイム](http://www.microsoft.com/download/details.aspx?id=38396)が使用されます。 Microsoft Rights Management 共有アプリケーションは、AD RMS 2.1 の機能を使用することにより、エンド ユーザーが簡単に保護および使用できるようにします。

RMS の 2013 年 10 月リリースでは、Office 2010 を使用してネイティブにドキュメントを保護し、それを別の企業のユーザーに送信できます。次に、そのユーザーは Azure Information Protection から Azure Rights Management サービスを使用してドキュメントを利用できます。 さらに、このリリースでは、暗号化モード 2 で AD RMS を使用すると、個人向け RMS を使用して、Azure Rights Management サービスを使用する別の企業内のユーザーからのコンテンツを利用できます。 暗号化モード 2 について詳しくは、「[AD RMS の暗号化モード](https://technet.microsoft.com/library/hh867439%28v=ws.10%29.aspx)」をご覧ください。

デプロイ情報については、「[Automatic deployment for the Microsoft Rights Management sharing application (Microsoft Rights Management 共有アプリケーションの自動デプロイ)](sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application)」を参照してください。

## <a name="levels-of-protection--native-and-generic"></a>保護のレベル - ネイティブとジェネリック
Microsoft Rights Management 共有アプリケーションは、次の表に示すように、2 つの異なるレベルの保護をサポートします。

|保護の種類|ネイティブ|ジェネリック|
|----------------------|----------|-----------|
|説明|テキスト、イメージ、Microsoft Office (Word、Excel、PowerPoint) ファイル、.pdf ファイル、および Rights Management サービスをサポートする他のアプリケーションのファイルの種類については、ネイティブ保護で、暗号化と権限の適用 (アクセス許可) の両方を含む強力なレベルの保護が提供されます。|他のすべてのアプリケーションとファイルの種類については、ジェネリック保護で、ファイルの種類として .pfile を使用したファイルのカプセル化と、ユーザーにファイルを開く権限があるかどうかを確認する認証の両方を含むレベルの保護が提供されます。|
|保護|ファイルは完全に暗号化され、次の方法で保護が適用されます。<br /><br />- 保護されたコンテンツが表示される前に、電子メールでファイルを受け取るユーザー、あるいはファイルや共有のアクセス許可によってそれに対するアクセス権が付与されるユーザーについて、認証が正しく行われる必要があります。<br /><br />- さらに、ファイルが保護されるときにコンテンツの所有者によって設定される使用権限およびポリシーは、コンテンツが IP ビューアーで表示される (保護されたテキストとイメージ ファイルの場合) か、関連付けられたアプリケーションで表示される (他のサポートされているすべてのファイルの種類の場合) ときに、完全に適用されます。|ファイルの保護は次の方法で適用されます。<br /><br />- 保護されたコンテンツが表示される前に、ファイルを開く権限があり、それに対するアクセス権が付与されるユーザーについて、認証が正しく行われる必要があります。 承認に失敗すると、ファイルは開きません。<br /><br />- コンテンツの所有者によって設定された使用権限とポリシーが表示され、目的の使用ポリシーが承認済みユーザーに通知されます。<br /><br />- 承認済みユーザーがファイルを開き、アクセスする操作の監査ロギングが行われますが、サポートされていないアプリケーションからは使用権限は適用されません。|
|ファイルの種類の既定値|次のファイルの種類の既定の保護レベルを次に示します。<br /><br />- テキストとイメージ ファイル<br /><br />- Microsoft Office (Word、Excel、PowerPoint) ファイル<br /><br />- Portable Document Format (.pdf)<br /><br />詳細については、後の「[サポートされているファイルの種類とファイル名拡張子](#supported-file-types-and-file-name-extensions)」セクションを参照してください。|これは、完全な保護によってサポートされない他のすべてのファイルの種類 (.vsdx、.rtf など) の既定の保護です。|
RMS 共有アプリケーションで適用される既定の保護レベルは変更することができます。 既定のレベルをネイティブからジェネリックに、またジェネリックからネイティブに変更することができます。さらに、RMS 共有アプリケーションで保護を適用しないようにすることもできます。 詳細については、この記事の「[ファイルの既定の保護レベルの変更](#changing-the-default-protection-level-of-files)」セクションを参照してください。

## <a name="supported-file-types-and-file-name-extensions"></a>サポートされているファイルの種類とファイル名拡張子
Microsoft Rights Management 共有アプリケーションでネイティブにサポートされているファイルの種類を、次の表にリストします。 これらのファイルの種類については、ネイティブの保護が適用され、これらのファイルが読み取り専用になると、元のファイル名拡張子が変更されます。

さらに、RMS 共有アプリケーションで、ユーザーが共有によって保護している Word、Excel、または PowerPoint ファイルをネイティブに保護する場合、この操作により、ファイル名は同じで、ファイル名拡張子が **.ppdf** ¹ である、元のファイルのコピーである 2 番目のファイルが自動的に作成されます。 このバージョンのファイルにより、RMS 共有アプリケーションをインストールする受信者は、常にネイティブ保護が適用されたファイルを開くことができます。

一般的に保護されているファイルの場合、元のファイル名拡張子は常に .pfile に変わります。

> [!WARNING]
> ファイル名拡張子に基づいて検査とアクションを実行するファイアウォール、Web プロキシ、またはセキュリティ ソフトウェアがある場合は、新しいファイル名拡張子をサポートするようにそれらの再構成が必要になる場合があります。

|元のファイル名拡張子|RMS で保護されたファイル名拡張子|
|--------------------------------|-------------------------------------|
|.txt|.ptxt|
|.xml|.pxml|
|.jpg|.pjpg|
|.jpeg|.pjeg|
|.pdf|。ppdf|
|.png|.ppng|
|.tif|.ptif|
|.tiff|.ptiff|
|.bmp|.pbmp|
|.gif|.pgif|
|.jpe|.pjpe|
|.jfif|。pjfif|
|.jt|。pjt|
¹ PDF Rendering Powered by Foxit. Copyright © 2003–2014 by Foxit Corporation.

Microsoft Rights Management 共有アプリケーションが Microsoft Office 2016、Office 2013、および Office 2010 でネイティブにサポートしているファイルの種類の一覧を、次の表に示します。 これらのファイルの場合、ファイル名拡張子は、ファイルが Rights Management サービスで保護された後も変更されません。

|Office でサポートされているファイルの種類|Office でサポートされているファイルの種類|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm|.pptx<br /><br />.thmx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

### <a name="changing-the-default-protection-level-of-files"></a>ファイルの既定の保護レベルの変更
RMS 共有アプリケーションがファイルを保護する方法は、レジストリを編集して変更することができます。 たとえば、ネイティブ保護をサポートするファイルを、RMS 共有アプリケーションで一般的に保護されるように強制できます。

この操作を行う必要がある理由:

-   すべてのユーザーがモバイル デバイスからファイルを開けるようにするため。

-   ネイティブ保護をサポートするアプリケーションがない場合に、すべてのユーザーがファイルを開けるようにするため。

-   セキュリティ システムがファイル名拡張子に基づいてファイルに対するアクションを実行し、.pfile ファイル名拡張子に対応するように再構成できるが、ネイティブ保護のための複数のファイル名拡張子に対応するように再構成できないようにするため。

同様に、既定ではジェネリック保護が適用されるファイルに、RMS 共有アプリケーションでネイティブ保護を適用するように強制することができます。 これは、社内開発者によって作成された基幹業務アプリケーションや、独立系ソフトウェア ベンダー (ISV) から購入したアプリケーションなど、RMS API をサポートするアプリケーションがあるときに適切な場合があります。

また、RMS 共有アプリケーションでファイルの保護をブロックする (ネイティブ保護やジェネリック保護を適用しない) ように強制することもできます。 たとえば、内容を処理するために特定のファイルを開く必要がある自動化されたアプリケーションまたはサービスがある場合に、これが必要になることがあります。 ファイルの種類の保護をブロックすると、ユーザーは RMS 共有アプリケーションを使用して、そのファイルの種類を持つファイルを保護できなくなります。 ユーザーがこの操作を試みると、管理者が保護できないように設定したことと、ファイルを保護するには操作を取り消す必要があることを示すメッセージが表示されます。

既定ではネイティブ保護が適用されるすべてのファイルにジェネリック保護を適用するように RMS 共有アプリケーションを構成するには、次のレジストリ編集を行います。 RmsSharingApp キーまたは FileProtection キーが存在しない場合は、手動でそれらを作成する必要があることに注意してください。

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection**: * という名前の新しいキーを作成します。

    この設定は、任意のファイル名拡張子を持つファイルを表します。

2.  新しく追加したキー HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection\\\* の中に、新しい文字列値 (REG_SZ) を **Encryption** という名前で作成し、データ値は **Pfile** とします。

    この設定により、RMS 共有アプリケーションはジェネリック保護を適用します。

これら 2 つの設定により、RMS 共有アプリケーションは、ファイル名拡張子を持つすべてのファイルにジェネリック保護を適用します。 これが目的である場合、それ以上の構成は必要ありません。 ただし、引き続きネイティブで保護されるように、特定のファイルの種類の例外を定義できます。 そのためには、以下のように、ファイルの種類ごとに追加で 3 つのレジストリ編集を行う必要があります。

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection**: ファイル名拡張子の名前を持つ新しいキーを追加します (前にピリオドは付けません)。

    たとえば、.docx というファイル名拡張子を持つファイルの場合、 **DOCX**という名前のキーを作成します。

2.  新たに追加したファイル種類のキー (たとえば、**HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection\DOCX**) で、値が **0** の **AllowPFILEEncryption** という新しい DWORD 値を作成します。

3.  新たに追加したファイル種類のキー (たとえば、**HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection\DOCX**) で、値が **Native** の **Encryption** という新しい文字列値を作成します。

これらの設定の結果、RMS 共有アプリケーションでネイティブで保護される .docx というファイル名拡張子を持つファイルを除き、すべてのファイルが一般的に保護されます。

例外として定義するその他のファイルの種類ごとに、これらの 3 つの手順を繰り返します。これらのファイルはネイティブ保護をサポートしており、RMS 共有アプリケーションで一般的に保護しないようにする必要があるためです。

次の値をサポートする **Encryption** 文字列の値を変更することで、他のシナリオで同様のレジストリ編集を行うことができます。

-   **Pfile**:一般保護

-   **Native**:ネイティブ保護

-   **Off**:保護のブロック

## <a name="see-also"></a>参照
[Rights Management 共有アプリケーション ユーザー ガイド](sharing-app-user-guide.md)

