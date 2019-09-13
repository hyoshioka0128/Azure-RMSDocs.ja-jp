---
title: Azure Information Protection 統合されたラベル付けクライアント-バージョン履歴 & サポートポリシー
description: Windows 用 Azure Information Protection 統合ラベル付けクライアントのリリース情報を参照してください。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/09/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.reviewer: elkamins
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: a2093d33f53eb9991c0ef3f8c9d1ea798b3dd8ef
ms.sourcegitcommit: dc8a55e7a5500ede22cef2fabdaddc4bcee9fa24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2019
ms.locfileid: "70936953"
---
# <a name="azure-information-protection-unified-labeling-client---version-release-history-and-support-policy"></a>Azure Information Protection 統合されたラベル付けクライアント-バージョンのリリース履歴とサポートポリシー

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012, Windows Server 2008 R2*
>
> *手順:[Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


Azure Information Protection 統合されたラベル付けクライアントは、 [Microsoft ダウンロードセンター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)からダウンロードできます。

通常は数週間後に、一般公開されている最新バージョンが、 **Microsoft Azure Information Protection** > Microsoft Azure 情報の製品名と共に Microsoft Update カタログにも含まれるようになります。**保護の統合されたラベル付けクライアント**、および**更新**の分類。 このようにカタログに含まれることで、WSUS や Configuration Manager、または Microsoft Update を使うその他のソフトウェア展開メカニズムを使って、クライアントをアップグレードできるようになります。

詳細については、「 [Azure Information Protection の統合ラベル付けクライアントのアップグレードと保守](clientv2-admin-guide.md#upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client)」を参照してください。

### <a name="servicing-information-and-timelines"></a>サービスの情報とタイムライン

Azure Information Protection 統合ラベルクライアントの各一般公開 (GA) バージョンは、以降の GA バージョンのリリースから最大6か月間サポートされます。 ドキュメントには、サポートされていないバージョンのクライアントに関する情報は含まれません。 修正プログラムや新しい機能は常に最新の GA バージョンに適用され、古い GA バージョンには適用されません。

実稼働ネットワークのエンド ユーザー向けにプレビュー バージョンをデプロイしないでください。 最新のプレビュー バージョンは、次の GA バージョンに含まれる新しい機能や修正内容の確認と試用にお使いください。 最新でないプレビュー バージョンはサポートされません。

> [!NOTE]
> テクニカル サポートについては、「[サポート オプションとコミュニティ リソース](../information-support.md#support-options-and-community-resources)」の情報を参照してください。 [Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。

### <a name="release-information"></a>リリース情報

次の情報を使用して、Windows 用の Azure Information Protection 統合ラベルクライアントのサポートされているリリースの新機能と変更点を確認してください。 最新のリリースは一番上に表示されます。 このページで使用される日付形式は、*月/日/年*です。

> [!NOTE]
> マイナー修正は記載されていないので、統一されたラベル付けクライアントで問題が発生した場合は、最新の GA リリースで修正されているかどうかを確認することをお勧めします。 問題が引き続き発生する場合は、現在のプレビューバージョン (使用可能な場合) を確認します。
>  
> テクニカル サポートについては、「[サポート オプションとコミュニティ リソース](../information-support.md#support-options-and-community-resources)」の情報を参照してください。 [Yammer サイト](https://www.yammer.com/askipteam/)で Azure Information Protection チームと情報交換することもできます。

このクライアントは Azure Information Protection クライアント (クラシック) に置き換わるものです。 従来のクライアントとの機能を比較するには、「[クライアントを比較](use-client.md#compare-the-clients)する」を参照してください。

## <a name="version-22210"></a>バージョン2.2.21.0

**リリース日**: 09/03/2019

**関する**

- 詳細設定の[Outlookdefaultlabel](clientv2-admin-guide-customizations.md#set-a-different-default-label-for-outlook)を使用して Outlook に別の既定のラベルを設定し、指定したラベルにラベルポリシーのサブラベルがない場合は、ラベルが正しく適用されます。

- Azure Information Protection クライアントが Office アプリで使用されている場合、シングルサインオン用に構成されていない Active Directory アカウントを持つユーザーには、Azure Information Protection の認証を求めるメッセージが表示されます。 正常に認証されると、クライアントのステータスが [オンライン] に正しく変更され、ラベル付け機能が有効になります。

## <a name="version-22190"></a>バージョン2.2.19.0

**リリース日**: 08/06/2019

03/03/2020 でサポート

**関する**

- クライアントは、ポリシーを正常にダウンロードし、現在の機密ラベルを表示できます。 以前のバージョンからアップグレードした後で、ラベル付けセンターでカスタム情報の種類を構成していない場合は、この修正が必要です。

- 一般的なパフォーマンスと安定性の向上。

## <a name="version-22140"></a>バージョン2.2.14.0

**リリース日**: 07/15/2019

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
    - [ユーザーのサブセットに対して送信情報の種類の一致を無効にする](clientv2-admin-guide-customizations.md#disable-sending-information-type-matches-for-a-subset-of-users)
    - [Secure Islands からのラベルの移行と、その他のラベル付けのソリューション](clientv2-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)
    - [ラベルが適用されたときにカスタムプロパティを適用する](clientv2-admin-guide-customizations.md#apply-a-custom-property-when-a-label-is-applied)
    - [ラベルを構成して Outlook で S/MIME 保護を適用する](clientv2-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)
    - [親ラベルに既定のサブラベルを指定する](clientv2-admin-guide-customizations.md#specify-a-default-sublabel-for-a-parent-label)
    - [ラベルの色を指定します](clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)

- Word、Excel、PowerPoint、およびエクスプローラーのユーザー定義アクセス許可用に構成されたラベルのサポート。 詳細については、Office ドキュメントの「[ユーザーにアクセス許可の割り当てを許可](/Office365/SecurityCompliance/encryption-sensitivity-labels#let-users-assign-permissions)する」セクションを参照してください。

- AzureInformationProtection モジュールでの PowerShell の変更点は次のとおりです。
    - 新しいコマンドレット:[New-AIPCustomPermissions](/powershell/module/azureinformationprotection/New-AIPCustomPermissions) -RMSProtectionLicense を置き換えて、カスタムアクセス許可のアドホックポリシーを作成します。
    - 新しいパラメーター:
        -  *Custompermissions*と*Removeprotection* - [set-aipfilelabel](/powershell/module/azureinformationprotection/Set-AIPFileLabel)に追加されました
        -  *OnBeHalfOf* -非対話型セッションの*トークン*パラメーターの代わりに使用される、 [Set-aipauthentication](/powershell/module/azureinformationprotection/set-aipauthentication)に追加されました。
        -  *WhatIf*および*Discoveryinfotypes* - [set-aipfileclassification](/powershell/module/azureinformationprotection/set-aipfileclassification)に追加され、このコマンドレットがラベルを適用せずに検出モードで実行できるようになりました。
    - 保護サービスに直接接続する非推奨のコマンドレット:RMSAuthentication、も get-rmsfilestatus、RMSServer、、Set-rmsserverauthentication、get-rmstemplate、protect-rmsfile、set-rmsserverauthentication、protect-rmsfile、保護解除-のようになります。


**関する**

- *Discoveryinfotypes*パラメーターを使用して、Analytics と[set-aipfileclassification](https://docs.microsoft.com/powershell/module/azureinformationprotection/set-aipfileclassification?view=azureipps)の[コンテンツの一致](../reports-aip.md#content-matches-for-deeper-analysis)をサポートします。

- Windows で別のロケールに変更した後も、保護付きのラベルを PDF ドキュメントに適用できます。

- コンテンツからラベルを削除すると、ラベル構成の一部として適用された場合にのみ、保護も削除されます。 ラベルとは別に保護が適用されている場合、その保護は維持されます。 たとえば、ユーザーがファイルにカスタムアクセス許可を適用したとします。

- 自動ラベル付けが構成されている場合、ドキュメントを初めて保存するときにラベルが適用されます。

- 既定のラベル付けは、サブラベルをサポートします。

## <a name="version-207790"></a>バージョン2.0.779.0

**リリース日**: 05/01/2019

02/15/2020 でサポート

このリリースでは、Office アプリやエクスプローラーにラベルが表示されない場合がある競合状態の問題を解決するための修正プログラムが1つあります。

## <a name="version-207780"></a>バージョン2.0.778.0

**リリース日**: 04/16/2019

11/01/2019 でサポート

Windows 用の Azure Information Protection 統合ラベルクライアントの最初の一般公開バージョンでは、次の機能がサポートされています。 

- Azure Information Protection クライアントからのアップグレード。

- 手動、自動、および推奨ラベル付け:このクライアントの自動ラベル付けおよび推奨ラベル付けを構成する方法について詳しくは、「[機密ラベルをコンテンツに自動的に適用する](/Office365/SecurityCompliance/apply-sensitivity-label-automatically)」をご覧ください。

- エクスプローラー、右クリック アクションによるファイルの分類と保護、保護の削除、およびカスタムのアクセス許可の適用。

- 保護されたテキストとイメージ ファイル、保護された PDF ファイル、一般的に保護されているファイル用のビューアー。

- 次を実行するための PowerShell コマンド:
    - [ドキュメント上のラベルを設定または削除する](/powershell/module/azureinformationprotection/set-aipfilelabel)
    - [内容を検査してからドキュメントをラベル付けする](/powershell/module/azureinformationprotection/set-aipfileclassification)
    - [ドキュメントに適用されているラベル情報を読み取る](/powershell/module/azureinformationprotection/get-aipfilestatus)
    - [無人の PowerShell セッションをサポートするために認証する](/powershell/module/azureinformationprotection/set-aipauthentication)

- [Azure Information Protection analytics](../reports-aip.md)を使用した中央レポート作成のデータとエンドポイント検出の監査のサポート。

- 次のラベルおよびポリシー設定:
    - 視覚的なマーキング (ヘッダー、フッター、透かし)
    - 既定のラベル付け-現在、サブラベルなしでラベルに制限されています
    - 転送不可を適用し、Outlook でのみ表示されるラベル
    - ユーザーが分類レベルを下げるかどうか、またはラベルを削除するかどうかを確認する理由プロンプト
    - ラベルの色

- 管理センターからのポリシー更新:
    - Office アプリの起動ごと、および 4 時間ごと
    - 右クリックしてファイルまたはフォルダーを分類して保護したとき
    - ラベル付けと保護のために PowerShell コマンドレット を実行したとき

- 設定のリセットとログのエクスポートを含む、ヘルプとフィードバックのダイアログ ボックス。


## <a name="next-steps"></a>次の手順

完全な詳細については、[比較表](use-client.md#compare-the-clients)をご覧ください。

このクライアントをインストールして使用する方法の詳細については、次を参照してください。 

- ユーザー向け: [クライアントのダウンロードとインストール](install-unifiedlabelingclient-app.md)

- 管理者向け: [Azure Information Protection 統合されたラベル付けクライアント管理者ガイド](clientv2-admin-guide.md)

