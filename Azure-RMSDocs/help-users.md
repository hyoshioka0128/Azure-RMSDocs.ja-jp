---
title: Azure RMS を使用してユーザーによるファイル保護を支援する - AIP
description: Azure Information Protection から Azure Rights Management サービスをデプロイして構成した後に、ユーザー、管理者、ヘルプ デスクにヘルプとガイダンスを提供するための情報です。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 58f9a6ff-4121-4c8c-9865-1bb290604ad2
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 669764881af477e19ffcf9d63266fe19e1f26f92
ms.sourcegitcommit: 319c0691509748e04aecf839adaeb3b5cac2d2cf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "71683578"
---
# <a name="helping-users-to-protect-files-by-using-the-azure-rights-management-service"></a>Azure Rights Management サービスを利用したファイルの保護でユーザーを支援するヘルプ

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection を組織に合わせてデプロイして構成したら、ユーザー、管理者、およびヘルプ デスクにヘルプおよびガイダンスを提供します。

-   **エンド ユーザー情報**
    
    機密情報が含まれるドキュメントおよび電子メールを保護する方法とタイミングについて知らせます。 ユーザーが新しいプロセスを導入するのではなく、既に理解しているプロセスに対して追加の手順を組み込むことができるように、可能な限り、既存のワークフローに対してこの情報を提供します。 組織のビジネスに固有のメリット (およびリスク) を知らせ、どのようなときにファイルおよび電子メールを保護する必要があるかについてのガイダンスを提供します。 [テンプレート](configure-policy-templates.md)を構成した場合、ユーザーがテンプレートの名前と説明だけでは適切なテンプレートを選択できないときにどのテンプレートを選択すればよいのかについてのガイダンスを提供します。
    
    > [!TIP]
    > エンドユーザー向けの例示ビデオ:
    > -   [Microsoft Azure Information Protection](https://youtu.be/ToShAUdlrPo?list=PL8nfc9haGeb6qSm1kLU8n3Zqg398764h5)
    > -   [Azure RMS のドキュメントの追跡と取り消し](https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation)

-   **管理者情報**
    
    一部のアプリケーションは、管理者が構成したポリシーおよび設定を使用して、情報保護を自動的に適用します。 これらのアプリケーションの場合、これらのアプリケーションおよびサービスを管理する他の管理者に対して指示を提供する必要があります。 
    
    詳細については、[「アプリケーションによる Azure Rights Management サービスのサポート](applications-support.md)」と「[Azure Rights Management サービス用にアプリケーションを構成する](configure-applications.md)」を参照してください。
    
-   **ヘルプ デスク情報**
    
    ユーザーが Azure Information Protection クライアントを持っている場合、ヘルプ デスクはユーザーに、特定のエディションの Office で保護がサポートされているかどうか、および現在のサインインしているユーザーのアカウントの情報などについて、 **[ヘルプとフィードバック]** オプションを利用するように依頼します。 また、このオプションを利用し、ログ ファイルを収集したり、クライアントをリセットしたりできます。 詳細については、管理者ガイドの「[インストールのチェックとトラブルシューティング](./rms-client/client-admin-guide.md#installation-checks-and-troubleshooting)」を参照してください。
    
    保護されたドキュメントに対する完全な権限を持つ正当な要求がある場合は、Azure Information Protection[スーパーユーザー機能](configure-super-users.md)を使用して、ヘルプデスクにこのアクセスを要求するプロセスがあることを確認してください。 正当な要求とは、たとえば、従業員が組織を去った後の法務部門や管理者からの要求です。
    
    また、ユーザーから報告される可能性がある典型的な問題には、以下のようなものがあります。
    
    - **サインイン ヘルプ**
        
        Azure Rights Management サービスがユーザーを認証するときにキャッシュされた資格情報を使用できない場合、資格情報の入力を要求される場合があります。 通常、必要な資格情報は、Office 365 テナントまたは Azure Active Directory テナントに関連付けられている、ユーザーの企業または学校のアカウントとパスワードです。 Azure Rights Management サービスでは Azure AD アカウントを認証できますが、Microsoft アカウントが認証に使用されている場合は、一部のアプリケーションでも、保護されたコンテンツを開くことができます。 [詳細情報](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents) 
        
        Azure Rights Management サービスを使用するアプリケーションを実行しているときに資格情報を要求された場合、どのアカウントを使用すればいいのかについてユーザーとヘルプ デスクにガイダンスを提供します。
        
    - **コンテンツの保護または使用に関する問題**
        
        使用するアプリケーションに対する適切な指示をユーザーが受けていること、また、ユーザーが Azure Rights Management サービスでサポートされているアプリケーションとデバイスを使用していることを確認します。 サポートされているアプリケーションとデバイスの詳細については、「 [Azure Information Protection の要件](requirements.md)」を参照してください。
        
        特定のユーザーまたはグループによる、保護されたコンテンツの保護や使用を Azure Active Directory によって承認できることを確認するには、[Azure Information Protection 向けのユーザーとグループの準備](prepare.md)の検証チェックを使用します。
        
        保護されたコンテンツを開くことはできるが必要な権限を持っていないという報告がユーザーからあった場合、そのユーザーが Rights Management テンプレート用に構成された正しいグループに含まれていないことが問題である可能性があります。 または、そのユーザーまたはグループに[テンプレートの再構成が必要である](configure-policy-templates.md)という問題の場合があります。 
        
        ユーザーの持つ権限が想定通りでない場合は、[使用権限テーブル](configure-usage-rights.md#usage-rights-and-descriptions)で権限に関する説明とアプリケーション固有の実装について確認してください。

次のセクションでは、ドキュメントと電子メールを保護する際に役立つアプリケーション固有の情報を示します。

## <a name="using-information-protection-with-the-azure-information-protection-client"></a>Azure Information Protection クライアントでの情報保護の使用

ユーザーが Office 2010 を使用している場合は、保護されたドキュメントと電子メールを保護および使用するために、Azure Information Protection クライアントが必要です。 ただし、Azure Information Protection クライアントも、このサービスをサポートするすべてのコンピューターとモバイル デバイスに推奨されています。

Azure Information Protection クライアントを使用すると、ユーザーがドキュメントと電子メールを簡単に保護できるだけでなく、保護したドキュメントをユーザー自身で追跡できます。 また、過去に承認済みのユーザーが追跡対象のドキュメントにアクセスする必要がない場合は、そのドキュメントを無効にすることもできます。

この Windows コンピューター用クライアントを使用する手順については、「[Azure Information Protection クライアント ユーザー ガイド](./rms-client/client-user-guide.md)」を参照してください。


## <a name="using-information-protection-with-office365-office-2019-office-2016-or-office2013"></a>Office 365、Office 2019、Office 2016、または Office 2013 での情報保護の使用
Azure Rights Management サービスを使用していて、Azure Information Protection クライアントをインストールしていない場合、Office デスクトップ アプリに Azure Information Protection バーが表示されません。 リボンには **[保護]** ボタンが表示されず、エクスプローラーに **[分類して保護する]** も表示されません。 これらの追加によって、ユーザーはドキュメントと電子メールを簡単に保護できます。 これらのユーザーについては、次のような手順に従う必要があります。

> [!TIP]
> これらのアプリケーションで情報保護を使用するためのアプリケーション固有のヘルプおよび手順を見つけるには、**IRM**、アプリケーションの名前、およびアプリケーションのバージョンを検索します。

#### <a name="to-protect-a-document-in-wordfrom-office-365-proplus"></a>Office 365 ProPlus の Word でドキュメントを保護するには

1.  Microsoft Word で、ドキュメントを作成します。

2.  **[ファイル]** メニュー: **[情報]**  >  **[文書の保護]**  >   **[アクセスの制限]** 。

3. テンプレートを選択して適切な使用権限をすぐに適用するか、 **[アクセスの制限]** を選択して使用権限を自分で選択します。

    > [!NOTE]
    > お使いのコンピューターで Rights Management を以前使用したことがない場合、 **[アクセスの制限]** オプションは Azure Rights Management サービスに接続を行い、ユーザーは Office IRM クライアントの構成に使用する資格情報の入力を求められます。 それからテンプレートまたは使用権限を選択できます。

3.  ファイルを保存します。

他のユーザーがドキュメントを開いている場合、それらのユーザーが最初に認証されます。 ドキュメントを開く権限がない場合、ドキュメントは開きません。 ドキュメントを開く権限がある場合は、そのユーザーに対して指定された制限付き[使用権限](configure-usage-rights.md)でドキュメントが開きます。 

たとえば、使用権限が "表示のみ" の場合、ユーザーは別の場所にコピーした場合でもドキュメントを編集または保存できません。 

使用権限は、制限バナーを使用してドキュメントの上部に表示されます。 このバナーには、ドキュメントに適用されるアクセス許可やそれらを表示するためのリンクが表示される場合があります。

#### <a name="to-protect-an-email-message-using-outlookfrom-office-365-proplus-connecting-to-exchange-online"></a>Exchange Online に接続し、Office 365 ProPlus の Outlook を使ってメール メッセージを保護するには、

1.  Outlook で、組織内の受信者宛ての電子メール メッセージを作成します。

2.  **[オプション]** タブ: **[アクセス許可]** > オプションを選択します。 以下に例を示します。 **[転送不可]** 、 **[\<会社名>- 社外秘]** 、 **[\<会社名> - 社外秘、表示のみ]** 。

3.  メッセージを送信します。

保護された文書を表示するのと同様に、受信者が保護された電子メール メッセージを開くと、最初に認証されます。 電子メール メッセージを参照する権限が与えられると、そのユーザーに対して指定された制限付き[使用権限](configure-usage-rights.md)でメッセージが開きます。 

たとえば、電子メール メッセージが **[転送不可]** オプションを使用して保護されている場合、リボンの転送ボタンは使用できません。

#### <a name="to-protect-an-email-message-using-outlook-on-the-web"></a>Outlook on the web を使用して電子メール メッセージを保護するには

1. Outlook on the web で、組織内の受信者宛ての電子メール メッセージを作成します。

2. **[保護]** を選択します。 管理者によって既定値が変更されていない限り、 **[転送不可]** オプションが自動的に選択されます。 既定値を変更する場合は、 **[アクセス許可の変更]** を選択し、ドロップダウンからオプションを選択します。 以下に例を示します。 **[暗号化]** または **[\<会社名> - 社外秘]** 。

3. メッセージを送信します。

保護された文書を表示するのと同様に、受信者が電子メール メッセージを開くと、最初に認証されます。 電子メール メッセージを参照する権限が与えられると、そのユーザーに対して指定された制限付き[使用権限](configure-usage-rights.md)でメッセージが開きます。 

たとえば、既定の **[転送不可]** オプションを使う場合、メッセージ ウィンドウの **[転送]** オプションは使用できません。
