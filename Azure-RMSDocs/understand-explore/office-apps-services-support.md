---
title: Office のアプリとサービスが AIP から Azure RMS をサポートするしくみ
description: Word や Outlook などのエンド ユーザー Office アプリケーションと Exchange や SharePoint などの Office サービスで AIP から Azure Rights Management サービスを使用し、組織のデータを保護するしくみ。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: be1c41c2f17720d522770f9e023c7468602ceb67
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="how-office-applications-and-services-support-azure-rights-management"></a>Office のアプリケーションとサービスが Azure Rights Management をサポートするしくみ 

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

エンド ユーザー Office アプリケーションと Office サービスで Azure Information Protection から Azure Rights Management サービスを使用し、組織のデータを保護できます。 これらの Office アプリケーションは Word、Excel、PowerPoint、および Outlook です。 Office サービスは Exchange および SharePoint です。 Azure Rights Management サービスをサポートする Office 構成では、多くの場合、**IRM (Information Rights Management)** という用語が使用されます。

## <a name="office-applications-word-excel-powerpoint-outlook"></a>Office アプリケーション:Word、Excel、PowerPoint、Outlook
これらのアプリケーションは Azure Rights Management をネイティブでサポートし、ユーザーは保存済みのドキュメントまたは送信する電子メール メッセージに保護を適用できます。 ユーザーはテンプレートを適用して保護を適用できます。 あるいは、Word、Excel、PowerPoint の場合、アクセス、権限、使用制限にカスタマイズ設定を選択できます。 

たとえば、組織内の人だけがアクセスできるように Word 文書を設定できます。 あるいは、Excel スプレッドシートを編集可能にしたり、読み取り専用にしたり、印刷禁止にするかどうかを制御できます。 時間が重要なファイルの場合、ファイルにアクセスできなくなる有効期限を構成できます。 この構成はユーザーが直接行うか、テンプレートを適用して行うことができます。 Outlook の場合、ユーザーは、**[転送不可]** オプションを選択して、データの漏えいを防ぐこともできます。

これらのアプリケーションでは、Azure Rights Management のネイティブ Office サポートに加え、[Azure Information Protection クライアント](../rms-client/aip-client.md)と共にインストールされる Azure Information Protection バーもサポートされます。 このバーにはラベルが表示されます。これにより、ユーザーは機密データを含むドキュメントや電子メールに保護をより簡単に自動で適用することができます。

Office アプリと Azure Information Protection クライアントを構成する用意ができている場合:

- Office アプリを構成するには、「[Office アプリ: クライアントの構成](../deploy-use/configure-office-apps.md)」を参照してください。

- Azure Information Protection クライアントをインストールして構成するには、「[Azure Information Protection クライアント: クライアントのインストールと構成](../deploy-use/configure-client.md)」を参照してください。

## <a name="exchange-online-and-exchange-server"></a>Exchange Online と Exchange Server
Exchange Online または Exchange Server を使用するとき、Azure Rights Management をサポートする IRM (Information Rights Management) オプションを構成できます。 この構成では、Exchange は次の保護ソリューションを提供します。

-   **Exchange ActiveSync IRM** 。モバイル デバイスで、保護された電子メール メッセージを保護および使用することができます。

-   **Outlook on the web** の電子メール保護サポート。Outlook クライアントと同様に実装されます。 この構成では、テンプレートの利用により、あるいは個々のオプションを指定することでユーザーはメール メッセージを保護できます。 ユーザーは、自分に送信された保護メールのメッセージを読み、利用できます。

