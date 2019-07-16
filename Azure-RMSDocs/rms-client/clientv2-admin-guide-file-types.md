---
title: サポートされるファイルの種類-Azure Information Protection 統合されたラベル付けクライアント
description: サポートされているファイルの種類、ファイル名拡張子、および管理者の保護レベルに関する技術的な詳細については、「Windows 用の Azure Information Protection 統合ラベル付けクライアント」をご覧ください。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: a0da6a6390089c7d399ec4c2140feead3c015aa5
ms.sourcegitcommit: fdc1f3d76b48f4e865a538087d66ee69f0f9888d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68141624"
---
# <a name="admin-guide-file-types-supported-by-the-azure-information-protection-unified-labeling-client"></a>管理者ガイド: Azure Information Protection 統合ラベル付けクライアントでサポートされるファイルの種類

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*>
>
> *手順:[Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection の統一されたラベル付けクライアントは、次のものをドキュメントや電子メールに適用できます。

- 分類のみ

- 分類と保護

- 保護のみ

Azure Information Protection の統一されたラベル付けクライアントは、既知の機密情報の種類または定義した正規表現を使用して、一部のファイルの種類の内容を検査することもできます。

次の情報を使用して、Azure Information Protection 統合されたラベル付けクライアントがサポートするファイルの種類を確認し、さまざまな保護レベルを理解し、既定の保護レベルを変更する方法と、自動的にファイルを識別する方法について説明します。分類と保護から除外 (スキップ)。

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

次に例を示します。

- **一般**秘密度ラベルが分類を適用し、保護を適用しない場合:**全般ラベル**の場合 sales.pdf という名前のファイルに適用することは可能ですが、sales.txt という名前のファイルに適用することはできません。 

- **社外秘 \ すべての従業員の機密**度ラベルに分類と保護が適用される場合:このラベルの場合は、sales.pdf とい名前のファイルと sales.txt という名前のファイルに、このラベルを適用することが可能です。 また、保護のみをこれらのファイルに適用し、分類は対象外とすることも可能です。

## <a name="file-types-supported-for-protection"></a>保護がサポートされているファイルの種類

Azure Information Protection の統合ラベル付けクライアントは、次の表に示すように、2つの異なるレベルの保護をサポートします。

|保護の種類|ネイティブ|ジェネリック|
|----------------------|----------|-----------|
|説明|テキスト、イメージ、Microsoft Office (Word、Excel、PowerPoint) ファイル、.pdf ファイル、および Rights Management サービスをサポートする他のアプリケーションのファイルの種類については、ネイティブ保護で、暗号化と権限の適用 (アクセス許可) の両方を含む強力なレベルの保護が提供されます。|他のすべてのアプリケーションとファイルの種類については、ジェネリック保護で、ファイルの種類として .pfile を使用したファイルのカプセル化と、ユーザーにファイルを開く権限があるかどうかを確認する認証の両方を含むレベルの保護が提供されます。|
|保護|ファイルの保護は次の方法で適用されます。<br /><br />- 保護されたコンテンツが表示される前に、電子メールでファイルを受け取るユーザー、あるいはファイルや共有のアクセス許可によってそれに対するアクセス権が付与されるユーザーについて、認証が正しく行われる必要があります。<br /><br />- さらに、ファイルが保護されたときにコンテンツの所有者によって設定された使用権限およびポリシーは、コンテンツが Azure Information Protection ビューアーで表示される (保護されたテキストとイメージ ファイルの場合) か、関連付けられたアプリケーションで表示される (他のサポートされているすべてのファイルの種類の場合) ときに適用されます。|ファイルの保護は次の方法で適用されます。<br /><br />- 保護されたコンテンツが表示される前に、ファイルを開く権限があり、それに対するアクセス権が付与されるユーザーについて、認証が正しく行われる必要があります。 承認に失敗すると、ファイルは開きません。<br /><br />- コンテンツの所有者によって設定された使用権限とポリシーが表示され、目的の使用ポリシーが承認済みユーザーに通知されます。<br /><br />- 承認済みユーザーがファイルを開きアクセスしていることを確認する監査ログが実行されます。 ただし、使用権限は適用されません。|
|ファイルの種類の既定値|次のファイルの種類の既定の保護レベルを次に示します。<br /><br />- テキストとイメージ ファイル<br /><br />- Microsoft Office (Word、Excel、PowerPoint) ファイル<br /><br />- Portable Document Format (.pdf)<br /><br />詳細については、下記の「[分類と保護がサポートされているファイルの種類](#supported-file-types-for-classification-and-protection)」 を参照してください。|これは、ネイティブな保護によってサポートされない他のすべてのファイルの種類 (.vsdx、.rtf など) の既定の保護です。|

現時点では、Azure Information Protection 統合ラベル付けクライアントに適用される既定の保護レベルを変更することはできません。

保護は、管理者が構成した機密ラベルをユーザーが選択したときに自動的に適用することも、ユーザーが[アクセス許可レベル](../configure-usage-rights.md#rights-included-in-permissions-levels)を使用して独自のカスタム保護設定を指定することもできます。 

### <a name="file-sizes-supported-for-protection"></a>保護がサポートされているファイルのサイズ

Azure Information Protection 統合されたラベル付けクライアントが保護のためにサポートする最大ファイルサイズがあります。

- **Office ファイル:**


  |                                                     Office アプリケーション                                                      |                                                サポートされる最大ファイル サイズ                                                 |
  |-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
  |             Word 2010<br /><br />Word 2013<br /><br />Word 2016             |                                          32ビット:512 MB<br /><br />64ビット:512 MB                                          |
  |           Excel 2010<br /><br />Excel 2013<br /><br />Excel 2016           |                      32ビット:2 GB<br /><br />64ビット:使用可能なディスク領域とメモリによってのみ制限されます                       |
  | PowerPoint 2010<br /><br />PowerPoint 2013<br /><br />PowerPoint 2016 | 32ビット:使用可能なディスク領域とメモリによってのみ制限されます<br /><br />64ビット:使用可能なディスク領域とメモリによってのみ制限されます |


- **その他のすべてのファイル**: 

  - その他のファイルの種類を保護し、これらのファイルの種類を Azure Information Protection ビューアーで開く場合:ファイルの最大サイズは、使用可能なディスク領域とメモリによってのみ制限されます。

  - [Unprotect-rmsfile](/powershell/module/azureinformationprotection/unprotect-rmsfile) コマンドレットを使用してファイルの保護を解除する場合:.pst ファイルに対してサポートされるファイルの最大サイズは 5 GB です。 その他のファイルの種類の場合は、使用可能なディスク領域とメモリによってのみ制限されます。

    ヒント :大きな .pst ファイルの保護された項目を検索したり復元したりする必要がある場合は、「[電子情報開示での Unprotect-RMSFile の使用に関するガイダンス](../configure-super-users.md#guidance-for-using-unprotect-rmsfile-for-ediscovery)」をご覧ください。

### <a name="supported-file-types-for-classification-and-protection"></a>分類と保護がサポートされているファイルの種類

次の表に、Azure Information Protection 統合されたラベル付けクライアントによるネイティブ保護をサポートするファイルの種類のサブセットを示します。これは、分類することもできます。 

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

次の表に、Azure Information Protection 統合されたラベル付けクライアントによるネイティブ保護をサポートするその他のファイルの種類の一覧を示します。これは、分類することもできます。 これらは、Microsoft Office アプリのファイルの種類であることがわかります。 これらのファイルの種類に対してサポートされるファイル形式は、次の Office プログラム用の 97-2003 ファイル形式と Office Open XML 形式です:Word、Excel、PowerPoint。

これらのファイルの場合、ファイル名拡張子は、ファイルが Rights Management サービスで保護された後も変更されません。

|Office でサポートされているファイルの種類|Office でサポートされているファイルの種類|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vsdm|.vsdx<br /><br />.vssm<br /><br />.vssx<br /><br />.vstm<br /><br />.vstx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|


## <a name="file-types-that-are-excluded-from-classification-and-protection"></a>分類と保護から除外されるファイルの種類

コンピューターの動作に不可欠なファイルをユーザーが変更しないように、一部のファイルの種類とフォルダーは分類と保護から自動的に除外されます。 ユーザーが Azure Information Protection 統合されたラベル付けクライアントを使用してこれらのファイルを分類または保護しようとすると、除外されていることを示すメッセージが表示されます。

- **除外されるファイルの種類**: .lnk、.exe、.com、.cmd、.bat、.dll、.ini、.pst、.sca、.drm、.sys、.cpl、.inf、.drv、.dat、.tmp、msg、.msp、.msi、.pdb、.jar


- **除外されるフォルダー**: 
    - Windows
    - Program Files (\Program Files および \Program Files (x86))
    - \ProgramData 
    - \AppData (すべてのユーザー)

### <a name="files-that-cannot-be-protected-by-default"></a>既定では保護できないファイル

パスワードで保護されているファイルは、保護を適用するアプリケーションでファイルが現在開いていない限り、Azure Information Protection 統合されたラベル付けクライアントでネイティブに保護することはできません。 パスワード保護されている PDF ファイルをよく見かけますが、Office アプリなど、他のアプリケーションもこの機能を備えています。

### <a name="limitations-for-container-files-such-as-zip-files"></a>.zip ファイルなど、コンテナー ファイルの制限事項

コンテナー ファイルは、その他のファイルが含まれるファイルです。典型的な例は、圧縮ファイルが含まれる .zip ファイルです。 その他の例には、.rar、.7z、.msg ファイルや、添付ファイルを含む PDF ドキュメントなどが含まれます。

これらのコンテナー ファイルを分類し、保護できますが、分類と保護はコンテナー内の各ファイルに適用されません。

分類され、保護されているファイルがコンテナー ファイル内にある場合、先にファイルを抽出し、分類または保護設定を変更する必要があります。

Azure Information Protection ビューアーでは、保護された PDF ドキュメント内の添付ファイルを開くことはできません。 このシナリオでは、ビューアーでドキュメントを開いたときに、添付ファイルは表示されません。

## <a name="file-types-supported-for-inspection"></a>検査に対してサポートされているファイルの種類

追加の構成を行わないと、Azure Information Protection 統合されたラベル付けクライアントは、Windows IFilter を使用してドキュメントの内容を検査します。 Windows IFilter は、インデックス作成のために Windows Search によって使用されます。 その結果、 [Set-aipfileclassification](/powershell/module/azureinformationprotection/set-aipfileclassification) PowerShell コマンドを使用すると、次のファイルの種類を検査できます。

|アプリケーションの種類|ファイルの種類|
|--------------------------------|-------------------------------------|
|Word|.docx; .docm; .dotm; .dotx|
|Excel|.xls; .xlt; .xlsx; .xltx; .xltm; .xlsm; .xlsb|
|PowerPoint|.ppt; .pps; .pot; .pptx; .ppsx; .pptm; .ppsm; .potx; .potm|
|PDF |.pdf|
|テキスト|.txt; .xml; .csv|

構成を追加すると、その他のファイルの種類も検査できます。 たとえば、[カスタム ファイル名拡張子を登録してテキスト ファイルに既存の Windows フィルター ハンドラーを使用する](https://docs.microsoft.com/windows/desktop/search/-search-ifilter-registering-filters)ことや、ソフトウェア ベンダーから追加のフィルターをインストールすることができます。

インストールされているフィルターを確認する方法については、Windows Search 開発者ガイドの「[Finding a Filter Handler for a Given File Extension (特定のファイル拡張子用のフィルター ハンドラーの検索)](https://docs.microsoft.com/windows/desktop/search/-search-ifilter-registering-filters#finding-a-filter-handler-for-a-given-file-extension)」セクションをご覧ください。

以下のセクションでは、.zip ファイルと .tiff ファイルを検査するための構成方法について説明します。

### <a name="to-inspect-zip-files"></a>.zip ファイルを検査するには

[Set-aipfileclassification](/powershell/module/azureinformationprotection/set-aipfileclassification) powershell コマンドは、powershell セッションを実行しているコンピューターに[Office 2010 Filter Pack SP2](https://support.microsoft.com/en-us/help/2687447/description-of-office-2010-filter-pack-sp2)をインストールするときに .zip ファイルを検査できます。

これらの手順の実行後のシナリオ例: 

**accounts.zip** という名前のファイルには、クレジット カード番号が含まれる Excel のスプレッドシートが含まれています。 **機密 \ Finance**という名前の秘密度ラベルがあり、クレジットカード番号を検出するように構成されています。また、金融グループへのアクセスを制限する保護を使用してラベルを自動的に適用します。 

ファイルを検査した後、PowerShell セッションの統一されたラベル付けクライアントはこのファイルを**機密 \ Finance**として分類し、ファイルに汎用的な保護を適用します。これにより、Finance グループのメンバーだけがそのファイルを解凍し、ファイル**の名前を変更できるようになります。pfile**。

### <a name="to-inspect-tiff-files-by-using-ocr"></a>OCR を使用して .tiff ファイルを検査するには

[AIPFileClassiciation](/powershell/module/azureinformationprotection/set-aipfileclassification) PowerShell コマンドは、Windows tiff ifilter 機能をインストールするときに、光学式文字認識 (OCR) を使用して tiff ファイル名拡張子を持つ tiff イメージを検査し、 [windows tiff ifilter を構成できます。](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/dd744701%28v%3dws.10%29)PowerShell セッションを実行しているコンピューターの設定。

## <a name="next-steps"></a>次の手順
Azure Information Protection 統合されたラベル付けクライアントでサポートされるファイルの種類を確認したので、このクライアントのサポートに必要な追加情報については、次のリソースを参照してください。

- [カスタマイズ](clientv2-admin-guide-customizations.md)

- [クライアント ファイルおよび使用状況ログの記録](clientv2-admin-guide-files-and-logging.md)

- [PowerShell コマンド](clientv2-admin-guide-powershell.md)

