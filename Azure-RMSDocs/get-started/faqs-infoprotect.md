---
title: "分類とラベル付けに関してよく寄せられる質問 | Azure Information Protection"
description: "Azure Information Protection のプレビュー リリースに関して質問がある場合は、 ここで回答を探してみてください。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/21/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 8bb0058940eaf1663ec82b38bc37c33400ea8b87


---

# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Azure Information Protection の分類とラベル付けに関してよく寄せられる質問

>*適用対象: Azure Information Protection、Office 365*

Azure Information Protection に関して、特に分類とラベル付けに関して質問はございますか。  ここで回答を探してみてください。 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>Azure Information Protection の分類機能はどのように使用しますか。

Azure Information Protection クライアントでは、Information Protection バーが Microsoft Office アプリケーションに追加されました。このバーを使うと、データに割り当てられている分類ラベルを表示および変更できます。 分類は、手動、ユーザーへの推奨、または自動で適用されます。 指定した分類に対して、Rights Management サービスを使用してデータを保護できます。  

分類のラベルと動作は、Azure ポータルで構成します。 既定の組み込みポリシーを使用して Azure Information Protection を非常に短時間で評価したり、独自のポリシーを完全にカスタマイズしたりできます。 ユーザーに表示される分類ラベルの色、名称、順序を変更できます。 ツール ヒントおよびヘッダー、フッター、透かしなどの分類のビジュアル マーキングを構成することもできます。

「[Azure Information Protection のクイック スタート チュートリアル](infoprotect-quick-start-tutorial.md)」に従えば、わずか数分でこの動作を確認できます。

現在のリリースには次の制限があります。 追加機能が利用可能になる時期については、[Enterprise Mobility and Security ブログ](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection)および [Yammer サイト](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)での案内をご確認ください。

- ラベル名とツール ヒントは&1; 言語でのみサポートされます。

- 分類とラベル付けには集中的なログはありません。

- 自動分類の条件は、語句またはパターンでなければなりません。

- モバイル デバイス (iOS および Android) および Mac コンピューター用の Office アプリ、および Office Web アプリ (Office Online) は、まだサポートされていません。

- Exchange Online または SharePoint Online とは統合されません。

- パートナー向けおよび開発者向けの SDK はありません。

