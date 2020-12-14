---
title: 個人用 RMS と Azure Information Protection
description: 個人向け RMS について説明します。これは、保護されたファイルを送信されているものの、IT 部門が Azure でユーザー用のアカウントを管理していないために認証されないユーザー向けの、無料のセルフサービス サブスクリプションです。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/08/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2efcb440-fefd-45e9-872b-f471573aadf2
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ac5b596c87649e32d27da8e2797bafe5b9745792
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97384793"
---
# <a name="rms-for-individuals-and-azure-information-protection"></a>個人用 RMS と Azure Information Protection

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***関連**: [AIP のラベル付けクライアントと従来のクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 *

>[!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

個人用 RMS は、Azure Information Protection によって保護されたファイルを開く必要があるユーザー向けの、無料セルフサービス サブスクリプションです。 そのようなユーザーを Azure Active Directory で認証できない場合は、この無料登録サービスでユーザーのために Azure Active Directory にアカウントを作成できます。 結果的に、会社のメール アドレスでユーザーを認証できるようになり、保護されているファイルをコンピューターまたはモバイル デバイスで読み取ることができます。

個人用 RMS では、Azure Active Directory のセルフサービス サインアップが使用されます。 ユーザーがこのサブスクリプションを使用して組織のアカウントを作成していた場合は、組織の管理者として、ユーザーのアカウントの所有権を要求し、[アカウントを制御する](/azure/active-directory/users-groups-roles/domains-admin-takeover#external-admin-takeover)ことができます。 

この無料アカウントにサインアップするには、[Microsoft Azure Information Protection のページ](https://aka.ms/rms-signup)に移動して、仕事用メール アドレスを指定します。 ユーザーは、Microsoft からの応答メールを受信したら、アカウントの作成に必要な詳細情報を入力してサインアップ プロセスを完了できます。 

アカウントが作成されると、各種デバイス用の Azure Information Protection クライアントまたはビューアーをダウンロードするためのリンク、ユーザー ガイドへのリンク、Rights Management による保護をネイティブでサポートするアプリケーションの最新の一覧へのリンクが、最終ページに表示されます。 

### <a name="alternatives-use-office-365-message-encryption-or-microsoft-accounts"></a>代替手段: Office 365 メッセージ暗号化または Microsoft アカウントを使用する

個人用 RMS は、組織外の承認されたユーザーが、組織が保護しているファイルを常に読み取ることができるようにするための1つのオプションです。 

代替オプションは次のとおりです。

- **[Office 365 Message Encryption と新機能](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)を使用して、ドキュメントを電子メールで送信します。** 電子メールによるこのソリューションは、あらゆるデバイスのあらゆる電子メール アドレスに対して利用できます。組織外の人と、ブラウザーで安全に情報を共有し、Office ドキュメントを確認することができる、お勧めの方法です。
 
- **Microsoft アカウントを使用します。** 認証に Microsoft アカウントが使用されている場合、保護されたコンテンツを開くことができないアプリケーションもあります。 [詳細情報](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents) 


## <a name="to-sign-up-for-rms-for-individuals"></a>個人用 RMS にサインアップするには

1. Windows または Mac のコンピューター、またはモバイル デバイスを使用して [Microsoft Azure Information Protection のページ](https://aka.ms/rms-signup)にアクセスします。

2. 開く必要があるドキュメントを保護するのに使用された電子メール アドレスを入力します。

3. **[サインアップ]** をクリックします。

    Microsoft では、ユーザーの電子メール アドレスを使用して、組織が既に [Azure Information Protection Premium のサブスクリプション](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing)、または [Azure Information Protection を使用したデータ保護を含む Office 365 サブスクリプション](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)を利用しているかどうかを確認します。 これらのサブスクリプションのいずれかが見つかったら、個人用 RMS は必要ありません。 すぐにサインインが行われ、個人用 RMS のセルフ サービス サインアップはキャンセルされます。 これらのサブスクリプションのいずれも見つからない場合は、次の手順に進みます。

4. 入力したアドレスに確認の電子メール メッセージが届くまで待ちます。 これは Microsoft 365 チーム () からのものであり、 support@email.microsoftonline.com サブジェクトが **Microsoft Azure Information Protection の** サインアップを完了しています。

5. このメールが届いたら、[**はい、私です**] をクリックすると電子メール アドレスが確認されたことになり、サインアップ プロセスが完了します。

6. [**最後に...**] というページが表示され、アカウントの詳細情報を入力できるようになります。 氏名とパスワードを入力し、パスワードを確認のため再入力してから [**開始**] をクリックします。

7. アカウントが作成されると、Microsoft Azure Information Protection の新しいページが表示されます。ここで、Azure Information Protection クライアントをダウンロードしてインストールすることができます。また、[ユーザー ガイド](./rms-client/client-user-guide.md) リンクをクリックして、Windows コンピューター用の操作手順を表示することができます。

これでアカウントが作成されたので、保護されたファイルを読み取るためにサインインを求められた場合は、個人用 RMS のアカウントを作成するときに指定したものと同じ電子メール アドレスとパスワードを入力します。

> [!IMPORTANT]
> このアカウントを使用してファイルを保護することもできるようになりましたが、組織が Azure Information Protection の[試用版または有料サブスクリプション](https://azure.microsoft.com/pricing/details/information-protection/)を取得するまでは実行しないでください。 この無料サブスクリプションを使用してファイルや電子メールを保護した後で、組織がアカウントを制御した場合、前に保護したコンテンツにアクセスできなくなる可能性があります。


## <a name="next-steps"></a>次のステップ
個人用 RMS は、Azure Active Directory でサポートされているセルフサービスサインアップ機能を使用する例です。 この機能の動作の詳細については、Azure Active Directory のドキュメントの「 [Azure Active Directory のサインアップ Self-Service](/azure/active-directory/users-groups-roles/directory-self-service-signup) について」を参照してください。

