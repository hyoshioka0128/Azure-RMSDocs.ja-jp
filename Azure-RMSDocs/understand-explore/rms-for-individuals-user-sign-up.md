---
title: "個人用 RMS にサインアップする方法 | Azure Information Protection"
description: "この無料アカウントのサインアップ手順、およびこのプロセスがどのように機能するかについての技術情報です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a60731bd-f78d-4f00-bb3e-354637b312ab
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: 82f59842420667c5ad28a6704c9df0d26043d50c


---

# <a name="how-users-sign-up-for-rms-for-individuals"></a>個人用 RMS にサインアップする方法

>*適用対象: Azure Information Protection*

この無料アカウントにサインアップするには、[Microsoft Azure Information Protection のページ](https://portal.office.com/signup?sku=rms&ru=https%3A%2F%2Fportal.azurerms.com%2F%23%2Fdownload)にアクセスし、職場のメール アドレスを入力してリクエストを送信します。 このサインアップ ページは一般的に、受信した電子メール メッセージに保護された添付ファイルが付いている場合に、そのメールに記載されたサインアップ方法に従ってアクセスされるものです。 Microsoft からの応答メールを受信したら、アカウントの作成に必要な詳細情報を入力してサインアップ プロセスを完了できます。 これが完了したときに表示されるページから、各種デバイス用の共有アプリケーションをダウンロードできます。このページには他にも、ユーザー ガイドへのリンクや、Rights Management による保護をネイティブでサポートするアプリケーションの最新の一覧へのリンクもあります。 

## <a name="to-sign-up-for-rms-for-individuals"></a>個人用 RMS にサインアップするには

1.  Windows または Mac のコンピューター、またはモバイル デバイスを使用して [Microsoft Azure Information Protection のページ](https://portal.office.com/signup?sku=rms&ru=https%3A%2F%2Fportal.azurerms.com%2F%23%2Fdownload)にアクセスします。

2.  組織で使用している電子メール アドレス (**janetm@contoso.com** または **p.dover@fabrikam.com** など) を入力します。

    > [!IMPORTANT]
    > 個人用の電子メール アカウントはサポートされていないため、Microsoft アカウント (以前の Microsoft Live ID アカウント) や、自宅で使用するインターネット プロバイダーから提供されている他の個人アカウントは入力しないてください。

3.  [**サインアップ**] をクリックします。

    Microsoft では、ユーザーの電子メール アドレスを使用して、[Azure Information Protection の有料サブスクリプション](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing)、または [Azure Resource Manager を使用したデータ保護を含む Office 365 サブスクリプション](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)をユーザーの組織が既に利用しているかどうかを確認しています。 組織が所有している場合、個人用 RMS は必要ないので、すぐにサインインされ、個人用 RMS へのセルフサービス サインアップは取り消されます。 有料のサブスクリプションが見つからない場合は、次の手順に進みます。

4.  入力したアドレスに確認の電子メール メッセージが届くまで待ちます。 このメールの差出人は Office 365 チーム ((support@email.microsoftonline.com)) で、件名は "**Finish signing up for Microsoft Azure Information Protection**" (Microsoft Azure Information Protection のサインアップ完了) です。

5.  このメールが届いたら、[**はい、私です**] をクリックすると電子メール アドレスが確認されたことになり、サインアップ プロセスが完了します。

6.  [**最後に...**] というページが表示され、アカウントの詳細情報を入力できるようになります。 氏名とパスワードを入力し、パスワードを確認のため再入力してから [**開始**] をクリックします。

7. アカウントが作成されると、新しい Microsoft Rights Management ページが表示され、ここから共有アプリケーションをダウンロードしてインストールできます。このページの [[詳細](../rms-client/sharing-app-user-guide.md)] リンクをクリックして、共有アプリケーションのユーザー ガイドを読むこともできます。

アカウントの作成が完了しました。ファイルの保護を開始したり、他のユーザーが保護しているファイルを読み取ったりすることができます。 ファイルを保護するときや保護されたファイルを読み取るときにサインイン画面が表示された場合は、個人用 RMS のアカウントを作成するときに指定したものと同じ電子メール アドレスとパスワードを入力します。

## <a name="technical-overview-of-the-signup-process"></a>サインアップ プロセスの技術概要
個人用 RMS では、ユーザーの認証に Microsoft のクラウド ベースの技術を使用するその他のサービスによって使用される、セルフサービスのサインアップ プロセスが使用されます。

組織が Office 365 サブスクリプションまたは Azure サブスクリプションを保有していない場合にユーザーが個人用 RMS にサインアップすると、Azure にユーザーを認証するディレクトリがなく、バックグラウンドでは次が発生します。

1.  組織の最初のユーザーが個人用 RMS のサブスクリプションを要求すると、入力された電子メール アドレスのドメイン名が、Azure テナントに既に関連付けられているかどうかがチェックされます。 既存のテナントが存在しない場合は、組織用の新しいテナントと Azure ディレクトリが自動的に作成されます。このとき、この最初のユーザーのアカウントも作成されます。 Azure の有料サブスクリプションとは異なり、この最初のアカウントはグローバル管理者ではなく、標準ユーザーになります。 新しいアカウントでは、ユーザーが指定した電子メール アドレスとパスワードが使用されます。

    > [!NOTE]
    > ディレクトリの作成には使用できないドメイン名が一部あり、それらは個人用 RMS では使用できません。

    既存のテナントが見つかった場合は、そのテナントが調べられ、Azure RMS のサブスクリプションを既に持っているかどうかが確認されます。 サブスクリプションが見つからない場合は、無料の個人用 RMS サブスクリプションを追加できます。

2.  組織には、個人用 RMS のサブスクリプションが付与されます。 これで、そのユーザーは、Azure によって認証されるようになり、Azure Rights Management を使用してファイルを保護するとともに、他のユーザーが保護しているファイルを読み取ることができるようになります。 ファイルの保護や保護されたファイルの読み取りを行うには、無料の [Rights Management 共有アプリケーション](../rms-client/sharing-app-windows.md)など、RMS 対応アプリケーションを用意する必要があります。

3.  同じ組織に属する 2 人目のユーザーが個人用 RMS サブスクリプションを要求すると、組織の個人用 RMS サブスクリプションを使用して、既に作成済みの Azure ディレクトリに新しいユーザー アカウントが追加されます。 この 2 人目のユーザーは、最初のユーザーが実行できるすべての操作を実行できます (ファイルの保護と保護されたファイルの読み取り)。さらに、これらの 2 人のユーザーは既定のテンプレートをファイルに即座に適用して、組織の Azure ディレクトリのアカウントにアクセス制限を適用することができるため、セキュリティで保護された共同作業を簡単に行えるようになります。

4.  同じ組織に属する以降のユーザーも同様のパターンに従い、組織の Azure ディレクトリに (新しいユーザーがサインアップすると) ユーザー アカウントが追加されます。 ディレクトリに多数のアカウントが追加されると、より多くのユーザーが同僚やパートナーとセキュリティで保護された共同作業を行うことができ、承認されていないユーザーがファイルにアクセスすべきでない場合に、そのファイルを読み取れないように簡単に設定できます。

このプロセス全体を通じて、組織に対して料金が発生することはなく、IT 部門による作業も不要です。 ただし、IT 部門は次のいずれかを行うことを選択できます。

-   **アカウントおよびサインアップ プロセスを管理する**: IT 管理者は、Azure に自動作成されたディレクトリとアカウントの所有権を取得できます。 パスワード同期やシングル サインオンなどのディレクトリ統合ソリューションを実装して、アカウントを管理できます。 または、ユーザーがアカウントの作成または個人用 RMS へのサインアップを行えないようにすることもできます。

    詳細については、「[個人用 RMS 向けに作成されたアカウントを管理者が制御する方法](rms-for-individuals-take-control.md)」を参照してください。

-   **Rights Management の管理**:IT 管理者は、組織の個人用 RMS サブスクリプションを、Azure Rights Management を含む有料サブスクリプションに変換できます。 この処理を行うと、既存の Azure ディレクトリとアカウントを保持しつつ、個人用 RMS を使用していた既存ユーザーをシームレスに移行することができます。 以前に保護していたすべてのファイルは、引き続き同じポリシーで保護され、ファイルの使用権限を付与されているユーザーは同じ方法でファイルを使用できます。

    この手順を選択すると、組織のワークフロー、サービス、およびデータ ストアに Rights Management を統合できるという利点があります。 さらに、組織の Azure Rights Management 用テナント キーを制御できるため、Rights Management を管理できるようになります。 以下を行うことができます。

    -   Exchange や SharePoint がオンプレミスで実行されている場合でも、Azure Rights Management をサポートするように構成できます。 Exchange と SharePoint はオンライン サービスでネイティブにサポートされており、オンプレミス サーバーのコネクタでもサポートされています。 詳細については、以下を参照してください。

        -   「[Office 365: Configuration for clients and online services (Office 365: クライアントとオンライン サービスの構成)](../deploy-use/configure-office365.md)」の Exchange Online と SharePoint Online に関するセクションを参照してください。

        -   [Azure Rights Management コネクタをデプロイする](../deploy-use/deploy-rms-connector.md)

    -   会社が所有するデータの電子情報開示を実行し、必要に応じて、Rights Management を使用して保護されているファイルの暗号化を解除できます。 詳細については、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../deploy-use/configure-super-users.md)」を参照してください。

    -   組織で使用された Rights Management のアクティビティをすべてログに記録できます。 この機能は非常に有用であり、保護されたファイルの監視や、それらのファイルに正常にアクセスしているユーザーの監視だけでなく、未承認のユーザーが保護されたファイルへのアクセスを試行している不審な行為を特定することもできます。 詳細については、「[Azure Rights Management サービスの使用状況をログに記録して分析する](../deploy-use/log-analyze-usage.md)」を参照してください。

    -   保護されたドキュメントの追跡および取り消しの機能が [Azure RMS サブスクリプション](https://technet.microsoft.com/dn858608)でサポートされている場合、ユーザーはそれらの機能を使用できます。 詳細については、「[RMS 共有アプリケーション ユーザー ガイド](../rms-client/sharing-app-user-guide.md)」の「[RMS 共有アプリケーションを使用してドキュメントを追跡および取り消す](../rms-client/sharing-app-track-revoke.md)」を参照してください。

    -   BYOK (Bring Your Own Key) ソリューションを実装して、組織の IT ポリシーに従って Azure Rights Management のテナント キーをオンプレミスで生成し、そのキーをハードウェア セキュリティ モジュール (HSM) を使用して Microsoft に安全に転送することができます。 詳細については、「[Azure Information Protection テナント キーを計画して実装する](../plan-design/plan-implement-tenant-key.md)」を参照してください。


## <a name="next-steps"></a>次のステップ
「[個人用 RMS 向けに作成されたアカウントを管理者が制御する方法](rms-for-individuals-take-control.md)」を参照してください。





<!--HONumber=Nov16_HO2-->


