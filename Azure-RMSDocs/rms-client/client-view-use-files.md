---
title: Azure Information Protection ビューアーで保護されたファイルを表示する
description: Azure Information Protection ビューアーをインストールする必要がある保護されたファイルを表示して使用する方法について説明します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ce1c7d4c-b5ff-4672-8b9a-a72129bac992
ms.subservice: v1client
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 3ba86bca223317204dc2067e39cb928a64de71e3
ms.sourcegitcommit: 1e25e7a32cc0b2a3a6c9b80575927009d8a96838
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "71690121"
---
# <a name="user-guide-view-protected-files-with-the-azure-information-protection-viewer"></a>ユーザー ガイド: Azure Information Protection ビューアーで保護されたファイルを表示する

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*
>
> *手順:[Windows 用 Azure Information Protection クライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

多くの場合、保護されたファイルは開くだけで表示できます。 たとえば、電子メール メッセージの添付ファイルをダブルクリックしたり、エクスプローラーでファイルをダブルクリックしたり、ファイルへのリンクをクリックします。

ファイルがすぐに開かない場合は、**Azure Information Protection ビューアー**で開くことができる場合があります。 このビューアーでは、保護されたテキスト ファイル、保護された画像ファイル、保護された PDF ファイル、およびファイル名拡張子が **.pfile** のすべてのファイルを開くことができます。

このビューアーは、Azure Information Protection クライアントの一部として自動的にインストールされますが、個別にインストールすることもできます。 クライアントとビューアーの両方のクライアントは、Microsoft Web サイトの [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) ページからインストールできます。 クライアントのインストールの詳細については、「[Azure Information Protection クライアントをダウンロードしてインストールする](install-client-app.md)」を参照してください。

> [!NOTE]
> クライアントをインストールする方が多くの機能を使用できますが、ローカル管理者のアクセス許可が必要であり、全機能を使用するには、組織に対応するサービスが必要です。 たとえば、Azure Information Protection や Active Directory Rights Management サービスです。
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

## <a name="to-view-and-use-a-protected-document"></a>保護されたファイルを表示して使用するには

1. 保護されたファイルを開きます (例：ファイルや添付ファイルをダブルクリック、またはファイルへのリンクをクリックする)。 アプリの選択を求められたら、 **[Azure Information Protection ビューアー]** を選択します。 

2. **[サインイン]** または **[サインアップ]** ページが表示された場合: **[サインイン]** をクリックして資格情報を入力します。 保護されたファイルが添付ファイルとして送信されてきた場合は、ファイルの送信に使用されたものと同じメール アドレスを指定するようにします。
    
    承認されているアカウントがない場合は、このページの「[認証のプロンプト](#prompts-for-authentication)」を参照してください。

3. 読み取り専用バージョンのファイルは、**Azure Information Protection Viewer (Azure Information Protection ビューアー)** で開きます。 十分なアクセス許可がある場合は、ファイルの印刷および編集ができます。 

    **[アクセス許可]** をクリックして、ファイルのアクセス許可を確認できます。 **[アクセス許可]** ダイアログ ボックスで、追加のアクセス許可が設定された新しいバージョンのファイルを要求するときに連絡する、ファイルの所有者を識別することもできます。
    
    アクセス許可と、各アクセス許可に含まれる使用権限の詳細については、「[アクセス許可レベルに含まれる権限](../configure-usage-rights.md#rights-included-in-permissions-levels)」を参照してください。

4. ファイルを編集するには、 **[名前を付けて保存]** をクリックし、保護されたファイルを元のファイル名拡張子に保存します。 そのファイルの種類に関連付けられているアプリケーションを使用してファイルを編集することができます。 この時点で、ファイルのラベルと保護が削除されます。
    
    ビューアーは保護されたファイル用のため、 **[名前を付けて保存]** ボタンは、保護されたファイルに対してのみ有効になることに注意してください。
    
5. ファイルの編集が完了したら、エクスプローラーで、ラベルを再適用するファイルを右クリックします。 このアクションにより保護が再適用されます。

6. 追加の保護されたファイルを開く場合は、 **[開く]** オプションを使用して、ビューアーから直接参照できます。 ビューアーで、元のファイルが選択したファイルに置き換えられます。 

> [!TIP]
> 保護されたファイルが開かず、Azure Information Protection クライアントが完全にインストールされている場合は、 **[設定のリセット]** オプションを試してください。 このオプションにアクセスするには、Office アプリから **[保護]** ボタン > **[ヘルプとフィードバック]**  >  **[設定のリセット]** の順に選択します。 
> 
> [[設定のリセット] オプションの詳細](client-admin-guide.md#more-information-about-the-reset-settings-option)

## <a name="other-instructions"></a>その他の手順
他の操作手順については、Azure Information Protection ユーザー ガイドを参照してください。

-   [目的に合ったトピックをクリックしてください](client-user-guide.md#what-do-you-want-to-do)

