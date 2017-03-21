---
title: "分類とラベル付けに関してよく寄せられる質問 - AIP"
description: "Azure Information Protection の使用について、特に分類とラベル付けに関して質問はございますか。 ここで回答を探してみてください。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/15/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.openlocfilehash: 854de3beea1f4b6e05461dee58cec6ca91f79034
ms.sourcegitcommit: 117e4016794d0cb9b7bd95603fb6c79114d65360
translationtype: HT
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Azure Information Protection の分類とラベル付けに関してよく寄せられる質問

>*適用対象: Azure Information Protection、Office 365*

Azure Information Protection に関して、特に分類とラベル付けに関して質問はございますか。  ここで回答を探してみてください。 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>Azure Information Protection の分類機能はどのように使用しますか。

「[Azure Information Protection のクイック スタート チュートリアル](infoprotect-quick-start-tutorial.md)」に従えば、わずか数分でこの動作を確認できます。

追加の分類機能が利用可能になる時期については、[Enterprise Mobility and Security ブログ](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection)および [Yammer サイト](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)での案内をご確認ください。 現在のリリースには、次のような制限がいくつかあります。

- ラベル名とツール ヒントは&1; 言語でのみサポートされます。

- 分類とラベル付けには集中的なログはありません。

- 自動分類の条件は、語句またはパターンでなければなりません。

- モバイル デバイス (iOS および Android) および Mac コンピューター用の Office アプリや Office Web アプリ (Office Online) ではラベル付けできません。

- 分類およびラベル付けは Exchange Online や SharePoint Online とは統合されません。

- パートナーおよび開発者用の SDK にはまだ分類とラベル付け機能は含まれていません。

2 月のリリースでは以前の多くの制限がなくなりました。 詳細については、[ブログの投稿のお知らせ](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/08/azure-information-protection-december-update-moves-to-general-availability/)を参照してください。

## <a name="do-i-need-to-be-a-global-admin-to-configure-classification-and-labels"></a>分類とラベルを構成するにはグローバル管理者である必要がありますか?

Azure Information Protection ポリシーを構成するには、Azure Active Directory のグローバル管理者として Azure Portal にサインインする必要があります。

