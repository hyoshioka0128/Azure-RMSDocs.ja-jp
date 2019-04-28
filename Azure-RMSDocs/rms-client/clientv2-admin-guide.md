---
title: Azure Information Protection クライアント管理者ガイドのラベル付けを統合します。
description: 手順とエンタープライズ ネットワーク上の管理者向けの情報は、Azure Information Protection の展開を担当する Windows 用のラベル付けのクライアントが統合されました。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: 7caa35896e0dcfd3cd6dc1cf407da87e41e71ef5
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60183189"
---
# <a name="azure-information-protection-unified-labeling-client-administrator-guide"></a>Azure Information Protection クライアント管理者ガイドのラベル付けを統合します。

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*
>
> "*手順:[Azure Information Protection unified Windows 用のラベル付けのクライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

このガイドの情報を使用して、Azure Information Protection の統合、エンタープライズ ネットワーク上のラベル付けのクライアントの責任者は場合、またはよりも詳細な技術情報を表示する場合、 [Azure Information Protection unified ラベル付けクライアント ユーザー ガイド](clientv2-user-guide.md)します。 

以下に例を示します。

- このクライアントのさまざまなコンポーネントについて知り、インストールする必要があるかどうかを理解する

- 前提条件、インストール オプションとパラメーター、検証チェックに関する情報を含む、ユーザー向けにクライアントをインストールする方法

- クライアント ファイルと使用状況ログを検索する

- クライアントでサポートされているファイルの種類を識別する

- クライアントで PowerShell を使用したコマンドラインでの制御

