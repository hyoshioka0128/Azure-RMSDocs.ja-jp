---
title: Azure Information Protection の統合ラベル付けクライアントを使用して保護されたファイルを表示する
description: Azure Information Protection 統合ラベルビューアーがインストールされている必要がある保護されたファイルを表示する手順。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/13/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 7ef8129e7a97dbd0a9903e177221beb938108b7a
ms.sourcegitcommit: 03dc2eb973b20897b30659c2ac6cb43ce0a40e71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2020
ms.locfileid: "75960801"
---
# <a name="user-guide-view-protected-files-with-the-azure-information-protection-unified-labeling-client"></a>ユーザーガイド: Azure Information Protection 統合ラベルクライアントを使用して保護されたファイルを表示する

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8*
>
> *手順: [Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

多くの場合、保護されたファイルは開くだけで表示できます。 たとえば、電子メール メッセージの添付ファイルをダブルクリックしたり、エクスプローラーでファイルをダブルクリックしたり、ファイルへのリンクをクリックします。

ファイルがすぐに開かない場合は、**Azure Information Protection ビューアー**で開くことができる場合があります。 このビューアーでは、保護されたテキスト ファイル、保護された画像ファイル、保護された PDF ファイル、およびファイル名拡張子が **.pfile** のすべてのファイルを開くことができます。

ビューアーは、Azure Information Protection 統合されたラベル付けクライアントの一部として自動的にインストールされます。または、個別にインストールすることもできます。 このクライアントとビューアーの両方を、Microsoft web サイトの[Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970)のページからインストールできます。 このクライアントのインストールの詳細については、「 [Azure Information Protection の統合ラベル付けクライアントのダウンロードとインストール](install-unifiedlabelingclient-app.md)」を参照してください。

> [!NOTE]
> クライアントをインストールする方が多くの機能を使用できますが、ローカル管理者のアクセス許可が必要であり、全機能を使用するには、組織に対応するサービスが必要です。 たとえば、Azure Information Protection のようにします。
> 
> 別組織の誰かから保護されたドキュメントを送信された場合、またはお使いの PC でローカル管理者のアクセス許可を持っていない場合は、ビューアーをインストールします。

保護されたドキュメントを開くには、アプリケーションが "RMS 対応" である必要があります。 RMS 対応アプリケーションは、たとえば Office アプリや Azure Information Protection ビューアーなどです。 種類およびサポートされるデバイス別にアプリケーションの一覧を確認するには、「[RMS-enlightened applications (RMS 対応アプリケーション)](../requirements-applications.md#rms-enlightened-applications)」の表をご覧ください。 

## <a name="messagerpmsg-as-an-email-attachment"></a>電子メールの添付ファイルとしての Message.rpmsg

電子メールに **message.rpmsg** ファイルが添付されている場合、このファイルは保護されたドキュメントではなく、保護された電子メール メッセージであり、添付ファイルとして表示されます。 Windows 用の Azure Information Protection ビューアーを使用して、Windows PC でこの保護された電子メール メッセージを表示することはできません。 表示するには、Office Outlook などの Rights Management 保護をサポートしている Windows 用の電子メール アプリケーションが必要です。 あるいは、Outlook on the web を使用することもできます。

ただし、iOS または Android デバイスがあれば、Azure Information Protection アプリを使用して保護された電子メール メッセージを開くことができます。 これらのデバイス用の Azure Information Protection アプリは、Microsoft Web サイトの [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) からダウンロードできます。

## <a name="prompts-for-authentication"></a>認証のプロンプト

保護されたファイルを表示するには、そのファイルの保護に使用された Rights Management サービスで、ユーザーがファイルを表示する権限を持つことを先に確認する必要があります。 サービスはこの確認にユーザー名とパスワードを使用します。 場合によっては、これらの資格情報がキャッシュに格納されていて、サインインを求められないことがあります。 それ以外の場合は、資格情報を指定するように求められます。

組織がユーザーのためにクラウドベースのアカウントを用意しておらず (Office 365 または Azure)、また、そのオンプレミス版 (AD RMS) も利用していない場合、次の 2 つの選択肢があります。

- 保護されているメールが届いた場合、指示に従い、ご利用のソーシャル ID プロバイダー (Gmail アカウントの Google など) でサインインするか、ワンタイム パスコードを申請します。

- 資格情報を受け付ける無料のアカウントを申請できます。Rights Management で保護されているドキュメントを開くことができます。 このアカウントを申請するには、リンクをクリックして[個人用 RMS](https://go.microsoft.com/fwlink/?LinkId=309469) を申請します。個人のメール アドレスではなく、会社のメール アドレスを使用します。 

## <a name="to-view-a-protected-file"></a>保護されたファイルを表示するには

1. 保護されたファイルを開きます (例：ファイルや添付ファイルをダブルクリック、またはファイルへのリンクをクリックする)。 アプリの選択を求められたら、 **[Azure Information Protection ビューアー]** を選択します。 

2. **[サインイン]** または **[サインアップ]** ページが表示されたら、 **[サインイン]** をクリックして資格情報を入力します。 保護されたファイルが添付ファイルとして送信されてきた場合は、ファイルの送信に使用されたものと同じメール アドレスを指定するようにします。
    
    承認されているアカウントがない場合は、このページの「[認証のプロンプト](#prompts-for-authentication)」を参照してください。

3. **Azure Information Protection ビューアー** 、またはファイル名拡張子に関連付けられているアプリケーションで、ファイルの読み取り専用バージョンが開きます。

4. 追加の保護されたファイルを開く場合は、 **[開く]** オプションを使用して、ビューアーから直接参照できます。 ビューアーで、元のファイルが選択したファイルに置き換えられます。 

> [!TIP]
> 保護されたファイルが開かず、Azure Information Protection クライアントが完全にインストールされている場合は、 **[設定のリセット]** オプションを試してください。 このオプションにアクセスするには、Office アプリから **秘密度** ボタンを選択し、**ヘルプとフィードバック** > **設定のリセット** > ます。 
> 
> [[設定のリセット] オプションの詳細](clientv2-admin-guide.md#more-information-about-the-reset-settings-option)

## <a name="other-instructions"></a>その他の手順
他の操作手順については、Azure Information Protection ユーザー ガイドを参照してください。

- [作業内容](client-user-guide.md#what-do-you-want-to-do)