[Azure Information Protection クライアント](https://www.microsoft.com/en-us/download/details.aspx?id=53018)をインストールするときにデモ ポリシーをインストールするオプションを選択した場合は、ポータルにサインインしなくてもラベル機能を試すことができます。 デモ ポリシーでは Azure Information Protection 用の既定のポリシーがローカルにインストールされるので、ドキュメントと電子メールへのラベル付けを試用できますが、ラベルの変更または新規追加には Azure Portal にサインインする必要があります。 

## <a name="which-options-in-the-azure-portal-are-p1-or-p2"></a>Azure Portal のオプションが P1 か P2 かを確認するにはどうすればよいですか?

**Azure Information Protection Premium 1 (P1)** サブスクリプションに含まれる機能か、**Azure Information Protection Premium 2 (P2)** サブスクリプションに含まれる機能かを確認するには、Azure Information Protection サイトの[機能一覧](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)を参照してください。 ただし、一般的なガイドとして、自動分類や Hold Your Own Key (HYOK) などの高度な機能は、Azure Information Protection Premium 2 のサブスクリプションに固有です。

## <a name="can-a-file-have-more-than-one-classification"></a>1 つのファイルに複数の分類を適用することはできますか?

ユーザーが一度に選択できるのはドキュメントまたは電子メールごとに&1; つのラベルのみです。したがって、多くの場合、適用できる分類は&1; つのみとなります。 ただし、ユーザーがサブラベルを選択した場合、実際は同時に&2; つのラベル (プライマリ ラベルとセカンダリ ラベル) が適用されます。 サブラベルを使用すれば、1 つのファイルで&2; つの分類 (制御の追加レベルの親\子関係を示す) を適用することができます。

たとえば、**Secret** というラベルに、**Legal** や **Finance** などのサブラベルを含めることができます。 これらのサブラベルには、異なる分類ビジュアル マーキングと異なる Rights Management テンプレートをそれぞれ適用することができます。 ユーザーは **Secret** ラベル自体を選択することはできません。選択できるのは、**Legal** などのそのサブラベルのいずれか&1; つのみです。 したがって、表示されるラベル セットは **Secret \ Legal** のようになります。 そのファイルのメタデータには、**Secret** のカスタム テキスト プロパティーが&1; つ、**Legal** のカスタム テキスト プロパティーが&1; つ、さらに両方の値 (**Secret Legal**) を含むものが含まれます。 

サブラベルを使用する場合は、プライマリ ラベルでビジュアル マーキング、保護、および条件を構成しないでください。 サブレベルを使用する場合は、サブラベルのみにこれらの設定を構成してください。 プライマリ ラベルとそのサブラベルでこれらの設定を構成した場合は、サブラベルの設定が優先されます。

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>電子メールにラベルが付けられた場合、添付ファイルにも同じラベルが自動的に付けられますか?

いいえ。 添付ファイルのある電子メール メッセージにラベルを付ける場合、これらの添付ファイルは同じラベルを継承しません。 添付ファイルは、ラベルがないか、個別に適用されたラベルが付けられた状態で保持されます。 ただし、電子メールのラベルが保護を適用する場合、その保護は添付ファイルに適用されます。

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>Azure Information Protection の電子メールの分類は、Exchange のメッセージ分類とどのように違いますか?

Exchange のメッセージ分類は電子メールを分類する古い機能で、Azure Information Protection の分類機能とは別に実装されます。 ただし、これら&2; つのソリューションを統合して、ユーザーが Outlook Web アプリを使用して電子メールを分類する場合や、一部のモバイル用メール アプリケーションで、Azure Information Protection の分類および対応するラベル マーキングが自動的に追加されるようにすることができます。 Exchange が分類を追加すると、Azure Information Protection クライアントによって、その分類に対応するラベルの設定が適用されます。

Outlook Web アプリは Azure Information Protection の分類および保護をネイティブでサポートしていませんが、この同じ手法を使って、デスクトップの Outlook クライアントだけでなく、この電子メール クライアントでもラベルを使用することができます。

このソリューションを実現するには: 

1. [New-MessageClassification](https://technet.microsoft.com/library/bb124400) Exchange PowerShell コマンドレットを使用して、Azure Information Protection ポリシーのラベル名にマップする名前プロパティでメッセージの分類を作成します。 

2. 各ラベルの Exchange トランスポート ルールを作成します。メッセージのプロパティに構成した分類が含まれる場合はルールを適用し、メッセージ ヘッダーを設定するメッセージ プロパティを変更します。 

    メッセージ ヘッダーについては、Azure Information Protection ラベルを使って分類した Office ファイルのプロパティを調べることによって、指定する情報を見つけます。 **MSIP_Label_<GUID>_Enabled** の形式のファイル プロパティを識別し、メッセージ ヘッダーにこの文字列を指定して、ヘッダー値を **True** に指定します。 たとえば、メッセージ ヘッダーは次の文字列のようになります。**MSIP_Label_132616b8-f72d-5d1e-aec1-dfd89eb8c5b2_Enabled**


ユーザーが Outlook Web Access アプリまたは Rights Management による保護をサポートするモバイル デバイス クライアントを使用すると、次のことが起こります。 

- ユーザーが Exchange のメッセージ分類を選択して電子メールを送信します。

- Exchange ルールにより Exchange の分類が検出され、ルールに従ってメッセージ ヘッダーが変更されて、Azure Information Protection の分類が追加されます。

- Azure Information Protection クライアントを実行する受信者が Outlook で電子メールを表示すると、Azure Information Protection の割り当てられたラベル、および対応する電子メールのヘッダー、フッター、または透かしが表示されます。 

Azure Information Protection ラベルが Rights Management による保護を適用する場合は、メッセージ セキュリティを変更するオプションを選択してルールの構成に追加し、Rights Management による保護を適用して、RMS テンプレートまたは [転送不可] オプションを選択します。

リバース マッピングを行うようにトランスポート ルールを構成することもできます。Azure Information Protection ラベルが検出された場合は、対応する Exchange メッセージ分類を設定します。 このためには、次の操作を行います。

- Azure Information Protection のラベルごとに、**msip_labels** ヘッダーにラベル名 (**Confidential** など) が含まれている場合に適用されるトランスポート ルールを作成し、このラベルにマップするメッセージ分類を適用します。

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>DLP ソリューションや他のアプリケーションは Azure Information Protection とどのように統合できますか?

Azure Information Protection は分類に永続的メタデータを使用し、これにはクリア テキストのラベルが含まれるので、DLP ソリューションや他のアプリケーションはこの情報を読み取ることができます。 ファイルでは、このメタデータはカスタム プロパティに格納されます。電子メールでは、この情報は電子メールのヘッダーに含まれます。

## <a name="how-do-i-sign-in-as-a-different-user"></a>別のユーザーとしてサインインする方法

通常、運用環境では、Azure Information Protection クライアントを使用しているときに別のユーザーとしてサインインする必要はありません。 ただし、複数のテナントがある場合はこのようなサインインが必要になることがあります。 たとえば、組織が使用する Office 365 や Azure テナントに加えてテスト テナントがある場合などです。

現在サインインしているアカウントを確認するには、**[Microsoft Azure Information Protection]** ダイアログ ボックスを使用します。Office アプリケーションを開き、**[ホーム]** タブの **[保護]** グループで、**[保護]** をクリックし、**[ヘルプとフィードバック]** をクリックします。 アカウント名が **[クライアント ステータス]** セクションに表示されます。

特に、管理者アカウントを使用している場合は、表示されるサインイン アカウントのドメイン名を必ず確認してください。 たとえば、2 つのテナントに "admin" アカウントがある場合、アカウント名は正しくてもドメインを間違えてサインインするという失敗が起こりやすくなります。 このような状況では、Azure Information Protection ポリシーのダウンロードが失敗したり、目的のラベルや機能が表示されなかったりする可能性があります。

別のユーザーとしてサインインするには、レジストリを正しく編集する必要があります。

1. レジストリ エディターを使用して **HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP** に移動し、**TokenCache** 値を削除します。

2. 開いている Office アプリケーションがあれば再起動し、別のユーザー アカウントでサインインします。 Azure Information Protection サービスにサインインするように求めるプロンプトが Office アプリケーションで表示されない場合、**[Microsoft Azure Information Protection]** ダイアログ ボックスに戻り、更新された **[クライアント ステータス]** セクションの **[サインイン]** をクリックします。

補足:

- シングル サインオンを使用している場合は、Windows からサインアウトし、レジストリを編集した後、別のユーザー アカウントにサインインする必要があります。 Azure Information Protection クライアントは、現在サインインしているユーザーアカウントを使用して、自動的に認証を行います。

- Azure Rights Management サービスの環境を再初期化 (ブートストラップ) するには、[RMS Analyzer ツール](https://www.microsoft.com/en-us/download/details.aspx?id=46437)の **[リセット]** オプションを使用します。

- 現在ダウンロードされている Azure Information Protection ポリシーを削除するには、%localappdata%\Microsoft\MSIP フォルダーから **Policy.msip** ファイルを削除します。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]