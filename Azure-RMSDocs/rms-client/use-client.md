---
title: Azure Information protection - AIP クライアント
description: Microsoft Azure Information Protection は、組織のデータを保護するクライアント/サーバー型のソリューションです。 クライアント (Azure Information Protection クライアントまたは Rights Management クライアント) は、コンピューターおよびモバイル デバイスで実行するアプリケーションに統合されます。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: 47a92d57b9408a1ba0a5b2d82240e24783718e60
ms.sourcegitcommit: 1ec4b926885331cb4bb31bbd5074c874205f49d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749977"
---
# <a name="the-client-side-of-azure-information-protection"></a>クライアント側での Azure Information Protection

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*

Azure Information Protection は、組織の文書や電子メールを保護するクライアント/サーバー型のソリューションです。

- クライアントは、Azure Information Protection クライアント、Azure Information Protection の統合されたラベル付けクライアントまたは Rights Management クライアントにすることができます。 コンピューターとモバイル デバイスで実行するアプリケーションと統合、これらのクライアントのどちらが使用します。 

- サービスは、クラウド (データの保護用に Azure Rights Management サービスを使用する Azure Information Protection)、またはオンプレミス (Active Directory Rights Management サービス、より一般的には AD RMS) にあります。 

Azure Information Protection クライアントと Azure Information Protection の統合されたラベル付けクライアントは、分類とラベル付けと保護をサポートします。 Azure Information Protection クライアントには、ラベルなしの保護もサポートしています。 両方のクライアントは、Office アプリケーションと統合し、個別にインストールする必要があります。

