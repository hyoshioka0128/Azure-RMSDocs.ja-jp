---
title: Azure Information Protection 統合されたラベル付けクライアント-バージョン履歴 & サポートポリシー
description: Windows 用 Azure Information Protection 統合ラベル付けクライアントのリリース情報を参照してください。
author: cabailey
ms.author: cabailey
manager: rkarlin
ms.date: 11/02/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 0ee20b6063dffd18b5067663de05c2d7a25cabd4
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73446026"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure Information Protection 統合されたラベル付けクライアント-バージョンのリリース履歴とサポートポリシー

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、WINDOWS 7 SP1、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012、windows Server 2008 r2*
>
> *手順: [Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


Azure Information Protection 統合されたラベル付けクライアントは、 [Microsoft ダウンロードセンター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)からダウンロードできます。

通常、数週間の遅延が発生すると、最新の一般公開バージョンが Microsoft Update カタログにも含まれます。これには、 **Microsoft Azure Information Protection** > の製品名と Microsoft Azure Information Protection の統合された**ラベル付けクライアント**、および**更新**の分類が含まれます。 このようにカタログに含まれることで、WSUS や Configuration Manager、または Microsoft Update を使うその他のソフトウェア展開メカニズムを使って、クライアントをアップグレードできるようになります。

詳細については、「 [Azure Information Protection の統合ラベル付けクライアントのアップグレードと保守](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client)」を参照してください。

### <a name="servicing-information-and-timelines"></a>サービスの情報とタイムライン

Azure Information Protection 統合ラベルクライアントの各一般公開 (GA) バージョンは、以降の GA バージョンのリリースから最大6か月間サポートされます。 ドキュメントには、サポートされていないバージョンのクライアントに関する情報は含まれません。 修正プログラムや新しい機能は常に最新の GA バージョンに適用され、古い GA バージョンには適用されません。

実稼働ネットワークのエンド ユーザー向けにプレビュー バージョンをデプロイしないでください。 最新のプレビュー バージョンは、次の GA バージョンに含まれる新しい機能や修正内容の確認と試用にお使いください。 最新でないプレビュー バージョンはサポートされません。

##### <a name="general-availability-versions-that-are-no-longer-supported"></a>サポートされなくなった一般提供のバージョン:

|クライアントのバージョン|リリース日|
|--------------|-------------|
|2.0.778.0|04/16/2019|

このページで使用される日付形式は、*月/日/年*です。


### <a name="release-information"></a>リリース情報

次の情報を使用して、Windows 用の Azure Information Protection 統合ラベルクライアントのサポートされているリリースの新機能と変更点を確認してください。 最新のリリースは一番上に表示されます。 このページで使用される日付形式は、*月/日/年*です。

> [!NOTE]
> マイナー修正は記載されていないので、統一されたラベル付けクライアントで問題が発生した場合は、最新の GA リリースで修正されているかどうかを確認することをお勧めします。 問題が引き続き発生する場合は、現在のプレビューバージョン (使用可能な場合) を確認します。
>  
> テクニカル サポートについては、「[サポート オプションとコミュニティ リソース](../information-support.md#support-options-and-community-resources)」の情報を参照してください。 [Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。

このクライアントは Azure Information Protection クライアント (クラシック) に置き換わるものです。 従来のクライアントとの機能を比較するには、「 [Windows コンピューターのラベル付けクライアント](use-client.md##compare-the-labeling-clients-for-windows-computers)」を参照してください。

## <a name="version-25330"></a>バージョン2.5.33.0

**リリース**日: 10/23/2019

**新機能:**

- [スキャナー](../deploy-aip-scanner.md)のプレビューバージョン。オンプレミスのデータストアを検査してラベル付けします。 このバージョンのスキャナーでは、次のことを行います。
    
    - 同じスキャナープロファイルを使用するようにスキャナーを構成するときに、複数のスキャナーが同じ SQL Server データベースを共有できます。 この構成により、複数のスキャナーの管理が容易になり、スキャン時間が短縮されます。 この構成を使用する場合は、スキャナーのインストールが完了するのを待ってから、同じプロファイルを使用して別のスキャナーをインストールします。
    
    - スキャナーをインストールするときにプロファイルを指定する必要があります。スキャナーデータベースは**AIPScannerUL_\<profile_name >** という名前が付けられます。 *プロファイル*パラメーターは、Set-AIPScanner にも必須です。
    
    - ドキュメントにラベルが既に付いている場合でも、すべてのドキュメントに既定のラベルを設定できます。 スキャナープロファイルまたはリポジトリの設定で、[ラベルの再設定 **] オプションを** **[オン**] に設定し、新しい [既定の**ラベルを強制**する] チェックボックスをオンにします。
    
    - すべてのドキュメントから既存のラベルを削除できます。ラベルによって以前に適用されていた場合、この操作には保護の削除が含まれます。 ラベルとは独立して適用された保護が保持されます。 このスキャナーの構成は、スキャナープロファイルまたはリポジトリの設定で次の設定を使用して実現されます。
        - **コンテンツに基づいてファイルにラベルを付ける**:**オフ**
        - **既定のラベル**:**なし**
        - **ファイル**のラベルの再設定: **[** **既定のラベルを強制**する] チェックボックスがオンになっている
    
    - 従来のクライアントのスキャナーと同様、既定では、スキャナーは Office ファイルと PDF ファイルを保護します。 [PowerShell の詳細設定](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect)を使用すると、他の種類のファイルを保護できます。
    
    - スキャナーサイクルの開始と終了に関するイベント Id は、Windows イベントログには書き込まれません。 代わりに、この情報に Azure portal を使用します。
    
    - 既知の問題: 新しいラベルと名前が変更されたラベルは、スキャナープロファイルまたはリポジトリの設定の既定のラベルとして選択できません。 回避策:
        - 新しいラベルの場合: Azure portal で、グローバルポリシーまたはスコープポリシーに使用する[ラベルを追加](../configure-policy-add-remove-label.md)します。
        - 名前を変更したラベルの場合: Azure portal を閉じてから再度開きます。
    
    Azure Information Protection クライアント (クラシック) からスキャナーをアップグレードすることができます。 アップグレード後に新しいデータベースが作成されると、スキャナーは初回実行時にすべてのファイルを再スキャンします。 手順については、管理者ガイドの「 [Azure Information Protection スキャナーをアップグレードする](clientv2-admin-guide.md#upgrading-the-azure-information-protection-scanner)」を参照してください。
    
    詳細については、ブログ投稿のお知らせを参照してください。統合された[ラベル付け AIP スキャナーのプレビューにより、スケールアウトなど](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Unified-labeling-AIP-scanner-preview-brings-scaling-out-and-more/ba-p/862552)ができます。

- PowerShell コマンドレットの[セット-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)は、ファイルに非対話形式でラベルを付ける場合の新しいパラメーター (*AppId*、 *appsecret*、 *TenantId*、 *DelegatedUser*、 *OnBehalfOf*) を備えています。また、新しい手順では、アプリを Azure AD に登録します。 シナリオ例としては、スキャナーや、ドキュメントにラベルを付けるための自動 PowerShell スクリプトがあります。 手順については、管理者ガイドの「[非対話形式でファイルにラベルを付ける方法](clientv2-admin-guide-powershell.md#how-to-label-files-non-interactively-for-azure-information-protection)」を参照してください。
    
    *DelegatedUser*は、統合されたラベル付けクライアントの最後のプレビューバージョン以降の新しいパラメーターであり、登録済みアプリの API アクセス許可が変更されたことに注意してください。

- [保護するファイルの種類を変更](clientv2-admin-guide-customizations.md#change-which-file-types-to-protect)するための新しい PowerShell ラベルポリシーの詳細設定。

- 新しい PowerShell ラベルポリシーの詳細設定を[使用して、ラベルの移行ルールを SharePoint プロパティに拡張](clientv2-admin-guide-customizations.md#extend-your-label-migration-rules-to-sharepoint-properties)します。

- 一致したカスタム機密情報の種類が[Azure Information Protection analytics](../reports-aip.md)に送信されます。

- 適用されたラベルには、[色が構成され](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)ている場合、ラベルに構成されている色が表示されます。

- ラベルに保護設定を追加または変更すると、クライアントは、ドキュメントが次に保存されるときに、これらの最新の保護設定でラベルを再適用します。 同様に、スキャナーは、強制モードでドキュメントが次回スキャンされるときに、これらの最新の保護設定でラベルを再適用します。

- 1つのクライアントからファイルをエクスポートし、切断されたコンピューターに手動でコピーすることによって、切断された[コンピューターをサポート](clientv2-admin-guide-customizations.md#support-for-disconnected-computers)します。 この構成は、ファイルエクスプローラー、PowerShell、およびスキャナーを使用したラベル付けでサポートされていることに注意してください。 この構成は、Office アプリのラベル付けではサポートされていません。

- %Localappdata%\Microsoft\MSIP\Logs からすべてのログファイルを収集し、.zip 形式の1つの圧縮されたファイルに保存する新しいコマンドレットである[Export](https://docs.microsoft.com/powershell/module/azureinformationprotection/export-aiplogs)。 このファイルは、報告された問題の調査に役立つログファイルを送信するように要求された場合に Microsoft サポートに送信できます。

**修正:**

- ファイルエクスプローラーを使用して保護されたファイルを正常に変更できます。ファイルのパスワードが削除されたら、右クリックします。

- ネイティブ保護されたファイルをビューアーで正常に開くには、[名前を付けて保存]、[エクスポート (エクスポート) [] の使用権限](../configure-usage-rights.md#usage-rights-and-descriptions)を必要としません。

- ラベルとポリシー設定は[、クリア-AIPAuthentication](/powershell/module/azureinformationprotection/clear-aipauthentication?)を実行しなくても期待どおりに更新されます。または、%LocalAppData%\Microsoft\MSIP\mip フォルダーを手動で削除します。

**その他の変更**

- [設定をリセット](clientv2-admin-guide.md#more-information-about-the-reset-settings-option)すると、%LocalAppData%\Microsoft\MSIP\mip\\ *\<ProcessName\>* \ mip フォルダーではなく、%LocalAppData%\Microsoft\MSIP\mip\\ *\<ProcessName\>* フォルダーが削除されるようになりました。

- [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)に、保護されたドキュメントのコンテンツ ID が含まれるようになりました。

## <a name="version-22210"></a>バージョン2.2.21.0

**リリース**日: 09/03/2020

04/23/2020 でサポート

**修正:**

- 詳細設定の[Outlookdefaultlabel](clientv2-admin-guide-customizations.md#set-a-different-default-label-for-outlook)を使用して Outlook に別の既定のラベルを設定し、指定したラベルにラベルポリシーのサブラベルがない場合は、ラベルが正しく適用されます。

- Azure Information Protection クライアントが Office アプリで使用されている場合、シングルサインオン用に構成されていない Active Directory アカウントを持つユーザーには、Azure Information Protection の認証を求めるメッセージが表示されます。 正常に認証されると、クライアントのステータスが [オンライン] に正しく変更され、ラベル付け機能が有効になります。

## <a name="version-22190"></a>バージョン2.2.19.0

**リリース**日: 08/06/2019

03/03/2020 でサポート

**修正:**

- クライアントは、ポリシーを正常にダウンロードし、現在の機密ラベルを表示できます。 以前のバージョンからアップグレードした後で、ラベル付けセンターでカスタム情報の種類を構成していない場合は、この修正が必要です。

- 一般的なパフォーマンスと安定性の向上。

## <a name="version-22140"></a>バージョン2.2.14.0

**リリース**日: 07/15/2019

02/06/2020 でサポート

**新機能:**

- セキュリティ/コンプライアンスセンター用に PowerShell を使用して構成する[詳細設定](clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)のサポート。
    
    これらの詳細設定では、次のカスタマイズがサポートされています。
     - [Office アプリの Information Protection バーを表示します](clientv2-admin-guide-customizations.md#display-the-information-protection-bar-in-office-apps)
    - [必須ラベルから Outlook メッセージを除外する](clientv2-admin-guide-customizations.md#exempt-outlook-messages-from-mandatory-labeling)
    - [Outlook で推奨分類を有効にする](clientv2-admin-guide-customizations.md#enable-recommended-classification-in-outlook)
    - [Outlook に別の既定ラベルを設定する](clientv2-admin-guide-customizations.md#set-a-different-default-label-for-outlook)
    - [必須のラベル付けを使用するときにドキュメントの "後で" を削除する](clientv2-admin-guide-customizations.md#remove-not-now-for-documents-when-you-use-mandatory-labeling)
    - [他のラベル付けソリューションからヘッダーとフッターを削除する](clientv2-admin-guide-customizations.md#remove-headers-and-footers-from-other-labeling-solutions)
    - [エクスプローラーでカスタムアクセス許可を無効にする](clientv2-admin-guide-customizations.md#disable-custom-permissions-in-file-explorer)
    - [カスタム アクセス許可で保護されているファイルについて、ファイル エクスプローラーでカスタム アクセス許可を常にユーザーに表示する](clientv2-admin-guide-customizations.md#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer)
    - [添付ファイルのある電子メール メッセージの場合、その添付ファイルの最上位の分類と一致するラベルを適用します](clientv2-admin-guide-customizations.md#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)
    - [ユーザーの "問題の報告" を追加する](clientv2-admin-guide-customizations.md#add-report-an-issue-for-users)
    - [Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](clientv2-admin-guide-customizations.md#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)
    - [ドキュメント内の検出された機密情報の Azure Information Protection analytics への送信を無効にする](clientv2-admin-guide-customizations.md#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)
    - [情報の種類の一致を Azure Information Protection analytics に送信する](clientv2-admin-guide-customizations.md#send-information-type-matches-to-azure-information-protection-analytics)
    - [Secure Islands からのラベルの移行と、その他のラベル付けのソリューション](clientv2-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)
    - [ラベルが適用されたときにカスタムプロパティを適用する](clientv2-admin-guide-customizations.md#apply-a-custom-property-when-a-label-is-applied)
    - [ラベルを構成して Outlook で S/MIME 保護を適用する](clientv2-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)
    - [親ラベルに既定のサブラベルを指定する](clientv2-admin-guide-customizations.md#specify-a-default-sublabel-for-a-parent-label)
    - [ラベルの色を指定します](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)

- Word、Excel、PowerPoint、およびエクスプローラーのユーザー定義アクセス許可用に構成されたラベルのサポート。 詳細については、Office ドキュメントの「[ユーザーにアクセス許可の割り当てを許可](/microsoft-365/compliance/encryption-sensitivity-labels#let-users-assign-permissions)する」セクションを参照してください。

- AzureInformationProtection モジュールでの PowerShell の変更点は次のとおりです。
    - 新しいコマンドレット: [new-AIPCustomPermissions](/powershell/module/azureinformationprotection/New-AIPCustomPermissions) -RMSProtectionLicense を置き換えて、カスタムアクセス許可のアドホックポリシーを作成します。
    - 新しいパラメーター:
        -  *Custompermissions*と*Removeprotection* - [set-aipfilelabel](/powershell/module/azureinformationprotection/Set-AIPFileLabel)に追加されました
        -  *OnBeHalfOf* -非対話型セッションの*トークン*パラメーターの代わりに使用される、 [Set-aipauthentication](/powershell/module/azureinformationprotection/set-aipauthentication)に追加されました。
        -  *WhatIf*および*Discoveryinfotypes* - [set-aipfileclassification](/powershell/module/azureinformationprotection/set-aipfileclassification)に追加され、このコマンドレットがラベルを適用せずに検出モードで実行できるようになりました。
    - 保護サービスに直接接続されている非推奨のコマンドレット: RMSAuthentication、も get-rmsfilestatus、RMSServer、Set-rmsserverauthentication、get-rmstemplate、protect-rmsfile、set-rmsserverauthentication、protect-rmsfile、保護解除-


**修正:**

- *Discoveryinfotypes*パラメーターを使用して、Analytics と[set-aipfileclassification](https://docs.microsoft.com/powershell/module/azureinformationprotection/set-aipfileclassification?view=azureipps)の[コンテンツの一致](../reports-aip.md#content-matches-for-deeper-analysis)をサポートします。

- Windows で別のロケールに変更した後も、保護付きのラベルを PDF ドキュメントに適用できます。

- コンテンツからラベルを削除すると、ラベル構成の一部として適用された場合にのみ、保護も削除されます。 ラベルとは別に保護が適用されている場合、その保護は維持されます。 たとえば、ユーザーがファイルにカスタムアクセス許可を適用したとします。

- 自動ラベル付けが構成されている場合、ドキュメントを初めて保存するときにラベルが適用されます。

- 既定のラベル付けは、サブラベルをサポートします。

## <a name="version-207790"></a>バージョン2.0.779.0

**リリース**日: 05/01/2019

02/15/2020 でサポート

このリリースでは、Office アプリやエクスプローラーにラベルが表示されない場合がある競合状態の問題を解決するための修正プログラムが1つあります。

## <a name="next-steps"></a>次のステップ

インストールするクライアントが適切かどうかは確認できません。  「 [Windows コンピューターに使用するラベル付けクライアントを選択](use-client.md#choose-which-labeling-client-to-use-for-windows-computers)する」を参照してください。

このクライアントをインストールして使用する方法の詳細については、次を参照してください。 

- ユーザー向け: [クライアントをダウンロードしてインストールする](install-unifiedlabelingclient-app.md)

- 管理者向け: Azure Information Protection 統一された[ラベル付けクライアント管理者ガイド](clientv2-admin-guide.md)

