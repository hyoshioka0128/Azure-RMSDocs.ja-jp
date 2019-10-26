---
title: カスタム構成-Azure Information Protection クライアント
description: Windows 用 Azure Information Protection クライアントのカスタマイズに関する情報。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/25/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.subservice: v1client
ms.reviewer: maayan
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: db282701b5374652d8469e5eadf42cd0a3472c3b
ms.sourcegitcommit: 7089f06723f609ce40558ae1346db68b9a47667f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916290"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-client"></a>管理者ガイド: Azure Information Protection クライアントのカスタム構成

>*適用対象: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、WINDOWS 7 SP1、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012、windows Server 2008 r2*
>
> *手順: [Windows 用の Azure Information Protection クライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

以下の情報を使用して、詳細構成を行います。これらの構成は、Azure Information Protection クライアントを管理する際に、特定のシナリオまたはユーザーのサブセットで必要となる場合があります。

これらの設定には、レジストリの編集が必要なものや、Azure Portal で構成する必要のある詳細設定を使用するものなどがあります。設定はこの後にクライアントに公開され、ダウンロードされます。  

### <a name="how-to-configure-advanced-client-configuration-settings-in-the-portal"></a>ポータルでクライアントの詳細構成設定を構成する方法

1. まだサインインしていない場合は、新しいブラウザーのウィンドウで [Azure Portal にサインイン](../configure-policy.md#signing-in-to-the-azure-portal)して、 **[Azure Information Protection]** ブレードに移動します。

2. **[分類]**  >  **[ラベル]** メニュー オプションから、 **[ポリシー]** を選択します。

3. **[Azure Information Protection - ポリシー]** ブレードで、詳細設定を含めるために、ポリシーの横にあるコンテキスト メニュー **[...]** を選択します。 次に **[詳細設定]** を選択します。
    
    スコープ付きポリシーだけでなく、グローバル ポリシーの詳細設定も構成できます。

4. **[詳細設定]** ブレードで、詳細設定の名前と値を入力し、 **[保存して閉じる]** を選択します。

5. このポリシーのユーザーが開いていたすべての Office アプリケーションを再起動するようにしてください。

6. 設定が不要になり、既定の動作に戻す場合は、 **[詳細設定]** ブレードで、不要になった設定の横にあるコンテキスト メニュー ( **...** ) を選択し、 **[削除]** を選択します。 次に、 **[保存して閉じる]** をクリックします。

#### <a name="available-advanced-client-settings"></a>使用可能なクライアントの詳細設定

|設定|シナリオと手順|
|----------------|---------------|
|DisableDNF|[Outlook の [転送不可] ボタンを表示または非表示にする](#hide-or-show-the-do-not-forward-button-in-outlook)|
|DisableMandatoryInOutlook|[必須ラベルから Outlook メッセージを除外する](#exempt-outlook-messages-from-mandatory-labeling)|
|CompareSubLabelsInAttachmentAction|[サブラベルの順序のサポートを有効にする](#enable-order-support-for-sublabels-on-attachments) 
|ContentExtractionTimeout|[スキャナーのタイムアウト設定を変更する](#change-the-timeout-settings-for-the-scanner)
|EnableBarHiding|[Azure Information Protection バーを完全に非表示にする](#permanently-hide-the-azure-information-protection-bar)|
|EnableCustomPermissions|[ユーザーに対してカスタムのアクセス許可オプションを利用可能または利用不可にする](#make-the-custom-permissions-options-available-or-unavailable-to-users)|
|EnableCustomPermissionsForCustomProtectedFiles|[カスタム アクセス許可で保護されているファイルについて、ファイル エクスプローラーでカスタム アクセス許可を常にユーザーに表示する](#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer) |
|EnablePDFv2Protection|[PDF 暗号化の ISO 標準を使用して PDF ファイルを保護しない](#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)|
|FileProcessingTimeout|[スキャナーのタイムアウト設定を変更する](#change-the-timeout-settings-for-the-scanner)
|LabelbyCustomProperty|[Secure Islands からのラベルの移行と、その他のラベル付けのソリューション](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|LabelToSMIME|[ラベルを構成して Outlook で S/MIME 保護を適用する](#configure-a-label-to-apply-smime-protection-in-outlook)|
|ログ レベル|[ローカルのログ記録レベルを変更する](#change-the-local-logging-level)
|LogMatchedContent|[ユーザーのサブセットに対して送信情報の種類の一致を無効にする](#disable-sending-information-type-matches-for-a-subset-of-users)|
|OutlookBlockTrustedDomains|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookBlockUntrustedCollaborationLabel|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookDefaultLabel|[Outlook に別の既定ラベルを設定する](#set-a-different-default-label-for-outlook)|
|Outlookジャスト Ifytrusteddomains|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookJustifyUntrustedCollaborationLabel|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookRecommendationEnabled|[Outlook で推奨分類を有効にする](#enable-recommended-classification-in-outlook)|
|OutlookOverrideUnlabeledCollaborationExtensions|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnTrustedDomains|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnUntrustedCollaborationLabel|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|PostponeMandatoryBeforeSave|[必須のラベル付けを使用するときにドキュメントの "後で" を削除する](#remove-not-now-for-documents-when-you-use-mandatory-labeling)|
|ProcessUsingLowIntegrity|[スキャナーの低整合性レベルを無効にする](#disable-the-low-integrity-level-for-the-scanner)|
|PullPolicy|[切断されたコンピューターのサポート](#support-for-disconnected-computers)
|RemoveExternalContentMarkingInApp|[他のラベル付けソリューションからヘッダーとフッターを削除する](#remove-headers-and-footers-from-other-labeling-solutions)|
|ReportAnIssueLink|[ユーザーの "問題の報告" を追加する](#add-report-an-issue-for-users)|
|Runauditinformationタイプの検出|[ドキュメント内の検出された機密情報の Azure Information Protection analytics への送信を無効にする](#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)|
|RunPolicyInBackground|[バックグラウンドでの分類の継続的実行をオンにする](#turn-on-classification-to-run-continuously-in-the-background)|
|ScannerConcurrencyLevel|[スキャナーで使用されるスレッドの数を制限する](#limit-the-number-of-threads-used-by-the-scanner)|
|SyncPropertyName|[既存のカスタム プロパティを使用して Office ドキュメントにラベルを付ける](#label-an-office-document-by-using-an-existing-custom-property)|
|SyncPropertyState|[既存のカスタム プロパティを使用して Office ドキュメントにラベルを付ける](#label-an-office-document-by-using-an-existing-custom-property)|

## <a name="prevent-sign-in-prompts-for-ad-rms-only-computers"></a>AD RMS 専用コンピューターのサインイン プロンプトが表示されないようにする

既定では、Azure Information Protection クライアントは Azure Information Protection サービスへ自動的に接続しようとします。 AD RMS とのみ通信するコンピューターの場合、この構成では不必要なサインイン プロンプトがユーザーに表示されます。 レジストリを編集し、このサインイン プロンプトが表示されないようにすることができます。

 - 次の値の名前を検索し、値データを **0** に設定します。
    
    **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

この設定に関係なく、Azure Information Protection クライアントは引き続き標準 [RMS サービス検索プロセス](client-deployment-notes.md#rms-service-discovery)に従い、その AD RMS クラスターを検出します。

## <a name="sign-in-as-a-different-user"></a>別のユーザーでのサイン イン

通常、運用環境では、Azure Information Protection クライアントを使用しているときに別のユーザーとしてサインインする必要はありません。 ただし管理者の場合は、テスト段階のときに別ユーザーとしてサインインする必要がある場合があります。 

現在サインインしているアカウントを確認するには、 **[Microsoft Azure Information Protection]** ダイアログ ボックスを使用します。Office アプリケーションを開き、 **[ホーム]** タブの **[保護]** グループで、 **[保護]** をクリックし、 **[ヘルプとフィードバック]** をクリックします。 アカウント名が **[クライアント ステータス]** セクションに表示されます。

表示されるサインイン アカウントのドメイン名も必ず確認してください。 正しいアカウントでサインインしていてもドメインが間違っている、という状況は気付きにくいものです。 適切ではないアカウントが使用された場合は、Azure Information Protection ポリシーのダウンロードが失敗することや、目的のラベルや機能が表示されないことがあります。

別のユーザーでサイン インする方法は以下の通りです。

1. **%localappdata%\Microsoft\MSIP** に移動し、**TokenCache** ファイルを削除します。

2. 開いている Office アプリケーションがあれば再起動し、別のユーザー アカウントでサインインします。 Azure Information Protection サービスにサインインするように求めるプロンプトが Office アプリケーションで表示されない場合、 **[Microsoft Azure Information Protection]** ダイアログ ボックスに戻り、更新された **[クライアント ステータス]** セクションの **[サインイン]** をクリックします。

さらに、本サービスには以下の規定が適用されます。

- これらの手順を完了した後も Azure Information Protection クライアントがまだ古いアカウントを使用してサインインしている場合は、Internet Explorer からすべての cookie を削除してから、手順 1 と 2 をもう一度実行します。

- シングル サインオンを使用する場合は、トークン ファイルを削除した後に Windows からサインアウトし、別のユーザー アカウントでサインインする必要があります。 Azure Information Protection クライアントは、現在サインインしているユーザーアカウントを使用して、自動的に認証を行います。

- このソリューションでは、同じテナントから別ユーザーとしてサインインする操作がサポートされています。 別のテナントから別のユーザーとしてサインインする操作はサポートされていません。 複数のテナントがある Azure Information Protection をテストするには、異なるコンピューターを使用します。

- **[ヘルプとフィードバック]** の **[設定のリセット]** オプションからサインアウトし、現在ダウンロードされている Azure Information Protection ポリシーを削除できます。


## <a name="enforce-protection-only-mode-when-your-organization-has-a-mix-of-licenses"></a>組織が種類の異なるライセンスを保有している場合の保護のみモードの適用

組織が Azure Information Protection のライセンスを保有せず、データ保護のために Azure Rights Management サービスを含む Office 365 のライセンスを保有している場合、Azure Information Protection クライアント (Windows 用) は自動的に[保護のみモード](client-protection-only-mode.md)で実行されます。

ただし、組織が Azure Information Protection のサブスクリプションを保有している場合は、既定で、すべての Windows コンピューターで Azure Information Protection ポリシーをダウンロードできます。 Azure Information Protection クライアントはライセンスのチェックと適用を行いません。 

Azure Information Protection のライセンスを保有せず、Azure Rights Management サービスを含む Office 365 のライセンスを保有しているユーザーがいる場合には、対象ユーザーのコンピューター上のレジストリを編集して、ライセンス付与されていない Azure Information Protection の分類とラベル付け機能が実行されないようにします。

次の値の名前を検索し、値を **0** に設定します。

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 

また、これらのコンピューターの **%LocalAppData%\Microsoft\MSIP** フォルダーに、**Policy.msip** という名前のファイルがないことを確認します。 このファイルが存在する場合は、削除します。 このファイルには Azure Information Protection ポリシーが含まれており、レジストリを編集する前、または Azure Information Protection クライアントをデモ オプションを使用してインストールした場合に、ダウンロードされた可能性があります。

## <a name="add-report-an-issue-for-users"></a>ユーザー向けの "問題の報告" を追加する

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。 

次のクライアントの詳細設定を指定すると、ユーザーに、 **[ヘルプとフィードバック]** クライアント ダイアログ ボックスから選択できる **[問題の報告]** オプションが表示されます。 リンクの HTTP 文字列を指定します。 たとえば、ユーザーが問題を報告するための、カスタマイズされた独自の Web ページや、ヘルプ デスクに送信される電子メール アドレスです。 

この詳細設定を構成するには、次の文字列を入力します。

- キー: **ReportAnIssueLink**

- 値: **\<HTTP string>**

Web サイトの値の例: `https://support.contoso.com`

メール アドレスの値の例: `mailto:helpdesk@contoso.com`

## <a name="hide-the-classify-and-protect-menu-option-in-windows-file-explorer"></a>エクスプローラーの [Hide the Classify and Protect]\(分類の非表示と保護) メニュー オプション

次の DWORD 値の名前を (任意の値と共に) 作成します。

**HKEY_CLASSES_ROOT\AllFilesystemObjects\shell\Microsoft.Azip.RightClick\LegacyDisable**

## <a name="support-for-disconnected-computers"></a>切断されたコンピューターのサポート

既定では、Azure Information Protection クライアントは Azure Information Protection サービスへ自動的に接続し、Azure Information Protection の最新のポリシーのダウンロードを試みます。 一定期間インターネットに接続できないコンピューターがある場合は、レジストリを編集することでサービスに接続しようとしないように設定することができます。 

インターネットに接続されていない場合、クライアントは、組織のクラウドベース キーを使用することによる保護 (または保護の削除) を適用できません。 代わりに、クライアントは、分類にのみ適用されるラベルの使用か、[HYOK](../configure-adrms-restrictions.md) を使用する保護に制限されます。

Azure Information Protection サービスへのサインイン プロンプトが表示されないようにするには、Azure portal で構成する必要がある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使い、コンピューターにポリシーをダウンロードします。 または、レジストリを編集してこのサインイン プロンプトが表示されないようにすることができます。

- クライアントの詳細設定を構成するには:
    
    1. 次の文字列を入力します。
    
        - キー: **PullPolicy**
        
        - 値: **False**
    
    2. この設定を含むポリシーをダウンロードし、後続の手順に従ってそれをコンピューターにインストールします。

- または、レジストリを編集するには:
    
    - 次の値の名前を検索し、値データを **0** に設定します。
    
        **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\EnablePolicyDownload** 


クライアントは、 **%LocalAppData%\Microsoft\MSIP** フォルダー内に、**Policy.msip** という名前の有効なポリシー ファイルを置く必要があります。

Azure portal からグローバル ポリシーまたはスコープ ポリシーをエクスポートし、エクスポートしたファイルをクライアントのコンピューターにコピーすることができます。 この方法を使用して、古いポリシー ファイルを最新のポリシーに置き換えることもできます。 ただし、ポリシーのエクスポートでは、ユーザーが複数のスコープ ポリシーに属しているシナリオはサポートされません。 また、ユーザーが [[ヘルプとフィードバック]](client-admin-guide.md#help-and-feedback-section) の **[設定のリセット]** オプションを選択する場合、このアクションによってポリシー ファイルが削除され、ポリシー ファイルを手動で交換するか、クライアントがポリシーをダウンロードするためにサービスに接続するまで、クライアントは動作できなくなります。

Azure Portal からポリシーをエクスポートすると、ポリシーの複数のバージョンを含む zip 形式のファイルがダウンロードされます。 ポリシーの各バージョンは、Azure Information Protection クライアントのさまざまなバージョンに対応しています。

1. ファイルを解凍し、次の表を利用して必要なポリシー ファイルを特定します。 
    
    |［ファイル名］|対応するクライアント バージョン|
    |--------------------------|---------------------------------------------|
    |Policy1.1.msip |バージョン 1.2|
    |Policy1.2.msip |バージョン 1.3 - 1.7|
    |Policy1.3.msip |バージョン 1.8 - 1.29|
    |Policy1.4.msip |バージョン 1.32 以降|
    
2. 特定したファイルの名前を **Policy.msip** に変更し、Azure Information Protection クライアントがインストールされているコンピューターの **%LocalAppData%\Microsoft\MSIP** フォルダーにコピーします。 

接続が切断されたコンピューターが Azure Information Protection スキャナーの現在の GA バージョンを実行している場合は、追加の構成手順を実行する必要があります。 詳細については、「制限: スキャナーサーバーがスキャナーの展開手順から[インターネットに接続できない](../deploy-aip-scanner.md#restriction-the-scanner-server-cannot-have-internet-connectivity)」を参照してください。

## <a name="hide-or-show-the-do-not-forward-button-in-outlook"></a>Outlook の [転送不可] ボタンを表示または非表示にする

このオプションを構成するには、[ポリシー設定](../configure-policy-settings.md)の **[Add the Do Not Forward button to the Outlook ribbon]\(Outlook リボンに [転送不可] ボタンを追加する\)** を使用することをお勧めします。 ただし、Azure Portal で構成する[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用して、このオプションを構成することもできます。

この設定を構成すると、Outlook のリボンの **[転送不可]** ボタンが表示または非表示になります。 この設定は、Office メニューからの [転送不可] オプションには影響しません。

この詳細設定を構成するには、次の文字列を入力します。

- キー: **DisableDNF**

- 値: ボタンを非表示にするには **True**、ボタンを表示するには **False**

## <a name="make-the-custom-permissions-options-available-or-unavailable-to-users"></a>ユーザーに対してカスタムのアクセス許可オプションを利用可能または利用不可にする

このオプションを構成するには、[ポリシー設定](../configure-policy-settings.md)の **[Make the custom permissions option available to users]\(ユーザーがカスタム アクセス許可オプションを使用できるようにする\)** を使用することをお勧めします。 ただし、Azure Portal で構成する[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用して、このオプションを構成することもできます。 

この設定を構成して、ユーザーにポリシーを公開した場合、ユーザーが独自の保護設定を選択できるように、カスタムのアクセス許可オプションが表示されるか、または、確認メッセージが表示されない限り、ユーザーが独自の保護設定を選択できないように非表示になります。

この詳細設定を構成するには、次の文字列を入力します。

- キー: **EnableCustomPermissions**

- 値: カスタム アクセス許可オプションを表示する場合は **True**、このオプションを非表示にする場合は **False**

## <a name="for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer"></a>カスタム アクセス許可で保護されているファイルについて、ファイル エクスプローラーでカスタム アクセス許可を常にユーザーに表示する

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。 この設定はプレビュー段階であり、変更される可能性があります。

[ポリシー設定](../configure-policy-settings.md)の **[Make the custom permissions option available to users]\(ユーザーがカスタム アクセス許可オプションを使用できるようにする\)** 、または前のセクションの同等のクライアント詳細設定を構成した場合、ユーザーは、保護されたドキュメントで既に設定されているカスタム アクセス許可を表示または変更できません。 

このクライアント詳細設定を作成して構成した場合、ユーザーはファイル エクスプローラーを使用してファイルを右クリックすることで、保護されたドキュメントのカスタム アクセス許可を表示および変更できます。 Office リボンの **[保護]** ボタンからの **[カスタム アクセス許可]** オプションは、非表示のままです。

この詳細設定を構成するには、次の文字列を入力します。

- キー: **EnableCustomPermissionsForCustomProtectedFiles**

- 値: **True**

## <a name="permanently-hide-the-azure-information-protection-bar"></a>Azure Information Protection バーを完全に非表示にする

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。 これは、[ポリシー設定](../configure-policy-settings.md)の **[Display the Information Protection bar in Office apps]\(Office アプリで Information Protection バーを表示する\)** を **[オン]** に設定している場合にのみ使用します。

既定では、ユーザーが **[ホーム]** タブ、 **[保護]** グループ、 **[保護]** ボタンから **[バーの表示]** オプションをクリアすると、その Office アプリに Information Protection バーが表示されなくなります。 ただし、バーは、次に Office アプリを開いたときに自動的に再表示されます。

ユーザーがバーを非表示にすることを選択した後に、自動的に再表示されることを防ぐには、このクライアント設定を使用します。 **[このバーを閉じる]** アイコンを使用してバーを閉じた場合、この設定は何も影響を与えません。

Azure Information Protection バーが非表示のままであっても、推奨の分類を構成している場合やドキュメントや電子メールにラベルを指定する必要がある場合、ユーザーは一時的に表示されるバーからラベルを選択できます。 

この詳細設定を構成するには、次の文字列を入力します。

- キー: **EnableBarHiding**

- 値: **True**

## <a name="enable-order-support-for-sublabels-on-attachments"></a>添付ファイルでサブラベルの順序のサポートを有効にする

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。

サブラベルがあり、次の[ポリシー設定](../configure-policy-settings.md)を構成している場合は、この設定を使います。

- **添付ファイルのある電子メール メッセージの場合、その添付ファイルの最上位の分類と一致するラベルを適用します**

次の文字列を構成します。

- キー: **CompareSubLabelsInAttachmentAction**

- 値: **True**

これを設定しない場合、最上位に分類されている親ラベルの最初のラベルが電子メールに適用されます。 

この設定を使用して、最上位に分類されている親ラベルで順序が最後のサブラベルが電子メールに適用されます。 このシナリオで適用されるラベルの順序を変更する必要がある場合は、「[Azure Information Protection のラベルを削除または順序変更する方法](../configure-policy-delete-reorder.md)」を参照してください。

## <a name="exempt-outlook-messages-from-mandatory-labeling"></a>必須ラベルから Outlook メッセージを除外する

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。

既定では、[ポリシー設定](../configure-policy-settings.md)を有効にすると、**すべてのドキュメントと電子メールにラベル**が設定され、保存されたすべてのドキュメントと送信された電子メールにラベルが適用されます。 次の詳細設定を構成すると、ポリシー設定は Office ドキュメントにのみ適用され、Outlook メッセージには適用されません。

この詳細設定を構成するには、次の文字列を入力します。

- キー: **DisableMandatoryInOutlook**

- 値: **True**

## <a name="enable-recommended-classification-in-outlook"></a>Outlook で推奨分類を有効にする

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。 この設定はプレビュー段階であり、変更される可能性があります。

推奨分類のラベルを設定すると、Word、Excel、PowerPoint では、推奨ラベルを受け入れるか、却下するように求められます。 また、このラベル推奨が Outlook でも表示されます。

この詳細設定を構成するには、次の文字列を入力します。

- キー: **OutlookRecommendationEnabled**

- 値: **True**


## <a name="implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent"></a>Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する

この構成では、Azure Portal で構成する必要のある、複数の[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。

次のクライアント詳細設定を作成して構成すると、Outlook でユーザーに対してポップアップ メッセージが表示されます。これにより、次のどちらかのシナリオで、電子メールを送信する前に警告したり、電子メールの送信理由の入力を求めたり、電子メールの送信を妨げることができます。

- **電子メール、または電子メールの添付ファイルに特定のラベルが含まれる**:
    - 添付ファイルはあらゆる種類のファイルである可能性がある

- **電子メール、または電子メールの添付ファイルにラベルがない**:
    - 添付ファイルは Office ドキュメントまたは PDF ドキュメントである可能性がある

これらの条件が満たされると、ユーザーには、次のいずれかの操作を含むポップアップメッセージが表示されます。

- **警告**: ユーザーは、確認して送信するか、キャンセルすることができます。

- **[ジャスティファイ]** : ユーザーに対して理由 (定義済みオプションまたは自由形式) の入力を求められます。  その後、ユーザーは電子メールを送信またはキャンセルできます。 理由のテキストは、他のシステムで読み取ることができるように電子メールの X ヘッダーに書き込まれます。 たとえば、データ損失防止 (DLP) サービスです。

- **ブロック**: 条件が残っている間、ユーザーは電子メールを送信できません。 メッセージには、ユーザーが問題に対処できるように、電子メールをブロックする理由が含まれます。 たとえば、特定の受信者を削除する、電子メールにラベルを付けるなどです。 

ポップアップメッセージが特定のラベルに対して実行されている場合は、ドメイン名を使用して受信者の例外を構成できます。

ポップアップメッセージの結果の操作は、ローカルの Windows イベントログの **[アプリケーションとサービスログ**]  > **Azure Information Protection**に記録されます。

- 警告メッセージ: 情報 ID 301

- メッセージの配置: 情報 ID 302

- ブロックメッセージ: 情報 ID 303

理由メッセージからのイベント エントリの例:

```
Client Version: 1.53.10.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Price list.msg
Item Name: Price list
Process Name: OUTLOOK
Action: Justify
User Justification: My manager approved sharing of this content
Action Source: 
User Response: Confirmed
```
以下のセクションでは、各アドバンストクライアント設定の構成手順について説明します。また、 [Outlook を使用して情報の過剰な共有を制御するように Azure Information Protection を構成する](../infoprotect-oversharing-tutorial.md)方法についても説明します。

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels"></a>特定のラベルに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装するには:

特定のラベルに対するポップアップ メッセージを実装するには、それらのラベルのラベル ID が必要です。 Azure Portal で Azure Information Protection ポリシーを表示または構成するとき、ラベル ID 値は **[ラベル]** ブレードに表示されます。 ファイルにラベルが適用されている場合、[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) PowerShell コマンドレットを実行してラベル ID (MainLabelId または SubLabelId) を特定することもできます。 ラベルにサブラベルがある場合、親ラベルではなく、サブラベルの ID だけを常に指定してください。

次のキーを使用して、次の 1 つまたは複数のクライアント詳細設定を作成します。 値については、1 つまたは複数のラベルの ID をそれぞれコンマで区切って指定します。

コンマ区切り文字列としての複数のラベル ID の値の例: `dcf781ba-727f-4860-b3c1-73479e31912b,1ace2cc3-14bc-4142-9125-bf946a70542c,3e9df74d-3168-48af-8b11-037e3021813f`


- 警告メッセージ:
    
    - キー: **OutlookWarnUntrustedCollaborationLabel**
    
    - 値: \<**コンマ区切りのラベル ID**>

- 理由の入力メッセージ:
    
    - キー: **OutlookJustifyUntrustedCollaborationLabel**
    
    - 値: \<**コンマ区切りのラベル ID**>

- ブロック メッセージ:
    
    - キー: **OutlookBlockUntrustedCollaborationLabel**
    
    - 値: \<**コンマ区切りのラベル ID**>

#### <a name="to-exempt-domain-names-for-pop-up-messages-configured-for-specific-labels"></a>特定のラベル用に構成されたポップアップメッセージのドメイン名を除外するには

これらのポップアップメッセージで指定したラベルについては、特定のドメイン名を除外して、そのドメイン名が電子メールアドレスに含まれている受信者のメッセージがユーザーに表示されないようにすることができます。 この場合、電子メールは中断なく送信されます。 複数のドメインを指定するには、ドメインをコンマで区切って 1 つの文字列として追加します。

一般的な構成では、組織の外部の受信者、または組織の承認済みのパートナーではない受信者についてのみ、ポップアップ メッセージが表示されます。 この場合は、お客様の組織およびパートナーによって使用されるすべての電子メール ドメインを指定します。

次のクライアントの詳細設定を作成し、値として1つ以上のドメインをコンマで区切って指定します。

コンマ区切り文字列としての複数のドメインの値の例: `contoso.com,fabrikam.com,litware.com`

- 警告メッセージ:
    
    - キー: **OutlookWarnTrustedDomains**
    
    - 値: **\<** コンマ区切りのドメイン名 **>**

- 理由の入力メッセージ:
    
    - キー: **Outlookジャスト Ifytrusteddomains**
    
    - 値: **\<** コンマ区切りのドメイン名 **>**

- ブロック メッセージ:
    
    - キー: **Outlookblocktrusteddomains**
    
    - 値: **\<** コンマ区切りのドメイン名 **>**

たとえば、 **[社外秘 \ すべての従業員]** ラベルに対して**OutlookBlockUntrustedCollaborationLabel**アドバンストクライアント設定を指定したとします。 ここで、 **Outlookblocktrusteddomains**と**contoso.com**の追加のアドバンストクライアント設定を指定します。 その結果、ユーザーは、"**社外秘 \ すべての従業員**" というラベルが付いたときに john@sales.contoso.com に電子メールを送信できますが、Gmail アカウントに同じラベルの電子メールを送信することは禁止されます。

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label"></a>ラベルのない電子メールまたは添付ファイルに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装するには:

次のいずれかの値を使用して、次のクライアント詳細設定を作成します。

- 警告メッセージ:
    
    - キー: **OutlookUnlabeledCollaborationAction**
    
    - 値: **Warn**

- 理由の入力メッセージ:
    
    - キー: **OutlookUnlabeledCollaborationAction**
    
    - 値:**均等**配置

- ブロック メッセージ:
    
    - キー: **OutlookUnlabeledCollaborationAction**
    
    - 値:**ブロック**

- これらのメッセージをオフにする:
    
    - キー: **OutlookUnlabeledCollaborationAction**
    
    - 値:**オフ**

#### <a name="to-define-specific-file-name-extensions-for-the-warn-justify-or-block-pop-up-messages-for-email-attachments-that-dont-have-a-label"></a>ラベルのない電子メールの添付ファイルのポップアップメッセージに対して、警告、配置、またはブロックを行うための特定のファイル名拡張子を定義するには

既定では、すべての Office ドキュメントおよび PDF ドキュメントに対して、ポップアップメッセージの警告、位置揃え、またはブロックが適用されます。 この一覧を調整するには、追加のアドバンストクライアントプロパティとファイル名拡張子のコンマ区切りの一覧を使用して、メッセージを表示するファイル名拡張子を指定します。

コンマ区切りの文字列として定義する複数のファイル名拡張子の値の例: `.XLSX,.XLSM,.XLS,.XLTX,.XLTM,.DOCX,.DOCM,.DOC,.DOCX,.DOCM,.PPTX,.PPTM,.PPT,.PPTX,.PPTM`

この例では、ラベル付けされていない PDF ドキュメントは、ポップアップメッセージの警告、配置、またはブロックにはなりません。


- キー: **OutlookOverrideUnlabeledCollaborationExtensions**

- 値: **\< 個**のメッセージを表示するファイル名拡張子、コンマ区切り **>**

#### <a name="to-specify-a-different-action-for-email-messages-without-attachments"></a>添付ファイルのない電子メールメッセージに対して別のアクションを指定するには

既定では、ポップアップメッセージを表示するために OutlookUnlabeledCollaborationAction に指定する値は、ラベルのない電子メールまたは添付ファイルに適用されます。 この構成を調整するには、添付ファイルのない電子メールメッセージに対して、別のアドバンストクライアント設定を指定します。

次のいずれかの値を使用して、次のクライアント詳細設定を作成します。

- 警告メッセージ:
    
    - キー: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - 値: **Warn**

- 理由の入力メッセージ:
    
    - キー: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - 値:**均等**配置

- ブロック メッセージ:
    
    - キー: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - 値:**ブロック**

- これらのメッセージをオフにする:
    
    - キー: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - 値:**オフ**

このクライアント設定を指定しない場合は、OutlookUnlabeledCollaborationAction に指定した値が、添付ファイルのない電子メールメッセージと、添付ファイルを含むラベルなしの電子メールメッセージに使用されます。


## <a name="set-a-different-default-label-for-outlook"></a>Outlook に別の既定ラベルを設定します

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。 

この設定を構成すると、Outlook では、Azure Information Protection ポリシーで **[既定のラベルを選択]** 設定に構成した既定のラベルが適用されません。 別の既定のラベルを適用できるか、ラベルがありません。

別のラベルを適用するには、ラベル ID を指定する必要があります。 Azure Portal で Azure Information Protection ポリシーを表示または構成するとき、ラベル ID 値は **[ラベル]** ブレードに表示されます。 ファイルにラベルが適用されている場合、[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) PowerShell コマンドレットを実行してラベル ID (MainLabelId または SubLabelId) を特定することもできます。 ラベルにサブラベルがある場合、親ラベルではなく、サブラベルの ID だけを常に指定してください。

Outlook で既定のラベルが適用されないように、 **[なし]** を指定します。

この詳細設定を構成するには、次の文字列を入力します。

- キー: **OutlookDefaultLabel**

- 値: \<**ラベル ID**> または**なし**

## <a name="configure-a-label-to-apply-smime-protection-in-outlook"></a>ラベルを構成して Outlook で S/MIME 保護を適用する

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。

動作中の [S/MIME の展開](https://docs.microsoft.com/exchange/s-mime-for-message-signing-and-encryption)があり、Azure Information Protection の Rights Management 保護ではなくこの保護方法をラベルが電子メールに対して自動的に適用するようにしたい場合にのみ、この設定を使用します。 結果として得られる保護は、ユーザーが Outlook から手動で S/MIME オプションを選択した場合と同じものです。

この構成では、S/MIME 保護を適用したい Azure Information Protection ラベルごとに、**LabelToSMIME** という名前のクライアントの詳細設定を指定する必要があります。 次に、各エントリに対して、次の構文を使用して値を設定します。

`[Azure Information Protection label ID];[S/MIME action]`

Azure Portal で Azure Information Protection ポリシーを表示または構成するとき、ラベル ID 値は **[ラベル]** ブレードに表示されます。 サブラベルと共に S/MIME を使うには、親ラベルではなく、サブラベルの ID だけを常に指定します。 サブラベルを指定する場合、親ラベルが同じスコープまたはグローバル ポリシー内にある必要があります。

次のような S/MIME アクションが可能です。

- `Sign;Encrypt`: デジタル署名と S/MIME 暗号化を適用する

- `Encrypt`: S/MIME 暗号化のみを適用する

- `Sign`: デジタル署名のみを適用する

**dcf781ba-727f-4860-b3c1-73479e31912b** のラベル ID の値の例:

- デジタル署名と S/MIME 暗号化を適用する:
    
    **dcf781ba-727f-4860-b3c1-73479e31912b;Sign;Encrypt**

- S/MIME 暗号化のみを適用する:
    
    **dcf781ba-727f-4860-b3c1-73479e31912b;Encrypt**
    
- デジタル署名のみを適用する:
    
    **dcf781ba-727f-4860-b3c1-73479e31912b;Sign**

この構成の結果として、電子メール メッセージに向けてこのラベルを適用すると、ラベルの分類に加えて S/MIME 保護が電子メールに適用されます。

指定するラベルが Azure portal で Rights Management の保護用に構成されている場合、S/MIME 保護は Outlook でのみ Rights Management の保護を置き換えます。 ラベル付けをサポートしているその他のすべてのシナリオでは、Rights Management の保護が適用されます。

ラベルが Outlook 内でのみ表示されるようにする必要がある場合は、「[クイック スタート: ラベルを構成して、ユーザーが機密情報を含む電子メールを簡単に保護できるようにする](../quickstart-label-dnf-protectedemail.md)」で説明されているように、ラベルを構成してユーザー定義の **[転送不可]** シングル アクションを適用します。

## <a name="remove-not-now-for-documents-when-you-use-mandatory-labeling"></a>必須のラベル付けを使用するときにドキュメントの "後で" を削除する

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。 

**[すべてのドキュメントとメールにラベルを付ける]** の[ポリシー設定](../configure-policy-settings.md)を使うと、ユーザーが Office ドキュメントを初めて保存するとき、およびメールを送信するときに、ラベルの選択を求めるメッセージが表示されます。 ドキュメントの場合、ユーザーは **[後で]** を選択して一時的にメッセージを無視し、ラベルを選んで、ドキュメントに戻ることができます。 ただし、ラベルを付けないと、保したドキュメントを閉じることはできません。 

この設定を構成すると、 **[後で]** オプションが削除され、ユーザーはドキュメントを初めて保存するときにラベルを選択する必要があります。

この詳細設定を構成するには、次の文字列を入力します。

- キー: **PostponeMandatoryBeforeSave**

- 値: **False**

## <a name="turn-on-classification-to-run-continuously-in-the-background"></a>バックグラウンドでの分類の継続的実行をオンにする

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。 この設定はプレビュー段階であり、変更される可能性があります。

この設定を構成すると、Azure Information Protection クライアントが推奨ラベルを自動的にドキュメントに適用する[既定の動作](../configure-policy-classification.md#how-automatic-or-recommended-labels-are-applied)が次のように変わります。 

- Word、Excel、PowerPoint に対して、自動分類はバックグラウンドで継続的に実行されます。  

この動作は Outlook でも変わりません。

Azure Information Protection クライアントがユーザーによって指定された条件規則をドキュメントで定期的にチェックするとき、この動作は SharePoint Online に格納されるドキュメントに対する自動的で推奨される分類と保護を有効にします。 条件規則が既に実行されているため、大きなファイルもすばやく保存されます。 

条件規則がユーザーの入力と同時にリアルタイムで実行されることはありません。 ドキュメントが変更された場合、バックグラウンド タスクとして定期的に実行されます。

この詳細設定を構成するには、次の文字列を入力します。

- キー: **RunPolicyInBackground**

- 値: **True**

## <a name="dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption"></a>PDF 暗号化の ISO 標準を使用して PDF ファイルを保護しない

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。 

最新バージョンの Azure Information Protection クライアントを使用して PDF ファイルを保護する場合、得られるファイル名の拡張子は .pdf のままとなり、PDF 暗号化の ISO 標準に準拠します。 この標準の詳細については、[ISO 32000-1 から派生し、Adobe Systems Incorporated が発行したドキュメント](https://www.adobe.com/content/dam/acom/en/devnet/pdf/pdfs/PDF32000_2008.pdf)のセクション「**7.6 Encryption**」(7.6 暗号化) を参照してください。

クライアントを、ファイル名拡張子 .ppdf を使って PDF ファイルを保護していた旧バージョンのクライアントの動作に戻す必要がある場合は、次の文字列を入力して以下の詳細設定を使います。

- キー: **EnablePDFv2Protection**

- 値: **False**

たとえば、PDF 暗号化の ISO 標準をサポートしていない PDF リーダーを使用している場合は、すべてのユーザーに対してこの設定が必要です。 または、新しい形式をサポートする PDF リーダーを段階的に導入する場合は、一部のユーザーに対してその設定を構成する必要があります。 この設定を使用する別の理由としては、署名された PDF ドキュメントに保護を追加することが必要な場合が挙げられます。 署名された PDF ドキュメントを .ppdf 形式を使用してさらに保護することができます。これは、この保護がファイルのラッパーとして実装されるために可能になります。 

Azure Information Protection スキャナーで新しい設定を使用するには、スキャナー サービスを再起動する必要があります。 また、スキャナーでは既定で PDF ドキュメントが保護されなくなります。 EnablePDFv2Protection が False に設定されているときにスキャナーで PDF ドキュメントを保護する場合は、[レジストリを編集する](../deploy-aip-scanner.md#editing-the-registry-for-the-scanner)必要があります。

新しい PDF の暗号化について詳しくは、ブログ投稿「[New support for PDF encryption with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/New-support-for-PDF-encryption-with-Microsoft-Information/ba-p/262757)」 (Microsoft Information Protection での PDF の新しい暗号化のサポート) をご覧ください。

PDF 暗号化の ISO 標準をサポートする PDF リーダー、および古い形式をサポートするリーダーの一覧については、「[Supported PDF readers for Microsoft Information Protection](protected-pdf-readers.md)」(Microsoft Information Protection でサポートされる PDF リーダー) を参照してください。

### <a name="to-convert-existing-ppdf-files-to-protected-pdf-files"></a>既存の .ppdf ファイルを保護された .pdf ファイルに変換するには

Azure Information Protection クライアントに新しい設定のクライアント ポリシーがダウンロードされると、既存の .ppdf ファイルを、PDF の暗号化に ISO 標準が使用された保護された .pdf ファイルに PowerShell コマンドを使用して変換することができます。 

ご自分で保護していないファイルに次の手順を行うには、[Rights Management の使用権限](../configure-usage-rights.md)を持っているか、スーパー ユーザーでないと、ファイルから保護を削除できません。 スーパー ユーザーの機能を有効にし、アカウントをスーパー ユーザーとして構成するには、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../configure-super-users.md)」をご覧ください。

また、自分で保護していないファイルにこれらの手順を使用する場合、そのユーザーは [RMS Issuer](../configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) になります。 このシナリオでは、ドキュメントを最初に保護したユーザーは、それを追跡して取り消すことができなくなります。 ユーザーが保護されている PDF 文書を追跡して取り消す必要がある場合、ファイル エクスプローラーの右クリックを使用して、ラベルを手動で削除して最適用するよう依頼します。

PowerShell コマンドを使用して既存の .ppdf ファイルを保護された .pdf ファイルに変換するには、PDF の暗号化に ISO 標準を使用します。

1. .ppdf ファイルに [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) を使用します。 たとえば、次のようになります。
    
        Get-AIPFileStatus -Path \\Finance\Projectx\sales.ppdf

2. 出力の次のパラメーター値のメモを取ります。
    
   - 存在する場合、**SubLabelId** の値 (GUID)。 この値が空の場合、サブラベルは使用されていないので、代わりに **MainLabelId** 値のメモを取ります。
    
     注: **MainLabelId** にも値がない場合、ファイルはレベル付けされていません。 この場合は、手順 3 と 4 のコマンドではなく、[Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile) コマンドと [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) コマンドを使用します。
    
   - **RMSTemplateId** の値。 この値が **Restricted Access** の場合、ユーザーはファイルを、ラベルに構成されている保護設定ではなく、カスタム アクセス許可を使用して保護しています。 続行すると、それらのカスタム設定はラベルの保護設定により上書きされます。 続行するか、ユーザー (**RMSIssuer** に表示される値) に対してラベルを削除し、元のカスタム アクセス許可と共にそれを再適用することを依頼するかどうかを決定します。

3. *RemoveLabel* パラメーターを使用し、[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) を使用して、ラベルを削除します。 **[Users must provide justification to set a lower classification label, remove a label, or remove protection]** \(ユーザーは分類ラベルの秘密度を下げる、ラベルを削除する、または保護を解除するときにその理由を示す必要があります) の[ポリシー設定](../configure-policy-settings.md)を使用している場合は、理由付きで *[位置揃え]* パラメーターも指定する必要があります。 たとえば、次のようになります。 
    
        Set-AIPFileLabel \\Finance\Projectx\sales.ppdf -RemoveLabel -JustificationMessage 'Removing .ppdf protection to replace with .pdf ISO standard'

4. 手順 1 で指定したラベルの値を指定して、元のラベルを最適用します。 たとえば、次のようになります。
    
        Set-AIPFileLabel \\Finance\Projectx\sales.pdf -LabelId d9f23ae3-1234-1234-1234-f515f824c57b

ファイルは .pdf ファイル名拡張子を維持しますが、以前と同様に分類され、PDF の暗号化のための ISO 標準を使用して保護されます。

## <a name="support-for-files-protected-by-secure-islands"></a>Secure Islands によって保護されたファイルのサポート

この構成オプションはプレビュー段階であり、変更される可能性があります。

ドキュメントを保護するために Secure Islands を使用した場合、この保護の結果、テキスト ファイル、画像ファイル、一般的に保護対象となるファイルが保護される可能性があります。 たとえば、ファイル名の拡張子が .ptxt、.pjpeg、または .pfile のファイルです。 以下のようにレジストリを編集すると、Azure Information Protection はこれらのファイルを復号化できます。


以下のように **EnableIQPFormats** という DWORD 値を次のレジストリ パスに追加し、値データを **1** に設定します。

- 64 ビット版の Windows: HKEY_LOCAL_MACHINE\\SOFTWARE\\WOW6432Node\\Microsoft\\MSIP

- 32 ビット版の Windows: HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\MSIP

このレジストリ編集の結果、次のシナリオがサポートされます。

- Azure Information Protection ビューアーは、これらの保護されたファイルを開くことができます。

- Azure Information Protection スキャナーは、これらのファイルに機密情報が含まれているかどうかを検査できます。

- エクスプローラー、PowerShell、Azure Information Protection スキャナーで、これらのファイルにラベルを付けることができます。 その結果、Azure Information Protection の新しい保護を適用する Azure Information Protection ラベルや、Secure Islands から既存の保護を削除する Azure Information Protection ラベルを適用することができます。

- [ラベル付け移行クライアントのカスタマイズ](#migrate-labels-from-secure-islands-and-other-labeling-solutions)を使用して、これらの保護されたファイルの Secure Islands ラベルを Azure Information Protection ラベルに自動的に変換することができます。

## <a name="migrate-labels-from-secure-islands-and-other-labeling-solutions"></a>Secure Islands からのラベルの移行と、その他のラベル付けのソリューション

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。

現在、この構成は、PDF 暗号化の ISO 標準を使用して PDF ファイルを保護する新しい既定の動作とは互換性がありません。 このシナリオでは、.ppdf ファイルをエクスプローラー、PowerShell、スキャナーで開くことはできません。 これを解決するには、クライアントの詳細設定を使用して、[PDF 暗号化の ISO 標準を使用しない](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption)ようにします。

Secure Islands によってラベル付けされた Office ドキュメントや PDF ドキュメントは、Azure Information Protection のラベルでラベル付けし直すことができます。そのためには、独自に定義したマッピングを使用します。 また、この方法を使用して、他のソリューションからのラベルを、そのラベルが Office ドキュメントにある場合は再利用することができます。 

> [!NOTE]
> PDF および Office ドキュメント以外に、Secure Islands によって保護されているファイルがある場合、[前のセクション](#support-for-files-protected-by-secure-islands)で説明したようにレジストリを編集した後に再びラベルを付けることができます。 

この構成オプションの結果として、Azure Information Protection の新しいラベルは、Azure Information Protection クライアントによって次のように適用されます。

- Office ドキュメントの場合: デスクトップ アプリでドキュメントを開くと、Azure Information Protection の新しいラベルが設定されたことが表示され、ドキュメントを保存すると適用されます。

- エクスプローラーの場合: [Azure Information Protection] ダイアログ ボックスで、Azure Information Protection の新しいラベルが設定されたことが表示され、ユーザーが **[適用]** を選択すると適用されます。 ユーザーが **[キャンセル]** を選択した場合、新しいラベルは適用されません。

- PowerShell の場合: [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) によって、Azure Information Protection の新しいラベルが適用されます。 [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) では、別の方法で設定されるまで、Azure Information Protection の新しいラベルは表示されません。

- Azure Information Protection スキャナーの場合: Azure Information Protection の新しいラベルが設定され、強制モードで適用される可能性がある場合、検出が報告されます。

この構成では、古いラベルにマッピングする Azure Information Protection のラベルごとに、**LabelbyCustomProperty** という名前のクライアントの詳細設定を指定する必要があります。 次に、各エントリに対して、次の構文を使用して値を設定します。

`[Azure Information Protection label ID],[migration rule name],[Secure Islands custom property name],[Secure Islands metadata Regex value]`

Azure Portal で Azure Information Protection ポリシーを表示または構成するとき、ラベル ID 値は **[ラベル]** ブレードに表示されます。 サブラベルを指定するには、親ラベルが同じスコープまたはグローバル ポリシー内にある必要があります。

任意の移行規則名を指定します。 以前のラベル付けソリューションから Azure Information Protection のラベルに、1 つまたは複数のラベルをマッピングする方法を特定するのに役立つ、わかりやすい名前を使用します。 名前は、スキャナー レポートおよびイベント ビューアーに表示されます。 この設定では、ドキュメントから元のラベルが削除されたり、元のラベルが適用された可能性がある視覚的マーキングが削除されたりすることはありません。 ヘッダーおよびフッターを削除するには、次のセクションの「[他のラベル付けソリューションからヘッダーとフッターを削除する](#remove-headers-and-footers-from-other-labeling-solutions)」を参照してください。

### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>例1: 同じラベル名の 1 対 1 のマッピング

要件: "社外秘" というセキュリティ保護された島ラベルを持つドキュメントは、Azure Information Protection によって "社外秘" というラベルが付けられます。

この例では:

- 使用する Azure Information Protection のラベルは **Confidential** という名前が付けられ、ラベル ID は **1ace2cc3-14bc-4142-9125-bf946a70542c** です。 

- Secure Islands のラベルは、**Confidential** という名前が付けられ、**Classification** という名前のカスタム プロパティに保存されます。

クライアントの詳細設定:

    
|名前|値|
|---------------------|---------|
|LabelbyCustomProperty|1ace2cc3-14bc-4142-9125-bf946a70542c、"Secure Islands label is Confidential" (Secure Islands のラベルは Confidential です)、Classification、Confidential|

### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>例 2: 異なるラベル名の 1 対 1 のマッピング

要件: セキュリティで保護されたアイランドによって "機微な" というラベルが付けられたドキュメントは、Azure Information Protection によって "機密性の高い" というラベルに再設定する

この例では:

- 使用する Azure Information Protection のラベルは **Highly Confidential** という名前が付けられ、ラベル ID は **3e9df74d-3168-48af-8b11-037e3021813f** です。

- Secure Islands のラベルは **Sensitive** という名前が付けられ、**Classification** という名前のカスタム プロパティに保存されます。

クライアントの詳細設定:

    
|名前|値|
|---------------------|---------|
|LabelbyCustomProperty|3e9df74d-3168-48af-8b11-037e3021813f、"Secure Islands label is Sensitive" (Secure Islands のラベルは Sensitive です)、Classification、Sensitive|


### <a name="example-3-many-to-one-mapping-of-label-names"></a>例 3: ラベル名の多対一のマッピング

要件: "Internal" という語を含む2つのセキュリティ保護された島々ラベルがあり、これらのセキュリティ保護された島々ラベルのいずれかを持つドキュメントを、Azure Information Protection によって "General" というラベルに書き換えます。

この例では:

- 使用する Azure Information Protection のラベルは **General** という名前が付けられ、ラベル ID は **2beb8fe7-8293-444c-9768-7fdc6f75014d** です。

- Secure Islands のラベルには、**Internal** という単語が含まれ、**Classification** という名前のカスタム プロパティに保存されます。

クライアントの詳細設定:

    
|名前|値|
|---------------------|---------|
|LabelbyCustomProperty|2beb8fe7-8293-444c-9768-7fdc6f75014d、"Secure Islands label contains Internal" (Secure Islands のラベルに Internal が含まれます)、Classification、\*Internal\*|


## <a name="remove-headers-and-footers-from-other-labeling-solutions"></a>他のラベル付けソリューションからヘッダーとフッターを削除する

この構成では、Azure Portal で構成する必要のある、複数の[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。 これらの設定はプレビュー段階であり、変更される可能性があります。

この設定では、その視覚的マーキングが別のラベル付けソリューションによって適用されている場合に、テキスト ベースのヘッダーまたはフッターをドキュメントから削除したり置き換えたりできるようになります。 たとえば、古いフッターに古いラベルの名前が含まれていますが、これを新しいラベル名と独自のフッターで Azure Information Protection に移行したとします。

クライアントがそのポリシーにこの構成を使用すると、Office アプリでドキュメントが開き、いずれかの Azure Information Protection ラベルがドキュメントに適用されたときに、古いヘッダーとフッターが削除または置換されます。

この構成は Outlook ではサポートされていません。そのため、この構成を Word、Excel、PowerPoint で使用すると、ユーザーのこれらのアプリのパフォーマンスに悪影響が生じる場合があります。 この構成ではアプリケーションごとの設定を定義することができます。たとえば、Word 文書のヘッダーとフッターのテキストは検索し、Excel のスプレッドシートや PowerPoint のプレゼンテーションのテキストは検索しないようにできます。

パターンマッチングはユーザーのパフォーマンスに影響するため、Office アプリケーションの種類 (**W**Ord、E**X**セル、 **P**owerpoint) は、検索する必要があるもののみに制限することをお勧めします。

- キー: **RemoveExternalContentMarkingInApp**

- 値: \<**Office アプリケーションの種類 WXP**> 

例:

- Word 文書のみを検索するには、**W** を指定します。

- Word 文書と PowerPoint プレゼンテーションを検索するには、**WP** を指定します。

この後、ヘッダーまたはフッターの内容と、その削除または置換方法を指定したりするために、少なくとも 1 つのより詳細なクライアント設定 **ExternalContentMarkingToRemove** が必要です。

### <a name="how-to-configure-externalcontentmarkingtoremove"></a>ExternalContentMarkingToRemove を構成する方法

**ExternalContentMarkingToRemove** キーに文字列値を指定するときには、正規表現を使用する 3 つのオプションがあります。

- ヘッダーまたはフッターのすべてを削除する部分一致。
    
    例: ヘッダーまたはフッターに文字列 **TEXT TO REMOVE** が含まれている場合。 これらのヘッダーまたはフッターを完全に削除したいとします。 値 `*TEXT*` を指定します。

- ヘッダーまたはフッターの特定の単語のみを削除する完全一致。
    
    例: ヘッダーまたはフッターに文字列 **TEXT TO REMOVE** が含まれている場合。 単語 **TEXT** のみを削除し、ヘッダーまたはフッター文字列は **TO REMOVE** として残したいとします。 値 `TEXT ` を指定します。

- ヘッダーまたはフッターのすべてを削除する完全一致。
    
    例: ヘッダーまたはフッターに文字列 **TEXT TO REMOVE** が含まれている場合。 正確にこの文字列が含まれているヘッダーまたはフッターを削除したいとします。 値 `^TEXT TO REMOVE$` を指定します。
    

指定した文字列のパターン マッチングでは大文字と小文字が区別されます。 文字列の最大長は 255 文字です。

一部のドキュメントには非表示の文字やさまざまな種類のスペースやタブが含まれているため、語句や文に指定した文字列が検出されない可能性があります。 値には、できるだけ単独の特徴的な単語を指定し、運用環境に展開する前に結果をテストしてください。

- キー: **ExternalContentMarkingToRemove**

- 値: \<**正規表現として定義された、マッチングする文字列**> 

#### <a name="multiline-headers-or-footers"></a>複数行のヘッダーまたはフッター

ヘッダーまたはフッターのテキストが複数行にわたる場合は、行ごとにキーと値を作成します。 たとえば、2 行にわたる次のフッターがあるとします。

**ファイルは社外秘として分類**

**ラベルは手動で適用**

この複数行のフッターを削除するには、次の 2 つのエントリを作成します。

- キー 1: **ExternalContentMarkingToRemove**

- キーの値 1: **\*社外秘***

- キー 2: **ExternalContentMarkingToRemove**

- キーの値 2: **\*ラベルの適用*** 

#### <a name="optimization-for-powerpoint"></a>PowerPoint 用の最適化

PowerPoint では、フッターが図形として実装されます。 指定したテキストのうち、ヘッダーまたはフッターでない図形が削除されるのを防ぐには、**PowerPointShapeNameToRemove** という名前の、追加のクライアントの詳細設定を使用します。 また、すべての図形のテキストのチェックはリソースを消費するプロセスであるため、この設定を使用して回避することをお勧めします。

この追加のクライアントの詳細設定を指定せず、PowerPoint が **RemoveExternalContentMarkingInApp** キーの値に含まれている場合、**ExternalContentMarkingToRemove** で指定したテキストがすべての図形でチェックされます。 

ヘッダーまたはフッターとして使用している図形の名前を検索するには:

1. PowerPoint の**選択**ウィンドウを表示し、 **[書式]** タブ > **[配置]** グループ > **[選択ウィンドウ]** の順に選択します。

2. ヘッダーまたはフッターを含むスライド上の図形を選択します。 選択した図形の名前が、**選択**ウィンドウで強調表示されます。

図形の名前を使用して、**PowerPointShapeNameToRemove** キーの文字列値を指定します。 

例: 図形の名前は **fc** です。 この名前の図形を削除するには、値 `fc` を指定します。

- キー: **PowerPointShapeNameToRemove**

- 値: \<**PowerPoint の図形の名前**> 

削除する PowerPoint の図形が複数ある場合は、削除する図形と同じ数だけ **PowerPointShapeNameToRemove** キーを作成します。 各エントリに、削除する図形の名前を指定します。

既定では、マスター スライドのヘッダーとフッターのみがチェックされます。 この検索の対象をすべてのスライドに広げるには、**RemoveExternalContentMarkingInAllSlides** という名前の、追加のクライアントの詳細設定を使用します。ただし、このプロセスはリソースをより多く消費します。

- キー: **RemoveExternalContentMarkingInAllSlides**

- 値: **True**

## <a name="label-an-office-document-by-using-an-existing-custom-property"></a>既存のカスタム プロパティを使用して Office ドキュメントにラベルを付ける

> [!NOTE]
> この構成と、[Secure Islands およびその他のラベル付けソリューションからラベルを移行する](#migrate-labels-from-secure-islands-and-other-labeling-solutions)ための構成を使用する場合は、ラベル付けの移行の設定が優先されます。 

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

たとえば、 **[公開]** 、 **[全般]** 、 **[非常に機密性の高い社外秘]** の値が考えられる、 **[分類]** という名前の SharePoint 列があるとします。 ドキュメントは SharePoint に格納され、[分類] プロパティの一連の値として **[公開]** 、 **[全般]** 、 **[非常に機密性の高い社外秘]** を持ちます。

Office ドキュメントにこれらの分類の値のいずれかのラベルを付けるには、 **[SyncPropertyName]** を **[公開]** に、 **[SyncPropertyState]** を **[OneWay]** に設定します。 

ここで、ユーザーがこれらの Office ドキュメントのいずれかを開いて保存するときに、Azure Information Protection ポリシーに **[公開]** 、 **[全般]** 、または **[非常に機密性の高い社外秘]** の名前のラベルがあると、このいずれかにラベル付けされます。 これらの名前のラベルがない場合、ドキュメントはラベル付けされないままです。

## <a name="disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics"></a>ドキュメント内の検出された機密情報の Azure Information Protection analytics への送信を無効にする

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。

Office アプリで Azure Information Protection クライアントが使用されている場合は、ドキュメントが最初に保存されたときに、機密情報が検索されます。 クライアントが監査情報を送信しないように構成されていない場合、検出された機密情報の種類 (定義済みまたはカスタム) は[Azure Information Protection analytics](../reports-aip.md)に送信されます。 

クライアントが監査情報を送信するかどうかを制御する構成は、 **[監査データを Azure Information Protection log analytics に送信する]** の[ポリシー設定](../configure-policy-settings.md)です。 このポリシー設定が**オン**の場合は、ラベル付け操作を含む監査情報を送信するが、クライアントが検出した機密情報の種類を送信しないようにするには、次の文字列を入力します。

- キー: **Runauditinformationタイプ検出**

- 値: **False**

この高度なクライアント設定を設定した場合でも、クライアントから監査情報を送信できますが、情報はラベル付けアクティビティに限定されます。

たとえば、次のようになります。

- この設定を使用すると、**社外秘 \ Sales**というラベルが付けられたユーザーによってアクセスされたことを確認できます。

- この設定を行わないと、".docx" に6個のクレジットカード番号が含まれていることがわかります。
    
    - また、機密性の[高いデータに](../reports-aip.md#content-matches-for-deeper-analysis)対してより深い分析を有効にすると、そのクレジットカード番号を確認することができます。

## <a name="disable-sending-information-type-matches-for-a-subset-of-users"></a>ユーザーのサブセットに対して送信情報の種類の一致を無効にする

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。

[Azure Information Protection analytics](../reports-aip.md)のチェックボックスをオンにすると、機微なデータに対してより深い分析が可能になり、機密情報の種類またはカスタム条件に一致する内容が収集されます。既定では、この情報は次のようになります。Azure Information Protection スキャナーを実行するサービスアカウントを含むすべてのユーザーによって送信されます。 このデータを送信できないユーザーがいる場合は、それらのユーザーの[スコープ付きポリシー](../configure-policy-scope.md)で、次のようなクライアントの詳細設定を作成します。 

- キー: **Logmatchedcontent**

- 値: **Disable**


## <a name="limit-the-number-of-threads-used-by-the-scanner"></a>スキャナーで使用されるスレッドの数を制限する

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。

既定では、スキャナー サービスを実行しているコンピューター上の利用可能なプロセッサ リソースのすべてがスキャナーによって使われます。 このサービスのスキャン中に CPU 使用量を制限する必要がある場合は、次の詳細設定を作成します。 

値には、スキャナーが並列で実行できる同時スレッドの数を指定します。 スキャナーでは、それがスキャンするファイルごとに個別のスレッドが使われます。このため、この調整構成によって並列でスキャンできるファイルの数も定義されます。 

最初にテスト用の値を構成するときは、コアごとに 2 を指定してから、その結果を監視することをお勧めします。 たとえば、4 コアのコンピューター上でスキャナーを実行する場合、最初は値を 8 に設定します。 必要な場合は、スキャナー コンピューターとスキャン速度に対してご自身が要求する結果のパフォーマンスに応じて、その数を増減させます。 

- キー: **ScannerConcurrencyLevel**

- 値: **\<同時スレッドの数>**

## <a name="disable-the-low-integrity-level-for-the-scanner"></a>スキャナーの低整合性レベルを無効にする

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。

既定では、Azure Information Protection スキャナーは低整合性レベルで実行されます。 この設定では、より高度なセキュリティ分離が提供されますが、パフォーマンスが低下します。 低整合性レベルは、特権を持ったアカウント (ローカル管理者アカウントなど) でスキャナーを実行する場合に適しています。この設定は、スキャナーを実行しているコンピューターを保護するのに役立ちます。

ただし、スキャナーを実行するサービス アカウントに、[スキャナーの前提条件](../deploy-aip-scanner.md#prerequisites-for-the-azure-information-protection-scanner)のセクションで説明されている権限だけが付与されている場合、低整合性レベルは必要ありません。これはパフォーマンスに悪影響を及ぼすため、推奨されません。 

Windows 整合性レベルについて詳しくは、「[What is the Windows Integrity Mechanism?](https://msdn.microsoft.com/library/bb625957.aspx)」(Windows 整合性メカニズムとは何ですか) をご覧ください。

この高度な設定を構成し、Windows によって自動的に割り当てられた整合性レベルでスキャナーが実行される (標準ユーザー アカウントが中程度の整合性レベルで実行される) ようにするには、次の文字列を入力します。

- キー: **ProcessUsingLowIntegrity**

- 値: **False**

## <a name="change-the-timeout-settings-for-the-scanner"></a>スキャナーのタイムアウト設定を変更する

この構成では、Azure portal で構成する必要のある[アドバンストクライアント設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。

既定では、Azure Information Protection スキャナーのタイムアウト期間は 00:15:00 (15 分) に設定されており、機密情報の種類やカスタム条件用に構成した regex 式の各ファイルを検査します。 このコンテンツ抽出プロセスのタイムアウト期間に達すると、タイムアウト前のすべての結果が返され、ファイルに対するさらなる検査が停止します。 このシナリオでは、%*localappdata*% \ Microsoft\MSIP\Logs\MSIPScanner.iplog (複数のログがある場合は zip) に次のエラーメッセージが記録されます: **getcontentparts が失敗**しました。詳細については、**操作が取り消されまし**た。

大きなファイルが原因でこのタイムアウトの問題が発生した場合は、コンテンツを完全に抽出するために、このタイムアウト期間を長くすることができます。

- キー: **Contentextractiontimeout**

- 値: **\< hh: min: sec >**

ファイルの種類は、ファイルのスキャンにかかる時間に影響を与える可能性があります。 スキャン時間の例:

- 一般的な 100 MB の Word ファイル: 0.5 ~ 5 分

- 一般的な 100 MB PDF ファイル: 5-20 分

- 一般的な 100 MB の Excel ファイル: 12-30 分

ビデオファイルなど、非常に大きいファイルの種類によっては、スキャナープロファイルの [**スキャンする**ファイルの種類] オプションにファイル名拡張子を追加して、スキャンから除外することを検討してください。

さらに、Azure Information Protection スキャナーでは、処理するファイルごとに 00:30:00 (30 分) のタイムアウト期間があります。 この値は、リポジトリからファイルを取得するためにかかる時間を考慮し、暗号化解除、検査、ラベル付け、および暗号化のためのコンテンツの抽出を含む操作のために、一時的にファイルをローカルに保存します。

Azure Information Protection スキャナーは、1分間に数十から数百のファイルをスキャンできますが、非常に大きなファイルを持つデータリポジトリがある場合、スキャナーはこの既定のタイムアウト期間を超えることがあり、Azure portal は30後に停止するように見えます。~. このシナリオでは、次のエラーメッセージが%*localappdata*% \ Microsoft\MSIP\Logs\MSIPScanner.iplog (複数のログがある場合は zip) と、スキャナーの .csv ログファイル (**操作が取り消されました**) に記録されます。

既定では、4コアプロセッサを搭載したスキャナーには、スキャン用に16個のスレッドがあり、30分間に16の大きなファイルを検出する確率は、大きなファイルの比率によって異なります。 たとえば、スキャンレートが1分あたり200ファイルで、ファイルの1% が30分のタイムアウトを超えると、85% を超える可能性があります。これは、スキャナーで30分間のタイムアウト状況が発生する可能性があります。 これらのタイムアウトによって、スキャン時間が長くなり、メモリ使用量が増加する可能性があります。

このような状況では、スキャナーコンピューターにコアプロセッサを追加できない場合は、スキャン速度の向上とメモリ消費量の削減のためにタイムアウト期間を短縮することを検討してください。ただし、一部のファイルは除外されます。 または、より正確なスキャン結果を得るために、タイムアウト期間を長くすることを検討してください。ただし、この構成では、スキャン速度が低下し、メモリ消費量が高くなる可能性があります。

ファイル処理のタイムアウト期間を変更するには、次の高度なクライアント設定を構成します。

- キー: **Fileprocessingtimeout**

- 値: **\< hh: min: sec >**

## <a name="change-the-local-logging-level"></a>ローカルのログ記録レベルを変更する

この構成では、Azure Portal で構成する必要のある[クライアントの詳細設定](#how-to-configure-advanced-client-configuration-settings-in-the-portal)を使用します。

既定では、Azure Information Protection クライアントでは **%localappdata%\Microsoft\MSIP** フォルダーにクライアント ログ ファイルが書き込まれます。 これらのファイルは、Microsoft サポートによるトラブルシューティングを目的としています。
 
これらのファイルに対するログ記録レベルを変更するには、次のクライアントの詳細設定を構成します。

- キー: **LogLevel**

- 値: **\<ログ記録レベル>**

ログ記録レベルに次の値のいずれかを設定します。

- **オフ**: ローカルログはありません。

- **エラー**: エラーのみ。

- **Info**: 最小ログ記録。イベント id が含まれません (スキャナーの既定の設定)。

- **デバッグ**: 完全な情報。

- **トレース**: 詳細なログ記録 (クライアントの既定の設定)。 スキャナーの場合、この設定はパフォーマンスに大きな影響を与えるため、スキャナーに対しては Microsoft サポートから要求された場合にのみ有効にする必要があります。 このレベルのログ記録をスキャナー用に設定するよう指示された場合は、関連ログの収集が完了したときに別の値に設定することを忘れないでください。

このクライアントの詳細設定によって、[中央レポート機能](../reports-aip.md)のために Azure Information Protection に送信される情報が変更されたり、ローカルの[イベント ログ](client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client)に書き込まれる情報が変更されたりすることはありません。

## <a name="integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution"></a>Exchange メッセージ分類との統合によるモバイル デバイスのラベル付けソリューション

Web 上の outlook では、Exchange Online のラベル付けがサポートされるようになりました。これは、Outlook で電子メールにラベルを付ける方法として推奨されています。 ただし、Office 365 セキュリティ/コンプライアンスセンター、Microsoft 365 Security center、または Microsoft コンプライアンスセンターから公開されている機密ラベルをまだ使用していない場合は、Exchange メッセージ分類を使用して Azure の情報を拡張できます。モバイルユーザーが web 上で Outlook を使用する場合の保護ラベル。 この方法は、Exchange Server にも使用できます。 

Outlook Mobile では、Exchange のメッセージ分類がサポートされません。

このソリューションを実現するには: 

1. [New-MessageClassification](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/New-MessageClassification?view=exchange-ps) Exchange PowerShell コマンドレットを使用して、Azure Information Protection ポリシーのラベル名にマップする名前プロパティでメッセージの分類を作成します。 

2. ラベルごとに Exchange メール フロー ルールを作成します。メッセージのプロパティに構成した分類が含まれる場合はルールを適用し、メッセージ プロパティを変更してメッセージ ヘッダーを設定します。 

     メッセージ ヘッダーについては、Azure Information Protection ラベルを使って送信および分類した電子メールのインターネット ヘッダーを調べることによって、指定する情報を見つけることができます。 ヘッダー **msip_labels** と、そのすぐあとに続く文字列 (セミコロンまでが対象) を探します。 たとえば、次のようになります。
    
    **msip_labels: MSIP_Label_0e421e6d-ea17-4fdb-8f01-93a3e71333b8_Enabled=True;**
    
    ルール内のメッセージ ヘッダーの場合は、ヘッダーとして **msip_labels** を指定し、ヘッダー値としてこの文字列の残りの部分を指定します。 たとえば、次のようになります。
    
    ![例: 特定の Azure Information Protection ラベルのメッセージ ヘッダーを設定する Exchange Online メール フロー ルール](../media/exchange-rule-for-message-header.png)
    
    注: ラベルがサブラベルである場合は、ヘッダー値のサブラベルの前に、同じ形式を使って親ラベルも指定する必要があります。 たとえば、サブラベルの GUID が 27efdf94-80a0-4d02-b88c-b615c12d69a9 である場合、値は `MSIP_Label_ab70158b-bdcc-42a3-8493-2a80736e9cbd_Enabled=True;MSIP_Label_27efdf94-80a0-4d02-b88c-b615c12d69a9_Enabled=True;` のようになります。

この構成のテストを行う前に、メール フロー ルールを作成または編集すると遅延 (たとえば、1 時間の遅延) がよく発生することを念頭においてください。 このルールを有効にすると、ユーザーが Outlook on the web を使用したときに次のイベントが発生するようになります。 

- ユーザーが Exchange のメッセージ分類を選択して電子メールを送信します。

- Exchange ルールにより Exchange の分類が検出され、ルールに従ってメッセージ ヘッダーが変更されて、Azure Information Protection の分類が追加されます。

- Azure Information Protection クライアントをインストール済みである内部受信者が Outlook で電子メールを表示すると、Azure Information Protection の割り当てられたラベルが表示されます。 

Azure Information Protection ラベルに保護が適用されている場合は、この保護をルールの構成に追加します。メッセージセキュリティを変更するオプションを選択し、権利保護を適用して、[保護] テンプレートまたは [転送不可] オプションを選択します。

また、メール フロー ルールを構成して、リバース マッピングを行うこともできます。 Azure Information Protection ラベルが検出された場合は、対応する Exchange メッセージの分類を設定します。

- Azure Information Protection のラベルごとに、**msip_labels** ヘッダーにラベル名 (**General** など) が含まれている場合に適用されるメール フロー ルールを作成し、このラベルにマッピングするメッセージ分類を適用します。


## <a name="next-steps"></a>次のステップ
これで Azure Information Protection クライアントのカスタマイズができました。次に、このクライアントのサポートに必要な追加情報を記載した以下の記事をご覧ください。

- [クライアント ファイルおよび使用状況ログの記録](client-admin-guide-files-and-logging.md)

- [ドキュメント追跡](client-admin-guide-document-tracking.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)


