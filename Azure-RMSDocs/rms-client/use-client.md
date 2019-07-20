---
title: Azure Information Protection のクライアント
description: Microsoft Azure Information Protection は、組織のデータを保護するクライアント/サーバー型のソリューションです。 クライアント (Azure Information Protection クライアントまたは Rights Management クライアント) は、コンピューターおよびモバイル デバイスで実行するアプリケーションに統合されます。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/18/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
search.appverid:
- MET150
ms.openlocfilehash: e4746246c13ece385cd19f9ace8422ae6210132f
ms.sourcegitcommit: a354b71d82dc5d456bff7e4472181cbdd962948a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68352864"
---
# <a name="the-client-side-of-azure-information-protection"></a>クライアント側での Azure Information Protection

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*

Azure Information Protection は、組織の文書や電子メールを保護するクライアント/サーバー型のソリューションです。

- クライアントには、Azure Information Protection クライアント (クラシック)、Azure Information Protection 統合されたラベル付けクライアント、または Rights Management クライアントを使用できます。 どちらのクライアントを使用しても、コンピューターやモバイルデバイスで実行するアプリケーションと統合されます。 
- サービスは、クラウド (データの保護用に Azure Rights Management サービスを使用する Azure Information Protection)、またはオンプレミス (Active Directory Rights Management サービス、より一般的には AD RMS) にあります。 

Azure Information Protection クライアント (クラシック) と Azure Information Protection の統一されたラベル付けクライアントは、ラベル付きの分類と保護をサポートします。 クラシッククライアントは、ラベル付けを行わずに保護もサポートします。 両方のクライアントが Office アプリケーションと統合されているため、個別にインストールする必要があります。

