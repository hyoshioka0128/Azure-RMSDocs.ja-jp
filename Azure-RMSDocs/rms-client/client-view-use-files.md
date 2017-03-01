---
title: "AIP クライアントでの保護されたファイルの表示と使用"
description: "Azure Information Protection クライアントがインストールされている必要がある保護されたファイルの表示および使用手順です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/10/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ce1c7d4c-b5ff-4672-8b9a-a72129bac992
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 408b57c5ff5ce3688763ef7b4c4b87b123ca4ea3
ms.lasthandoff: 02/24/2017


---

# <a name="view-and-use-files-that-have-been-protected-by-rights-management"></a>Rights Management によって保護されたファイルを表示して使用する

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*

多くの場合、保護されたファイルは開くだけで表示できます。 たとえば、電子メール メッセージの添付ファイルをダブルクリックしたり、エクスプローラーでファイルをダブルクリックしたり、ファイルへのリンクをクリックします。

ファイルが開かない場合、**Azure Information Protection ビューアー**を使用して開くことができます。 このビューアーは、Azure Information Protection クライアントの一部として自動的にインストールされますが、別にインストールすることもできます。 クライアントとビューアーの両方のクライアントは、Microsoft Web サイトの [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) ページからインストールできます。 クライアントのインストールの詳細については、「[Azure Information Protection クライアントをダウンロードしてインストールする](install-client-app.md)」を参照してください。

> [!NOTE]
> クライアントをインストールする方が多くの機能を使用できますが、ローカル管理者のアクセス許可が必要であり、全機能を使用するには、組織に対応するサービスが必要です。
> 
> - Azure Information Protection
> 
> - Azure Rights Management
> 
> - Active Directory Rights Management サービス 
> 
> 別組織の誰かから保護されたドキュメントを送信された場合、またはお使いの PC でローカル管理者のアクセス許可を持っていない場合は、ビューアーをインストールします。

## <a name="prompts-for-authentication"></a>認証のプロンプト

保護されたファイルを表示するには、そのファイルの保護に使用された Rights Management サービスで、ユーザーがファイルを表示する権限を持つことを先に確認する必要があります。 サービスはこの確認にユーザー名とパスワードを使用します。 場合によっては、ユーザー名とパスワードがキャッシュに格納されていて、資格情報の入力を求められないことがあります。 それ以外の場合は、資格情報を指定するように求められます。

組織に使用できるクラウド ベースのアカウント (Office 365 または Azure 用) がなく、同等のオンプレミス バージョン (AD RMS) を使用していない場合は、Rights Management で保護されたファイルを開けるように資格情報を受け付ける無料のアカウントを申請できます。

-   このアカウントを要求するには、リンクをクリックして、 [個人用 RMS](http://go.microsoft.com/fwlink/?LinkId=309469)を要求します。
    
    サインアップするときは、個人の電子メール アドレスではなく会社の電子メール アドレスを使用してください。 電子メールで保護された添付ファイルを受け取ったためにサインアップする場合は、その電子メール メッセージの送信に使用されたものと同じ電子メール アドレスを使用します。
    
-   詳細については、「[個人用 RMS と Microsoft Azure Rights Management](../understand-explore/rms-for-individuals.md)」を参照してください。

## <a name="to-view-and-use-a-protected-file"></a>保護されているファイルを表示して使用するには

1. 保護されたファイルを開きます (例：ファイルや添付ファイルをダブルクリック、またはファイルへのリンクをクリックする)。 アプリの選択を求められたら、**[Azure Information Protection ビューアー]** を選択します。 

2. **[サインイン]** または **[サインアップ]** ページが表示されたら、**[サインイン]** をクリックして資格情報を入力します。 保護されたファイルが添付ファイルとして送信されてきた場合は、ファイルの送信に使用されたものと同じメール アドレスを指定するようにします。
    
    承認されているアカウントがない場合は、このページの「[認証のプロンプト](#prompts-for-authentication)」を参照してください。 無料アカウントにサインアップして手順に戻ります。

3. 読み取り専用バージョンのファイルは、**Azure Information Protection Viewer (Azure Information Protection ビューアー)** で開きます。 十分なアクセス許可がある場合は、ファイルの印刷および編集ができます。 

    **[アクセス許可]** をクリックして、ファイルのアクセス許可を確認できます。 **[アクセス許可]** ダイアログ ボックスで、追加のアクセス許可が設定された新しいバージョンのファイルを要求するときに連絡する、ファイルの所有者を識別することもできます。
    
    アクセス許可と、各アクセス許可に含まれる使用権限の詳細については、「[アクセス許可レベルに含まれる権限](../deploy-use/configure-usage-rights.md#rights-included-in-permissions-levels)」を参照してください。

4. ファイルを編集するには、**[名前を付けて保存]** をクリックし、元のファイル名拡張子への保護なしにファイルを保存します。 そのファイルの種類に関連付けられているアプリケーションを使用してファイルを編集することができます。

5. 追加の保護されたファイルを開く場合は、**[開く]** オプションを使用して、ビューアーから直接参照できます。 ビューアーで、元のファイルが選択したファイルに置き換えられます。 

> [!TIP]
> 保護されたファイルが開かない場合は、[RMS アナライザー ツール](https://www.microsoft.com/en-us/download/details.aspx?id=46437)をダウンロードして使用します。 ツールの指示に従って、保護されたドキュメントが開かない原因となっている可能性のあるコンピューターの問題を確認します。


## <a name="other-instructions"></a>その他の手順
他の操作手順については、Azure Information Protection ユーザー ガイドを参照してください。

-   [作業内容](client-user-guide.md#what-do-you-want-to-do)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
