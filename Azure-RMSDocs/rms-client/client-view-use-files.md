---
title: Azure Information Protection クラシッククライアントビューアーで保護されたファイルを表示する
description: Azure Information Protection クラシッククライアントビューアーがインストールされている必要がある、保護されたファイルを表示して使用する方法について説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 1/13/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ce1c7d4c-b5ff-4672-8b9a-a72129bac992
ms.subservice: v1client
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 280fb2d86bf4c4c9165c1d74df6c17da69a499c0
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97385592"
---
# <a name="user-guide-view-protected-files-with-the-azure-information-protection-classic-client-viewer"></a>ユーザーガイド: Azure Information Protection 従来のクライアントビューアーで保護されたファイルを表示する

>***適用対象**: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8 *
>
>***関連**: [Windows 用のクラシッククライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)ます。 統一されたラベル付けクライアントについては、「 [ユニファイドクライアントユーザーガイド](clientv2-view-use-files.md)」を参照してください。

>[!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

多くの場合、保護されたファイルは開くだけで表示できます。 たとえば、電子メール メッセージの添付ファイルをダブルクリックしたり、エクスプローラーでファイルをダブルクリックしたり、ファイルへのリンクをクリックします。

ファイルがすぐに開かない場合は、**Azure Information Protection ビューアー** で開くことができる場合があります。 このビューアーでは、保護されたテキスト ファイル、保護された画像ファイル、保護された PDF ファイル、およびファイル名拡張子が **.pfile** のすべてのファイルを開くことができます。

このビューアーは、Azure Information Protection クライアントの一部として自動的にインストールされますが、個別にインストールすることもできます。 クライアントとビューアーの両方のクライアントは、Microsoft Web サイトの [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) ページからインストールできます。 クライアントのインストールの詳細については、「[Azure Information Protection クライアントをダウンロードしてインストールする](install-client-app.md)」を参照してください。

> [!NOTE]
> クライアントをインストールする方が多くの機能を使用できますが、ローカル管理者のアクセス許可が必要であり、全機能を使用するには、組織に対応するサービスが必要です。 たとえば、Azure Information Protection や Active Directory Rights Management サービスです。
> 
> 別組織の誰かから保護されたドキュメントを送信された場合、またはお使いの PC でローカル管理者のアクセス許可を持っていない場合は、ビューアーをインストールします。

保護されたドキュメントを開くには、アプリケーションが "RMS 対応" である必要があります。 RMS 対応アプリケーションは、たとえば Office アプリや Azure Information Protection ビューアーなどです。 種類とサポートされているデバイスごとにアプリケーションの一覧を表示するには、「 [RMS 対応 applications (RMS アプリケーション](../requirements-applications.md) テーブル)」を参照してください。
  
## <a name="messagerpmsg-as-an-email-attachment"></a>電子メールの添付ファイルとしての Message.rpmsg

電子メールに **message.rpmsg** ファイルが添付されている場合、このファイルは保護されたドキュメントではなく、保護された電子メール メッセージであり、添付ファイルとして表示されます。 Windows 用の Azure Information Protection ビューアーを使用して、Windows PC でこの保護された電子メール メッセージを表示することはできません。 表示するには、Office Outlook などの Rights Management 保護をサポートしている Windows 用の電子メール アプリケーションが必要です。 あるいは、Outlook on the web を使用することもできます。

ただし、iOS または Android デバイスがあれば、Azure Information Protection アプリを使用して保護された電子メール メッセージを開くことができます。 これらのデバイス用の Azure Information Protection アプリは、Microsoft Web サイトの [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) からダウンロードできます。

## <a name="prompts-for-authentication"></a>認証のプロンプト

保護されたファイルを表示するには、そのファイルの保護に使用された Rights Management サービスで、ユーザーがファイルを表示する権限を持つことを先に確認する必要があります。 サービスはこの確認にユーザー名とパスワードを使用します。 場合によっては、これらの資格情報がキャッシュに格納されていて、サインインを求められないことがあります。 それ以外の場合は、資格情報を指定するように求められます。

使用するクラウドベースのアカウント (Microsoft 365 または Azure の場合) が組織になく、同等のオンプレミスバージョン (AD RMS) を使用していない場合は、次の2つの方法があります。

- 保護されているメールが届いた場合、指示に従い、ご利用のソーシャル ID プロバイダー (Gmail アカウントの Google など) でサインインするか、ワンタイム パスコードを申請します。

- 資格情報を受け付ける無料のアカウントを申請できます。Rights Management で保護されているドキュメントを開くことができます。 このアカウントを申請するには、リンクをクリックして[個人用 RMS](https://go.microsoft.com/fwlink/?LinkId=309469) を申請します。個人のメール アドレスではなく、会社のメール アドレスを使用します。 

## <a name="to-view-and-use-a-protected-document"></a>保護されたファイルを表示して使用するには

1. 保護されたファイルを開きます (例：ファイルや添付ファイルをダブルクリック、またはファイルへのリンクをクリックする)。 アプリの選択を求められたら、**[Azure Information Protection ビューアー]** を選択します。 

2. **[サインイン]** または **[サインアップ]** ページが表示されたら、**[サインイン]** をクリックして資格情報を入力します。 保護されたファイルが添付ファイルとして送信されてきた場合は、ファイルの送信に使用されたものと同じメール アドレスを指定するようにします。
    
    承認されているアカウントがない場合は、このページの「[認証のプロンプト](#prompts-for-authentication)」を参照してください。

3. 読み取り専用バージョンのファイルは、**Azure Information Protection Viewer (Azure Information Protection ビューアー)** で開きます。 十分なアクセス許可がある場合は、ファイルの印刷および編集ができます。 

    **[アクセス許可]** をクリックして、ファイルのアクセス許可を確認できます。 **[アクセス許可]** ダイアログ ボックスで、追加のアクセス許可が設定された新しいバージョンのファイルを要求するときに連絡する、ファイルの所有者を識別することもできます。
    
    アクセス許可と、各アクセス許可に含まれる使用権限の詳細については、「[アクセス許可レベルに含まれる権限](../configure-usage-rights.md#rights-included-in-permissions-levels)」を参照してください。

4. ファイルを編集するには、**[名前を付けて保存]** をクリックし、保護されたファイルを元のファイル名拡張子に保存します。 そのファイルの種類に関連付けられているアプリケーションを使用してファイルを編集することができます。 この時点で、ファイルのラベルと保護が削除されます。
    
    ビューアーは保護されたファイル用のため、**[名前を付けて保存]** ボタンは、保護されたファイルに対してのみ有効になることに注意してください。
    
5. ファイルの編集が完了したら、エクスプローラーで、ラベルを再適用するファイルを右クリックします。 このアクションにより保護が再適用されます。

6. 追加の保護されたファイルを開く場合は、**[開く]** オプションを使用して、ビューアーから直接参照できます。 ビューアーで、元のファイルが選択したファイルに置き換えられます。 

> [!TIP]
> 保護されたファイルが開かず、Azure Information Protection クライアントが完全にインストールされている場合は、**[設定のリセット]** オプションを試してください。 このオプションにアクセスするには、Office アプリから **[保護]** ボタン > **[ヘルプとフィードバック]** > **[設定のリセット]** の順に選択します。 
> 
> [[設定のリセット] オプションの詳細](client-admin-guide.md#more-information-about-the-reset-settings-option)

## <a name="other-instructions"></a>その他の手順
他の操作手順については、Azure Information Protection ユーザー ガイドを参照してください。

-   [目的に合ったトピックをクリックしてください](client-user-guide.md#what-do-you-want-to-do)

