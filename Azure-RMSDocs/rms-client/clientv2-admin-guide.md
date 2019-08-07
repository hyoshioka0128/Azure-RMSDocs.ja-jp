---
title: Azure Information Protection 統合されたラベル付けクライアント管理者ガイド
description: Azure Information Protection 統合された Windows 用ラベル付けクライアントの展開を担当する企業ネットワーク上の管理者向けの手順と情報です。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 95c855701b1fc8de2e3f9f458b2cd760a3abdd4b
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2019
ms.locfileid: "68793224"
---
# <a name="azure-information-protection-unified-labeling-client-administrator-guide"></a>Azure Information Protection 統合されたラベル付けクライアント管理者ガイド

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*
>
> *手順:[Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

このガイドの情報は、エンタープライズネットワーク上の Azure Information Protection の統合されたラベル付けクライアントを担当している場合、または Azure Information Protection 統合された[ラベル付けクライアントユーザーよりも詳細な技術情報が必要な場合に使用します。ガイド](clientv2-user-guide.md)。 

例えば:

- このクライアントのさまざまなコンポーネントについて知り、インストールする必要があるかどうかを理解する

- 前提条件、インストール オプションとパラメーター、検証チェックに関する情報を含む、ユーザー向けにクライアントをインストールする方法

- クライアント ファイルと使用状況ログを検索する

- クライアントでサポートされているファイルの種類を識別する

- クライアントで PowerShell を使用したコマンドラインでの制御

**このドキュメントでわからない問題がある場合は**、 [Azure Information Protection についての Yammer サイト](https://www.yammer.com/AskIPTeam)をご覧ください。 

## <a name="technical-overview-of-the-azure-information-protection-unified-labeling-client"></a>Azure Information Protection 統合ラベル付けクライアントの技術概要

Azure Information Protection の統合ラベル付けクライアントには、次のものが含まれます。

- Office アドイン。ユーザーが感度ラベルを選択するための **[感度]** ボタンをリボンにインストールし、Azure Information Protection バーを表示してラベルを表示しやすくします。

- エクスプローラー。ユーザーがファイルに分類ラベルと保護を適用するための右クリック オプション。

- ネイティブ アプリケーションで開くことができないときに、保護されたファイルを表示するビューアー。

- ファイルに対して分類ラベルと保護を適用および削除するための PowerShell モジュール。 

- Azure Rights Management (Azure RMS) サービスと通信してファイルを暗号化および保護する Rights Management クライアント。

ビューアーを除き、Azure Information Protection 統合されたラベル付けクライアントは、Azure Rights Management サービスまたは Active Directory Rights Management サービスと直接通信するアプリケーションやサービスでは使用できません。

AD RMS を所有していて、Azure Information Protection に移行する場合は、「[AD RMS から Azure Information Protection に移行する](../migrate-from-ad-rms-to-azure-rms.md)」をご覧ください。


## <a name="should-you-deploy-the-azure-information-protection-unified-labeling-client"></a>Azure Information Protection 統合されたラベル付けクライアントを展開する必要がありますか。

[Office 365 セキュリティ/コンプライアンスセンターで機密ラベル](https://docs.microsoft.com/Office365/SecurityCompliance/sensitivity-labels)を使用していて、次のいずれかに該当する場合は、Azure Information Protection 統合されたラベル付けクライアントを展開します。

- Windows コンピューター上の Office アプリ (Word、Excel、PowerPoint、Outlook) 内からラベルを選択して、ドキュメントや電子メールメッセージを分類 (および必要に応じて保護) する。

- Office でサポートされているよりも多くのファイルの種類、複数選択、およびフォルダーをサポートするエクスプローラーを使って、ファイルを分類 (および必要に応じて保護) したい。

- PowerShell コマンドを使って、ドキュメントを分類 (および必要に応じて保護) するスクリプトを実行したい。

- オンプレミスに格納されているファイルを検出、分類 (および必要に応じて保護) する、現在プレビュー中のサービスをテストします。

- ファイルを表示するネイティブ アプリケーションがインストールされていないか、ドキュメントを開くことができない場合に、保護されているドキュメントを表示したい。

Azure Information Protection 統合ラベル付けクライアント用の Office アドインを示す例。リボンに新しい **[秘密度]** ボタンが表示され、オプションの Azure Information Protection バーが表示されます。

![Azure Information Protection バーと既定のポリシー](../media/v2word2016-calloutsv2.png)

## <a name="installing-and-supporting-the-azure-information-protection-unified-labeling-client"></a>Azure Information Protection の統合ラベル付けクライアントのインストールとサポート

実行可能ファイルまたは Windows インストーラーファイルを使用して、Azure Information Protection 統合されたラベル付けクライアントをインストールできます。 各オプションの詳細と手順については、「 [Install the Azure Information Protection uniform ラベリング client for users](clientv2-admin-guide-install.md)」を参照してください。  

クライアントのインストールに関するサポート情報については、次のセクションを利用してください。 

### <a name="installation-checks-and-troubleshooting"></a>インストールのチェックとトラブルシューティング

クライアントがインストールされたら、 **[ヘルプとフィードバック]** オプションで **[Microsoft Azure Information Protection]** ダイアログ ボックスを開きます。

- Office アプリケーションから: **[ホーム]** タブの **[秘密度]** グループで、 **[秘密度]** を選択し、 **[ヘルプとフィードバック]** を選択します。

- ファイル エクスプローラーから:単一ファイル、複数ファイル、またはフォルダーを右クリックで選択し、 **[分類して保護する]** 、 **[ヘルプとフィードバック]** の順に選択します。 

#### <a name="help-and-feedback-section"></a>**[ヘルプとフィードバック]** セクション

既定では、[詳細を表示]**リンク**を[Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) web サイトに移動します。 ラベル管理ポータルでポリシー設定の1つとしてカスタムヘルプページに移動する独自の URL リンクを構成することができます。Office 365 セキュリティ/コンプライアンス センター、Microsoft 365 セキュリティ センター、Microsoft 365 コンプライアンス センター。

これらを Microsoft サポートに送信するように求められた場合は、**エクスポートログ**によって、Azure Information Protection 統合されたラベル付けクライアントのログファイルが自動的に収集され、アタッチされます。 このオプションは、エンド ユーザーがログ ファイルをヘルプ デスクに送信するために使用することもできます。

**リセット設定**では、ユーザーをサインアウトし、現在ダウンロードされている機密ラベルとラベルポリシーを削除して、Azure Rights Management サービスのユーザー設定をリセットします。

##### <a name="more-information-about-the-reset-settings-option"></a>[設定のリセット] オプションの詳細

- このオプションを使用するためにローカル管理者の権限は必要ありません。また、この操作はイベント ビューアーのログに記録されません。 

- ファイルがロックされている場合を除き、この操作は、次の場所のすべてのファイルを削除します。 これらのファイルには、ラベル管理ポータルのクライアント証明書、保護テンプレート、秘密度ラベル、ポリシー、およびキャッシュされたユーザー資格情報が含まれます。 クライアント ログ ファイルは削除されません。
    
    - %LocalAppData%\Microsoft\DRM
    
    - %LocalAppData%\Microsoft\MSIPC
    
    - %LocalAppData%\Microsoft\MSIP\Policy.msip
    
    - %LocalAppData%\Microsoft\MSIP\TokenCache

- 次のレジストリ キーと設定が削除されます。 これらいずれかのレジストリ キーの設定にカスタムの値がある場合、クライアントをリセットした後に、設定を再構成する必要があります。 
    
    通常、エンタープライズ ネットワークでは、グループ ポリシーをコンピューター上で更新するときに、これらの設定が自動的に再適用される場合、設定はグループ ポリシーを使用して構成されます。 ただし、スクリプトで一度構成されているか、手動で構成されている設定がある場合があります。 これらの場合、設定を再構成するには、追加の手順を行う必要があります。 たとえば、AD RMS から移行しても、内部ネットワーク上にまだサービス接続ポイントがあるため、Azure Information Protection へのリダイレクトの設定を構成するには、コンピューターでスクリプトが一度実行される場合があります。 クライアントをリセットした後、コンピューターでこのスクリプトをもう一度実行する必要があります。
    
    - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\15.0\Common\Identity
    
    - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM
    
    - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\15.0\Common\DRM
    
    - HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\16.0\Common\DRM
    
    - HKEY_CURRENT_USER\SOFTWARE\Classes\Local Settings\Software\Microsoft\MSIPC

- 現在サインインしているユーザーは、サインアウトします。

#### <a name="client-status-section"></a>**クライアント ステータス** セクション

**接続**の値を使って、表示されているユーザー名が Azure Information Protection 認証に使用されるアカウントを識別するか確認します。 このユーザー名は、Office 365 または Azure Active Directory に使用しているアカウントに一致する必要があります。 また、アカウントは、ラベル管理ポータルでの秘密度ラベルが構成されている Office 365 テナントに属している必要があります。

表示されているユーザーに別のユーザーとしてサインインする必要がある場合は、「[別のユーザーとしてサインイン](clientv2-admin-guide-customizations.md#sign-in-as-a-different-user)する」を参照してください。

**[バージョン]** 情報を使用して、どちらのバージョンのクライアントがインストールされているか確認します。 クライアントの[バージョンリリース情報](unifiedlabelingclient-version-release-history.md)を読むことで、これが最新リリースバージョンであるかどうか、および対応する修正と新機能を確認できます。

## <a name="support-for-multiple-languages"></a>複数言語のサポート

Azure Information Protection の統一されたラベル付けクライアントは、Office 365 でサポートされている言語と同じ言語をサポートしています。 サポートされる言語の一覧については、Office の「[ご利用いただける国と地域](https://products.office.com/business/international-availability)」ページの「**Office 365、Exchange Online Protection、Power BI**」セクションを参照してください。

これらの言語の場合、メニューオプション、ダイアログボックス、および Azure Information Protection 統合ラベルクライアントからのメッセージは、ユーザーの言語で表示されます。 言語を検出するインストーラーが1つあるので、Azure Information Protection 統合されたラベル付けクライアントを別の言語用にインストールするために、追加の構成は必要ありません。 

ただし、Azure Information Protection の統一されたラベル付けクライアントは、現在、ラベルに対して異なる言語をサポートしていません。 また、視覚的なマーキングは翻訳されず、複数の言語をサポートしていません。

## <a name="post-installation-tasks"></a>インストール後のタスク

Azure Information Protection の統一されたラベル付けクライアントをインストールした後、ドキュメントや電子メールにラベルを付ける方法についてユーザーに指示し、特定のシナリオに対して選択するラベルについてのガイダンスを提供してください。 例えば:

- オンライン ユーザーの手順:[Azure Information Protection 統合されたラベル付けユーザーガイド](clientv2-user-guide.md)

- カスタマイズ可能なユーザー ガイドをダウンロードする: [Azure Information Protection エンド ユーザー導入ガイド](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf)

## <a name="upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client"></a>Azure Information Protection 統合ラベル付けクライアントのアップグレードと保守

> [!NOTE]
> Azure Information Protection の統一されたラベル付けクライアントは、Azure Information Protection クライアント (クラシック) のアップグレードに加えて、Azure Information Protection 統合されたラベル付けクライアントの以前のバージョンからのアップグレードもサポートします。

Azure Information Protection チームは、新しい機能と修正を行うために、Azure Information Protection 統合されたラベル付けクライアントを定期的に更新します。 アナウンスは、チームの [Yammer サイト](https://www.yammer.com/AskIPTeam)に投稿されます。

Windows Update を使用している場合は、クライアントのインストール方法に関係なく、Azure Information Protection の統一されたラベル付けクライアントがこのクライアントの一般公開バージョンを自動的にアップグレードします。 新しいクライアントのリリースは、リリースの数週間後にカタログに公開されます。

または、[Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)から新しいリリースをダウンロードして、クライアントを手動でアップグレードすることもできます。 ダウンロードしたら、新しいバージョンをインストールして、クライアントをアップグレードします。 Azure Information Protection クライアントからアップグレードする場合は、この方法を使用してプレビューバージョンをアップグレードする必要があります。

Windows 7 の Azure Information Protection クライアント (クラシック) からアップグレードする場合、クライアントのアップグレード中に、すべての Office アプリケーションが自動的に再起動されます。 この自動再起動は、それ以降のオペレーティングシステムには適用されません。また、以前のバージョンの統一されたラベル付けクライアントからアップグレードする場合にも当てはまりません。

手動でアップグレードし、かつインストール方法を変更する場合は、最初に以前のバージョンをアンインストールします。 たとえば、実行可能 (.exe) バージョンのクライアントから Windows インストーラ― (.msi) バージョンのクライアントに変更する場合です。 または、クライアントの以前のバージョンをインストールする必要がある場合です。 たとえば、テスト用に現在のプレビュー バージョンがインストールされていて、現在の一般公開バージョンに戻す必要がある場合です。

バージョンの[リリース履歴とサポートポリシー](unifiedlabelingclient-version-release-history.md)を使用して、Azure Information Protection 統合されたラベル付けクライアントのサポートポリシー、現在サポートされているバージョン、サポートされているリリースの新機能と変更された機能について理解します。 

## <a name="uninstalling-the-azure-information-protection-unified-labeling-client"></a>Azure Information Protection 統合ラベル付けクライアントのアンインストール

クライアントは、以下のいずれかの方法でアンインストールできます。

- [コントロール パネル] を使用してプログラムをアンインストールする: **[Microsoft Azure Information Protection]**  >  **[アンインストール]** をクリックします。

- 実行可能ファイル (たとえば、 **AzInfoProtection_UL**) を再実行し、 **[セットアップの変更]** ページで **[アンインストール]** をクリックします。 

- **/uninstall** を付けて実行可能ファイルを実行します。 例: `AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>次の手順
クライアントをインストールするには、「[ユーザー用に Azure Information Protection 統合ラベルクライアントをインストール](clientv2-admin-guide-install.md)する」を参照してください。

クライアントを既にインストールしている場合、このクライアントのサポートに必要な追加情報を以下の記事でご覧ください。

- [カスタマイズ](clientv2-admin-guide-customizations.md)

- [クライアント ファイルおよび使用状況ログの記録](client-admin-guide-files-and-logging.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)