-   Outlook クライアントの**保護ルール**。保護テンプレートが特定受信者の電子メール メッセージに自動的に適用されるように管理者が構成します。 たとえば、社内電子メールが法務部門に送信されるときに、法務部門の所属者のみが読むことが可能で、ただし転送できないようにすることができます。 送信前に電子メール メッセージに保護が適用されたことがユーザーに表示され、既定では、ユーザーは不要と判断した場合にこの保護を削除できます。 電子メールは送信される前に暗号化されます。 詳細については、Exchange ライブラリの「[Outlook の保護ルール](https://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx)」および「[Outlook 保護ルールを作成する](https://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx)」を参照してください。

-   **トランスポート ルール**。保護テンプレートが電子メール メッセージに自動的に適用されるように管理者が構成します。 ルールの基盤は送信者、受信者、メッセージの件名、内容などのプロパティになります。 ルールは概念上、保護ルールに似ていますが、ユーザーは保護を削除できません。 Outlook on the web とモバイル デバイスにより送信されるメールに適用できます。 また、クライアントから送信される前にメール メッセージが暗号化されることはありません。 詳細については、Exchange ライブラリの「[トランスポート保護ルールを作成する](https://technet.microsoft.com/library/dd302432.aspx)」を参照してください。

-   **データ損失防止 (DLP) ポリシー** 。このポリシーは、電子メール メッセージにフィルターを適用するための条件のセットを含み、機密コンテンツのデータの損失を防ぐために役立つ操作を実行します。 機密コンテンツには、たとえば、個人情報やクレジット カード情報があります。 ポリシーのヒントを使用すると、機密データが検出されたときに、保護の適用が必要な可能性があることをユーザーに警告できます。 詳細については、Exchange ライブラリの「[データ損失防止](https://technet.microsoft.com/library/jj150527(v=exchg.160\).aspx)」を参照してください。

-   **Office 365 Message Encryption** では、保護されているメール メッセージと保護されている Office ドキュメントを添付ファイルとしてあらゆるデバイスであらゆるアドレスに送信できます。 Azure AD を使用しないユーザー アカウントの場合、インターネットがあれば、ソーシャル ID プロバイダーやワンタイム パスコードを利用できます。 詳細については、Office Web サイトの「[Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)」 (Azure Information Protection 上に構築される新しい Office 365 メッセージの暗号化機能の設定) を参照してください。

オンプレミスで Exchange を使用している場合、Azure Rights Management コネクタを展開し、IRM 機能と Azure Rights Management サービスを利用できます。 このコネクタはオンプレミス サーバーと Azure Rights Management サービスの間のリレーとして機能します。

Exchange の IRM を構成する用意ができている場合:

- Exchange Online については、「[Exchange Online: IRM 構成](../deploy-use/configure-office365.md#exchange-online-irm-configuration)」を参照してください。

- Exchange On-Premises については、「[Azure Rights Management コネクタをデプロイする](../deploy-use/deploy-rms-connector.md)」を参照してください。


## <a name="sharepoint-online-and-sharepoint-server"></a>SharePoint Online と SharePoint Server

SharePoint Online または SharePoint Server を使用するとき、SharePoint IRM (Information Rights Management) でドキュメントを保護できます。 この機能では、管理者がリストやライブラリを保護できます。ユーザーが文書をチェックアウトしたときに、指定した情報保護ポリシーに従って許可されたユーザーのみがファイルを表示および使用できるようにダウンロードされたファイルが保護されます。 たとえば、ファイルが読み取り専用のときに、テキストのコピーを無効にし、ローカル コピーの保存やファイルの印刷を防止することができます。

Word、PowerPoint、Excel、PDF ドキュメントがこの SharePoint IRM 保護に対応しています。 既定では、保護はドキュメントをダウンロードした人に限定されます。 SharePoint でドキュメントにアクセスできるすべてのユーザー、または指定したグループに保護を拡張できる構成オプションを使用すれば、この既定を変更できます。

SharePoint のリストとライブラリについては、この保護は常にエンド ユーザーではなく管理者によって構成されます。 アクセス許可はサイト レベルで設定します。そのようなアクセス許可は、既定では、そのサイトのリストまたはライブラリにより継承されます。 SharePoint Online を使用する場合、ユーザーは OneDrive for Business ライブラリの IRM 保護も構成できます。

さらに細かく制御するには、サイトのリストまたはライブラリを構成し、親からアクセス許可を継承することを停止できます。 その後、そのレベル (リストまたはライブラリ) で IRM アクセス許可を構成できます。構成後、アクセス許可は "固有のアクセス許可" と呼ばれます。 ただし、アクセス許可は常にコンテナー レベルで設定されます。個々のファイルにアクセス許可を設定することはできません。 

最初に SharePoint の IRM サービスを有効にする必要があります。 次に、ライブラリの IRM アクセス許可を指定します。 SharePoint Online と OneDrive for Business の場合、ユーザーは OneDrive for Business ライブラリに対しても IRM アクセス許可を指定できます。 SharePoint は権限ポリシー テンプレートを使用しませんが、テンプレートに指定できるいくつかの設定と同じ設定を SharePoint の構成で選択できます。

SharePoint Server を使用する場合、Azure Rights Management コネクタをデプロイすることでこの IRM 保護を使用できます。 このコネクタはオンプレミス サーバーと Rights Management クラウド サービスの間のリレーとして機能します。 詳細については、「[Azure Rights Management コネクタをデプロイする](../deploy-use/deploy-rms-connector.md)」を参照してください。

> [!NOTE]
> 現在のところ、SharePoint IRM を使用するとき、いくつかの制限があります。
> 
> - Azure ポータルで管理する既定のテンプレートまたはカスタム テンプレートを使用できません。 
> 
> - ファイル名拡張子が保護された PDF ファイルのための .ppdf であるファイルはサポートされていません。 ファイル名拡張子が .pdf で、Rights Management がネイティブで保護しているファイルは、Rights Management をネイティブでサポートする PDF リーダーを使用する場合にサポートされます。
> 
> - 共同編集はサポートされていません。 IRM で保護されたライブラリ内のドキュメントをチェックアウトし、ダウンロードする必要があるため、ファイルは一度に 1 人のユーザーしか編集できません。

IRM で保護されていないライブラリについては、SharePoint または OneDrive にアップロードするファイルを保護する場合、そのファイルは共同編集、Office Online、検索、ドキュメント プレビュー、サムネイル、電子情報開示、データ損失防止 (DLP) で使用できません。

SharePoint IRM 保護を使用する場合、Azure Rights Management サービスは、ドキュメントが SharePoint からダウンロードされる際には使用制限およびデータ暗号化を適用し、ドキュメントが最初に SharePoint で作成される場合、またはライブラリにアップロードされる際には適用しません。 ドキュメントをダウンロードする前に保護する方法については、SharePoint ドキュメントの「[OneDrive for Business および SharePoint Online のデータ暗号化](https://technet.microsoft.com/library/dn905447.aspx)」をご覧ください。

新しい投稿ではありませんが、「[What’s New with Information Rights Management in SharePoint and SharePoint Online](https://blogs.office.com/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/)」 (SharePoint の Information Rights Management と SharePoint Online の新機能) という Office ブログの投稿に追加情報があります。

SharePoint の IRM を構成する用意ができている場合:

- SharePoint Online については、「[SharePoint Online と OneDrive for Business: IRM 構成](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)」を参照してください。

- Sharepoint Server の詳細については、「[Azure Rights Management コネクタをデプロイする](../deploy-use/deploy-rms-connector.md)」を参照してください。


## <a name="next-steps"></a>次の手順

Office 365 をお持ちの場合、「[Office 365 のファイル保護ソリューション](https://technet.microsoft.com/library/dn919927.aspx#BKMK_O365fileprotect)」をご覧になることをお勧めします。Office 365 のファイルを保護するための推奨機能を説明しています。

他のアプリケーションおよびサービスで Azure Information Protection からの Azure Rights Management サービスをサポートする方法については、「[アプリケーションによる Azure Rights Management サービスのサポート](applications-support.md)」をご覧ください。

アプリケーションとサービスの構成など、デプロイを開始する用意ができたら、「[Azure Information Protection デプロイ ロードマップ](../plan-design/deployment-roadmap.md)」を参照してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]