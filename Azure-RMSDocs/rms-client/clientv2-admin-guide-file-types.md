---
title: サポートされるファイルの種類-Azure Information Protection 統合されたラベル付けクライアント
description: サポートされているファイルの種類、ファイル名拡張子、および管理者の保護レベルに関する技術的な詳細については、「Windows 用の Azure Information Protection 統合ラベル付けクライアント」をご覧ください。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 06/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 779eb6e3847aaccaef47753bd75c1052a56c1180
ms.sourcegitcommit: 6d10435c67434bdbbdd51b4a3535d0efaf8307da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86868895"
---
# <a name="admin-guide-file-types-supported-by-the-azure-information-protection-unified-labeling-client"></a>管理者ガイド: Azure Information Protection 統合されたラベル付けクライアントでサポートされるファイルの種類

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012*>
>
> **Windows 7 と Office 2010 向けに拡張された Microsoft サポートをご利用のお客様は、これらのバージョンの Azure Information Protection サポートを受けることもできます。詳細については、サポート担当者にお問い合わせください。*
>
> *手順: [Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Azure Information Protection の統一されたラベル付けクライアントは、次のものをドキュメントや電子メールに適用できます。

- 分類のみ

- 分類と保護

- 保護のみ

Azure Information Protection の統一されたラベル付けクライアントは、既知の機密情報の種類または定義した正規表現を使用して、一部のファイルの種類の内容を検査することもできます。

次の情報を使用して、Azure Information Protection 統合ラベルクライアントがサポートするファイルの種類を確認し、さまざまな保護レベルを理解し、既定の保護レベルを変更し、分類と保護から自動的に除外 (スキップ) されるファイルを特定します。

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

- **Microsoft Office**: 次の表に示すファイルの種類。

    これらのファイルの種類に対してサポートされるファイル形式は、次の Office プログラム用の 97-2003 ファイル形式と Office Open XML 形式です: Word、Excel、PowerPoint。

    |Office ファイルの種類|Office ファイルの種類|
    |----------------------------------|----------------------------------|
    |.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vdw<br /><br />.vsd|.vsdm<br /><br /> .vsdx<br /><br />.vss<br /><br />.vssm<br /><br />.vst<br /><br />.vstm<br /><br />.vssx<br /><br />.vstx<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx|

他のファイルの種類では、保護されている場合に分類がサポートされます。 これらのファイルの種類については、下記の「[分類と保護がサポートされているファイルの種類](#supported-file-types-for-classification-and-protection)」を参照してください。

例 :

- **一般**秘密度ラベルが分類を適用し、保護を適用しない場合: sales.pdf という名前のファイルに**general**ラベルを適用できますが、このラベルを sales.txt という名前のファイルに適用することはできません。

- [**社外秘 \ すべての従業員の機密**度] ラベルに分類と保護が適用される場合は、このラベルを sales.pdf という名前のファイルと sales.txt という名前のファイルに適用できます。 また、保護のみをこれらのファイルに適用し、分類は対象外とすることも可能です。

## <a name="file-types-supported-for-protection"></a>保護がサポートされているファイルの種類

Azure Information Protection の統合ラベル付けクライアントは、次の表に示すように、2つの異なるレベルの保護をサポートします。

|保護の種類|ネイティブ|ジェネリック|
|----------------------|----------|-----------|
|説明|テキスト、イメージ、Microsoft Office (Word、Excel、PowerPoint) ファイル、.pdf ファイル、および Rights Management サービスをサポートする他のアプリケーションのファイルの種類については、ネイティブ保護で、暗号化と権限の適用 (アクセス許可) の両方を含む強力なレベルの保護が提供されます。|他のすべてのアプリケーションとファイルの種類では、.pfile ファイルの種類を使用したファイルのカプセル化と、ユーザーがファイルを開くことを許可されているかどうかの検証を含む、一般的な保護が提供されます。|
|保護|ファイルの保護は次の方法で適用されます。<br /><br />- 保護されたコンテンツが表示される前に、電子メールでファイルを受け取るユーザー、あるいはファイルや共有のアクセス許可によってそれに対するアクセス権が付与されるユーザーについて、認証が正しく行われる必要があります。<br /><br />- さらに、ファイルが保護されたときにコンテンツの所有者によって設定された使用権限およびポリシーは、コンテンツが Azure Information Protection ビューアーで表示される (保護されたテキストとイメージ ファイルの場合) か、関連付けられたアプリケーションで表示される (他のサポートされているすべてのファイルの種類の場合) ときに適用されます。|ファイルの保護は次の方法で適用されます。<br /><br />- 保護されたコンテンツが表示される前に、ファイルを開く権限があり、それに対するアクセス権が付与されるユーザーについて、認証が正しく行われる必要があります。 認証が失敗した場合、ファイルは開きません。<br /><br />- コンテンツの所有者によって設定された使用権限とポリシーが表示され、目的の使用ポリシーが承認済みユーザーに通知されます。<br /><br />- 承認済みユーザーがファイルを開きアクセスしていることを確認する監査ログが実行されます。 ただし、使用権限は適用されません。|
|ファイルの種類ごとの既定値|これは、次のファイルの種類の既定の保護レベルです。<br /><br />- テキストとイメージ ファイル<br /><br />- Microsoft Office (Word、Excel、PowerPoint) ファイル<br /><br />- Portable Document Format (.pdf)<br /><br />詳細については、下記の「[分類と保護がサポートされているファイルの種類](#supported-file-types-for-classification-and-protection)」 を参照してください。|これは、ネイティブな保護によってサポートされない他のすべてのファイルの種類 (.vsdx、.rtf など) の既定の保護です。|

Azure Information Protection 統合されたラベル付けクライアントまたはスキャナーによって適用される既定の保護レベルを変更することはできません。 ただし、保護するファイルの種類を変更することはできます。 詳細については、「[保護するファイルの種類を変更](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect)する」を参照してください。

保護は、管理者が構成した機密ラベルをユーザーが選択したときに自動的に適用することも、ユーザーが[アクセス許可レベル](../configure-usage-rights.md#rights-included-in-permissions-levels)を使用して独自のカスタム保護設定を指定することもできます。

### <a name="file-sizes-supported-for-protection"></a>保護がサポートされているファイルのサイズ

Azure Information Protection 統合されたラベル付けクライアントが保護のためにサポートする最大ファイルサイズがあります。

- **Office ファイル:**

  |                                                     Office アプリケーション                                                      |                                                サポートされる最大ファイル サイズ                                                 |
  |-----------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
  |             Word 2010<br /><br />Word 2013<br /><br />Word 2016             |                                          32 ビット: 512 MB<br /><br />64 ビット: 512 MB                                          |
  |           Excel 2010<br /><br />Excel 2013<br /><br />Excel 2016           |                      32 ビット: 2 GB<br /><br />64 ビット: 使用可能なディスク領域とメモリによってのみ制限されます                       |
  | PowerPoint 2010<br /><br />PowerPoint 2013<br /><br />PowerPoint 2016 | 32 ビット: 使用可能なディスク領域とメモリによってのみ制限されます<br /><br />64 ビット: 使用可能なディスク領域とメモリによってのみ制限されます |

- **その他のすべてのファイル**:

  - その他のファイルの種類を保護し、これらのファイルの種類を Azure Information Protection ビューアーで開く場合: ファイルの最大サイズは、使用可能なディスク領域とメモリによってのみ制限されます。

  - [Unprotect-rmsfile](/powershell/module/azureinformationprotection/unprotect-rmsfile) コマンドレットを使用してファイルの保護を解除する場合: .pst ファイル向けにサポートされるファイルの最大サイズは 5 GB です。 その他のファイルの種類の場合は、使用可能なディスク領域とメモリによってのみ制限されます。

    ヒント: 大きな .pst ファイルの保護された項目を検索したり復元する必要がある場合、「[Guidance for using Unprotect-RMSFile for eDiscovery](../configure-super-users.md#guidance-for-using-unprotect-rmsfile-for-ediscovery)」 (電子情報開示での Unprotect-RMSFile の使用に関するガイダンス) を参照してください。

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
|.jfif|.pjfif|
|.jt|.pjt|

次の表に、Azure Information Protection 統合されたラベル付けクライアントによるネイティブ保護をサポートするその他のファイルの種類の一覧を示します。これは、分類することもできます。 これらは、Microsoft Office アプリのファイルの種類であることがわかります。 これらのファイルの種類に対してサポートされるファイル形式は、次の Office プログラム用の 97-2003 ファイル形式と Office Open XML 形式です: Word、Excel、PowerPoint。

これらのファイルの場合、ファイル名拡張子は、ファイルが Rights Management サービスで保護された後も変更されません。

|Office でサポートされるファイルの種類|Office でサポートされるファイルの種類|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vsdm|.vsdx<br /><br />.vssm<br /><br />.vssx<br /><br />.vstm<br /><br />.vstx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

## <a name="file-types-that-are-excluded-from-classification-and-protection"></a>分類と保護から除外されるファイルの種類

コンピューターの動作に不可欠なファイルをユーザーが変更しないように、一部のファイルの種類とフォルダーは分類と保護から自動的に除外されます。 ユーザーが Azure Information Protection 統合されたラベル付けクライアントを使用してこれらのファイルを分類または保護しようとすると、除外されていることを示すメッセージが表示されます。

- **除外されるファイルの種類**: .lnk、.exe、.com、.cmd、.bat、.dll、.ini、.pst、.sca、.drm、.sys、.cpl、.inf、.drv、.dat、.tmp、.msp、.msi、.pdb、.jar

- **除外されるフォルダー**:
    - Windows
    - Program Files (\Program Files および \Program Files (x86))
    - \ProgramData
    - \AppData (すべてのユーザー)

### <a name="file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-scanner"></a>Azure Information Protection スキャナーによる分類と保護から除外されるファイルの種類

既定では、スキャナーは、次の例外を除き、Azure Information Protection 統合されたラベル付けクライアントと同じファイルの種類を除外します。

- .msg、.rtf、および rar も除外されます。

スキャナーによるファイル検査について、対象または対象外となるファイルの種類を変更することができます。

- [Azure portal を使って](../deploy-aip-scanner-configure-install.md#configure-the-scanner-in-the-azure-portal)、スキャナー プロファイルの **[スキャンするファイルの種類]** を構成します。
    
    > [!NOTE]
    > スキャン対象に .rtf ファイルを含める場合は、スキャナーを注意深く監視してください。 一部の .rtf ファイルはスキャナーで正常に検査できません。このようなファイルの検査は完了せず、サービスを再開する必要があります。

既定では、スキャナーによって保護されるのは、Office ファイルの種類と、PDF の暗号化のための ISO 標準を使用して保護されている PDF ファイルだけです。 スキャナーのこの動作を変更するには、PowerShell の詳細設定の**PFileSupportedExtensions**を使用します。 詳細については、「 [PowerShell を使用して、保護するファイルの種類](../deploy-aip-scanner-configure-install.md#change-which-file-types-to-protect)をスキャナーの展開手順から変更する」を参照してください。

### <a name="files-that-cannot-be-protected-by-default"></a>既定では保護できないファイル

パスワードで保護されているファイルは、保護を適用するアプリケーションでファイルが現在開いていない限り、Azure Information Protection 統合されたラベル付けクライアントでネイティブに保護することはできません。 パスワード保護されている PDF ファイルをよく見かけますが、Office アプリなど、他のアプリケーションもこの機能を備えています。

### <a name="limitations-for-container-files-such-as-zip-files"></a>.zip ファイルなど、コンテナー ファイルの制限事項

詳細については、 [Azure Information Protection](../known-issues.md#client-support-for-container-files-such-as-zip-files)に関する既知の問題を参照してください。

## <a name="file-types-supported-for-inspection"></a>検査に対してサポートされているファイルの種類

追加の構成を行わないと、Azure Information Protection 統合されたラベル付けクライアントは、Windows IFilter を使用してドキュメントの内容を検査します。 Windows IFilter は、インデックス作成のために Windows Search によって使用されます。 その結果、 [Set-aipfileclassification](/powershell/module/azureinformationprotection/set-aipfileclassification) PowerShell コマンドを使用すると、次のファイルの種類を検査できます。

|アプリケーションの種類|ファイルの種類|
|--------------------------------|-------------------------------------|
|Word|ドック.docx; .docm; .dot; normal.dotm; .dotx|
|Excel|.xls; .xlt; .xlsx; .xltx; .xltm; .xlsm; .xlsb|
|PowerPoint|.ppt; .pps; .pot; .pptx; .ppsx; .pptm; .ppsm; .potx; .potm|
|PDF |.pdf|
|Text|.txt; .xml; .csv|

構成を追加すると、その他のファイルの種類も検査できます。 たとえば、[カスタム ファイル名拡張子を登録してテキスト ファイルに既存の Windows フィルター ハンドラーを使用する](https://docs.microsoft.com/windows/desktop/search/-search-ifilter-registering-filters)ことや、ソフトウェア ベンダーから追加のフィルターをインストールすることができます。

インストールされているフィルターを確認する方法については、Windows Search 開発者ガイドの「[Finding a Filter Handler for a Given File Extension (特定のファイル拡張子用のフィルター ハンドラーの検索)](https://docs.microsoft.com/windows/desktop/search/-search-ifilter-registering-filters#finding-a-filter-handler-for-a-given-file-extension)」セクションをご覧ください。

以下のセクションでは、.zip ファイルと .tiff ファイルを検査するための構成方法について説明します。

### <a name="to-inspect-zip-files"></a>.zip ファイルを検査するには

以下の手順のようにすると、Azure Information Protection スキャナーおよび [Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification) PowerShell コマンドで .zip ファイルを検査できます。

1. スキャナーまたは PowerShell セッションが実行されているコンピューターに、[Office 2010 Filter Pack SP2](https://support.microsoft.com/help/2687447/description-of-office-2010-filter-pack-sp2) をインストールします。

2. スキャナーの場合: 機密情報を見つけた後、.zip ファイルをラベルで分類して保護する必要がある場合は、「 [powershell を使用して保護するファイルの種類](../deploy-aip-scanner-configure-install.md#change-which-file-types-to-protect)をスキャナーの展開手順から変更する」の説明に従って、powershell の詳細設定**PFileSupportedExtensions**を使用して .zip ファイル名拡張子を指定します。

これらの手順の実行後のシナリオ例:

**accounts.zip** という名前のファイルには、クレジット カード番号が含まれる Excel のスプレッドシートが含まれています。 **機密 \ Finance**という名前の秘密度ラベルがあり、クレジットカード番号を検出するように構成されています。また、金融グループへのアクセスを制限する保護を使用してラベルを自動的に適用します。

ファイルを検査した後、PowerShell セッションからの統一されたラベル付けクライアントは、このファイルを**機密 \ Finance**として分類し、ファイルに汎用的な保護を適用して、Finance グループのメンバーだけがそのファイルを解凍し、ファイル**accounts.zip pfile**の名前を変更します。

### <a name="to-inspect-tiff-files-by-using-ocr"></a>OCR を使用して .tiff ファイルを検査するには

[AIPFileClassiciation](/powershell/module/azureinformationprotection/set-aipfileclassification) powershell コマンドは、Windows tiff ifilter 機能をインストールするときに、光学式文字認識 (OCR) を使用して tiff ファイル名拡張子を持つ tiff イメージを検査し、powershell セッションを実行しているコンピューターで[Windows tiff ifilter 設定](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/dd744701%28v%3dws.10%29)を構成できます。

スキャナーの場合: 機密情報を見つけた後、tiff ファイルをラベルで分類して保護する必要がある場合は、powershell の詳細設定**PFileSupportedExtensions**でこのファイル名拡張子を指定します。詳細については、「Powershell を使用して、スキャナーの展開手順から[保護するファイルの種類を変更する](../deploy-aip-scanner-configure-install.md#change-which-file-types-to-protect)」を参照してください。

## <a name="next-steps"></a>次のステップ

Azure Information Protection 統合されたラベル付けクライアントでサポートされるファイルの種類を確認したので、このクライアントのサポートに必要な追加情報については、次のリソースを参照してください。

- [カスタマイズ](clientv2-admin-guide-customizations.md)

- [クライアントのファイルと使用状況ログ](clientv2-admin-guide-files-and-logging.md)

- [PowerShell コマンド](clientv2-admin-guide-powershell.md)
