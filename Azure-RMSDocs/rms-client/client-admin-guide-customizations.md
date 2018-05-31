---
title: Azure Information Protection クライアントのカスタム構成
description: Windows 用 Azure Information Protection クライアントのカスタマイズに関する情報。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/21/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: c0e1011da16c9e3e91595cd06375cb744aa8fe00
ms.sourcegitcommit: 10f530fa1a43928581da4830a32f020c96736bc8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2018
ms.locfileid: "34402270"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-client"></a>管理者ガイド: Azure Information Protection クライアントのカスタム構成

>*適用対象: Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012, Windows Server 2008 R2*

以下の情報を使用して、詳細構成を行います。これらの構成は、Azure Information Protection クライアントを管理する際に、特定のシナリオまたはユーザーのサブセットで必要となる場合があります。

これらの設定には、レジストリの編集が必要なものや、Azure Portal で構成する必要のある詳細設定を使用するものなどがあります。設定はこの後にクライアントに公開され、ダウンロードされます。  

### <a name="how-to-configure-advanced-client-configuration-settings-in-the-portal"></a>ポータルでクライアントの詳細構成設定を構成する方法

1. まだサインインしていない場合は、新しいブラウザーのウィンドウで [Azure Portal にサインイン](../deploy-use/configure-policy.md#signing-in-to-the-azure-portal)して、**[Azure Information Protection]** ブレードに移動します。

2. **[分類]** > **[ラベル]** メニュー オプションから、**[ポリシー]** を選択します。

3. **[Azure Information Protection - ポリシー]** ブレードで、詳細設定を含めるために、ポリシーの横にあるコンテキスト メニュー **[...]** を選択します。 次に **[詳細設定]** を選択します。
    
    スコープ付きポリシーだけでなく、グローバル ポリシーの詳細設定も構成できます。

4. **[詳細設定]** ブレードで、詳細設定の名前と値を入力し、**[保存して閉じる]** を選択します。

5. このポリシーのユーザーが開いていたすべての Office アプリケーションを再起動するようにしてください。

6. 設定が不要になり、既定の動作に戻す場合は、**[詳細設定]** ブレードで、不要になった設定の横にあるコンテキスト メニュー (**...**) を選択し、**[削除]** を選択します。 次に、**[保存して閉じる]** をクリックします。

## <a name="prevent-sign-in-prompts-for-ad-rms-only-computers"></a>AD RMS 専用コンピューターのサインイン プロンプトが表示されないようにする

既定では、Azure Information Protection クライアントは Azure Information Protection サービスへ自動的に接続しようとします。 AD RMS とのみ通信するコンピューターの場合、この構成では不必要なサインイン プロンプトがユーザーに表示されます。 レジストリを編集し、このサインイン プロンプトが表示されないようにすることができます。

次の値の名前を検索し、値データを **0** に設定します。

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

この設定に関係なく、Azure Information Protection クライアントは標準 [RMS サービス検索プロセス](../rms-client/client-deployment-notes.md#rms-service-discovery)に従い、その AD RMS クラスターを検出します。

## <a name="suppress-the-initial-congratulations-welcome-page"></a>最初の "設定完了" の抑制 ようこそページ

プレビュー クライアントでは、この [設定完了] ウェルカム ページは表示されなくなりました。

初めて Azure Information Protection クライアントをコンピューターにインストールし、ユーザーが Word、Excel、PowerPoint または Outlook を開くと、**[設定完了]**  ページに、ラベルを選択するために、新しい Information Protection バーを使用する方法の簡単な説明が表示されます。 このページは、レジストリを編集して抑制することができます。

1. 次のレジストリ キーが存在しない場合は、作成します。
    
    **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP**

2. **EnableWelcomeExperience** という名前の DWORD (32 ビット) 値 (REG-DWORD) が存在しない場合は、作成し、データ値を **0** に設定します。

## <a name="suppress-the-whats-new-in-azure-information-protection-page"></a>[Azure Information Protection の新機能] を非表示にする ページ

プレビュー クライアントでは、[Azure Information Protection の新機能] は表示されなくなりました。 ページに表示される名前です。

Azure Information Protection クライアントをコンピューターに初めてインストールするか、アップグレードすると、Azure Information Protection バーが Word、Excel、PowerPoint、または Outlook に表示され、**[Azure Information Protection の新機能]** ページにユーザーの同意と使用状況の追跡に関する通知が表示されます。 このページは、レジストリを編集して抑制することができます。

1. 次のレジストリ キーが存在しない場合は、作成します。
    
    **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP**

2. **WhatsNewVersion** という名前の文字列値 (REG-SZ) が存在しない場合は作成し、データ値を **1.4** に設定します。

## <a name="sign-in-as-a-different-user"></a>別のユーザーでのサイン イン

通常、運用環境では、Azure Information Protection クライアントを使用しているときに別のユーザーとしてサインインする必要はありません。 ただし管理者の場合は、テスト段階のときに別ユーザーとしてサインインする必要がある場合があります。 

現在サインインしているアカウントを確認するには、**[Microsoft Azure Information Protection]** ダイアログ ボックスを使用します。Office アプリケーションを開き、**[ホーム]** タブの **[保護]** グループで、**[保護]** をクリックし、**[ヘルプとフィードバック]** をクリックします。 アカウント名が **[クライアント ステータス]** セクションに表示されます。

表示されるサインイン アカウントのドメイン名も必ず確認してください。 正しいアカウントでサインインしていてもドメインが間違っている、という状況は気付きにくいものです。 適切ではないアカウントが使用された場合は、Azure Information Protection ポリシーのダウンロードが失敗することや、目的のラベルや機能が表示されないことがあります。

別のユーザーでサイン インする方法は以下の通りです。

1. **%localappdata%\Microsoft\MSIP** に移動し、**TokenCache** ファイルを削除します。

2. 開いている Office アプリケーションがあれば再起動し、別のユーザー アカウントでサインインします。 Azure Information Protection サービスにサインインするように求めるプロンプトが Office アプリケーションで表示されない場合、**[Microsoft Azure Information Protection]** ダイアログ ボックスに戻り、更新された **[クライアント ステータス]** セクションの **[サインイン]** をクリックします。

補足:

- このソリューションでは、同じテナントから別ユーザーとしてサインインする操作がサポートされています。 別のテナントから別のユーザーとしてサインインする操作はサポートされていません。 複数のテナントがある Azure Information Protection をテストするには、異なるコンピューターを使用します。

- シングル サインオンを使用する場合は、レジストリを編集した後に Windows からサインアウトし、別のユーザー アカウントでサインインする必要があります。 Azure Information Protection クライアントは、現在サインインしているユーザーアカウントを使用して、自動的に認証を行います。

- **[ヘルプとフィードバック]** の **[設定のリセット]** オプションからサインアウトし、現在ダウンロードされている Azure Information Protection ポリシーを削除できます。


## <a name="enforce-protection-only-mode-when-your-organization-has-a-mix-of-licenses"></a>組織が種類の異なるライセンスを保有している場合の保護のみモードの適用

組織が Azure Information Protection のライセンスを保有せず、Azure Rights Management サービスのデータ保護を含む Office 365 のライセンスを保有している場合、Azure Information Protection クライアント (Windows 用) は自動的に[保護のみモード](../rms-client/client-protection-only-mode.md)で実行されます。

ただし、組織が Azure Information Protection のサブスクリプションを保有している場合は、既定で、すべての Windows コンピューターで Azure Information Protection ポリシーをダウンロードできます。 Azure Information Protection クライアントはライセンスのチェックと適用を行いません。 

Azure Information Protection のライセンスを保有せず、Azure Rights Management サービスを含む Office 365 のライセンスを保有しているユーザーがいる場合には、対象ユーザーのコンピューター上のレジストリを編集して、ライセンス付与されていない Azure Information Protection の分類とラベル付け機能が実行されないようにします。

次の値の名前を検索し、値を **0** に設定します。

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

また、これらのコンピューターの **%LocalAppData%\Microsoft\MSIP** フォルダーに、**Policy.msip** という名前のファイルがないことを確認します。 このファイルが存在する場合は、削除します。 このファイルには Azure Information Protection ポリシーが含まれており、レジストリを編集する前、または Azure Information Protection クライアントをデモ オプションを使用してインストールした場合に、ダウンロードされた可能性があります。

## <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>エクスプローラーの [Hide the Classify and Protect]\(分類の非表示と保護) メニュー オプション

次の DWORD 値の名前を (任意の値と共に) 作成します。

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

## <a name="support-for-disconnected-computers"></a>切断されたコンピューターのサポート

既定では、Azure Information Protection クライアントは Azure Information Protection サービスへ自動的に接続し、Azure Information Protection の最新のポリシーのダウンロードを試みます。 一定期間インターネットに接続できないコンピューターをお持ちの場合は、レジストリを編集することでサービスに接続しようとしないように設定することができます。 

次の値の名前を検索し、値を **0** に設定します。

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

クライアントの **%LocalAppData%\Microsoft\MSIP** フォルダーの中に、**Policy.msip** という名前の有効なポリシー ファイルがあることを確認してください。 必要に応じて、Azure Portal からポリシーをエクスポートしたり、クライアントのコンピューターにエクスポートされたファイルをコピーできます。 この方法を使用して、古いポリシー ファイルを公開されている最新のポリシーに置き換えることもできます。

ポリシーをエクスポートすると、Azure Information Protection クライアントのさまざまなバージョンに対応するさまざまなバージョンのポリシーが含まれる圧縮ファイルがダウンロードされます。

1. ファイルを解凍し、次の表を利用して必要なポリシー ファイルを特定します。 
    
    |［ファイル名］|対応するクライアント バージョン|
    |--------------------------|---------------------------------------------|
    |Policy1.1.msip |バージョン 1.2|
    |Policy1.2.msip |バージョン 1.3 - 1.7|
    |Policy1.3.msip |バージョン 1.8 以降|
    
2. 特定したファイルの名前を **Policy.msip** に変更し、Azure Information Protection 保護クライアントがインストールされているコンピューターの **%LocalAppData%\Microsoft\MSIP** フォルダーにコピーします。 


## <a name="hide-or-show-the-do-not-forward-button-in-outlook"></a>Outlook の [転送不可] ボタンを表示または非表示にする

このオプションを構成するには、[ポリシー設定](../deploy-use/configure-policy-settings.md)の **[Add the Do Not Forward button to the Outlook ribbon]\(Outlook リボンに [転送不可] ボタンを追加する\)** を使用することをお勧めします。 ただし、Azure Portal で構成する[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用して、このオプションを構成することもできます。

この設定を構成すると、Outlook のリボンの **[転送不可]** ボタンが表示または非表示になります。 この設定は、Office メニューからの [転送不可] オプションには影響しません。

この詳細設定を構成するには、次の文字列を入力します。

- キー: **DisableDNF**

- 値: ボタンを非表示にするには **True**、ボタンを表示するには **False**

## <a name="make-the-custom-permissions-options-available-or-unavailable-to-users"></a>ユーザーに対してカスタムのアクセス許可オプションを利用可能または利用不可にする

このオプションを構成するには、[ポリシー設定](../deploy-use/configure-policy-settings.md)の **[Make the custom permissions option available to users]\(ユーザーがカスタム アクセス許可オプションを使用できるようにする\)** を使用することをお勧めします。 ただし、Azure Portal で構成する[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用して、このオプションを構成することもできます。 

この設定を構成して、ユーザーにポリシーを公開した場合、ユーザーが独自の保護設定を選択できるように、カスタムのアクセス許可オプションが利用できるようになるか、または、確認メッセージが表示されない限り、ユーザーが独自の保護設定を選択できないように利用不可になります。

この詳細設定を構成するには、次の文字列を入力します。

- キー: **EnableCustomPermissions**

- 値: カスタム アクセス許可オプションを利用できるようにする場合は **True**、このオプションを利用不可にする場合は **False**


## <a name="permanently-hide-the-azure-information-protection-bar"></a>Azure Information Protection バーを完全に非表示にする

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。 これは、[ポリシー設定](../deploy-use/configure-policy-settings.md)の **[Display the Information Protection bar in Office apps]\(Office アプリで Information Protection バーを表示する\)** を **[オン]** に設定している場合にのみ使用します。

この設定を構成してユーザーのポリシーを発行し、ユーザーが Office アプリケーションで Azure Information Protection バーを表示しないように選択すると、バーは非表示のままになります。 これが起こるのは、ユーザーが **[ホーム]** タブ、**[保護]** グループ、**[保護]** ボタンから **[バーの表示]** オプションをクリアするときです。 **[このバーを閉じる]** アイコンを使用してバーを閉じた場合、この設定は何も影響を与えません。

Azure Information Protection バーが非表示のままであっても、推奨の分類を構成している場合やドキュメントや電子メールにラベルを指定する必要がある場合、ユーザーは一時的に表示されるバーからラベルを選択できます。 

この詳細設定を構成するには、次の文字列を入力します。

- キー: **EnableBarHiding**

- 値: **True**


## <a name="enable-recommended-classification-in-outlook"></a>Outlook で推奨分類を有効にする

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。 この設定はプレビュー段階であり、変更される可能性があります。

推奨分類のラベルを設定すると、Word、Excel、PowerPoint では、推奨ラベルを受け入れるか、却下するように求められます。 また、このラベル推奨が Outlook でも表示されます。

この詳細設定を構成するには、次の文字列を入力します。

- キー: **OutlookRecommendationEnabled**

- 値: **True**


## <a name="set-a-different-default-label-for-outlook"></a>Outlook に別の既定ラベルを設定します

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。 

この設定を構成すると、Outlook では、Azure Information Protection ポリシーで **[既定のラベルを選択]** 設定に構成した既定のラベルが適用されません。 別の既定のラベルを適用できるか、ラベルがありません。

別のラベルを適用するには、ラベル ID を指定する必要があります。 Azure Portal で Azure Information Protection ポリシーを表示または構成するとき、ラベル ID 値は **[ラベル]** ブレードに表示されます。 ファイルにラベルが適用されている場合、[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) PowerShell コマンドレットを実行してラベル ID (MainLabelId または SubLabelId) を特定することもできます。 ラベルにサブラベルがある場合、親ラベルではなく、サブラベルの ID だけを常に指定してください。

Outlook で既定のラベルが適用されないように、**[なし]** を指定します。

この詳細設定を構成するには、次の文字列を入力します。

- キー: **OutlookDefaultLabel**

- 値: \<**ラベル ID**> または**なし**

## <a name="remove-not-now-for-documents-when-you-use-mandatory-labeling"></a>必須のラベル付けを使用するときにドキュメントの "後で" を削除する

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。 

**[すべてのドキュメントとメールにラベルを付ける]** の[ポリシー設定](../deploy-use/configure-policy-settings.md)を使うと、ユーザーが Office ドキュメントを初めて保存するとき、およびメールを送信するときに、ラベルの選択を求めるメッセージが表示されます。 ドキュメントの場合、ユーザーは **[後で]** を選択して一時的にメッセージを無視し、ラベルを選んで、ドキュメントに戻ることができます。 ただし、ラベルを付けないと、保したドキュメントを閉じることはできません。 

この設定を構成すると、**[後で]** オプションが削除され、ユーザーはドキュメントを初めて保存するときにラベルを選択する必要があります。

この詳細設定を構成するには、次の文字列を入力します。

- キー: **PostponeMandatoryBeforeSave**

- 値: **False**

## <a name="turn-on-classification-to-run-continuously-in-the-background"></a>バックグラウンドでの分類の継続的実行をオンにする

この構成オプションは、現在プレビューの段階で、変更される可能性があります。

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。 

この設定を構成すると、Azure Information Protection クライアントが推奨ラベルを自動的に適用する[既定の動作](../deploy-use/configure-policy-classification.md#how-automatic-or-recommended-labels-are-applied)が次のように変わります。

- 自動分類は、Word、Excel、PowerPoint、Outlook に適用されます。 ドキュメントに対して、自動分類はバックグラウンドで継続的に実行されます。 Outlook の場合、電子メールを送信すると、自動分類が実行されます。 
    
    以前に手動でラベルが付けられているか、以前に上位の分類で自動的にラベルが付けられているドキュメントには自動分類を使用できません。 例外は、OverrideLabel パラメーターをオンに設定して Azure Information Protection スキャナーを使用する場合です。

- 推奨分類は、Word、Excel、PowerPoint に適用されます。 これらのドキュメントに対して、推奨分類はバックグラウンドで継続的に実行されます。 Outlook の場合、推奨分類を使用できません。
    
    上位の分類の有無に関係なく、以前にラベルが付けられたドキュメントには推奨分類を使用できます。 

Azure Information Protection クライアントがユーザーによって指定された条件規則をドキュメントで定期的にチェックするとき、この動作は SharePoint Online に格納されるドキュメントに対する自動的で推奨される分類と保護を有効にします。 条件規則が既に実行されているため、大きなファイルもすばやく保存されます。 

条件規則がユーザーの入力と同時にリアルタイムで実行されることはありません。 ドキュメントが変更された場合、バックグラウンド タスクとして定期的に実行されます。

この詳細設定を構成するには、次の文字列を入力します。

- キー: **RunPolicyInBackground**

- 値: **True**

## <a name="migrate-labels-from-secure-islands-and-other-labeling-solutions"></a>Secure Islands からのラベルの移行と、その他のラベル付けのソリューション

この構成オプションは、現在プレビューの段階で、変更される可能性があります。 さらに、この構成オプションには、クライアントのプレビュー バージョンまたは Azure Information Protection スキャナーが必要です。

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。 

Secure Islands によってラベル付けされた Office ドキュメントや PDF ドキュメントは、Azure Information Protection のラベルでラベル付けし直すことができます。そのためには、独自に定義したマッピングを使用します。 また、この方法を使用して、他のソリューションからのラベルを、そのラベルが Office ドキュメントにある場合は再利用することができます。 

この構成オプションの結果として、Azure Information Protection の新しいラベルは、Azure Information Protection クライアントによって次のように適用されます。

- Office ドキュメントの場合: デスクトップ アプリでドキュメントを開くと、Azure Information Protection の新しいラベルが設定されたことが表示され、ドキュメントを保存すると適用されます。

- エクスプローラーの場合: [Azure Information Protection] ダイアログ ボックスで、Azure Information Protection の新しいラベルが設定されたことが表示され、ユーザーが **[適用]** を選択すると適用されます。 ユーザーが **[キャンセル]** を選択した場合、新しいラベルは適用されません。

- PowerShell の場合: [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) によって、Azure Information Protection の新しいラベルが適用されます。 [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) では、別の方法で設定されるまで、Azure Information Protection の新しいラベルは表示されません。

- Azure Information Protection スキャナーの場合: Azure Information Protection の新しいラベルが設定され、強制モードで適用される可能性がある場合、検出が報告されます。

この構成では、古いラベルにマッピングする Azure Information Protection のラベルごとに、**LabelbyCustomProperty** という名前のクライアントの詳細設定を指定する必要があります。 次に、各エントリに対して、次の構文を使用して値を設定します。

`[Azure Information Protection label ID],[migration rule name],[Secure Islands custom property name],[Secure Islands metadata Regex value]`

Azure Portal で Azure Information Protection ポリシーを表示または構成するとき、ラベル ID 値は **[ラベル]** ブレードに表示されます。 サブラベルを指定するには、親ラベルが同じスコープまたはグローバル ポリシー内にある必要があります。

任意の移行規則名を指定します。 以前のラベル付けソリューションから Azure Information Protection のラベルに、1 つまたは複数のラベルをマッピングする方法を特定するのに役立つ、わかりやすい名前を使用します。 名前は、スキャナー レポートおよびイベント ビューアーに表示されます。 

### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>例1: 同じラベル名の 1 対 1 のマッピング

Secure Islands の "Confidential" というラベルを持ったドキュメントは、Azure Information Protection の "Confidential" というラベルに変更されます。

この例では、次の点に注意してください。

- Azure Information Protection のラベル **Confidential** のラベルID は、1ace2cc3-14bc-4142-9125-bf946a70542c です。 

- Secure Islands のラベルは、**Classification** という名前のカスタム プロパティに保存されます。

クライアントの詳細設定:

    
|名前|値|
|---------------------|---------|
|LabelbyCustomProperty|1ace2cc3-14bc-4142-9125-bf946a70542c、"Secure Islands label is Confidential" (Secure Islands のラベルは Confidential です)、Classification、Confidential|

### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>例 2: 異なるラベル名の 1 対 1 のマッピング

Secure Islands によって "Sensitive" というラベルを付けられたドキュメントは、Azure Information Protection によって "Highly Confidential" というラベルに変更されます。

この例では、次の点に注意してください。

- Azure Information Protection のラベル **Highly Confidential** のラベルID は、3e9df74d-3168-48af-8b11-037e3021813f です。

- Secure Islands のラベルは、**Classification** という名前のカスタム プロパティに保存されます。

クライアントの詳細設定:

    
|名前|値|
|---------------------|---------|
|LabelbyCustomProperty|3e9df74d-3168-48af-8b11-037e3021813f、"Secure Islands label is Sensitive" (Secure Islands のラベルは Sensitive です)、Classification、Sensitive|


### <a name="example-3-many-to-one-mapping-of-label-names"></a>例 3: ラベル名の多対一のマッピング

"Internal" という単語を含む Secure Islands のラベルが 2 つあり、この Secure Islands のラベルのいずれかを含んでいるドキュメントを、Azure Information Protection によって "General" にラベル付けし直します。

この例では、次の点に注意してください。

- Azure Information Protection のラベル **General** のラベル ID は、2beb8fe7-8293-444 c-9768-7fdc6f75014d です。

- Secure Islands のラベルは、**Classification** という名前のカスタム プロパティに保存されます。

クライアントの詳細設定:

    
|名前|値|
|---------------------|---------|
|LabelbyCustomProperty|2beb8fe7-8293-444c-9768-7fdc6f75014d、"Secure Islands label contains Internal" (Secure Islands のラベルに Internal が含まれます)、Classification、\*Internal\*|


## <a name="label-an-office-document-by-using-an-existing-custom-property"></a>既存のカスタム プロパティを使用して Office ドキュメントにラベルを付ける

> [!NOTE]
> この構成と前のセクションの構成を使用して、別のラベル付けソリューションから移行する場合は、ラベル付けの移行の設定が優先されます。 

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。 

この設定を構成すると、既存のカスタム プロパティの値がいずれかのラベル名と一致するときに Office ドキュメントを分類する (さらに必要に応じて保護する) ことができます。 このカスタム プロパティは、別の分類ソリューションから設定するか、または SharePoint によってプロパティとして設定することができます。

この構成の結果として、Azure Information Protection ラベルのないドキュメントが Office アプリのユーザーによって開かれて保存されると、ドキュメントが対応するプロパティ値と一致するようにラベル付けされます。 

この構成では、連動する 2 つの詳細設定を指定する必要があります。 1 つ目は **SyncPropertyName** で、他の分類ソリューションから設定されているカスタム プロパティ名、または SharePoint によって設定されるプロパティです。 2 つ目は **SyncPropertyState** で、これは OneWay に設定する必要があります。

この詳細設定を構成するには、次の文字列を入力します。

- キー 1: **SyncPropertyName**

- キー 1 の値: \<**プロパティ名**> 

- キー 2: **SyncPropertyName**

- キー 2 の値: **OneWay**

これらのキーと、1 つだけのカスタム プロパティに対応する値を使用します。

たとえば、**[公開]**、**[全般]**、**[社外秘]** の値が考えられる、**[分類]** という名前の SharePoint 列があるとします。 ドキュメントは SharePoint に格納され、[分類] プロパティに設定されたいずれかの値を持ちます。

Office ドキュメントにこれらの分類の値のいずれかのラベルを付けるには、**[SyncPropertyName]** を **[公開]** に、**[SyncPropertyState]** を **[OneWay]** に設定します。 

ここで、ユーザーがこれらの Office ドキュメントのいずれかを開いて保存するときに、Azure Information Protection ポリシーに **[公開]**、**[全般]**、または **[社外秘]** の名前のラベルがあると、このいずれかにラベル付けされます。 これらの名前のラベルがない場合、ドキュメントはラベル付けされないままです。

## <a name="disable-the-low-integrity-level-for-the-scanner"></a>スキャナーの低整合性レベルを無効にする

この構成オプションは、現在プレビューの段階で、変更される可能性があります。 また、この構成オプションには、Azure Information Protection クライアントの最新プレビュー版が必要です。

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。 

既定では、Azure Information Protection スキャナーのプレビュー バージョンは、低整合性レベルで実行されます。 この設定では、より高度なセキュリティ分離が提供されますが、パフォーマンスが低下します。 低整合性レベルは、特権を持ったアカウント (ローカル管理者アカウントなど) でスキャナーを実行する場合に適しています。この設定は、スキャナーを実行しているコンピューターを保護するのに役立ちます。

ただし、スキャナーを実行するサービス アカウントに、[スキャナーの前提条件](../deploy-use/deploy-aip-scanner.md#prerequisites-for-the-azure-information-protection-scanner)のセクションで説明されている権限だけが付与されている場合、低整合性レベルは必要ありません。これはパフォーマンスに悪影響を及ぼすため、推奨されません。 

Windows 整合性レベルについて詳しくは、「[What is the Windows Integrity Mechanism?](https://msdn.microsoft.com/library/bb625957.aspx)」(Windows 整合性メカニズムとは何ですか) をご覧ください。

この高度な設定を構成し、Windows によって自動的に割り当てられた整合性レベルでスキャナーが実行される (標準ユーザー アカウントが中程度の整合性レベルで実行される) ようにするには、次の文字列を入力します。

- キー: **ProcessUsingLowIntegrity**

- 値: **False**


## <a name="integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution"></a>Exchange メッセージ分類との統合によるモバイル デバイスのラベル付けソリューション

Outlook on the web では、Azure Information Protection の分類と保護の機能がまだネイティブでサポートされていませんが、ユーザーが Outlook on the web を使用する場合は、Exchange のメッセージ分類を使用して Azure Information Protection ラベルをモバイル ユーザーに拡張することができます。 Outlook Mobile では、Exchange のメッセージ分類がサポートされません。

このソリューションを実現するには: 

1. [New-MessageClassification](https://technet.microsoft.com/library/bb124400) Exchange PowerShell コマンドレットを使用して、Azure Information Protection ポリシーのラベル名にマップする名前プロパティでメッセージの分類を作成します。 

2. ラベルごとに Exchange メール フロー ルールを作成します。メッセージのプロパティに構成した分類が含まれる場合はルールを適用し、メッセージ プロパティを変更してメッセージ ヘッダーを設定します。 

     メッセージ ヘッダーについては、Azure Information Protection ラベルを使って送信および分類した電子メールのインターネット ヘッダーを調べることによって、指定する情報を見つけることができます。 ヘッダー **msip_labels** と、そのすぐあとに続く文字列 (セミコロンまでが対象) を探します。 次に例を示します。
    
    **msip_labels: MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;**
    
    ルール内のメッセージ ヘッダーの場合は、ヘッダーとして **msip_labels** を指定し、ヘッダー値としてこの文字列の残りの部分を指定します。 次に例を示します。
    
    ![例: 特定の Azure Information Protection ラベルのメッセージ ヘッダーを設定する Exchange Online メール フロー ルール](../media/exchange-rule-for-message-header.png)
    
    注: ラベルがサブラベルである場合は、ヘッダー値のサブラベルの前に、同じ形式を使って親ラベルも指定する必要があります。 たとえば、サブラベルの GUID が 27efdf94-80a0-4d02-b88c-b615c12d69a9 である場合、値は `MSIP_Label_ab70158b-bdcc-42a3-8493-2a80736e9cbd_Enabled=True;MSIP_Label_27efdf94-80a0-4d02-b88c-b615c12d69a9_Enabled=True;` のようになります。

この構成のテストを行う前に、メール フロー ルールを作成または編集すると遅延 (たとえば、1 時間の遅延) がよく発生することを念頭においてください。 このルールを有効にすると、ユーザーが Outlook on the web または Exchange ActiveSync IRM をサポートするモバイル デバイス クライアントを使用する際に、次のことが起こるようになります。 

- ユーザーが Exchange のメッセージ分類を選択して電子メールを送信します。

- Exchange ルールにより Exchange の分類が検出され、ルールに従ってメッセージ ヘッダーが変更されて、Azure Information Protection の分類が追加されます。

- Azure Information Protection クライアントをインストール済みである受信者が Outlook で電子メールを表示すると、Azure Information Protection の割り当てられたラベルや、対応する電子メールのヘッダー、フッター、または透かしが表示されます。 

Azure Information Protection ラベルが保護を適用する場合は、この保護をルールの構成に追加します。メッセージ セキュリティを変更するオプションを選択して、権利保護を適用し、RMS テンプレートまたは [転送不可] オプションを選択します。

また、メール フロー ルールを構成して、リバース マッピングを行うこともできます。 Azure Information Protection ラベルが検出された場合は、対応する Exchange メッセージの分類を設定します。

- Azure Information Protection のラベルごとに、**msip_labels** ヘッダーにラベル名 (**General** など) が含まれている場合に適用されるメール フロー ルールを作成し、このラベルにマッピングするメッセージ分類を適用します。


## <a name="next-steps"></a>次の手順
これで Azure Information Protection クライアントのカスタマイズができました。次に、このクライアントのサポートに必要な追加情報を記載した以下の記事をご覧ください。

- [クライアント ファイルおよび使用状況ログの記録](client-admin-guide-files-and-logging.md)

- [ドキュメント追跡](client-admin-guide-document-tracking.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