Rights Management (RMS) クライアントは、Office アプリケーション、Azure Information Protection クライアント (クラシック)、Azure Information Protection の統一されたラベル付けクライアント、RMS 対応アプリケーションなど、一部のアプリケーションと共に自動的にインストールされます。ソフトウェアベンダーから。 ただし、[IRM で保護されたライブラリと OneDrive for Business のファイルの同期](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668)をサポートするため、および Rights Management の保護を基幹業務アプリケーションに統合したい開発者向けに、これを[単体でインストールする](https://www.microsoft.com/en-us/download/details.aspx?id=38396)ことも可能です。

## <a name="choose-which-azure-information-protection-client-to-use"></a>使用する Azure Information Protection クライアントを選択する

**Azure Information Protection クライアント (クラシック)** は、Azure portal からラベルとポリシー設定をダウンロードします。 このクライアントの詳細については、 [Azure Information Protection クライアントに関する説明を参照してください。バージョン リリース履歴とサポート ポリシー](client-version-release-history.md)」をご覧ください。

**Azure Information Protection 統合ラベル付けクライアント**では、次の管理センターからラベルとポリシー設定をダウンロードします: Office 365 セキュリティ/コンプライアンス センター、Microsoft 365 セキュリティ センター、Microsoft 365 コンプライアンス センター。 このクライアントの詳細については、 [Azure Information Protection 統合ラベル付けクライアント:バージョン リリース情報](unifiedlabelingclient-version-release-history.md)」を参照してください。

どのクライアントをインストールすべきでしょうか?

- MacOS、iOS、および Android でも使用できるラベルおよびポリシー設定用の Azure Information Protection 統合ラベル付けクライアントをインストールします。また、従来のクライアントでまだサポートされていない一部の機能が不要な場合はインストールします。 これらの機能には、オンプレミスのキー (HYOK) でコンテンツを保護し、オンプレミスのデータストア用のスキャナーを使用することが含まれます。

- 統一されたラベル付けクライアントでまだ使用できない機能を持つクライアントのバージョンが必要な場合は、Azure Information Protection クライアント (クラシック) をインストールします。 トレードオフは、すべてのラベル設定が他のクライアントプラットフォームで使用できるわけではなく、別の管理ポータルを使用して管理することもできます。

現時点では、従来のクライアントと、統合されたラベル付けクライアントには、その機能のためのパリティがありません。 ただし、このギャップは終了しており、新しい機能は、統合されたラベル付けクライアントにのみ追加されることを期待できます。 このため、現在の機能セットと機能がビジネス要件を満たしている場合は、統一されたラベル付けクライアントを展開することをお勧めします。 それ以外の場合、または[統合ラベルストアにまだ移行](../configure-policy-migrate-labels.md)していない Azure portal でラベルを構成した場合は、クラシッククライアントを使用します。

次の例に示すように、両方のクライアントを同じ環境にインストールし、さまざまなビジネス要件をサポートすることもできます。 このシナリオでは、管理を容易にするために、両方のクライアントセットが同じラベルのセットを共有するように、Azure portal のラベルを移行することをお勧めします。

##### <a name="example-deployment-strategy"></a>展開方法の例:

- 多くのユーザーにとっては、このクライアントがこれらのユーザーのビジネスニーズを満たしているため、Azure Information Protection 統合されたラベル付けクライアントを展開します。 
    
    これらのユーザーには、Windows、Mac、iOS、および Android に共通のラベルが発行されており、同じポリシー設定が発行されているため、ラベル付けのエクスペリエンスが非常によく似ています。 管理者は、これらのラベルとポリシー設定を同じ管理ポータルで管理します。

- ユーザーのサブセットでは、従来のクライアントを展開します。これらのユーザーには、独自のキー (HYOK) 保護を適用する1つまたは複数のラベルが必要であるためです。
    
    このようなユーザーの場合、このクライアントを使用すると、ラベル付けエクスペリエンスが若干異なります。 たとえば、Office アプリの **[秘密度]** ボタンではなく、 **[保護]** ボタンが表示されます。 管理者は、別の管理ポータルで HYOK 設定とポリシー設定のラベルを管理して、他のクライアントプラットフォームのラベルと設定を管理する必要があります。

- 機密情報のスキャンや分類、保護が必要なドキュメントを含むオンプレミスのデータストアがある。 クラシッククライアントをサーバーに展開し、Azure Information Protection スキャナーを実行します。

### <a name="compare-the-clients"></a>クライアントを比較する

次の表を使用して、2つの Azure Information Protection クライアントでサポートされている機能を比較してください。

|機能|従来のクライアント|統一されたラベル付けクライアント|
|-------|-----------------------------------|----------------------------------------------------|
|ラベル付けアクション:手動、推奨、自動| [はい] | [はい] |
|中央レポート機能 (分析):| [はい] | [はい] |
|ラベルの多言語サポート:| [はい] | [はい] |
|設定のリセットとログのエクスポート:| [はい] | [はい] |
|ユーザー定義のアクセス許可:| [はい] | はい (制限あり): <br /><br />-Outlook の場合のみ (転送不可):Supported<br /><br />-Word、Excel、PowerPoint、エクスプローラーの場合:Azure portal でラベルを構成するときにサポートされます。 |
|カスタム アクセス許可:| [はい] | エクスプローラーと PowerShell <br /><br /> Office アプリでは、別の方法として、ユーザーが **ファイル情報** >  **ドキュメント** > の保護 **アクセスの制限** または 管理者がユーザー定義のアクセス許可のラベルを構成できる を選択できます。|
|Office アプリの Information Protection バー:| [はい] | はい (制限あり):<br /><br /> - タイトルもカスタマイズ可能なヒントもありません<br /><br /> - ラベルの色は適用されたラベルに表示されません|
|ラベルでは視覚的なマーキング (ヘッダー、フッター、透かし) を適用できます。| [はい] | はい (制限あり):<br /><br /> ヘッダーとフッターでは、動的な値の変数はサポートされていません <br /><br /> Word、Excel、PowerPoint、Outlook で異なる視覚的なマーキングを使うためのサポートはありません|
|エクスプローラー、右クリック アクション:| [はい] | はい (制限あり):<br /><br /> - .ppdf 形式の PDF ドキュメントを保護できません <br /><br />  - 保護のみモードはサポートされません|
|保護されたファイル用のビューアー:| [はい] | はい (制限あり):<br /><br /> -一般的に保護されているファイル (pfile) の場合、従来のクライアントのビューアーとは異なり、最初に開いたファイルに変更を保存することはできません。|
|PowerShell コマンド:| [はい] | はい (制限あり):<br /><br />- 含まれているコマンドレット:[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)、 [New-Aipfilestatus](/powershell/module/azureinformationprotection/New-AIPCustomPermissions)、 [set-aipfileclassification](/powershell/module/azureinformationprotection/set-aipfileclassification)、 [set-aipfilelabel](/powershell/module/azureinformationprotection/set-aipfilelabel)、 [set-aipauthentication](/powershell/module/azureinformationprotection/set-aipauthentication) <br /><br />-現時点では、コンテナーファイル (zip、rar、7z、.msg、および .pst) から保護を削除することはできません。|
|保護アクションに対するオフライン サポート:| [はい] | はい (制限あり): <br /><br />- エクスプローラーおよび PowerShell コマンドについては、ファイルを保護するためにユーザーがインターネットに接続している必要があります。 |
|オフラインのコンピュータに対するポリシー ファイルを使用した手動での管理:| [はい] |いいえ |
|HYOK のサポート:| [はい] | いいえ<br /><br /> Azure portal から移行する HYOK 保護用に構成されたラベルは、Azure Information Protection 統合ラベル付けクライアントにより表示されますが、保護は適用されません。 |
|イベント ビューアーに対する使用状況ログの記録:| [はい] | いいえ|
|メールの添付ファイルからのラベル継承:| [はい] | [はい]  |
|Outlook の [転送不可] ボタンを表示する| [はい] | いいえ |
|以下を含む[カスタマイズ](client-admin-guide-customizations.md#available-advanced-client-settings):<br />- メールの既定のラベル<br />- カスタム アクセス許可を有効にする <br />- S/MIME のサポート<br />- [問題の報告] オプション| [はい] | はい ( [PowerShell](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用) |
|オンプレミスのデータ ストア用のスキャナー:| [はい] | いいえ |
|追跡と取り消し:| [はい] | いいえ |
|テンプレートを使用した保護専用モード (ラベルなし):| [はい] | いいえ |
|AD RMS のサポート:| [はい] | 次のアクションのみがサポートされます。<br /><br /> - [Active Directory Rights Management サービスのモバイル デバイス拡張機能](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))をデプロイすると、保護されたドキュメントをビューアーで開くことができます|

#### <a name="detailed-comparisons-for-the-clients"></a>クライアントの詳細な比較

両方のクライアントが同じ機能をサポートしている場合は、次の表を使用して、2つのクライアントの機能上の相違点を特定してください。

|機能 |従来のクライアント|統一されたラベル付けクライアント|
|--------------|-----------------------------------|-----------------------------------------------------------|
|セットアップ:| ローカルのデモ ポリシーをインストールするオプション | ローカルのデモ ポリシーなし|
|Office アプリで適用した場合のラベルの選択と表示:|リボン上の **[保護]** ボタンから <br /><br /> Information Protection バーから (リボンの下の水平バー)|リボン上の **[秘密度]** ボタンから<br /><br /> Information Protection バーから (リボンの下の水平バー)|
|Office アプリの Information Protection バーを管理する:|ユーザー向け: <br /><br />- リボン上の **[保護]** ボタンからバーを表示または非表示にするオプション<br /><br />- ユーザーがバーを非表示にするよう選択した場合、既定では、バーはそのアプリ内で非表示になりますが、新しく開いたアプリでは自動的に表示され続けます <br /><br /> 管理者向け: <br /><br />- アプリを最初に開いたときにバーを自動的に表示または非表示にする、および、ユーザーがバーの非表示を選択した後に新しく開いたアプリに対してバーを自動的に非表示のままにするかどうかを制御するポリシー設定|ユーザー向け: <br /><br />- リボン上の **[秘密度]** ボタンからバーを表示または非表示にするオプション<br /><br />- ユーザーがバーを非表示にするよう選択すると、バーはそのアプリ内でも新しく開いたアプリ内でも非表示になります <br /><br />管理者向け: <br /><br />-バーを管理するための PowerShell 設定 |
|ラベルの色: | Azure portal で構成します | Office 365 へのラベルの移行後に保持され、PowerShell で構成可能 <br /><br /> 色は[PowerShell](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)を使用して構成できます。|
|ラベルは、さまざまな言語をサポートします。| Azure portal で構成します | Office 365 Security & Compliance PowerShell を使用して構成し、 *LocaleSettings*パラメーターと[新しいラベル](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/new-label?view=exchange-ps)と[セットラベル](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps)を使用して構成します。|
|ポリシーの更新: | Office アプリを開いたとき <br /><br /> 右クリックしてファイルまたはフォルダーを分類して保護したとき <br /><br />ラベル付けと保護のために PowerShell コマンドレット を実行したとき<br /><br />24 時間ごと | Office アプリを開いたとき <br /><br /> 右クリックしてファイルまたはフォルダーを分類して保護したとき <br /><br />ラベル付けと保護のために PowerShell コマンドレット を実行したとき<br /><br />4 時間ごと|
|サポートされている PDF 形式:| 保護: <br /><br /> - PDF の暗号化における ISO 標準 (既定) <br /><br /> - .ppdf <br /><br /> 消費: <br /><br /> - PDF の暗号化における ISO 標準 <br /><br />- .ppdf<br /><br />- SharePoint IRM 保護| 保護: <br /><br /> - PDF の暗号化における ISO 標準 <br /><br /> <br /><br /> 消費: <br /><br /> - PDF の暗号化における ISO 標準 <br /><br />- .ppdf<br /><br />- SharePoint IRM 保護|
|サポートされているコマンドレット:| [AzureInformatioProtection](/powershell/module/azureinformationprotection) に記載されているすべてのコマンドレット | Set-aipfileclassification、Set-aipfilelabel、および Get-AIPFileStatus は SharePoint のパスをサポートしていません <br /><br /> Set-aipfileclassification と Set-aipfilelabel は*Owner*パラメーターをサポートしていません <br /><br /> さらに、ラベルが適用されないすべてのシナリオに対して、"No label to apply" (適用するラベルがありません) というコメントが 1 つ付きます <br /><br /> Set-aipfileclassification は*WhatIf*パラメーターをサポートするため、検出モードで実行できます。 <br /><br /> Set-AIPFileLabel は *EnableTracking* パラメーターをサポートしていません <br /><br /> Get-AIPFileStatus は他のテナントからのラベル情報を返しません。また、*RMSIssuedTime* パラメーターを表示しません<br /><br />また、Get-AIPFileStatus の*Labelingmethod*パラメーターには、**手動**または**自動**ではなく**Privileged**または**Standard**が表示されます。 詳細については、[オンライン ドキュメント](/powershell/module/azureinformationprotection/get-aipfilestatus)をご覧ください。|
|Office でのアクションごとの理由プロンプト (構成している場合): | 頻度:ファイルごと <br /><br /> 秘密度レベルを下げる <br /><br /> ラベルの削除<br /><br /> 保護の削除 | 頻度:セッションごと <br /><br /> 秘密度レベルを下げる<br /><br /> ラベルの削除|
|適用されたラベルのアクションを削除する: | ユーザーは確認するよう求められます <br /><br />既定のラベルや自動ラベル (構成している場合) は、Office アプリで次にファイルを開いたときに自動的に適用されません  <br /><br />| ユーザーは確認するよう求められません<br /><br /> 既定のラベルや自動ラベル (構成している場合) は、Office アプリで次にファイルを開いたときに自動的に適用されます|
|自動および推奨ラベル: | 組み込みの情報の種類と、語句や正規表現を使ったカスタム条件を使って、Azure portal で[ラベル条件](../configure-policy-classification.md)として構成されます <br /><br />構成のオプションには、次のようなものがあります。 <br /><br />- 一意の / 一意でない数 <br /><br /> - 最小数| 組み込みの機密情報の種類と[カスタムの情報の種類](https://docs.microsoft.com/office365/securitycompliance/create-a-custom-sensitive-information-type)を使用して、管理センターで構成されます<br /><br />構成のオプションには、次のようなものがあります。  <br /><br />- 一意の数のみ <br /><br />- 最小および最大数 <br /><br />- 情報の種類での AND と OR のサポート <br /><br />- キーワード ディクショナリ<br /><br />- カスタマイズ可能な信頼度レベルと文字の近接|
|自動および推奨ラベルのカスタマイズ可能なポリシーヒント: | [はい] <br /><br />Azure portal を使用して、既定のメッセージをユーザーに置き換えます。 | いいえ <br /><br /> 管理センターには、カスタマイズされたポリシーヒントを指定するオプションがありますが、このオプションは、統一されたラベル付けクライアントでは現在サポートされていません。|
|ファイルの既定の保護レベルを変更します。 | [はい] <br /><br />[レジストリの編集](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files)を使用して、ネイティブ保護と汎用保護の既定値を上書きすることができます。 | いいえ |

特定の保護設定の動作の違いの詳細な比較については、「[ラベルの保護設定の動作の比較](../configure-policy-migrate-labels.md#comparing-the-behavior-of-protection-settings-for-a-label)」を参照してください。

#### <a name="features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client"></a>Azure Information Protection 統合されたラベル付けクライアントに含まれていない機能

Azure Information Protection 統合されたラベル付けクライアントはまだ開発中ですが、従来のクライアントとの次の機能と動作の違いは、現在、統合されたラベル付けクライアントの今後のリリースで使用できるとは想定されていません。 

- ポリシーファイルの手動管理を使用して、切断されたコンピューターの Office アプリをサポートする

- Office アプリでユーザーが選択できるオプションとしてのカスタムアクセス許可:Word、Excel、PowerPoint

- Office アプリとエクスプローラーからの追跡と取り消し

- Information Protection バーのタイトルとヒント

- テンプレートを使用した保護のみのモード (ラベルなし)

- .ppdf 形式で PDF ドキュメントを保護する

- Outlook の [転送不可] ボタンを表示する

- デモ ポリシー

- 保護を削除する場合の理由

- 確認プロンプト **[このラベルを削除しますか?]** ポリシー設定を使用しない場合、ユーザーに対してこのラベルを削除します。

- 既存のカスタム プロパティを使用して Office ドキュメントにラベルを付ける (SyncPropertyName および SyncPropertyState クライアント詳細設定)

- Rights Management サービスに接続するために PowerShell コマンドレットを分離させる


#### <a name="parent-labels-and-their-sublabels"></a>親ラベルとそのサブラベル 

Azure Information Protection クライアント (クラシック) では、サブラベルを持つ親ラベルを指定する構成はサポートされていません。 これらの構成には、既定のラベルと、推奨または自動分類のラベルの指定が含まれます。 ラベルにサブラベルがある場合は、親ラベルではなく、サブラベルのいずれかを指定できます。

パリティについて、Azure Information Protection 統合ラベル付けクライアントでも、管理センターでこれらのラベルを選択できる場合でも、サブラベルのある親ラベルの適用はサポートされていません。 このシナリオでは、Azure Information Protection 統合ラベル付けクライアントで親ラベルが適用されません。

## <a name="see-also"></a>関連項目
これらのクライアントをデプロイおよび使用する方法について詳しい情報が必要な場合は、次のドキュメントを使用してください。

- [Azure Information Protection クライアント](AIP-client.md)

- [Azure Information Protection 統合ラベル付けクライアント](unifiedlabelingclient-version-release-history.md)

- [RMS クライアントのデプロイに関する注意事項](client-deployment-notes.md)

Azure Information Protection クライアント (クラシック) は AD RMS と共に使用できますが、このクライアントは Azure サービスを使用する場合に最も適しています。Azure Information Protection とその保護サービス、Azure Rights Management。 Azure Information Protection のサービス側の比較については、「[Azure Information Protection と AD RMS の比較](../compare-on-premise.md)」をご覧ください。