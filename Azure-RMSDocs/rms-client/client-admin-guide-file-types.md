---
title: サポートされているファイルの種類-Azure Information Protection クライアント
description: Windows 用 Azure Information Protection クライアントを担当する管理者のために、サポートされるファイルの種類、ファイル名拡張子、保護のレベルに関する技術の詳細について説明します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/26/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ''
ms.subservice: v1client
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 350f687a61899046346f26b5beb2944b9f3caf13
ms.sourcegitcommit: 3464f9224b34dc54ad6fc1b7bc4dc11ad1ab8d59
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/28/2019
ms.locfileid: "72984869"
---
# <a name="admin-guide-file-types-supported-by-the-azure-information-protection-client"></a>管理者ガイド: Azure Information Protection クライアントでサポートされるファイルの種類

>*適用対象:Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、WINDOWS 7 SP1、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012、windows Server 2008 r2*
>
> *手順:[Windows 用 Azure Information Protection クライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection クライアントは、次のことをドキュメントとメールに適用できます。

- 分類のみ

- 分類と保護

- 保護のみ

Azure Information Protection クライアントでは、よく知られている機密情報の種類またはユーザーによって定義された正規表現を使用して、いくつかのファイルの種類の内容を調べることもできます。

以下では、Azure Information Protection クライアントでサポートされているファイルの種類を確認し、さまざまな保護レベルと既定の保護レベルを変更する方法を理解し、分類と保護から自動的に除外 (スキップ) されるファイルを特定する方法について説明します。

一覧表示されているファイルの種類に対して、WebDav の場所はサポートされません。

## <a name="file-types-supported-for-classification-only"></a>分類のみにサポートされているファイルの種類

次のファイルの種類は、保護されていない場合でも分類することができます。

- **Adobe Portable Document Format**: .pdf

- **Microsoft Project**: .mpp、.mpt

- **Microsoft Publisher**: .pub

- **Microsoft XPS**: .xps、.oxps

- **イメージ**: .jpg、.jpe、.jpeg、.jif、.jfif、.jfi、 .png、.tif、.tiff

- **Autodesk Design Review 2013**: .dwfx

- **Adobe Photoshop**: .psd

- **Digital Negative**: .dng

- **Microsoft Office**:次の表のファイルの種類。

    これらのファイルの種類に対してサポートされるファイル形式は、次の Office プログラム用の 97-2003 ファイル形式と Office Open XML 形式です:Word、Excel、PowerPoint。

    |Office ファイルの種類|Office ファイルの種類|
    |----------------------------------|----------------------------------|
    |.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vdw<br /><br />.vsd|.vsdm<br /><br /> .vsdx<br /><br />.vss<br /><br />.vssm<br /><br />.vst<br /><br />.vstm<br /><br />.vssx<br /><br />.vstx<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx|

他のファイルの種類では、保護されている場合に分類がサポートされます。 これらのファイルの種類については、下記の「[分類と保護がサポートされているファイルの種類](#supported-file-types-for-classification-and-protection)」を参照してください。

たとえば、現在の[既定のポリシー](../configure-policy-default.md)では、**全般**ラベルは、分類を適用しますが、保護を適用しません。 **全般ラベル**の場合 sales.pdf という名前のファイルに適用することは可能ですが、sales.txt という名前のファイルに適用することはできません。 

また、現在の既定のポリシーでは、**社外秘 \ すべての従業員**は分類と保護を適用します。 このラベルの場合は、sales.pdf とい名前のファイルと sales.txt という名前のファイルに、このラベルを適用することが可能です。 また、保護のみをこれらのファイルに適用し、分類は対象外とすることも可能です。

## <a name="file-types-supported-for-protection"></a>保護がサポートされているファイルの種類

Azure Information Protection クライアントは、次の表に示すように、2 つの異なるレベルの保護をサポートします。

|保護の種類|ネイティブ|ジェネリック|
|----------------------|----------|-----------|
|説明|テキスト、イメージ、Microsoft Office (Word、Excel、PowerPoint) ファイル、.pdf ファイル、および Rights Management サービスをサポートする他のアプリケーションのファイルの種類については、ネイティブ保護で、暗号化と権限の適用 (アクセス許可) の両方を含む強力なレベルの保護が提供されます。|他のすべてのアプリケーションとファイルの種類については、ジェネリック保護で、ファイルの種類として .pfile を使用したファイルのカプセル化と、ユーザーにファイルを開く権限があるかどうかを確認する認証の両方を含むレベルの保護が提供されます。|
|保護|ファイルの保護は次の方法で適用されます。<br /><br />- 保護されたコンテンツが表示される前に、電子メールでファイルを受け取るユーザー、あるいはファイルや共有のアクセス許可によってそれに対するアクセス権が付与されるユーザーについて、認証が正しく行われる必要があります。<br /><br />- さらに、ファイルが保護されたときにコンテンツの所有者によって設定された使用権限およびポリシーは、コンテンツが Azure Information Protection ビューアーで表示される (保護されたテキストとイメージ ファイルの場合) か、関連付けられたアプリケーションで表示される (他のサポートされているすべてのファイルの種類の場合) ときに適用されます。|ファイルの保護は次の方法で適用されます。<br /><br />- 保護されたコンテンツが表示される前に、ファイルを開く権限があり、それに対するアクセス権が付与されるユーザーについて、認証が正しく行われる必要があります。 承認に失敗すると、ファイルは開きません。<br /><br />- コンテンツの所有者によって設定された使用権限とポリシーが表示され、目的の使用ポリシーが承認済みユーザーに通知されます。<br /><br />- 承認済みユーザーがファイルを開きアクセスしていることを確認する監査ログが実行されます。 ただし、使用権限は適用されません。|
|ファイルの種類の既定値|次のファイルの種類の既定の保護レベルを次に示します。<br /><br />- テキストとイメージ ファイル<br /><br />- Microsoft Office (Word、Excel、PowerPoint) ファイル<br /><br />- Portable Document Format (.pdf)<br /><br />詳細については、下記の「[分類と保護がサポートされているファイルの種類](#supported-file-types-for-classification-and-protection)」 を参照してください。|これは、ネイティブな保護によってサポートされない他のすべてのファイルの種類 (.vsdx、.rtf など) の既定の保護です。|

Azure Information Protection クライアントで適用される既定の保護レベルを変更できます。 既定のレベルをネイティブからジェネリックに、またジェネリックからネイティブに変更することができます。さらに、Azure Information Protection クライアントで保護を適用しないようにすることもできます。 詳細については、この記事の「[ファイルの既定の保護レベルの変更](#changing-the-default-protection-level-of-files)」セクションを参照してください。

ユーザーは、管理者によって構成されたラベルを選んで、データ保護を自動的に適用できます。または、ユーザーは、[アクセス許可レベル](../configure-usage-rights.md#rights-included-in-permissions-levels)を使って、独自のカスタム保護設定を指定できます。 

### <a name="file-sizes-supported-for-protection"></a>保護がサポートされているファイルのサイズ

Azure Information Protection クライアントが保護をサポートするファイルのサイズには上限があります。

- **Office ファイル:**


  |                                                     Office アプリケーション                                                      |                                                サポートされる最大ファイル サイズ                                                 |
  |-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
  |             Word 2007 (AD RMS のみでサポート)<br /><br />Word 2010<br /><br />Word 2013<br /><br />Word 2016             |                                          32ビット:512 MB<br /><br />64ビット:512 MB                                          |
  |           Excel 2007 (AD RMS のみでサポート)<br /><br />Excel 2010<br /><br />Excel 2013<br /><br />Excel 2016           |                      32ビット:2 GB<br /><br />64ビット:使用可能なディスク領域とメモリによってのみ制限されます                       |
  | PowerPoint 2007 (AD RMS のみでサポート)<br /><br />PowerPoint 2010<br /><br />PowerPoint 2013<br /><br />PowerPoint 2016 | 32ビット:使用可能なディスク領域とメモリによってのみ制限されます<br /><br />64ビット:使用可能なディスク領域とメモリによってのみ制限されます |


- **その他のすべてのファイル**: 

  - その他のファイルの種類を保護し、これらのファイルの種類を Azure Information Protection ビューアーで開く場合:ファイルの最大サイズは、使用可能なディスク領域とメモリによってのみ制限されます。

  - [Unprotect-rmsfile](/powershell/module/azureinformationprotection/unprotect-rmsfile) コマンドレットを使用してファイルの保護を解除する場合:.pst ファイルに対してサポートされるファイルの最大サイズは 5 GB です。 その他のファイルの種類の場合は、使用可能なディスク領域とメモリによってのみ制限されます。

    ヒント:大きな .pst ファイルの保護された項目を検索したり復元したりする必要がある場合は、「[電子情報開示での Unprotect-RMSFile の使用に関するガイダンス](../configure-super-users.md#guidance-for-using-unprotect-rmsfile-for-ediscovery)」をご覧ください。

### <a name="supported-file-types-for-classification-and-protection"></a>分類と保護がサポートされているファイルの種類

次の表には、Azure Information Protection クライアントによるネイティブ保護をサポートし、かつ分類も可能であるファイルの種類のサブセットを一覧表示します。 

これらの種類のファイルは、ネイティブに保護されると、元のファイルの拡張子が変更され読み取り専用になるため、別々に識別されます。 一般的に保護されるファイルの場合、元のファイル名拡張子が常に .pfile に変わる点に注意してください。

> [!WARNING]
> ファイル名拡張子に基づいて検査とアクションを実行するファイアウォール、Web プロキシ、またはセキュリティ ソフトウェアがある場合は、新しいファイル名拡張子をサポートするように、これらのネットワーク デバイスとソフトウェアの再構成が必要になる場合があります。

|元のファイル名拡張子|保護されるファイル名拡張子|
|--------------------------------|-------------------------------------|
|.txt|.ptxt|
|.xml|.pxml|
|.jpg|.pjpg|
|.jpeg|.pjpeg|
|.pdf|.ppdf [[1]](#footnote-1)|
|.png|.ppng|
|.tif|.ptif|
|.tiff|.ptiff|
|.bmp|.pbmp|
|.gif|.pgif|
|.jpe|.pjpe|
|.jfif|。pjfif|
|.jt|.pjt|

###### <a name="footnote-1"></a>脚注 1
最新バージョンの Azure Information Protection クライアントを使用する場合、[既定では](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)、保護された PDF ドキュメントのファイル名の拡張子は .pdf のままです。

次の表には、Azure Information Protection クライアントによるネイティブ保護をサポートし、かつ分類も可能である残りのファイルの種類を一覧表示します。 これらは、Microsoft Office アプリのファイルの種類であることがわかります。 これらのファイルの種類に対してサポートされるファイル形式は、次の Office プログラム用の 97-2003 ファイル形式と Office Open XML 形式です:Word、Excel、PowerPoint。

これらのファイルの場合、ファイル名拡張子は、ファイルが Rights Management サービスで保護された後も変更されません。

|Office でサポートされているファイルの種類|Office でサポートされているファイルの種類|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vsdm|.vsdx<br /><br />.vssm<br /><br />.vssx<br /><br />.vstm<br /><br />.vstx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

### <a name="changing-the-default-protection-level-of-files"></a>ファイルの既定の保護レベルの変更
Azure Information Protection クライアントがファイルを保護する方法は、レジストリを編集して変更することができます。 たとえば、ネイティブ保護をサポートするファイルを、Azure Information Protection クライアントで一般的に保護されるように強制できます。

この操作を行う必要がある理由:

- ネイティブ保護をサポートするアプリケーションがない場合に、すべてのユーザーがファイルを開けるようにするため。

- セキュリティ システムがファイル名拡張子に基づいてファイルに対するアクションを実行し、.pfile ファイル名拡張子に対応するように再構成できるが、ネイティブ保護のための複数のファイル名拡張子に対応するように再構成できないようにするため。

同様に、既定では汎用的な保護が適用されるファイルに、Azure Information Protection クライアントでネイティブ保護を適用するように強制することができます。 この操作は、RMS API をサポートするアプリケーションがあるときに適切な場合があります。 たとえば、社内開発者によって作成された基幹業務アプリケーションや、独立系ソフトウェア ベンダー (ISV) から購入したアプリケーションです。

また、Azure Information Protection クライアントでファイルの保護をブロックする (ネイティブ保護や汎用的な保護を適用しない) ように強制することもできます。 たとえば、内容を処理するために特定のファイルを開く必要がある自動化されたアプリケーションやサービスがある場合に、この操作が必要になることがあります。 ファイルの種類の保護をブロックすると、ユーザーは Azure Information Protection クライアントを使ってその種類のファイルを保護できなくなります。 ユーザーがこの操作を試みると、管理者が保護できないように設定したことと、ファイルを保護するには操作を取り消す必要があることを示すメッセージが表示されます。

既定ではネイティブ保護が適用されるすべてのファイルに汎用的な保護を適用するように Azure Information Protection クライアントを構成するには、次のレジストリ編集を行います。 FileProtection キーが存在しない場合は、手動でそれを作成する必要があることに注意してください。

1. ファイルにファイル拡張子があることを示す * という名前の新しいキーを次のレジストリのパスに作成します。

    - 32 ビット版の Windows の場合:**HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection**

    - 64 ビット版の Windows の場合:**HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\FileProtection** および **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection**

2. 新しく追加したキー (例: HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\\\*) の中に、新しい文字列値 (REG_SZ) を **Encryption** という名前で作成し、データ値は **Pfile** とします。

    この設定により、Azure Information Protection クライアントは汎用的な保護を適用します。

これら 2 つの設定により、Azure Information Protection クライアントは、ファイル名拡張子を持つすべてのファイルに汎用的な保護を適用します。 これが目的である場合、それ以上の構成は必要ありません。 ただし、引き続きネイティブで保護されるように、特定のファイルの種類の例外を定義できます。 そのためには、以下のように、ファイルの種類ごとに追加で 3 つ (32 ビット Windows の場合) または 6 つ (64 ビット Windows の場合) のレジストリ編集を行う必要があります。

1. **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection** および **HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\FileProtection** (該当する場合):(前のピリオドを除く) ファイル名拡張子の名前を持つ新しいキーを追加します。

    たとえば、.docx というファイル名拡張子を持つファイルの場合、 **DOCX**という名前のキーを作成します。

2. 新たに追加したファイル種類のキー (たとえば、**HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**) で、値が **0** の **AllowPFILEEncryption** という新しい DWORD 値を作成します。

3. 新たに追加したファイル種類のキー (たとえば、**HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**) で、値が **Native** の **Encryption** という新しい文字列値を作成します。

これらの設定の結果、.docx というファイル名拡張子を持つファイルを除き、すべてのファイルが一般的に保護されます。 これらのファイルは、Azure Information Protection クライアントによってネイティブに保護されます。

例外として定義するその他のファイルの種類ごとに、これらの 3 つの手順を繰り返します。これらのファイルはネイティブ保護をサポートしており、Azure Information Protection クライアントで一般的に保護しないようにする必要があるためです。

次の値をサポートする **Encryption** 文字列の値を変更することで、他のシナリオで同様のレジストリ編集を行うことができます。

- **Pfile**: 一般的な保護

- **Native**: ネイティブ保護

- **Off**: 保護をブロックする

これらのレジストリに変更を加えた後、コンピューターを再起動する必要はありません。 ただし、ファイルを保護するために PowerShell コマンドを使っている場合は、変更を反映させるために新しい PowerShell セッションを開始する必要があります。

ファイルの既定の保護レベルを変更するためのレジストリの編集について詳しくは、開発者ガイドの「[ファイル API の構成](../develop/file-api-configuration.md)」をご覧ください。 この開発者向けドキュメントでは、汎用的な保護は "PFile" と呼ばれています。

## <a name="file-types-that-are-excluded-from-classification-and-protection"></a>分類と保護から除外されるファイルの種類

コンピューターの動作に不可欠なファイルをユーザーが変更しないように、一部のファイルの種類とフォルダーは分類と保護から自動的に除外されます。 ユーザーが Azure Information Protection クライアントを使用してこのようなファイルを分類または保護しようとすると、ファイルが除外されることを示すメッセージが表示されます。

- **除外されるファイルの種類**: .lnk、.exe、.com、.cmd、.bat、.dll、.ini、.pst、.sca、.drm、.sys、.cpl、.inf、.drv、.dat、.tmp、msg、.msp、.msi、.pdb、.jar


- **除外されるフォルダー**: 
    - Windows
    - Program Files (\Program Files および \Program Files (x86))
    - \ProgramData 
    - \AppData (すべてのユーザー)

### <a name="file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーによる分類と保護から除外されるファイルの種類

既定では、以下の例外を除き、スキャナーでも Azure Information Protection クライアントと同じファイルの種類が除外されます。

- .rtf、.rar も除外されます

スキャナーによるファイル検査について、対象または対象外となるファイルの種類を変更することができます。

- [Azure portal を使って](../deploy-aip-scanner.md#configure-the-scanner-in-the-azure-portal)、スキャナー プロファイルの **[スキャンするファイルの種類]** を構成します。

> [!NOTE]
> スキャン対象に .rtf ファイルを含める場合は、スキャナーを注意深く監視してください。 一部の .rtf ファイルはスキャナーで正常に検査できません。このようなファイルの検査は完了せず、サービスを再開する必要があります。 

既定では、スキャナーによって保護されるのは、Office ファイルの種類と、PDF の暗号化のための ISO 標準を使用して保護されている PDF ファイルだけです。 このスキャナーの動作を変更するには、レジストリを編集し、保護する追加のファイルの種類を指定します。 手順については、「レジストリの編集」を参照して、[保護するファイルの種類](../deploy-aip-scanner.md#scanner-from-the-classic-client-use-the-registry-to-change-which-file-types-are-protected)をスキャナーの展開手順から変更します。

### <a name="files-that-cannot-be-protected-by-default"></a>既定では保護できないファイル

パスワードで保護されているファイルは、保護を適用するアプリケーションでファイルが現在開かれている場合を除き、Azure Information Protection クライアントでネイティブで保護することはできません。 パスワード保護されている PDF ファイルをよく見かけますが、Office アプリなど、他のアプリケーションもこの機能を備えています。

ファイル名拡張子 .ppdf を使って PDF ファイルを保護するように Azure Information Protection クライアントの[既定の動作](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)を変更した場合、クライアントは次のいずれの状況においても PDF ファイルをネイティブに保護または保護解除することができません。

- フォームベースの PDF ファイル。

- ファイル名の拡張子が .pdf の、保護されている PDF ファイル。

    Azure Information Protection クライアントは保護されていない PDF ファイルを保護できます。ファイル名の拡張子が .ppdf である場合は、保護されている PDF ファイルを保護解除し、再保護することができます。

### <a name="limitations-for-container-files-such-as-zip-files"></a>.zip ファイルなど、コンテナー ファイルの制限事項

コンテナー ファイルは、その他のファイルが含まれるファイルです。典型的な例は、圧縮ファイルが含まれる .zip ファイルです。 その他の例には、.rar、.7z、.msg ファイルや、添付ファイルを含む PDF ドキュメントなどが含まれます。

これらのコンテナー ファイルを分類し、保護できますが、分類と保護はコンテナー内の各ファイルに適用されません。

分類され、保護されているファイルがコンテナー ファイル内にある場合、先にファイルを抽出し、分類または保護設定を変更する必要があります。 ただし、[Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) コマンドレットを利用し、サポートされているコンテナー ファイル内の全ファイルの保護を削除できます。

Azure Information Protection ビューアーでは、保護された PDF ドキュメント内の添付ファイルを開くことはできません。 このシナリオでは、ビューアーでドキュメントを開いたときに、添付ファイルは表示されません。

## <a name="file-types-supported-for-inspection"></a>検査に対してサポートされているファイルの種類

構成を何も追加しなくても、Azure Information Protection クライアントでは、Windows IFilter を使用してドキュメントの内容が検査されます。 Windows IFilter は、インデックス作成のために Windows Search によって使用されます。 結果として、[Azure Information Protection スキャナー](../deploy-aip-scanner.md)または [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) PowerShell コマンドを使用すると、次のファイルの種類を検査できます。

|アプリケーションの種類|ファイルの種類|
|--------------------------------|-------------------------------------|
|Word|ドック.docx; .docm; .dot; normal.dotm; .dotx|
|Excel|.xls; .xlt; .xlsx; .xltx; .xltm; .xlsm; .xlsb|
|PowerPoint|.ppt; .pps; .pot; .pptx; .ppsx; .pptm; .ppsm; .potx; .potm|
|PDF |.pdf|
|テキスト|.txt; .xml; .csv|

構成を追加すると、その他のファイルの種類も検査できます。 たとえば、[カスタム ファイル名拡張子を登録してテキスト ファイルに既存の Windows フィルター ハンドラーを使用する](https://docs.microsoft.com/windows/desktop/search/-search-ifilter-registering-filters)ことや、ソフトウェア ベンダーから追加のフィルターをインストールすることができます。

インストールされているフィルターを確認する方法については、Windows Search 開発者ガイドの「[Finding a Filter Handler for a Given File Extension (特定のファイル拡張子用のフィルター ハンドラーの検索)](https://docs.microsoft.com/windows/desktop/search/-search-ifilter-registering-filters#finding-a-filter-handler-for-a-given-file-extension)」セクションをご覧ください。

以下のセクションでは、.zip ファイルと .tiff ファイルを検査するための構成方法について説明します。

### <a name="to-inspect-zip-files"></a>.zip ファイルを検査するには

以下の手順のようにすると、Azure Information Protection スキャナーおよび [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) PowerShell コマンドで .zip ファイルを検査できます。

1. スキャナーまたは PowerShell セッションが実行されているコンピューターに、[Office 2010 Filter Pack SP2](https://support.microsoft.com/en-us/help/2687447/description-of-office-2010-filter-pack-sp2) をインストールします。

2. スキャナーの場合:機密情報を検索した後、.zip ファイルをラベルで分類して保護する必要がある場合は、「[レジストリの編集による保護されるファイルの種類の変更」の説明に従って、汎用的な保護 (pfile) を持つように、このファイル名拡張子のレジストリエントリを追加します。](../deploy-aip-scanner.md#scanner-from-the-classic-client-use-the-registry-to-change-which-file-types-are-protected)スキャナーのデプロイ手順から。

これらの手順の実行後のシナリオ例: 

**accounts.zip** という名前のファイルには、クレジット カード番号が含まれる Excel のスプレッドシートが含まれています。 Azure Information Protection のポリシーに **Confidential \ Finance** という名前のラベルがあります。これはクレジット カード番号を検出するために構成されており、ラベルでは Finance グループへのアクセスを制限する保護が自動的に適用されます。 

ファイルの検査後、スキャナーではこのファイルは **Confidential \ Finance** として分類され、Finance グループのメンバーのみが解凍できるよう、ファイルへ汎用的な保護が適用され、ファイルは **accounts.zip.pfile** に名前変更されます。

### <a name="to-inspect-tiff-files-by-using-ocr"></a>OCR を使用して .tiff ファイルを検査するには

スキャナーまたは PowerShell セッションが実行されているコンピューターに Windows TIFF IFilter 機能をインストールして、[Windows TIFF IFilter 設定](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/dd744701%28v%3dws.10%29)を構成すると、Azure Information Protection スキャナーおよび [Set-AIPFileClassiciation](/powershell/module/azureinformationprotection/set-aipfileclassification) PowerShell コマンドで光学式文字認識 (OCR) を使用して、ファイル名拡張子 .tiff を持つ TIFF イメージを検査できます。

スキャナーの場合:機密情報を検索した後、tiff ファイルを分類してラベルで保護する必要がある場合は、「レジストリの編集」の説明に従って、このファイル名拡張子のレジストリエントリを追加して、[保護するファイルの種類を変更](../deploy-aip-scanner.md#scanner-from-the-classic-client-use-the-registry-to-change-which-file-types-are-protected)します。スキャナーの展開手順。

## <a name="next-steps"></a>次の手順
Azure Information Protection クライアントによってサポートされるファイルの種類がわかったので、このクライアントのサポートに必要な追加情報を以下のリソースで参照してください。

- [カスタマイズ](client-admin-guide-customizations.md)

- [クライアント ファイルおよび使用状況ログの記録](client-admin-guide-files-and-logging.md)

- [ドキュメント追跡](client-admin-guide-document-tracking.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)

