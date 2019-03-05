---
title: Azure Information Protection クライアント
description: Microsoft Azure Information Protection は、組織のデータを保護するクライアント/サーバー型のソリューションです。 クライアント (Azure Information Protection クライアントまたは Rights Management クライアント) は、コンピューターおよびモバイル デバイスで実行するアプリケーションに統合されます。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/26/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a6fa85be-f92a-4e00-9efc-9dbfd4dfbfcb
ms.suite: ems
ms.openlocfilehash: 5d49a1ad6bed86b6041b66feb3017b716584c5b7
ms.sourcegitcommit: 55782e58508051f0ecf460e8b126f70ab9b9ceec
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2019
ms.locfileid: "56756217"
---
# <a name="the-client-side-of-azure-information-protection"></a>クライアント側での Azure Information Protection

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*

Azure Information Protection は、組織の文書や電子メールを保護するクライアント/サーバー型のソリューションです。

- クライアントは、Azure Information Protection クライアントまたは Rights Management クライアントで、コンピューターやモバイル デバイスで実行するアプリケーションと統合されます。 

- サービスは、クラウド (データの保護用に Azure Rights Management サービスを使用する Azure Information Protection)、またはオンプレミス (Active Directory Rights Management サービス、より一般的には AD RMS) にあります。 

Azure Information Protection クライアントは、ラベルなしの保護に加え、ラベル付けを使った分類と保護をサポートしています。 このクライアントは Office アプリケーションと統合できますが、別にインストールする必要があります。