**このドキュメントでわからない問題がある場合は**、 [Azure Information Protection についての Yammer サイト](https://www.yammer.com/AskIPTeam)をご覧ください。 

## <a name="technical-overview-of-the-azure-information-protection-unified-labeling-client"></a>Azure Information Protection の統合されたラベル付けクライアントの技術概要

Azure Information Protection の統合されたラベル付けクライアント、次のとおりです。

- Office アドインをインストールする、**感度**ユーザー秘密度ラベル、およびラベルの可視性の向上に Azure Information Protection バーを表示するオプションを選択するためのリボンのボタンをクリックします。

- エクスプローラー。ユーザーがファイルに分類ラベルと保護を適用するための右クリック オプション。

- ネイティブ アプリケーションで開くことができないときに、保護されたファイルを表示するビューアー。

- ファイルに対して分類ラベルと保護を適用および削除するための PowerShell モジュール。 

- 暗号化ファイルを保護し、Azure Rights Management (Azure RMS) サービスと通信する Rights Management クライアント。

を除き、ビューアーでは、Azure Information Protection の統合されたラベル付けクライアントは、Azure Rights Management サービスまたは Active Directory Rights Management サービスと直接通信するアプリケーションとサービスでは使用できません。

AD RMS を所有していて、Azure Information Protection に移行する場合は、「[AD RMS から Azure Information Protection に移行する](../migrate-from-ad-rms-to-azure-rms.md)」をご覧ください。


## <a name="should-you-deploy-the-azure-information-protection-unified-labeling-client"></a>Azure Information Protection の統合されたラベル付けクライアントを展開する必要がありますか。

使用する場合は、Azure Information Protection の統合されたラベル付けクライアントを展開[Office 365 セキュリティ/コンプライアンス センターでの機密ラベル](https://docs.microsoft.com/Office365/SecurityCompliance/sensitivity-labels)、し、次のいずれかを適用します。

- Windows コンピューターで Office アプリケーション (Word、Excel、PowerPoint、Outlook) 内からラベルを選択してドキュメントや電子メール メッセージを分類 (および必要に応じて保護) にします。

- Office でサポートされているよりも多くのファイルの種類、複数選択、およびフォルダーをサポートするエクスプローラーを使って、ファイルを分類 (および必要に応じて保護) したい。

- PowerShell コマンドを使って、ドキュメントを分類 (および必要に応じて保護) するスクリプトを実行したい。

- ファイルを表示するネイティブ アプリケーションがインストールされていないか、ドキュメントを開くことができない場合に、保護されているドキュメントを表示したい。

アドインで、Azure Information protection、Office を示す例が、新しいを表示する、ラベル付けのクライアントをユニファイド**感度**リボンと省略可能な Azure Information Protection バーのボタン。

![Azure Information Protection バーと既定のポリシー](../media/v2word2016-calloutsv2.png)

## <a name="installing-and-supporting-the-azure-information-protection-unified-labeling-client"></a>インストールと Azure Information Protection の統合されたラベル付けクライアントのサポート

Azure Information Protection の統合されたラベル付けクライアントをインストールするには、実行可能ファイルまたは Windows インストーラー ファイルを使用します。 詳細については、各選択肢と手順については、次を参照してください。[ユーザーの Azure Information Protection の統合されたラベル付けクライアントをインストール](clientv2-admin-guide-install.md)します。  

クライアントのインストールに関するサポート情報については、次のセクションを利用してください。 

### <a name="installation-checks-and-troubleshooting"></a>インストールのチェックとトラブルシューティング

クライアントがインストールされたら、**[ヘルプとフィードバック]** オプションで **[Microsoft Azure Information Protection]** ダイアログ ボックスを開きます。

- Office アプリケーション: から**ホーム** タブで、**感度**グループで、**感度**、し、**ヘルプとフィードバック**。

- ファイル エクスプローラーから:単一ファイル、複数ファイル、またはフォルダーを右クリックで選択し、**[分類して保護する]**、**[ヘルプとフィードバック]** の順に選択します。 

#### <a name="help-and-feedback-section"></a>**[ヘルプとフィードバック]** セクション

**詳細情報のリンクを知りたい**既定では、 [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) web サイト。 Office 365 セキュリティ/コンプライアンス センターでポリシー設定の 1 つとしてカスタム ヘルプ ページに移動する、独自の URL リンクを構成することができます。

**ログのエクスポート**自動的に収集し、Microsoft サポートに送信するよう依頼されている場合、Azure Information Protection unified ラベル付けのクライアントのログ ファイルが添付されます。 このオプションは、エンド ユーザーがログ ファイルをヘルプ デスクに送信するために使用することもできます。

**設定のリセット**がユーザーをサインアウトすると、現在ダウンロードされている機密ラベルと、ポリシーを削除しますおよび Azure Rights Management サービスのユーザー設定をリセットします。

##### <a name="more-information-about-the-reset-settings-option"></a>[設定のリセット] オプションの詳細

- このオプションを使用するためにローカル管理者の権限は必要ありません。また、この操作はイベント ビューアーのログに記録されません。 

- ファイルがロックされている場合を除き、この操作は、次の場所のすべてのファイルを削除します。 これらのファイルには、クライアント証明書、Rights Management テンプレート、機密ラベルおよびポリシーから Office 365 のセキュリティとコンプライアンス センターでは、キャッシュされたユーザーの資格情報が含まれます。 クライアント ログ ファイルは削除されません。
    
    - %LocalAppData%\Microsoft\DRM
    
    - %LocalAppData%\Microsoft\MSIPC
    
    - %LocalAppData%\Microsoft\MSIP\Policy.msip
    
    - %LocalAppData%\Microsoft\MSIP\TokenCache

- 次のレジストリ キーと設定が削除されます。 これらいずれかのレジストリ キーの設定にカスタムの値がある場合、クライアントをリセットした後に、設定を再構成する必要があります。 
    
    通常、エンタープライズ ネットワークでは、グループ ポリシーをコンピューター上で更新するときに、これらの設定が自動的に再適用される場合、設定はグループ ポリシーを使用して構成されます。 ただし、スクリプトで一度構成されているか、手動で構成されている設定がある場合があります。 これらの場合、設定を再構成するには、追加の手順を行う必要があります。 たとえば、AD RMS から移行しても、内部ネットワーク上にまだサービス接続ポイントがあるため、Azure Information Protection へのリダイレクトの設定を構成するには、コンピューターでスクリプトが一度実行される場合があります。 クライアントをリセットした後、コンピューターでこのスクリプトをもう一度実行する必要があります。
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\15.0\Common\Identity
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\15.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Microsoft\Office\16.0\Common\DRM
    
    - HKEY_CURRENT-USER\SOFTWARE\Classes\Local Settings\Software\Microsoft\MSIPC    

- 現在サインインしているユーザーは、サインアウトします。

#### <a name="client-status-section"></a>**クライアント ステータス** セクション

**接続**の値を使って、表示されているユーザー名が Azure Information Protection 認証に使用されるアカウントを識別するか確認します。 このユーザー名は、Office 365 または Azure Active Directory に使用しているアカウントに一致する必要があります。 アカウントは、Office 365 セキュリティ/コンプライアンス センターでの機密ラベル用に構成された Office 365 テナントにも属する必要があります。

参照してください、表示されている別のユーザーとしてサインインする必要がある場合、[別のユーザーとしてサインイン](clientv2-admin-guide-customizations.md#sign-in-as-a-different-user)指示します。

**[バージョン]** 情報を使用して、どちらのバージョンのクライアントがインストールされているか確認します。 これは、最新であるかどうかを確認することができますを読み取ることによって、バージョンと対応する修正プログラムと新機能をリリース、[バージョンのリリース情報](unifiedlabelingclient-version-release-history.md)クライアント。

## <a name="support-for-multiple-languages"></a>複数言語のサポート

Azure Information Protection の統合されたラベル付けクライアントには、Office 365 でサポートされているものと同じ言語がサポートしています。 サポートされる言語の一覧については、Office の「[ご利用いただける国と地域](https://products.office.com/business/international-availability)」ページの「**Office 365、Exchange Online Protection、Power BI**」セクションを参照してください。

これらの言語、メニュー オプション、ダイアログ ボックス、および Azure Information Protection からのメッセージには、統一されたラベル付けクライアントは、ユーザーの言語で表示します。 さまざまな言語の Azure Information Protection の統合されたラベル付けクライアントをインストールする追加の構成は必要ありませんので、言語を検出する 1 つのインストーラーがあります。 

ただし、Azure Information Protection の統合されたラベル付けクライアントは現在サポートしていませんさまざまな言語のラベル。 さらに、視覚的なマーキングは翻訳されませんし、1 つ以上の言語をサポートしていません。

## <a name="post-installation-tasks"></a>インストール後のタスク

Azure Information Protection の統合されたラベル付けクライアントをインストールした後、ドキュメントや電子メールにラベルを付ける方法については、ユーザーと特定のシナリオを選択するには、どのラベルのガイダンスを与えることを確認します。 以下に例を示します。

- オンライン ユーザーの手順:[Azure Information Protection ユーザー ガイド](client-user-guide.md)

- カスタマイズ可能なユーザー ガイドをダウンロードする: [Azure Information Protection エンド ユーザー導入ガイド](https://download.microsoft.com/download/7/1/2/712A280C-1C66-4EF9-8DC3-88EE43BEA3D4/Azure_Information_Protection_End_User_Adoption_Guide_EN_US.pdf)

## <a name="upgrading-and-maintaining-the-azure-information-protection-unified-labeling-client"></a>アップグレードと維持、Azure Information Protection の統合のラベル付けクライアント

> [!NOTE]
> Azure Information Protection 統合ラベル付けの client では、Azure Information Protection クライアントをアップグレードすると、Azure Information Protection の統一されたラベル付けクライアントの以前のバージョンからアップグレードされています。

Azure Information Protection チームは、新機能と修正プログラムの Azure Information Protection のクライアントを統一されたにラベル付けを定期的に更新します。 アナウンスは、チームの [Yammer サイト](https://www.yammer.com/AskIPTeam)に投稿されます。

Windows Update を使用している Azure 情報保護の Azure Information Protection の統合されたラベル付けクライアントは自動的にクライアントのインストール方法に関係なく、このクライアントの一般公開バージョンをアップグレードします。 新しいクライアントのリリースは、リリースの数週間後にカタログに公開されます。

または、[Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)から新しいリリースをダウンロードして、クライアントを手動でアップグレードすることもできます。 ダウンロードしたら、新しいバージョンをインストールして、クライアントをアップグレードします。 このメソッドは、プレビュー バージョンと、Azure Information Protection クライアントをアップグレードするかどうかのアップグレードを使用する必要があります。

手動でアップグレードし、かつインストール方法を変更する場合は、最初に以前のバージョンをアンインストールします。 たとえば、実行可能 (.exe) バージョンのクライアントから Windows インストーラ― (.msi) バージョンのクライアントに変更する場合です。 または、クライアントの以前のバージョンをインストールする必要がある場合です。 たとえば、テスト用に現在のプレビュー バージョンがインストールされていて、現在の一般公開バージョンに戻す必要がある場合です。

使用して、[バージョン リリース履歴とサポート ポリシー](unifiedlabelingclient-version-release-history.md) Azure Information Protection unified バージョンは現在サポートされて、ラベル付けのクライアントと新機能と変更された、サポートされている機能のサポート ポリシーを理解するには解放します。 

## <a name="uninstalling-the-azure-information-protection-unified-labeling-client"></a>クライアントのラベル付けを統合、Azure Information Protection のアンインストール

クライアントは、以下のいずれかの方法でアンインストールできます。

- [コントロール パネル] を使用してプログラムをアンインストールする: **[Microsoft Azure Information Protection]** > **[アンインストール]** をクリックします。

- 実行可能ファイルを再実行 (たとえば、 **AzInfoProtection_UL.exe**) との間、**セットアップの変更**] ページで [**アンインストール**します。 

- **/uninstall** を付けて実行可能ファイルを実行します。 例: `AzInfoProtection.exe /uninstall`

## <a name="next-steps"></a>次の手順
クライアントをインストールするを参照してください。[ユーザーの Azure Information Protection の統合されたラベル付けクライアントをインストール](clientv2-admin-guide-install.md)します。

クライアントを既にインストールしている場合、このクライアントのサポートに必要な追加情報を以下の記事でご覧ください。

- [カスタマイズ](clientv2-admin-guide-customizations.md)

- [クライアント ファイルおよび使用状況ログの記録](client-admin-guide-files-and-logging.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)


