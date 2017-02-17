---
title: "Rights Management によって保護されたファイルを表示して使用する | Azure Information Protection"
description: "Azure Information Protection クライアントがインストールされている必要がある保護されたファイルの表示および使用手順です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ce1c7d4c-b5ff-4672-8b9a-a72129bac992
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 364891123720daaacacbea1b382b7d101d75cd1a


---

# <a name="view-and-use-files-that-have-been-protected-by-rights-management"></a>Rights Management によって保護されたファイルを表示して使用する

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*

**[このバージョンのクライアントはプレビュー段階にあり、変更される可能性があります。]**

[Azure Information Protection クライアントがコンピューターにインストールされている](install-client-app.md)場合は、保護されたファイルを開くだけで表示できます。 たとえば、電子メール メッセージの添付ファイルをダブルクリックしたり、エクスプローラーでファイルをダブルクリックしたり、ファイルへのリンクをクリックします。

> [!NOTE]
> 保護されたファイルを表示するには、先にユーザーがファイルを表示する権限を持つことを Rights Management サービスが確認する必要があります。それには、ユーザー名とパスワードを調べます。 場合によっては、ユーザー名とパスワードがキャッシュに格納されていて、資格情報の入力を求められないことがあります。 それ以外の場合は、資格情報を指定するように求められます。
>
> 組織に使用できるクラウドベースのアカウント (Office 365 または Azure 用) がなく、AD RMS を使用していない場合は、Rights Management で保護されたファイルを開けるように資格情報を受け付ける無料のアカウントを申請できます。
>
> -   このアカウントを要求するには、リンクをクリックして、 [個人用 RMS](http://go.microsoft.com/fwlink/?LinkId=309469)を要求します。
>
>     サインアップするときは、個人の電子メール アドレスではなく会社の電子メール アドレスを使用してください。 電子メールで保護された添付ファイルを受け取ったためにサインアップする場合は、その電子メール メッセージの送信に使用されたものと同じ電子メール アドレスを使用します。
> -   詳細については、「[個人用 RMS と Microsoft Azure Rights Management](../understand-explore/rms-for-individuals.md)」を参照してください。

## <a name="to-view-and-use-a-protected-file"></a>保護されているファイルを表示して使用するには

1. 保護されたファイルを開きます (例：ファイルや添付ファイルをダブルクリック、またはファイルへのリンクをクリックする)。 アプリの選択を要求された場合は、**[Azure Information Protection ビューア (プレビュー)]** を選択します。 

2. **[サインイン]** または **[サインアップ]** ページが表示されたら、**[サインイン]** をクリックして資格情報を入力します。 保護されたファイルが添付ファイルとして送信されてきた場合は、ファイルの送信に使用されたものと同じメール アドレスを指定するようにします。
    
    承認されるアカウントがない場合は、このページの上部のメモを参照してください。 無料アカウントにサインアップして手順に戻ります。

3. 読み取り専用バージョンのファイルは、**Azure Information Protection Viewer (Azure Information Protection ビューアー)** で開きます。 十分なアクセス許可がある場合は、ファイルの印刷および編集ができます。 

    **[アクセス許可]** をクリックして、ファイルのアクセス許可を確認できます。 **[アクセス許可]** ダイアログ ボックスで、追加のアクセス許可が設定された新しいバージョンのファイルを要求するときに連絡する、ファイルの所有者を識別することもできます。
    
    アクセス許可と、各アクセス許可に含まれる使用権限の詳細については、「[アクセス許可レベルに含まれる権限](../deploy-use/configure-usage-rights.md#rights-included-in-permissions-levels)」を参照してください。

4. ファイルを編集するには、**[名前を付けて保存]** をクリックし、元のファイル名拡張子への保護なしにファイルを保存します。 そのファイルの種類に関連付けられているアプリケーションを使用してファイルを編集することができます。

5. 追加の保護されたファイルを開く場合は、**[開く]** オプションを使用して、ビューアーから直接参照できます。 ビューアーで、元のファイルが選択したファイルに置き換えられます。 

> [!TIP]
> 保護されたファイルが開かない場合は、[RMS アナライザー ツール](https://www.microsoft.com/en-us/download/details.aspx?id=46437)をダウンロードして使用します。 ツールの指示に従って、保護されたドキュメントが開かない原因となっている可能性のあるコンピューターの問題を確認します。


## <a name="other-instructions"></a>その他の手順
操作方法に関する手順については、「Azure Information Protection ユーザー ガイド」の次のセクションを参照してください。

-   [作業内容](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


