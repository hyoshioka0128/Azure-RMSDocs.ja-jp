---
title: ファイルの種類がサポートされています - Azure Information Protection ラベル付けクライアントの統合
description: サポートされているファイルの種類、ファイル名拡張子、および保護する管理者のためのレベルに関する技術的な詳細は、Windows 用 Azure Information Protection の統合されたラベル付けクライアントを担当します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: 61d7dfa6fa1fe86c930e9c6a6d2c21a807433583
ms.sourcegitcommit: f9077101a974459a4252e763b5fafe51ff15a16f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64768136"
---
# <a name="admin-guide-file-types-supported-by-the-azure-information-protection-unified-labeling-client"></a>管理者ガイド: Azure Information Protection の統合されたラベル付けクライアントでサポートされるファイルの種類

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*>
>
> *手順:[Azure Information Protection unified Windows 用のラベル付けのクライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection の統合されたラベル付けクライアントは、ドキュメントや電子メールに、次を適用できます。

- 分類のみ

- 分類と保護

- 保護のみ

Azure Information Protection の統合されたラベル付けクライアントは、よく知られている機密情報の種類または定義する正規表現を使用していくつかのファイルの種類のコンテンツを調べることもできます。

次の情報を使用して、統合型ラベル付けの Azure Information Protection クライアントをサポートするファイルの種類を確認したり、別のレベルの保護とは、自動的にファイルを識別するために既定の保護レベルを変更する方法を理解します。除外 (スキップ) 分類と保護から。

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

例 :

- 場合、**全般**機密ラベルは分類を適用し、保護は適用されません。**全般ラベル**の場合 sales.pdf という名前のファイルに適用することは可能ですが、sales.txt という名前のファイルに適用することはできません。 

- 場合、**社外秘 \ すべての従業員**分類と保護、機密ラベルが適用されます。このラベルの場合は、sales.pdf とい名前のファイルと sales.txt という名前のファイルに、このラベルを適用することが可能です。 また、保護のみをこれらのファイルに適用し、分類は対象外とすることも可能です。

## <a name="file-types-supported-for-protection"></a>保護がサポートされているファイルの種類

Azure Information Protection の統合されたラベル付けクライアントではの次の表に示す 2 つの異なるレベルの保護をサポートしています。

|保護の種類|ネイティブ|ジェネリック|
|----------------------|----------|-----------|
|説明|テキスト、イメージ、Microsoft Office (Word、Excel、PowerPoint) ファイル、.pdf ファイル、および Rights Management サービスをサポートする他のアプリケーションのファイルの種類については、ネイティブ保護で、暗号化と権限の適用 (アクセス許可) の両方を含む強力なレベルの保護が提供されます。|他のすべてのアプリケーションとファイルの種類については、ジェネリック保護で、ファイルの種類として .pfile を使用したファイルのカプセル化と、ユーザーにファイルを開く権限があるかどうかを確認する認証の両方を含むレベルの保護が提供されます。|
|保護|ファイルの保護は次の方法で適用されます。<br /><br />- 保護されたコンテンツが表示される前に、電子メールでファイルを受け取るユーザー、あるいはファイルや共有のアクセス許可によってそれに対するアクセス権が付与されるユーザーについて、認証が正しく行われる必要があります。<br /><br />- さらに、ファイルが保護されたときにコンテンツの所有者によって設定された使用権限およびポリシーは、コンテンツが Azure Information Protection ビューアーで表示される (保護されたテキストとイメージ ファイルの場合) か、関連付けられたアプリケーションで表示される (他のサポートされているすべてのファイルの種類の場合) ときに適用されます。|ファイルの保護は次の方法で適用されます。<br /><br />- 保護されたコンテンツが表示される前に、ファイルを開く権限があり、それに対するアクセス権が付与されるユーザーについて、認証が正しく行われる必要があります。 承認に失敗すると、ファイルは開きません。<br /><br />- コンテンツの所有者によって設定された使用権限とポリシーが表示され、目的の使用ポリシーが承認済みユーザーに通知されます。<br /><br />- 承認済みユーザーがファイルを開きアクセスしていることを確認する監査ログが実行されます。 ただし、使用権限は適用されません。|
|ファイルの種類の既定値|次のファイルの種類の既定の保護レベルを次に示します。<br /><br />- テキストとイメージ ファイル<br /><br />- Microsoft Office (Word、Excel、PowerPoint) ファイル<br /><br />- Portable Document Format (.pdf)<br /><br />詳細については、下記の「[分類と保護がサポートされているファイルの種類](#supported-file-types-for-classification-and-protection)」 を参照してください。|これは、ネイティブな保護によってサポートされない他のすべてのファイルの種類 (.vsdx、.rtf など) の既定の保護です。|

Azure Information Protection の統合されたラベル付けクライアントに適用される既定の保護レベルを変更することができます。 ネイティブ ジェネリックからネイティブに汎用的で、既定のレベルを変更し、Azure Information Protection の統合されたラベル付けクライアントが保護を適用できないこともできます。 詳細については、この記事の「[ファイルの既定の保護レベルの変更](#changing-the-default-protection-level-of-files)」セクションを参照してください。

ユーザーが、管理者が構成されている機密ラベルを選択すると、保護を自動的に適用できますか、ユーザーを使用して、独自のカスタム保護設定を指定できます[アクセス許可レベル](../configure-usage-rights.md#rights-included-in-permissions-levels)します。 

### <a name="file-sizes-supported-for-protection"></a>保護がサポートされているファイルのサイズ

Azure Information Protection の統合されたラベル付けクライアントが保護をサポートする最大ファイル サイズがあります。

- **Office ファイル:**


  |                                                     Office アプリケーション                                                      |                                                サポートされる最大ファイル サイズ                                                 |
  |-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
  |             Word 2010<br /><br />Word 2013<br /><br />Word 2016             |                                          32 ビット。512 MB<br /><br />64 ビット。512 MB                                          |
  |           Excel 2010<br /><br />Excel 2013<br /><br />Excel 2016           |                      32 ビット。2 GB<br /><br />64 ビット。使用可能なディスク領域とメモリによってのみ制限されます                       |
  | PowerPoint 2010<br /><br />PowerPoint 2013<br /><br />PowerPoint 2016 | 32 ビット。使用可能なディスク領域とメモリによってのみ制限されます<br /><br />64 ビット。使用可能なディスク領域とメモリによってのみ制限されます |


- **その他のすべてのファイル**: 

  - その他のファイルの種類を保護し、これらのファイルの種類を Azure Information Protection ビューアーで開く場合:ファイルの最大サイズは、使用可能なディスク領域とメモリによってのみ制限されます。

  - [Unprotect-rmsfile](/powershell/module/azureinformationprotection/unprotect-rmsfile) コマンドレットを使用してファイルの保護を解除する場合:.pst ファイルに対してサポートされるファイルの最大サイズは 5 GB です。 その他のファイルの種類の場合は、使用可能なディスク領域とメモリによってのみ制限されます。

    ヒント:大きな .pst ファイルの保護された項目を検索したり復元したりする必要がある場合は、「[電子情報開示での Unprotect-RMSFile の使用に関するガイダンス](../configure-super-users.md#guidance-for-using-unprotect-rmsfile-for-ediscovery)」をご覧ください。

### <a name="supported-file-types-for-classification-and-protection"></a>分類と保護がサポートされているファイルの種類

次の表では、Azure Information Protection の統合されたラベル付けクライアントによってネイティブの保護を分類することもサポートするファイルの種類のサブセットを示します。 

これらの種類のファイルは、ネイティブに保護されると、元のファイルの拡張子が変更され読み取り専用になるため、別々に識別されます。 一般的に保護されるファイルの場合、元のファイル名拡張子が常に .pfile に変わる点に注意してください。

> [!WARNING]
> ファイル名拡張子に基づいて検査とアクションを実行するファイアウォール、Web プロキシ、またはセキュリティ ソフトウェアがある場合は、新しいファイル名拡張子をサポートするように、これらのネットワーク デバイスとソフトウェアの再構成が必要になる場合があります。

|元のファイル名拡張子|保護されるファイル名拡張子|
|--------------------------------|-------------------------------------|
|.txt|.ptxt|
|.xml|.pxml|
|.jpg|.pjpg|
|.jpeg|.pjpeg|
|.png|.ppng|
|.tif|.ptif|
|.tiff|.ptiff|
|.bmp|.pbmp|
|.gif|.pgif|
|.jpe|.pjpe|
|.jfif|。pjfif|
|.jt|.pjt|

次の表は、Azure Information Protection の統合されたラベル付けクライアントによってネイティブの保護を分類することもサポートする残りのファイルの種類を一覧表示します。 これらは、Microsoft Office アプリのファイルの種類であることがわかります。 これらのファイルの種類に対してサポートされるファイル形式は、次の Office プログラム用の 97-2003 ファイル形式と Office Open XML 形式です:Word、Excel、PowerPoint。

これらのファイルの場合、ファイル名拡張子は、ファイルが Rights Management サービスで保護された後も変更されません。

|Office でサポートされているファイルの種類|Office でサポートされているファイルの種類|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vsdm|.vsdx<br /><br />.vssm<br /><br />.vssx<br /><br />.vstm<br /><br />.vstx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

### <a name="changing-the-default-protection-level-of-files"></a>ファイルの既定の保護レベルの変更
Azure Information Protection の統合されたラベル付けクライアントが、レジストリを編集してファイルを保護する方法を変更することができます。 たとえば、Azure Information Protection の統合されたラベル付けクライアントで一般的に保護をネイティブ保護をサポートするファイルを強制できます。

この操作を行う必要がある理由:

- ネイティブ保護をサポートするアプリケーションがない場合に、すべてのユーザーがファイルを開けるようにするため。

- セキュリティ システムがファイル名拡張子に基づいてファイルに対するアクションを実行し、.pfile ファイル名拡張子に対応するように再構成できるが、ネイティブ保護のための複数のファイル名拡張子に対応するように再構成できないようにするため。

同様に、既定では、汎用的な保護を適用しているファイルにネイティブな保護を適用する Azure Information Protection のクライアントを統一されたにラベル付けを強制することができます。 この操作は、RMS API をサポートするアプリケーションがあるときに適切な場合があります。 たとえば、社内開発者によって作成された基幹業務アプリケーションや、独立系ソフトウェア ベンダー (ISV) から購入したアプリケーションです。

ファイルの保護をブロックする Azure Information Protection のクライアントを統一されたにラベル付けを強制することもできます (ネイティブ保護または汎用的な保護は適用されません)。 たとえば、内容を処理するために特定のファイルを開く必要がある自動化されたアプリケーションやサービスがある場合に、この操作が必要になることがあります。 ファイルの種類の保護をブロックすると、ユーザーは、そのファイルの種類を含むファイルを保護するのに Azure Information Protection の統合されたラベル付けクライアントを使用できません。 ユーザーがこの操作を試みると、管理者が保護できないように設定したことと、ファイルを保護するには操作を取り消す必要があることを示すメッセージが表示されます。

既定では、ネイティブ保護を適用しているすべてのファイルに汎用的な保護を適用する Azure Information Protection のクライアントを統一されたにラベル付けを構成するには、次のレジストリ編集を行います。 FileProtection キーが存在しない場合は、手動でそれを作成する必要があることに注意してください。

1. ファイルにファイル拡張子があることを示す * という名前の新しいキーを次のレジストリのパスに作成します。

    - 32 ビット版の Windows の場合:**HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection**

    - 64 ビット版の Windows の場合:**HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\FileProtection** および **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection**

2. 新しく追加したキー (例: HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\\\*) の中に、新しい文字列値 (REG_SZ) を **Encryption** という名前で作成し、データ値は **Pfile** とします。

    この設定により、Azure Information Protection クライアントは汎用的な保護を適用します。

これら 2 つの設定と、ファイル名の拡張子を持つすべてのファイルに汎用的な保護を適用する、Azure Information Protection の統合のラベル付けクライアント。 これが目的である場合、それ以上の構成は必要ありません。 ただし、引き続きネイティブで保護されるように、特定のファイルの種類の例外を定義できます。 そのためには、以下のように、ファイルの種類ごとに追加で 3 つ (32 ビット Windows の場合) または 6 つ (64 ビット Windows の場合) のレジストリ編集を行う必要があります。

1. **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection** および **HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\FileProtection** (該当する場合):ファイル名拡張子 (ピリオドは付けません) なしの名前を持つ新しいキーを追加します。

    たとえば、.docx というファイル名拡張子を持つファイルの場合、 **DOCX**という名前のキーを作成します。

2. 新たに追加したファイル種類のキー (たとえば、**HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**) で、値が **0** の **AllowPFILEEncryption** という新しい DWORD 値を作成します。

3. 新たに追加したファイル種類のキー (たとえば、**HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**) で、値が **Native** の **Encryption** という新しい文字列値を作成します。

これらの設定の結果、.docx というファイル名拡張子を持つファイルを除き、すべてのファイルが一般的に保護されます。 これらのファイルは、Azure Information Protection の統合されたラベル付けクライアントによってネイティブに保護されます。

ネイティブ保護をサポートし、それらを Azure Information Protection の統合されたラベル付けクライアントで一般的に保護しないため、例外として定義するその他のファイルの種類には、これら 3 つの手順を繰り返します。

次の値をサポートする **Encryption** 文字列の値を変更することで、他のシナリオで同様のレジストリ編集を行うことができます。

- **Pfile**: 汎用的な保護

- **Native**: ネイティブ保護

- **Off**: 保護のブロック

これらのレジストリに変更を加えた後、コンピューターを再起動する必要はありません。 ただし、ファイルを保護するために PowerShell コマンドを使っている場合は、変更を反映させるために新しい PowerShell セッションを開始する必要があります。

ファイルの既定の保護レベルを変更するためのレジストリの編集について詳しくは、開発者ガイドの「[ファイル API の構成](../develop/file-api-configuration.md)」をご覧ください。 この開発者向けドキュメントでは、汎用的な保護は "PFile" と呼ばれています。

## <a name="file-types-that-are-excluded-from-classification-and-protection"></a>分類と保護から除外されるファイルの種類

コンピューターの動作に不可欠なファイルをユーザーが変更しないように、一部のファイルの種類とフォルダーは分類と保護から自動的に除外されます。 ユーザーは、分類または Azure Information Protection の統合されたラベル付けクライアントを使用してこれらのファイルを保護すると、除外されているメッセージが表示されます。

- **除外されるファイルの種類**: .lnk、.exe、.com、.cmd、.bat、.dll、.ini、.pst、.sca、.drm、.sys、.cpl、.inf、.drv、.dat、.tmp、msg、.msp、.msi、.pdb、.jar


- **除外されるフォルダー**: 
    - Windows
    - Program Files (\Program Files および \Program Files (x86))
    - \ProgramData 
    - \AppData (すべてのユーザー)


### <a name="files-that-cannot-be-protected-by-default"></a>既定では保護できないファイル

パスワードで保護されているすべてのファイル ネイティブ保護できません、Azure Information Protection の統合されたラベル付けクライアントによってファイルが、保護を適用するアプリケーションで現在開いていない場合。 パスワード保護されている PDF ファイルをよく見かけますが、Office アプリなど、他のアプリケーションもこの機能を備えています。

### <a name="limitations-for-container-files-such-as-zip-files"></a>.zip ファイルなど、コンテナー ファイルの制限事項

コンテナー ファイルは、その他のファイルが含まれるファイルです。典型的な例は、圧縮ファイルが含まれる .zip ファイルです。 その他の例には、.rar、.7z、.msg ファイルや、添付ファイルを含む PDF ドキュメントなどが含まれます。

これらのコンテナー ファイルを分類し、保護できますが、分類と保護はコンテナー内の各ファイルに適用されません。

分類され、保護されているファイルがコンテナー ファイル内にある場合、先にファイルを抽出し、分類または保護設定を変更する必要があります。

Azure Information Protection ビューアーでは、保護された PDF ドキュメント内の添付ファイルを開くことはできません。 このシナリオでは、ビューアーでドキュメントを開いたときに、添付ファイルは表示されません。

## <a name="next-steps"></a>次の手順
Azure Information Protection の統合されたラベル付けクライアントでサポートされるファイルの種類を特定したら、これでは、このクライアントをサポートする必要があります追加情報については、次のリソースを参照してください。

- [カスタマイズ](clientv2-admin-guide-customizations.md)

- [クライアント ファイルおよび使用状況ログの記録](clientv2-admin-guide-files-and-logging.md)

- [PowerShell コマンド](clientv2-admin-guide-powershell.md)