Rights Management (RMS) クライアントは、Office アプリケーション、Azure Information Protection クライアント、ソフトウェア ベンダー製の RMS 対応アプリケーションなど、一部のアプリケーションと共に自動的にインストールされます。 ただし、[IRM で保護されたライブラリと OneDrive for Business のファイルの同期](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668)をサポートするため、および Rights Management の保護を基幹業務アプリケーションに統合したい開発者向けに、これを[単体でインストールする](https://www.microsoft.com/en-us/download/details.aspx?id=38396)ことも可能です。

## <a name="choose-which-azure-information-protection-client-to-use"></a>使用する Azure Information Protection クライアントを選択する

Azure portal からラベルとポリシー設定をダウンロードする **Azure Information Protection クライアント**は、一般提供されています。また、新機能と修正プログラムをテストするためのプレビュー バージョンがあります。 これらのバージョンのクライアントについて詳しくは、「[Azure Information Protection クライアント:バージョン リリース履歴とサポート ポリシー](client-version-release-history.md)」をご覧ください。 

**Azure Information Protection 統合ラベル付けクライアント**では、Office 365 セキュリティ/コンプライアンス センターからラベルとポリシー設定をダウンロードします。 現在、このクライアントはテスト用のプレビュー段階です。 これらのバージョンのクライアントについて詳しくは、「[Azure Information Protection 統合ラベル付けクライアント:バージョン リリース情報](unifiedlabelingclient-version-release-history.md)」を参照してください。

どのクライアントをインストールすべきでしょうか?

- 運用環境にデプロイする場合は、一般提供されている Azure Information Protection クライアントを使います。

- テストと評価のフェーズにいる場合は、プレビュー クライアントのいずれかを使います。
    
    現在、プレビュー バージョンの Azure Information Protection クライアントおよび Azure Information Protection 統合ラベル付けクライアントには、各自の機能についてパリティがありません。 ただし、このギャップはなくなる予定であり、新しい機能は Azure Information Protection 統合ラベル付けクライアントにのみ追加されます。 このため、Azure Information Protection 統合ラベル付けクライアントの現在の機能セットや機能がビジネス要件を満たしている場合は、これを使ってテストすることをお勧めします。 そうでない場合、または Azure portal でラベルを構成し、それをまだ[統合ラベル付けストアに移行](../configure-policy-migrate-labels.md)していない場合は、Azure Information Protection クライアントを使います。

### <a name="feature-comparisons-for-the-clients"></a>クライアントの機能比較

次の表を使用して、現在の 2 つのプレビュー バージョンでサポートされている機能を比較することができます。

|機能|Azure Information Protection クライアント|Azure Information Protection<br /> 統合ラベル付けクライアント|
|-------|-----------------------------------|----------------------------------------------------|
|ラベル付けアクション:手動、推奨、自動| はい | はい |
|Office アプリの Information Protection バー<br />カスタマイズ可能なヒント付き:| はい | はい|
|中央レポート機能 (分析):| はい | はい |
|設定のリセットとログのエクスポート:| はい | はい |
|ユーザー定義のアクセス許可:| はい | Outlook のみ (転送不可) |
|カスタム アクセス許可:| はい | エクスプローラーのみ <br /><br /> Office アプリでは、代替として、**[ファイル情報]** > **[文書の保護]** > **[アクセスの制限]** を選択できます |
|エクスプローラー、右クリック アクション:| はい | はい (制限あり):<br /><br /> - .ppdf 形式の PDF ドキュメントを保護できません <br /><br />  - 保護のみモードはサポートされません|
|保護されたファイル用のビューアー:| はい | はい (制限あり):<br /><br /> 一般的に保護されたファイル (.pfile) に関しては、Azure Information Protection クライアントのビューアーとは異なり、最初に開いたファイルへの変更を保存することができません。|
|PowerShell コマンド:| はい | はい (制限あり):<br /><br />- 含まれているコマンドレット:[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)、[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)、[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)、[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) <br /><br />- 保護サービスに直接接続するコマンドレットは含まれていません|
|保護アクションに対するオフライン サポート:| はい | はい (制限あり): <br /><br />- エクスプローラーおよび PowerShell コマンドについては、ファイルを保護するためにユーザーがインターネットに接続している必要があります。 |
|HYOK のサポート:| はい | [いいえ]<br /><br /> Azure portal から移行する HYOK 保護用に構成されたラベルは、Azure Information Protection 統合ラベル付けクライアントにより表示されますが、保護は適用されません。 |
|イベント ビューアーに対する使用状況ログの記録:| はい | [いいえ]|
|メールの添付ファイルからのラベル継承:| はい | [いいえ] |
|Outlook の [転送不可] ボタンを表示する| はい | [いいえ] |
|以下を含む[カスタマイズ](client-admin-guide-customizations.md#available-advanced-client-settings):<br />- メールの既定のラベル<br />- カスタム アクセス許可を有効にする <br />- S/MIME のサポート<br />- [問題の報告] オプション| はい | [いいえ] |
|オンプレミスのデータ ストア用のスキャナー:| はい | [いいえ] |
|追跡と取り消し:| はい | [いいえ] |
|保護のみモード (ラベルなし):| はい | [いいえ] |
|多言語のサポート:| はい | [いいえ] |
|AD RMS のサポート:| はい | 次のアクションのみがサポートされます。<br /><br /> - ビューアーで保護されたドキュメントを開くことができます|

#### <a name="functional-comparison-for-the-clients"></a>クライアントの機能の比較

両方のクライアントで同じ機能がサポートされている場合は、次の表を使用して 2 つの現在のプレビュー バージョン間にある機能の違いを特定することができます。

|機能 |Azure Information Protection クライアント|Azure Information Protection<br /> 統合ラベル付けクライアント|
|--------------|-----------------------------------|-----------------------------------------------------------|
|セットアップ:| ローカルのデモ ポリシーをインストールするオプション | ローカルのデモ ポリシーなし|
|Office アプリで適用した場合のラベルの選択と表示:|リボン上の **[保護]** ボタンから <br /><br /> Information Protection バーから (リボンの下の水平バー)|リボン上の **[秘密度]** ボタンから<br /><br /> Information Protection バーから (リボンの下の水平バー)|
|Office アプリの Information Protection バーを管理する:|ユーザー向け:  <br /><br />- リボン上の **[保護]** ボタンからバーを表示または非表示にするオプション<br /><br />- ユーザーがバーを非表示にするよう選択した場合、既定では、バーはそのアプリ内で非表示になりますが、新しく開いたアプリでは自動的に表示され続けます <br /><br /> 管理者向け:  <br /><br />- アプリを最初に開いたときにバーを自動的に表示または非表示にする、および、ユーザーがバーの非表示を選択した後に新しく開いたアプリに対してバーを自動的に非表示のままにするかどうかを制御するポリシー設定|ユーザー向け:  <br /><br />- リボン上の **[秘密度]** ボタンからバーを表示または非表示にするオプション<br /><br />- ユーザーがバーを非表示にするよう選択すると、バーはそのアプリ内でも新しく開いたアプリ内でも非表示になります <br /><br />管理者向け:  <br /><br />- バーを管理するポリシー設定はありません|
|ラベルの色:  | Azure portal で構成します | Office 365 にラベルを移行した後も保持されます <br /><br /> セキュリティ/コンプライアンス センターで作成した新しいラベルの色は、既定のブラックです|
|ポリシーの更新: | Office アプリを開いたとき <br /><br /> 右クリックしてファイルまたはフォルダーを分類して保護したとき <br /><br />ラベル付けと保護のために PowerShell コマンドレット を実行したとき<br /><br />24 時間ごと | Office アプリを開いたとき <br /><br /> 右クリックしてファイルまたはフォルダーを分類して保護したとき <br /><br />ラベル付けと保護のために PowerShell コマンドレット を実行したとき<br /><br />4 時間ごと|
|サポートされている PDF 形式:| 保護: <br /><br /> - PDF の暗号化における ISO 標準 (既定) <br /><br /> - .ppdf <br /><br /> 消費:  <br /><br /> - PDF の暗号化における ISO 標準 <br /><br />- .ppdf<br /><br />- SharePoint IRM 保護| 保護: <br /><br /> - PDF の暗号化における ISO 標準 <br /><br /> <br /><br /> 消費:  <br /><br /> - PDF の暗号化における ISO 標準 <br /><br />- .ppdf<br /><br />- SharePoint IRM 保護|
|サポートされているコマンドレット:| [AzureInformatioProtection](/powershell/module/azureinformationprotection) に記載されているすべてのコマンドレット | Set-AIPFileClassification と Set-AIPFileLabel は、*Owner* パラメーターまたは SharePoint Server ライブラリをサポートしていません <br /><br /> さらに、ラベルが適用されないすべてのシナリオに対して、"No label to apply" (適用するラベルがありません) というコメントが 1 つ付きます <br /><br /> Set-AIPFileLabel は *EnableTracking* パラメーターをサポートしていません <br /><br /> Get-AIPFileStatus は他のテナントからのラベル情報を返しません。また、*RMSIssuedTime* パラメーターを表示しません<br /><br />さらに、Get-AIPFileStatus の *LabelingMethod* パラメーターでは、**[手動]** または **[自動]** の代わりに **[特権]**、**[標準]**、または **[自動]** が表示されます。 詳細については、[オンライン ドキュメント](/powershell/module/azureinformationprotection/get-aipfilestatus)をご覧ください。|
|Office でのアクションごとの理由プロンプト (構成している場合): | 頻度:ファイルごと <br /><br /> 秘密度レベルを下げる <br /><br /> ラベルの削除<br /><br /> 保護の削除 | 頻度:セッションごと <br /><br /> 秘密度レベルを下げる<br /><br /> ラベルの削除|
|ラベルのアクションを削除する: | ユーザーは確認するよう求められます <br /><br />既定のラベルや自動ラベル (構成している場合) は、Office アプリで次にファイルを開いたときに自動的に適用されません  <br /><br />| ユーザーは確認するよう求められません<br /><br /> 既定のラベルや自動ラベル (構成している場合) は、Office アプリで次にファイルを開いたときに自動的に適用されます|
|自動および推奨される分類: | 組み込みの情報の種類と、語句や正規表現を使ったカスタム条件を使って、Azure portal で[ラベル条件](../configure-policy-classification.md)として構成されます <br /><br />構成のオプションには、次のようなものがあります。 <br /><br />- 一意の / 一意でない数 <br /><br /> - 最小数| 組み込みの機密情報の種類と[カスタムの情報の種類](https://docs.microsoft.com/office365/securitycompliance/create-a-custom-sensitive-information-type)を使って、セキュリティ/コンプライアンス センターで構成されます<br /><br />構成のオプションには、次のようなものがあります。  <br /><br />- 一意の数のみ <br /><br />- 最小および最大数 <br /><br />- 情報の種類での AND と OR のサポート <br /><br />- キーワード ディクショナリ<br /><br />- カスタマイズ可能な信頼度レベルと文字の近接|

##### <a name="parent-labels-and-their-sublabels"></a>親ラベルとそのサブラベル 

Azure Information Protection クライアントでは、サブラベルを持つ親ラベルを指定する構成がサポートされていません。 これらの構成には、既定のラベルと、推奨または自動分類のラベルの指定が含まれます。 ラベルにサブラベルがある場合は、親ラベルではなく、サブラベルのいずれかを指定できます。

パリティについて、Azure Information Protection 統合ラベル付けクライアントでも、Office 365 セキュリティ/コンプライアンス センターでこれらのラベルを選択できる場合でも、サブラベルのある親ラベルの適用はサポートされていません。 このシナリオでは、Azure Information Protection 統合ラベル付けクライアントで親ラベルが適用されません。

## <a name="see-also"></a>関連項目
これらのクライアントをデプロイおよび使用する方法について詳しい情報が必要な場合は、次のドキュメントを使用してください。

- [Azure Information Protection クライアント](AIP-client.md)

- [Azure Information Protection 統合ラベル付けクライアント](unifiedlabelingclient-version-release-history.md)

- [RMS クライアントのデプロイに関する注意事項](client-deployment-notes.md)

AD RMS と共に Azure Information Protection を使うことができますが、Azure Information Protection クライアントは、その Azure サービス (Azure Information Protection とそのデータ保護サービス、Azure Rights Management) と併用するのが最適です。 Azure Information Protection のサービス側の比較については、「[Azure Information Protection と AD RMS の比較](../compare-on-premise.md)」をご覧ください。