Rights Management (RMS) クライアントが Office アプリケーション、Azure Information Protection クライアントと Azure Information Protection ラベル付けのクライアント統合、および製の RMS 対応アプリケーションなど、一部のアプリケーションと共に自動的にインストールされています。ソフトウェアのベンダー。 ただし、[IRM で保護されたライブラリと OneDrive for Business のファイルの同期](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668)をサポートするため、および Rights Management の保護を基幹業務アプリケーションに統合したい開発者向けに、これを[単体でインストールする](https://www.microsoft.com/en-us/download/details.aspx?id=38396)ことも可能です。

## <a name="choose-which-azure-information-protection-client-to-use"></a>使用する Azure Information Protection クライアントを選択する

**Azure Information Protection クライアント**ラベルとポリシー設定を Azure portal からダウンロードします。 このクライアントの詳細については、次を参照してください。、 [Azure Information Protection クライアント。バージョン リリース履歴とサポート ポリシー](client-version-release-history.md)」をご覧ください。

**Azure Information Protection 統合ラベル付けクライアント**では、次の管理センターからラベルとポリシー設定をダウンロードします: Office 365 セキュリティ/コンプライアンス センター、Microsoft 365 セキュリティ センター、Microsoft 365 コンプライアンス センター。 このクライアントの詳細については、次を参照してください。、 [Azure Information Protection クライアントのラベル付けを統合します。バージョン リリース情報](unifiedlabelingclient-version-release-history.md)」を参照してください。

どのクライアントをインストールすべきでしょうか?

- インストールは、Azure Information Protection unified MacOS、iOS、Android、によっても使用できるラベルのラベル付けのクライアントとユーザー定義アクセス許可は、オンプレミスのキー (HYOK) の高度なクライアントの設定などの高度な機能を必要としない場合、またはスキャナーのオンプレミス データ ストア。

- まだ統合型のラベル付けクライアントで使用できる高度な機能を作成する必要がありますが、他のクライアント プラットフォームで、ラベルは使用できませんがある場合は、Azure Information Protection クライアントをインストールします。

現時点では、Azure Information Protection クライアントと Azure Information Protection の統合されたラベル付けクライアントは、その機能のパリティを必要はありません。 ただし、このギャップはなくなる予定であり、新しい機能は Azure Information Protection 統合ラベル付けクライアントにのみ追加されます。 このため、その現在の機能セットと機能は、ビジネス要件を満たしている場合、Azure Information Protection の統合されたラベル付けクライアントを展開するをお勧めします。 そうでない場合、または Azure portal でラベルを構成し、それをまだ[統合ラベル付けストアに移行](../configure-policy-migrate-labels.md)していない場合は、Azure Information Protection クライアントを使います。

次の例のように、さまざまなビジネスの要件をサポートするために同じ環境内で両方のクライアントをインストールできます。 このシナリオでは、クライアントの両方のセットは、管理容易性のラベルの同じセットを共有できるように、Azure portal で、ラベルの移行をお勧めします。

##### <a name="example-deployment-strategy"></a>展開戦略の例:

- ほとんどのユーザーは、ほとんどのユーザーが Azure Information Protection クライアントでのみ利用できる機能や機能に必要ないため、Azure Information Protection の統一されたラベル付けクライアントを展開します。 
    
    これらのユーザーがラベル付けの操作は、MacOS、iOS、および Android を実行するデバイスもあるし、これらのデバイス秘密度ラベルをサポートする Office のバージョンがない場合とよく似ています。

- ユーザーのサブセットを適用するラベルを保持、独自のキー (HYOK) 保護またはユーザー定義のアクセス許可をプロンプトにこれらのユーザーが必要なため、Azure Information Protection クライアントを展開します。
    
    これらのユーザーの追加機能と機能があるが、機密ラベルをサポートする Office のバージョンの MacOS、iOS、および Android を実行しているデバイスとこれらのデバイスにも持っている場合に、若干異なる経験があります。 たとえば、表示、**保護**ボタンではなく**感度**既定では、Office のリボンで、Information Protection バーのボタンを表示することができます。

- 機密の情報をスキャンまたは分類および保護する必要があるドキュメントをオンプレミス データ ストアがあります。 Azure Information Protection スキャナーを実行するサーバー上で Azure Information Protection クライアントを展開するとします。

### <a name="compare-the-clients"></a>クライアントを比較します。

2 つの Azure Information Protection クライアントでサポートされている機能を比較できるように、次の表を使用します。

|機能|Azure Information Protection クライアント|Azure Information Protection<br /> 統合ラベル付けクライアント|
|-------|-----------------------------------|----------------------------------------------------|
|ラベル付けアクション:手動、推奨、自動| [はい] | [はい] |
|中央レポート機能 (分析):| [はい] | はい (制限あり):<br /><br /> -サポート[コンテンツの一致](../reports-aip.md#content-matches-for-deeper-analysis) |
|設定のリセットとログのエクスポート:| はい | はい |
|ユーザー定義のアクセス許可:| [はい] | Outlook のみ (転送不可) |
|カスタム アクセス許可:| [はい] | エクスプローラーのみ <br /><br /> Office アプリでは、代替として、 **[ファイル情報]**  >  **[文書の保護]**  >  **[アクセスの制限]** を選択できます |
|Office アプリの Information Protection バー:| はい | はい (制限あり):<br /><br /> - タイトルもカスタマイズ可能なヒントもありません<br /><br /> - ラベルの色は適用されたラベルに表示されません|
|ラベルでは視覚的なマーキング (ヘッダー、フッター、透かし) を適用できます。| はい | はい (制限あり):<br /><br /> ヘッダーとフッターでは、動的な値の変数はサポートされていません <br /><br /> Word、Excel、PowerPoint、Outlook で異なる視覚的なマーキングを使うためのサポートはありません|
|エクスプローラー、右クリック アクション:| はい | はい (制限あり):<br /><br /> - .ppdf 形式の PDF ドキュメントを保護できません <br /><br />  - 保護のみモードはサポートされません|
|保護されたファイル用のビューアー:| はい | はい (制限あり):<br /><br /> 一般的に保護されたファイル (.pfile) に関しては、Azure Information Protection クライアントのビューアーとは異なり、最初に開いたファイルへの変更を保存することができません。|
|PowerShell コマンド:| [はい] | はい (制限あり):<br /><br />- 含まれているコマンドレット:[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)、[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)、[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)、[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) <br /><br />- 保護サービスに直接接続するコマンドレットは含まれていません|
|保護アクションに対するオフライン サポート:| [はい] | はい (制限あり): <br /><br />- エクスプローラーおよび PowerShell コマンドについては、ファイルを保護するためにユーザーがインターネットに接続している必要があります。 |
|オフラインのコンピュータに対するポリシー ファイルを使用した手動での管理:| はい |いいえ |
|HYOK のサポート:| [はい] | いいえ<br /><br /> Azure portal から移行する HYOK 保護用に構成されたラベルは、Azure Information Protection 統合ラベル付けクライアントにより表示されますが、保護は適用されません。 |
|イベント ビューアーに対する使用状況ログの記録:| [はい] | いいえ|
|メールの添付ファイルからのラベル継承:| [はい] | いいえ |
|Outlook の [転送不可] ボタンを表示する| [はい] | いいえ |
|以下を含む[カスタマイズ](client-admin-guide-customizations.md#available-advanced-client-settings):<br />- メールの既定のラベル<br />- カスタム アクセス許可を有効にする <br />- S/MIME のサポート<br />- [問題の報告] オプション| はい | いいえ |
|オンプレミスのデータ ストア用のスキャナー:| はい | いいえ |
|追跡と取り消し:| [はい] | いいえ |
|保護のみモード (ラベルなし):| [はい] | いいえ |
|多言語のサポート:| [はい] | いいえ |
|AD RMS のサポート:| はい | 次のアクションのみがサポートされます。<br /><br /> - [Active Directory Rights Management サービスのモバイル デバイス拡張機能](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574\(v=ws.11\))をデプロイすると、保護されたドキュメントをビューアーで開くことができます|

#### <a name="detailed-comparisons-for-the-clients"></a>クライアントの詳細な比較

両方のクライアントでは、同じ機能がサポートされている場合は、2 つのクライアントのいくつか機能の違いを識別できるように、次の表を使用します。

|機能 |Azure Information Protection クライアント|Azure Information Protection<br /> 統合ラベル付けクライアント|
|--------------|-----------------------------------|-----------------------------------------------------------|
|セットアップ:| ローカルのデモ ポリシーをインストールするオプション | ローカルのデモ ポリシーなし|
|Office アプリで適用した場合のラベルの選択と表示:|リボン上の **[保護]** ボタンから <br /><br /> Information Protection バーから (リボンの下の水平バー)|リボン上の **[秘密度]** ボタンから<br /><br /> Information Protection バーから (リボンの下の水平バー)|
|Office アプリの Information Protection バーを管理する:|ユーザー向け: <br /><br />- リボン上の **[保護]** ボタンからバーを表示または非表示にするオプション<br /><br />- ユーザーがバーを非表示にするよう選択した場合、既定では、バーはそのアプリ内で非表示になりますが、新しく開いたアプリでは自動的に表示され続けます <br /><br /> 管理者向け: <br /><br />- アプリを最初に開いたときにバーを自動的に表示または非表示にする、および、ユーザーがバーの非表示を選択した後に新しく開いたアプリに対してバーを自動的に非表示のままにするかどうかを制御するポリシー設定|ユーザー向け: <br /><br />- リボン上の **[秘密度]** ボタンからバーを表示または非表示にするオプション<br /><br />- ユーザーがバーを非表示にするよう選択すると、バーはそのアプリ内でも新しく開いたアプリ内でも非表示になります <br /><br />管理者向け: <br /><br />- バーを管理するポリシー設定はありません|
|ラベルの色: | Azure portal で構成します | Office 365 にラベルを移行した後も保持されます <br /><br /> 管理センターで作成された新しいラベルには、色はありません|
|ポリシーの更新: | Office アプリを開いたとき <br /><br /> 右クリックしてファイルまたはフォルダーを分類して保護したとき <br /><br />ラベル付けと保護のために PowerShell コマンドレット を実行したとき<br /><br />24 時間ごと | Office アプリを開いたとき <br /><br /> 右クリックしてファイルまたはフォルダーを分類して保護したとき <br /><br />ラベル付けと保護のために PowerShell コマンドレット を実行したとき<br /><br />4 時間ごと|
|サポートされている PDF 形式:| 保護: <br /><br /> - PDF の暗号化における ISO 標準 (既定) <br /><br /> - .ppdf <br /><br /> 消費: <br /><br /> - PDF の暗号化における ISO 標準 <br /><br />- .ppdf<br /><br />- SharePoint IRM 保護| 保護: <br /><br /> - PDF の暗号化における ISO 標準 <br /><br /> <br /><br /> 消費: <br /><br /> - PDF の暗号化における ISO 標準 <br /><br />- .ppdf<br /><br />- SharePoint IRM 保護|
|サポートされているコマンドレット:| [AzureInformatioProtection](/powershell/module/azureinformationprotection) に記載されているすべてのコマンドレット | Set-aipauthentication 非対話型セッションをサポートしていません <br /><br /> Set-AIPFileClassification と Set-AIPFileLabel は、*Owner* パラメーターまたは SharePoint Server ライブラリをサポートしていません <br /><br /> さらに、ラベルが適用されないすべてのシナリオに対して、"No label to apply" (適用するラベルがありません) というコメントが 1 つ付きます <br /><br /> Set-AIPFileLabel は *EnableTracking* パラメーターをサポートしていません <br /><br /> Get-AIPFileStatus は他のテナントからのラベル情報を返しません。また、*RMSIssuedTime* パラメーターを表示しません<br /><br />さらに、 *LabelingMethod* Get-aipfilestatus のパラメーターが表示されます**特権**または**標準**の代わりに**手動**または**自動**します。 詳細については、[オンライン ドキュメント](/powershell/module/azureinformationprotection/get-aipfilestatus)をご覧ください。|
|Office でのアクションごとの理由プロンプト (構成している場合): | 頻度:ファイルごと <br /><br /> 秘密度レベルを下げる <br /><br /> ラベルの削除<br /><br /> 保護の削除 | 頻度:セッションごと <br /><br /> 秘密度レベルを下げる<br /><br /> ラベルの削除|
|適用されたラベルのアクションを削除する: | ユーザーは確認するよう求められます <br /><br />既定のラベルや自動ラベル (構成している場合) は、Office アプリで次にファイルを開いたときに自動的に適用されません  <br /><br />| ユーザーは確認するよう求められません<br /><br /> 既定のラベルや自動ラベル (構成している場合) は、Office アプリで次にファイルを開いたときに自動的に適用されます|
|自動および推奨のラベル。 | 組み込みの情報の種類と、語句や正規表現を使ったカスタム条件を使って、Azure portal で[ラベル条件](../configure-policy-classification.md)として構成されます <br /><br />構成のオプションには、次のようなものがあります。 <br /><br />- 一意の / 一意でない数 <br /><br /> - 最小数| 組み込みの機密情報の種類と[カスタムの情報の種類](https://docs.microsoft.com/office365/securitycompliance/create-a-custom-sensitive-information-type)を使用して、管理センターで構成されます<br /><br />構成のオプションには、次のようなものがあります。  <br /><br />- 一意の数のみ <br /><br />- 最小および最大数 <br /><br />- 情報の種類での AND と OR のサポート <br /><br />- キーワード ディクショナリ<br /><br />- カスタマイズ可能な信頼度レベルと文字の近接|
|自動および推奨のラベルのカスタマイズ可能なポリシーのヒント: | はい <br /><br />Azure portal を使用して、ユーザーに既定のメッセージを交換するには | いいえ <br /><br /> 管理センターでは、カスタマイズしたポリシー ヒントを指定するオプションがありますが、このオプションは現在サポートされていません、統一されたラベル付けクライアントによって|
|ファイルの既定の保護レベルを変更します。 | はい <br /><br />使用することができます[レジストリの編集](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files)ネイティブと汎用的な保護の既定値をオーバーライドするには | いいえ |

特定の保護設定の動作の違いの詳細な比較についてを参照してください。[ラベルの保護設定の動作を比較する](../configure-policy-migrate-labels.md#comparing-the-behavior-of-protection-settings-for-a-label)します。

#### <a name="features-not-planned-to-be-in-the-azure-information-protection-unified-labeling-client"></a>Azure Information Protection の統合されたラベル付けクライアントに計画されていない機能

Azure Information Protection の統合されたラベル付けクライアントは、まだ開発中は、次の機能と動作の違い、Azure Information Protection クライアントからが現在計画されていない Azure の将来のリリースで使用できるInformation Protection には、ラベル付けのクライアントが統合。 

- Office アプリでのカスタムのアクセス許可: Word、Excel、PowerPoint

- Office アプリとエクスプローラーからの追跡と取り消し

- Information Protection バーのタイトルとヒント

- 保護のみモード (ラベルなし)

- .ppdf 形式で PDF ドキュメントを保護する

- Outlook の [転送不可] ボタンを表示する

- デモ ポリシー

- 保護を削除する場合の理由

- 確認プロンプト**このラベルを削除しますか?** 妥当性のポリシー設定を使用しない場合、ユーザーの

- 既存のカスタム プロパティを使用して Office ドキュメントにラベルを付ける (SyncPropertyName および SyncPropertyState クライアント詳細設定)

- Rights Management サービスに接続するために PowerShell コマンドレットを分離させる


#### <a name="parent-labels-and-their-sublabels"></a>親ラベルとそのサブラベル 

Azure Information Protection クライアントでは、サブラベルを持つ親ラベルを指定する構成がサポートされていません。 これらの構成には、既定のラベルと、推奨または自動分類のラベルの指定が含まれます。 ラベルにサブラベルがある場合は、親ラベルではなく、サブラベルのいずれかを指定できます。

パリティについて、Azure Information Protection 統合ラベル付けクライアントでも、管理センターでこれらのラベルを選択できる場合でも、サブラベルのある親ラベルの適用はサポートされていません。 このシナリオでは、Azure Information Protection 統合ラベル付けクライアントで親ラベルが適用されません。

## <a name="see-also"></a>関連項目
これらのクライアントをデプロイおよび使用する方法について詳しい情報が必要な場合は、次のドキュメントを使用してください。

- [Azure Information Protection クライアント](AIP-client.md)

- [Azure Information Protection 統合ラベル付けクライアント](unifiedlabelingclient-version-release-history.md)

- [RMS クライアントのデプロイに関する注意事項](client-deployment-notes.md)

AD RMS と共に Azure Information Protection を使うことができますが、Azure Information Protection クライアントは、その Azure サービス (Azure Information Protection とそのデータ保護サービス、Azure Rights Management) と併用するのが最適です。 Azure Information Protection のサービス側の比較については、「[Azure Information Protection と AD RMS の比較](../compare-on-premise.md)」をご覧ください。
