---
title: 個人用 RMS と Azure Information Protection
description: 個人向け RMS について説明します。これは、保護されたファイルを送信されているものの、IT 部門が Azure でユーザー用のアカウントを管理していないために認証されないユーザー向けの、無料のセルフサービス サブスクリプションです。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/17/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2efcb440-fefd-45e9-872b-f471573aadf2
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3885dfcdf9c5858fe6e3a43b3980e0862dc4cb51
ms.sourcegitcommit: 85a56a778973be1c95df08bcd5b56e4f0bc12ad7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2018
ms.locfileid: "39104932"
---
# <a name="rms-for-individuals-and-azure-information-protection"></a>個人用 RMS と Azure Information Protection

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

個人用 RMS は、Azure Information Protection によって保護されたファイルを開く必要があるユーザー向けの、無料セルフサービス サブスクリプションです。 そのようなユーザーを Azure Active Directory で認証できない場合は、この無料登録サービスでユーザーのために Azure Active Directory にアカウントを作成できます。 結果的に、会社のメール アドレスでユーザーを認証できるようになり、保護されているファイルをコンピューターまたはモバイル デバイスで読み取ることができます。

個人用 RMS では、Azure Active Directory のセルフサービス サインアップが使用されます。 ユーザーがこのサブスクリプションを使用して組織のアカウントを作成していた場合は、組織の管理者として、ユーザーのアカウントの所有権を要求し、[アカウントを制御する](/active-directory/domains-admin-takeover#external-admin-takeover)ことができます。 


> [!NOTE]
> この無料のサブスクリプションは、組織外のユーザーで認証されている人が、組織が保護しているファイルを常に読めるようにするための方法の 1 つです。 他には [Office 365 Message Encryption と新機能](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)でドキュメントをメール送信する方法があります。 電子メールによるこのソリューションは、あらゆるデバイスのあらゆる電子メール アドレスに対して利用できます。組織外の人と、ブラウザーで安全に情報を共有し、Office ドキュメントを確認することができる、お勧めの方法です。
> 
> なお、Microsoft アカウントを使用することもできます。 ただし、Microsoft アカウントが認証に使用されている場合、アプリケーションによっては、保護されたコンテンツを開けない場合があます。 [詳細情報](../get-started/secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents) 

この無料アカウントにサインアップするには、[Microsoft Azure Information Protection のページ](https://aka.ms/rms-signup)に移動して、仕事用メール アドレスを指定します。 ユーザーは、Microsoft からの応答メールを受信したら、アカウントの作成に必要な詳細情報を入力してサインアップ プロセスを完了できます。 

アカウントが作成されると、各種デバイス用の Azure Information Protection クライアントまたはビューアーをダウンロードするためのリンク、ユーザー ガイドへのリンク、Rights Management による保護をネイティブでサポートするアプリケーションの最新の一覧へのリンクが、最終ページに表示されます。 

## <a name="to-sign-up-for-rms-for-individuals"></a>個人用 RMS にサインアップするには

1. Windows または Mac のコンピューター、またはモバイル デバイスを使用して [Microsoft Azure Information Protection のページ](https://aka.ms/rms-signup)にアクセスします。

2. 開く必要があるドキュメントを保護するのに使用された電子メール アドレスを入力します。

3. **[サインアップ]** をクリックします。

    Microsoft では、ユーザーの電子メール アドレスを使用して、組織が既に [Azure Information Protection Premium のサブスクリプション](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing)、または [Azure Information Protection を使用したデータ保護を含む Office 365 サブスクリプション](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)を利用しているかどうかを確認します。 これらのサブスクリプションのいずれかが見つかったら、個人用 RMS は必要ありません。 すぐにサインインが行われ、個人用 RMS のセルフ サービス サインアップはキャンセルされます。 これらのサブスクリプションのいずれも見つからない場合は、次の手順に進みます。

4. 入力したアドレスに確認の電子メール メッセージが届くまで待ちます。 このメールの差出人は Office 365 チーム (support@email.microsoftonline.com) で、件名は "**Finish signing up for Microsoft Azure Information Protection**" (Microsoft Azure Information Protection のサインアップ完了) です。

5. このメールが届いたら、**[はい、私です]** をクリックすると電子メール アドレスが確認されたことになり、サインアップ プロセスが完了します。

6. **[最後に...]** というページが表示され、アカウントの詳細情報を入力できるようになります。 氏名とパスワードを入力し、パスワードを確認のため再入力してから **[開始]** をクリックします。

7. アカウントが作成されると、Microsoft Azure Information Protection の新しいページが表示されます。ここで、Azure Information Protection クライアントをダウンロードしてインストールすることができます。また、[ユーザー ガイド](../rms-client/client-user-guide.md) リンクをクリックして、Windows コンピューター用の操作手順を表示することができます。

これでアカウントが作成されたので、保護されたファイルを読み取るためにサインインを求められた場合は、個人用 RMS のアカウントを作成するときに指定したものと同じ電子メール アドレスとパスワードを入力します。

> [!IMPORTANT]
> このアカウントを使用してファイルを保護することもできるようになりましたが、組織が Azure Information Protection の[試用版または有料サブスクリプション](https://azure.microsoft.com/pricing/details/information-protection/)を取得するまでは実行しないでください。 この無料サブスクリプションを使用してファイルや電子メールを保護した後で、組織がアカウントを制御した場合、前に保護したコンテンツにアクセスできなくなる可能性があります。


## <a name="next-steps"></a>次の手順
個人用 RMS は、Azure Active Directory でサポートされているセルフサービス サインアップの使用例です。 セルフサービス サインアップのしくみの詳細については、Azure Active Directory ドキュメントの「[Azure のセルフサービス サインアップについて](/active-directory/active-directory-self-service-signup)」を参照してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