以前記載されていた制限事項の一部が、プレビューで利用可能になりました。 詳細については、ブログ投稿のお知らせ「[Azure Information Protection December preview now available (Azure Information Protection の&12; 月のプレビュー版が利用可能になりました)](https://blogs.technet.microsoft.com/enterprisemobility/2016/12/07/azure-information-protection-december-preview-now-available/)」を参照してください。


## <a name="do-i-need-to-be-a-global-admin-to-try-azure-information-protection"></a>Azure Information Protection を試すにはグローバル管理者である必要がありますか。

Azure Information Protection ポリシーを構成するには、Azure Active Directory のグローバル管理者として Azure ポータルにサインインする必要があります。

ただし、[Azure Information Protection クライアント](https://www.microsoft.com/en-us/download/details.aspx?id=53018)をインストールするときにデモ ポリシーをインストールするオプションを選択した場合は、ポータルにサインインしなくてもラベル機能を試すことができます。 デモ ポリシーでは Azure Information Protection 用の既定のポリシーがローカルにインストールされるので、ドキュメントと電子メールへのラベル付けを試用できますが、ラベルの変更または新規追加には Azure ポータルにサインインする必要があります。 

## <a name="which-options-in-the-azure-portal-are-p1-or-p2"></a>Azure ポータルのオプションが P1 か P2 かを確認するにはどうすればよいですか?

**Azure Information Protection Premium 1 (P1)** サブスクリプションに含まれる機能か、**Azure Information Protection Premium 2 (P2)** サブスクリプションに含まれる機能かを確認するには、Azure Information Protection サイトの[機能一覧](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)を参照してください。 ただし、一般的なガイドとして、自動分類や Hold Your Own Key (HYOK) などの高度な機能は、Azure Information Protection Premium 2 のサブスクリプションに固有です。

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>Azure Information Protection はオンプレミスおよびハイブリッドのシナリオをサポートしますか?

Azure Information Protection はクラウド ベースのソリューションです。 ハイブリッド シナリオで Azure Information Protection をデプロイする方法に興味がある場合は、askipteam@microsoft.com 宛てに電子メールを送って Information Protection チームにお問い合わせください。

## <a name="how-do-computers-get-the-policy-information-from-azure-information-protection-and-how-often-is-it-refreshed"></a>コンピューターはどのような方法および更新頻度で Azure Information Protection からポリシー情報を取得しますか?

ユーザーが Office アプリケーションを開くたびに、Azure Information Protection クライアントは Azure Information Protection ポリシーの新しいバージョンがあるかどうかを確認します。 これに加えて、Office アプリケーションが 24 時間ごとに確認します。 新しいバージョンがある場合、クライアントは HTTPS リンクによりデータを保護してポリシーをダウンロードします。 

新しい Azure Information Protection ポリシーの発行時に Office アプリケーションの複数のインスタンスが読み込まれる場合、ポリシーの最新バージョンを取得するためにすべてのインスタンスを閉じる必要があります。 たとえば、2 つの Word 文書を開いていて、更新された Azure Information Protection ポリシーを一方の文書でのみテストするには、両方の Word 文書を閉じて、最新のポリシーで使用する文書を再度開きます。

## <a name="where-can-files-be-stored-to-use-azure-information-protection"></a>Azure Information Protection を使用するにはファイルをどこに格納すればよいですか? 

Azure Information Protection はファイルと電子メールに永続的なラベルおよび保護を適用するので、ファイルの保存場所はどこでもかまいません。

## <a name="can-i-classify-only-new-data-or-can-i-also-classify-existing-data"></a>分類できるのは新しいデータのみですか、既存のデータも分類できますか?

Azure Information Protection ポリシーのアクションは、ドキュメントの保存時および電子メールの送信時に、新規コンテンツおよび既存コンテンツへの変更の両方に対して反映されます。

プレビュー クライアントがある場合は、ファイル エクスプローラーから既存のファイルをすばやく分類 (および必要に応じて、保護) することもできます。 

## <a name="can-i-use-azure-information-protection-for-classification-only-without-enforcing-encryption-and-restricting-usage-rights"></a>Azure Information Protection を分類のみに使用し、暗号化の適用と使用権限の制限が行われないようにすることはできますか?

はい。 ファイルの種類でこの操作がサポートされている場合は、保護なしで、分類のみを適用するように Azure Information Protection ポリシーを構成することができます。 実際、このような使い方が、ドキュメントまたは電子メールのサブセットのみを保護する必要がある、特別なデータ管理を必要とするデプロイ ネットワークのほとんどのケースであると思われます。

## <a name="how-does-automatic-classification-work"></a>自動分類はどのように行われますか?

Azure ポータルでは、"クレジット カード番号" や "米国社会保障番号" などの定義済みのパターンを使用できます。 または、自動分類の条件として、ユーザー指定の文字列またはパターンを定義することもできます。

この例については、「[Azure Information Protection のクイック スタート チュートリアル](infoprotect-quick-start-tutorial.md)」を参照してください。 

分類の精度は、条件に基づく分類ルールの構成方法によって異なります。 現時点では、条件はテキスト パターンと正規表現をサポートしています。 プレビュー中に使用できる各オプションの説明と、テスト用に推奨されるいくつかの例については、「[Azure Information Protection の自動および推奨分類の条件を構成する方法](../deploy-use/configure-policy-classification.md)」を参照してください。 検出は、ドキュメントの保存時または電子メールの送信時に実行されます。

最適なユーザー エクスペリエンスおよびビジネス継続性の確保のためには、完全自動アクションではなく、ユーザー推奨アクションで始めることをお勧めします。 このようにすると、ユーザーは、ラベル付けまたは保護のアクションを受け入れることも、これらの推奨アクションをオーバーライドすることもできます。   

## <a name="can-azure-information-protection-prompt-users-to-classify-files-themselves-rather-than-use-automatic-classification"></a>Azure Information Protection では、自動分類を使用するのではなく、自分でファイルを分類するようにユーザーに要求できますか? 

はい。 Azure ポータルで自動分類または推奨のどちらを使うかを構成できます。**[Select how this label is applied: automatically or recommended to user]** (このラベルの適用方法を選択: 自動または推奨) オプションを **[Recommended]** (推奨) に設定すると、ユーザーに対して推奨が行われます。

この例については、「[Azure Information Protection のクイック スタート チュートリアル](infoprotect-quick-start-tutorial.md)」を参照してください。  

## <a name="can-i-force-all-documents-to-be-classified"></a>強制的にすべてのドキュメントを分類できますか?

はい。 ユーザーに保存するすべてのファイルを分類するよう要求するには、Azure Portal で、**[すべてのドキュメントとメールにラベルを付ける]** を**オン**に設定するポリシーを構成します。 

## <a name="can-i-remove-classification-from-a-file"></a>ファイルから分類を削除できますか?

はい。 ファイルから分類を削除するには、Office アプリケーションでファイルを開き、Information Protection バーの **[ラベルの編集]** アイコンをクリックして、**[ラベルの削除]** アイコンの順にクリックし、**[OK]** をクリックしてアクションを確認します。 


## <a name="can-i-prompt-users-to-justify-why-they-are-changing-the-classification-level"></a>ユーザーに分類レベルを変更する理由の説明を求めることはできますか?

はい。 分類を変更する理由をユーザーに入力させるには、Azure ポータルで **[Users must provide justification to set a lower classification label, remove a label, or remove protection]** (ユーザーは分類ラベルの秘密度を下げる、ラベルを削除する、または保護を解除するときにその理由を示す必要があります) オプションを **[On]** (オン) に設定します。 このように設定すると、ユーザーのアクションと理由が、ローカル Windows イベント ログの **[アプリケーションとサービス ログ]**  >  **[Microsoft Azure Information Protection]** に記録されます。

## <a name="how-can-i-automatically-protect-the-content-after-its-been-classified"></a>分類された後のコンテンツを自動的に保護するにはどうすればよいですか?

Azure ポータルで Rights Management テンプレートを選択することにより、指定した分類レベルに従ってコンテンツを自動的に保護できます。

この例については、「[Azure Information Protection のクイック スタート チュートリアル](infoprotect-quick-start-tutorial.md)」を参照してください。 詳しくは、「[Rights Management による保護を適用するためのラベルを構成する方法](../deploy-use/configure-policy-protection.md)」を参照してください。

## <a name="can-a-file-have-more-than-one-classification"></a>1 つのファイルに複数の分類を適用することはできますか?

ユーザーが一度に選択できるのはドキュメントまたは電子メールごとに&1; つのラベルのみです。したがって、多くの場合、適用できる分類は&1; つのみとなります。 ただし、ユーザーがサブラベルを選択した場合、実際は同時に&2; つのラベル (プライマリ ラベルとセカンダリ ラベル) が適用されます。 サブラベルを使用すれば、1 つのファイルで&2; つの分類 (制御の追加レベルの親\子関係を示す) を適用することができます。

たとえば、**Secret** というラベルに、**Legal** や **Finance** などのサブラベルを含めることができます。 これらのサブラベルには、異なる分類ビジュアル マーキングと異なる Rights Management テンプレートをそれぞれ適用することができます。 ユーザーは **Secret** ラベル自体を選択することはできません。選択できるのは、**Legal** などのそのサブラベルのいずれか&1; つのみです。 したがって、表示されるラベル セットは **Secret \ Legal** のようになります。 そのファイルのメタデータには、**Secret** のカスタム テキスト プロパティーが&1; つ、**Legal** のカスタム テキスト プロパティーが&1; つ、さらに両方の値 (**Secret Legal**) を含むものが含まれます。 

サブラベルを使用する場合は、プライマリ ラベルでビジュアル マーキング、保護、および条件を構成しないでください。 サブレベルを使用する場合は、サブラベルのみにこれらの設定を構成してください。 プライマリ ラベルとそのサブラベルでこれらの設定を構成した場合は、サブラベルの設定が優先されます。

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>電子メールにラベルが付けられた場合、添付ファイルにも同じラベルが自動的に付けられますか?

いいえ。 添付ファイルのある電子メール メッセージにラベルを付ける場合、これらの添付ファイルは同じラベルを継承しません。 添付ファイルは、ラベルがないか、個別に適用されたラベルが付けられた状態で保持されます。 ただし、電子メールのラベルが保護を適用する場合、その保護は添付ファイルに適用されます。

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>Azure Information Protection の電子メールの分類は、Exchange のメッセージ分類とどのように違いますか?

Exchange のメッセージ分類は電子メールを分類する古い機能で、Azure Information Protection の分類機能とは別に実装されます。 ただし、これら&2; つのソリューションを統合して、ユーザーが Outlook Web アプリを使用して電子メールを分類する場合や、一部のモバイル用メール アプリケーションで、Azure Information Protection の分類および対応するラベル マーキングが自動的に追加されるようにすることができます。 Exchange が分類を追加すると、プレビュー バージョンの Azure Information Protection クライアントによって、その分類に対応するラベルの設定が適用されます。

Outlook Web アプリは Azure Information Protection の分類および保護をネイティブでサポートしていませんが、この同じ手法を使って、デスクトップの Outlook クライアントだけでなく、この電子メール クライアントでもラベルを使用することができます。

このソリューションを実現するには: 

1. [New-MessageClassification](https://technet.microsoft.com/library/bb124400) Exchange PowerShell コマンドレットを使用して、Azure Information Protection ポリシーのラベル名にマップする名前プロパティでメッセージの分類を作成します。 

2. 各ラベルの Exchange トランスポート ルールを作成します。メッセージのプロパティに構成した分類が含まれる場合はルールを適用し、メッセージ ヘッダーを設定するメッセージ プロパティを変更します。 

    メッセージ ヘッダーについては、Azure Information Protection ラベルを使って分類した Office ファイルのプロパティを調べることによって、指定する情報を見つけます。 **MSIP_Label_<GUID>_Enabled** の形式のファイル プロパティを識別し、メッセージ ヘッダーにこの文字列を指定して、ヘッダー値を **True** に指定します。 たとえば、メッセージ ヘッダーは次の文字列のようになります。**MSIP_Label_132616b8-f72d-5d1e-aec1-dfd89eb8c5b2_Enabled**


ユーザーが Outlook Web Access アプリまたは Rights Management による保護をサポートするモバイル デバイス クライアントを使用すると、次のことが起こります。 

- ユーザーが Exchange のメッセージ分類を選択して電子メールを送信します。

- Exchange ルールにより Exchange の分類が検出され、ルールに従ってメッセージ ヘッダーが変更されて、Azure Information Protection の分類が追加されます。

- プレビュー バージョンの Azure Information Protection クライアントを実行する受信者が Outlook で電子メールを表示すると、Azure Information Protection の割り当てられたラベル、および対応する電子メールのヘッダー、フッター、または透かしが表示されます。 

Azure Information Protection ラベルが Rights Management による保護を適用する場合は、メッセージ セキュリティを変更するオプションを選択してルールの構成に追加し、Rights Management による保護を適用して、RMS テンプレートまたは [転送不可] オプションを選択します。

リバース マッピングを行うようにトランスポート ルールを構成することもできます。Azure Information Protection ラベルが検出された場合は、対応する Exchange メッセージ分類を設定します。 このためには、次の操作を行います。

- Azure Information Protection のラベルごとに、**msip_labels** ヘッダーにラベル名 (**Confidential** など) が含まれている場合に適用されるトランスポート ルールを作成し、このラベルにマップするメッセージ分類を適用します。

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>DLP ソリューションや他のアプリケーションは Azure Information Protection とどのように統合できますか?

Azure Information Protection は分類に永続的メタデータを使用し、これにはクリア テキストのラベルが含まれるので、DLP ソリューションや他のアプリケーションはこの情報を読み取ることができます。 ファイルでは、このメタデータはカスタム プロパティに格納されます。電子メールでは、この情報は電子メールのヘッダーに含まれます。

## <a name="how-does-document-tracking-and-revocation-work-for-azure-information-protection"></a>Azure Information Protection では、ドキュメントの追跡と失効はどのように行われますか?

Azure Information Protection を使用して分類および保護されたファイルのドキュメントの追跡は、Azure Rights Management 保護や RMS 共有アプリケーションと連動します。 また、Azure Information Protection クライアント (バージョン 1.0.233 以降) を使用してドキュメント追跡サイトにもアクセスできます。 

- Office アプリケーションの **[ホーム]** タブの **[保護]** グループで、**[保護]** > **[使用の追跡]** をクリックします。 

詳細については、「[RMS 共有アプリケーションを使用してドキュメントを追跡および取り消す](../rms-client/sharing-app-track-revoke.md)」を参照してください。

## <a name="can-i-control-which-users-can-use-azure-information-protection-to-classify-and-protect-content"></a>Azure Information Protection を使用してコンテンツを分類および保護できるユーザーを制御できますか?

Azure Information Protection クライアントの配布を制御することで、データを分類および保護するユーザーを制限できます。 [スコープ ポリシー](../deploy-use\configure-policy-scope.md)を構成するときに、指定したユーザーだけに新しいラベルを追加します。 

Azure Information Protection によって分類されたファイルおよび電子メールは、Azure Information Protection クライアントのインストールの有無に関係なく、すべてのユーザーが使用または編集できます。 

## <a name="how-do-i-sign-in-as-a-different-user"></a>別のユーザーとしてサインインする方法

通常、運用環境では、Azure Information Protection クライアントを使用しているときに別のユーザーとしてサインインする必要はありません。 ただし、複数のテナントがある場合はこのようなサインインが必要になることがあります。 たとえば、組織が使用する Office 365 や Azure テナントに加えてテスト テナントがある場合などです。

現在サインインしているアカウントを確認するには、**[Microsoft Azure Information Protection]** ダイアログ ボックスを使用します。Office アプリケーションを開き、**[ホーム]** タブの **[保護]** グループで、**[保護]** をクリックし、**[ヘルプとフィードバック]** をクリックします。 アカウント名が **[クライアント ステータス]** セクションに表示されます。

特に、管理者アカウントを使用している場合は、表示されるサインイン アカウントのドメイン名を必ず確認してください。 たとえば、2 つのテナントに "admin" アカウントがある場合、アカウント名は正しくてもドメインを間違えてサインインするという失敗が起こりやすくなります。 このような状況では、Azure Information Protection ポリシーのダウンロードが失敗したり、目的のラベルや機能が表示されなかったりする可能性があります。

別のユーザーとしてサインインするには、レジストリを正しく編集する必要があります。

1. レジストリ エディターを使用して **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP** に移動し、**TokenCache** 値を削除します。

2. 開いている Office アプリケーションがあれば再起動し、別のユーザー アカウントでサインインします。 Azure Information Protection サービスにサインインするように求めるプロンプトが Office アプリケーションで表示されない場合、**[Microsoft Azure Information Protection]** ダイアログ ボックスに戻り、更新された **[クライアント ステータス]** セクションの **[サインイン]** をクリックします。

補足:

- Azure Rights Management サービスの環境を再初期化 (ブートストラップ) するには、[RMS Analyzer ツール](https://www.microsoft.com/en-us/download/details.aspx?id=46437)の **[リセット]** オプションを使用します。

- 現在ダウンロードされている Azure Information Protection ポリシーを削除するには、%localappdata%\Microsoft\MSIP フォルダーから **Policy.msip** ファイルを削除します。

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>Azure Information Protection の問題を報告またはフィードバックを送信するにはどうすればよいですか。

Azure Information Protection に問題があり、クライアントの現行リリースを使用している場合: お使いの Office アプリケーションの **[ホーム]** タブの **[保護]** グループで、**[保護]** をクリックし、**[ヘルプとフィードバック]** をクリックします。 **[Microsoft Azure Information Protection]** ダイアログ ボックスで、**[フィードバックの送信]** をクリックします。 これにより、Information Protection チームに電子メールが送信され、問題の診断に役立つ PC のログ ファイルが自動的に添付されます。 

質問やご意見がある場合は、[Azure Information Protection の Yammer サイト](https://www.yammer.com/askipteam/)を使用してください。 

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


