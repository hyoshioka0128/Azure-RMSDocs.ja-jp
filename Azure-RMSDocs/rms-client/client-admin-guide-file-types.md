---
title: "Azure Information Protection でサポートされるファイルの種類"
description: "Windows 用 Azure Information Protection クライアントを担当する管理者のために、サポートされるファイルの種類、ファイル名拡張子、保護のレベルに関する技術の詳細について説明します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/06/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 84a0d335d0be97180c904182c98f6fa9ad46a0de
ms.sourcegitcommit: 81b5c111627246a4094ef87da17d260f66ae985c
translationtype: HT
---
# <a name="file-types-supported-by-the-azure-information-protection-client"></a>Azure Information Protection クライアントでサポートされるファイルの種類

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*

Azure Information Protection クライアントは、次のことをドキュメントとメールに適用できます。

- 分類のみ

- 分類と保護

- 保護のみ

以下では、サポートされているファイルの種類、さまざまな保護レベルと既定の保護レベルを変更する方法、分類と保護から自動的に除外 (スキップ) されるファイルについて説明します。

## <a name="file-types-supported-for-classification-only"></a>分類のみにサポートされているファイルの種類

次のファイルの種類では分類のみがサポートされています。 その他のファイルの種類では、分類と保護の両方がサポートされます ([「分類と保護がサポートされているファイルの種類」](#supported-file-types-for-classification-and-protection) セクションを参照してください)。

- **Adobe Portable Document Format**: .pdf

- **Microsoft Visio**: .vsdx、.vsdm、.vssx、.vssm、.vsd、.vdw、.vst

- **Microsoft Project**: .mpp、.mpt

- **Microsoft Publisher**: .pub

- **Microsoft Office 97、Office 2010、Office 2003**: .xls、.xlt、.doc、.dot、.ppt、.pps、.pot
- **Microsoft XPS**: .xps、.oxps

- **イメージ**: .jpg、.jpe、.jpeg、.jif、.jfif、.jfi.png、.tif、.tiff

- **SolidWorks**: .sldprt、.slddrw、.sldasm

- **Autodesk Design Review 2013**: .dwfx

- **Adobe Photoshop**: .psd

- **Digital Negative**: .dng

## <a name="file-types-supported-for-protection"></a>保護がサポートされているファイルの種類

Azure Information Protection クライアントは、次の表に示すように、2 つの異なるレベルの保護をサポートします。

|保護の種類|ネイティブ|ジェネリック|
|----------------------|----------|-----------|
|説明|テキスト、イメージ、Microsoft Office (Word、Excel、PowerPoint) ファイル、.pdf ファイル、および Rights Management サービスをサポートする他のアプリケーションのファイルの種類については、ネイティブ保護で、暗号化と権限の適用 (アクセス許可) の両方を含む強力なレベルの保護が提供されます。|他のすべてのアプリケーションとファイルの種類については、ジェネリック保護で、ファイルの種類として .pfile を使用したファイルのカプセル化と、ユーザーにファイルを開く権限があるかどうかを確認する認証の両方を含むレベルの保護が提供されます。|
|保護|ファイルの保護は次の方法で適用されます。<br /><br />- 保護されたコンテンツが表示される前に、電子メールでファイルを受け取るユーザー、あるいはファイルや共有のアクセス許可によってそれに対するアクセス権が付与されるユーザーについて、認証が正しく行われる必要があります。<br /><br />- さらに、ファイルが保護されるときにコンテンツの所有者によって設定される使用権限およびポリシーは、コンテンツが Azure Information Protection ビューアーで表示される (保護されたテキストとイメージ ファイルの場合) か、関連付けられたアプリケーションで表示される (他のサポートされているすべてのファイルの種類の場合) ときに、完全に適用されます。|ファイルの保護は次の方法で適用されます。<br /><br />- 保護されたコンテンツが表示される前に、ファイルを開く権限があり、それに対するアクセス権が付与されるユーザーについて、認証が正しく行われる必要があります。 承認に失敗すると、ファイルは開きません。<br /><br />- コンテンツの所有者によって設定された使用権限とポリシーが表示され、目的の使用ポリシーが承認済みユーザーに通知されます。<br /><br />- 承認済みユーザーがファイルを開きアクセスしていることを確認する監査ログが実行されます。 ただし、使用権限は適用されません。|
|ファイルの種類の既定値|次のファイルの種類の既定の保護レベルを次に示します。<br /><br />- テキストとイメージ ファイル<br /><br />- Microsoft Office (Word、Excel、PowerPoint) ファイル<br /><br />- Portable Document Format (.pdf)<br /><br />詳細については、下記の「[分類と保護がサポートされているファイルの種類](#supported-file-types-for-classification-and-protection)」 を参照してください。|これは、ネイティブな保護によってサポートされない他のすべてのファイルの種類 (.vsdx、.rtf など) の既定の保護です。|

Azure Information Protection クライアントで適用される既定の保護レベルを変更できます。 既定のレベルをネイティブからジェネリックに、またジェネリックからネイティブに変更することができます。さらに、Azure Information Protection クライアントで保護を適用しないようにすることもできます。 詳細については、この記事の「[ファイルの既定の保護レベルの変更](#changing-the-default-protection-level-of-files)」セクションを参照してください。

ユーザーは、管理者によって構成されたラベルを選んで、データ保護を自動的に適用できます。または、ユーザーは、[アクセス許可レベル](../deploy-use/configure-usage-rights.md#rights-included-in-permissions-levels)を使って、独自のカスタム保護設定を指定できます。 

### <a name="supported-file-types-for-classification-and-protection"></a>分類と保護がサポートされているファイルの種類

次の表には、Azure Information Protection クライアントによるネイティブ保護をサポートし、かつ分類も可能であるファイルの種類のサブセットを一覧表示します。 

これらの種類のファイルは、ネイティブに保護されると、元のファイルの拡張子が変更され読み取り専用になるため、別々に識別されます。 一般的に保護されるファイルの場合、元のファイル名拡張子が常に .pfile に変わる点に注意してください。

> [!WARNING]
> ファイル名拡張子に基づいて検査とアクションを実行するファイアウォール、Web プロキシ、またはセキュリティ ソフトウェアがある場合は、新しいファイル名拡張子をサポートするようにそれらの再構成が必要になる場合があります。

|元のファイル名拡張子|保護されるファイル名拡張子|
|--------------------------------|-------------------------------------|
|.txt|.ptxt|
|.xml|.pxml|
|.jpg|.pjpg|
|.jpeg|.ppng|
|.pdf|.ppdf|
|.png|.ppng|
|.tif|.ptif|
|.tiff|.ptiff|
|.bmp|.pbmp|
|.gif|.pgif|
|.jpe|.pjpe|
|.jfif|.pjfif|
|.jt|.pjt|


次の表には、Azure Information Protection クライアントによるネイティブ保護をサポートし、かつ分類も可能である残りのファイルの種類を一覧表示します。 これらは、Microsoft Office アプリのファイルの種類であることがわかります。 

これらのファイルの場合、ファイル名拡張子は、ファイルが Rights Management サービスで保護された後も変更されません。

|Office でサポートされているファイルの種類|Office でサポートされているファイルの種類|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm|.pptx<br /><br />.thmx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

### <a name="changing-the-default-protection-level-of-files"></a>ファイルの既定の保護レベルの変更
Azure Information Protection クライアントがファイルを保護する方法は、レジストリを編集して変更することができます。 たとえば、ネイティブ保護をサポートするファイルを、Azure Information Protection クライアントで一般的に保護されるように強制できます。

この操作を行う必要がある理由:

- ネイティブ保護をサポートするアプリケーションがない場合に、すべてのユーザーがファイルを開けるようにするため。

- セキュリティ システムがファイル名拡張子に基づいてファイルに対するアクションを実行し、.pfile ファイル名拡張子に対応するように再構成できるが、ネイティブ保護のための複数のファイル名拡張子に対応するように再構成できないようにするため。

同様に、既定では汎用的な保護が適用されるファイルに、Azure Information Protection クライアントでネイティブ保護を適用するように強制することができます。 これは、社内開発者によって作成された基幹業務アプリケーションや、独立系ソフトウェア ベンダー (ISV) から購入したアプリケーションなど、RMS API をサポートするアプリケーションがあるときに適切な場合があります。

また、Azure Information Protection クライアントでファイルの保護をブロックする (ネイティブ保護や汎用的な保護を適用しない) ように強制することもできます。 たとえば、内容を処理するために特定のファイルを開く必要がある自動化されたアプリケーションまたはサービスがある場合に、これが必要になることがあります。 ファイルの種類の保護をブロックすると、ユーザーは Azure Information Protection クライアントを使ってその種類のファイルを保護できなくなります。 ユーザーがこの操作を試みると、管理者が保護できないように設定したことと、ファイルを保護するには操作を取り消す必要があることを示すメッセージが表示されます。

既定ではネイティブ保護が適用されるすべてのファイルに汎用的な保護を適用するように Azure Information Protection クライアントを構成するには、次のレジストリ編集を行います。 FileProtection キーが存在しない場合は、手動でそれを作成する必要があることに注意してください。

1. **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection**: * という名前の新しいキーを作成します。

    この設定は、任意のファイル名拡張子を持つファイルを表します。

2. 新しく追加したキー HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\\\* の中に、新しい文字列値 (REG_SZ) を **Encryption** という名前で作成し、データ値は **Pfile** とします。

    この設定により、Azure Information Protection クライアントは汎用的な保護を適用します。

これら 2 つの設定により、Azure Information Protection クライアントは、ファイル名拡張子を持つすべてのファイルに汎用的な保護を適用します。 これが目的である場合、それ以上の構成は必要ありません。 ただし、引き続きネイティブで保護されるように、特定のファイルの種類の例外を定義できます。 そのためには、以下のように、ファイルの種類ごとに追加で 3 つのレジストリ編集を行う必要があります。

1. **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection**: ファイル名拡張子の名前を持つ新しいキーを追加します (前にピリオドは付けません)。

    たとえば、.docx というファイル名拡張子を持つファイルの場合、 **DOCX**という名前のキーを作成します。

2. 新たに追加したファイル種類のキー (たとえば、**HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**) で、値が **0** の **AllowPFILEEncryption** という新しい DWORD 値を作成します。

3. 新たに追加したファイル種類のキー (たとえば、**HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**) で、値が **Native** の **Encryption** という新しい文字列値を作成します。

これらの設定の結果、Azure Information Protection クライアントでネイティブで保護される .docx というファイル名拡張子を持つファイルを除き、すべてのファイルが一般的に保護されます。

例外として定義するその他のファイルの種類ごとに、これらの 3 つの手順を繰り返します。これらのファイルはネイティブ保護をサポートしており、Azure Information Protection クライアントで一般的に保護しないようにする必要があるためです。

次の値をサポートする **Encryption** 文字列の値を変更することで、他のシナリオで同様のレジストリ編集を行うことができます。

- **Pfile**:一般保護

- **Native**:ネイティブ保護

- **Off**:保護のブロック

詳しくは、開発者ガイドの「[ファイル API の構成](../develop/file-api-configuration.md)」をご覧ください。 この開発者向けドキュメントでは、汎用的な保護は "PFile" と呼ばれています。 

## <a name="file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-client"></a>Azure Information Protection クライアントによる分類と保護から除外されるファイルの種類

コンピューターの動作に不可欠なファイルをユーザーが変更しないように、一部のファイルの種類とフォルダーは分類と保護から自動的に除外されます。 このようなファイルをユーザーが分類または保護しようとすると、除外されていることを示すメッセージが表示されます。

- **除外されるファイルの種類**: .lnk、.exe、.com、.cmd、.bat、.dll、.ini、.pst、.sca、.drm、.sys、.cpl、.inf、.drv、.dat、.tmp、.msp、.msi、.pdb、.jar

- **除外されるフォルダー**: 
    - Windows
    - Program Files (\Program Files および \Program Files (x86))
    - \ProgramData 
    - \AppData (すべてのユーザー)


## <a name="next-steps"></a>次のステップ
Azure Information Protection クライアントによってサポートされるファイルの種類がわかったので、このクライアントのサポートに必要な追加情報を以下の記事でご覧ください。

- [クライアント ファイルおよび使用状況ログの記録](client-admin-guide-files-and-logging.md)

- [ドキュメント追跡](client-admin-guide-document-tracking.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
