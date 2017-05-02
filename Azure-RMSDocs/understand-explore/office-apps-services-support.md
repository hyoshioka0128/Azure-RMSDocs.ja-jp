---
title: "Azure Information Protection を使用した Office アプリとサービス"
description: "エンド ユーザー Office アプリケーション (Word、Excel、PowerPoint、Outlook など) と Office サービス (Exchange、SharePoint など) で Azure Rights Management サービスを使用して、組織のデータを保護する方法について説明します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/21/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 5c106d46befc2a2d3c42ba8840dac65a243220d9
ms.sourcegitcommit: 9edcb4a55a331e02f999c78d97eb0beb21f96f07
translationtype: HT
---
# <a name="office-applications-and-services"></a>Office アプリケーションおよびサービス

>*適用対象: Azure Information Protection、Office 365*

エンド ユーザー Office アプリケーション (Word、Excel、PowerPoint、Outlook など) と Office サービス (Exchange、SharePoint など) で、Azure Information Protection から Azure Rights Management サービスを使用して、組織のデータを保護することができます。

## <a name="office-applications-word-excel-powerpoint-outlook"></a>Office アプリケーション:Word、Excel、PowerPoint、Outlook
これらのアプリケーションでは、Information Rights Management (IRM) を使用することで Rights Management がネイティブでサポートされ、ユーザーは保存済みドキュメントまたは送信される電子メール メッセージに保護を適用できます。 ユーザーは、テンプレートを適用するか、Word、Excel、PowerPoint の場合にはアクセス、権限、および使用制限の細かくカスタマイズされた設定を選択できます。 

たとえば、ユーザーは、組織内のユーザーのみがアクセスできるように Word 文書を構成することも、Excel スプレッドシートの編集の可否、読み取り専用への制限、印刷防止などを制御することもできます。 時間が重要なファイルの場合、ファイルにアクセスできなくなる有効期限を (ユーザーが直接またはテンプレートの適用により) 構成できます。 Outlook の場合、ユーザーは、テンプレートを選択できるだけでなく、[**転送不可**] オプションを選択して、データの漏えいを防ぐこともできます。

これらのアプリケーションでは、IRM のネイティブ サポートに加え、[Azure Information Protection クライアント](../rms-client/aip-client.md)と共にインストールされる Azure Information Protection バーもサポートされます。 このバーにはラベルが表示されます。これにより、ユーザーは機密データを含むドキュメントや電子メールに Rights Management 保護をより簡単に自動で適用することができます。

Office アプリと Azure Information Protection クライアントを構成する用意ができている場合:

- Office アプリを構成するには、「[Office アプリ: クライアントの構成](../deploy-use/configure-office-apps.md)」を参照してください。

- Azure Information Protection クライアントをインストールして構成するには、「[Azure Information Protection クライアント: クライアントのインストールと構成](../deploy-use/configure-client.md)」を参照してください。

## <a name="exchange-online-and-exchange-server"></a>Exchange Online と Exchange Server
Exchange Online または Exchange Server を使用する場合、追加の情報保護ソリューションを提供する Information Rights Management (IRM) 統合を使用できます。

-   **Exchange ActiveSync IRM** 。モバイル デバイスで、保護された電子メール メッセージを保護および使用することができます。

-   **Outlook Web App**用の RMS のサポート。これは、Outlook クライアントと同様に実装されるので、ユーザーは、テンプレートを使用するか個別のオプションを指定して電子メール メッセージを保護したり、自分に送信された保護された電子メール メッセージを読んで使用したりできます。

-   Outlook クライアントの**保護ルール**。管理者が構成し、Rights Management テンプレートが特定受信者向けの電子メール メッセージに自動的に適用されるようにします。 たとえば、社内電子メールが法務部門に送信されるときに、法務部門の所属者のみが読むことが可能で、ただし転送できないようにすることができます。 送信前に電子メール メッセージに保護が適用されたことがユーザーに表示され、既定では、ユーザーは不要と判断した場合にそれを削除できます。 電子メールは送信される前に暗号化されます。 詳細については、Exchange ライブラリの「[Outlook の保護ルール](https://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx)」および「[Outlook 保護ルールを作成する](https://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx)」を参照してください。

-   **トランスポート ルール**。管理者が構成し、送信者、受信者、メッセージの件名、および内容などのプロパティを基にして電子メール メッセージに Rights Management テンプレートを自動的に適用します。 これらは、概念的に保護ルールと似ていますが、ユーザーが保護を削除することはできず、Outlook Web Access とモバイル デバイスによって送信される電子メールに適用され、クライアントから送信される前に電子メール メッセージを暗号化しません。 詳細については、Exchange ライブラリの「[トランスポート保護ルールを作成する](https://technet.microsoft.com/library/dd302432.aspx)」を参照してください。

-   **データ損失防止 (DLP) ポリシー** 。このポリシーは、電子メール メッセージにフィルターを適用するための条件のセットを含み、機密コンテンツ (個人情報やクレジット カード情報など) のデータの損失を防ぐために役立つ操作を実行します。 ポリシーのヒントを使用すると、機密データが検出されたときに、電子メール メッセージ内の情報を基にして、情報保護の適用が必要な可能性があることをユーザーに警告することができます。 詳細については、Exchange ライブラリの「[データ損失防止](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx)」を参照してください。

-   **Office 365 メッセージ暗号化** 。トランスポート ルールを使用して暗号化された電子メールを社外のユーザーに送信し、Outlook Web App に似たブラウザーのインターフェイスで電子メールを読み取ります。 会社の暗号化された電子メールの免責事項のテキストとヘッダーのテキストをカスタマイズすることが可能で、会社のロゴを追加することもできます。 詳細については、Office Web サイトの「[Office 365 Message Encryption](https://office.microsoft.com/o365-message-encryption-FX104179182.aspx)」を参照してください。

Exchange Server を使用する場合は、オンプレミス サーバーと Azure Rights Management サービスの間のリレーとして機能する RMS コネクタをデプロイすることで、Azure Rights Management サービスと情報保護機能を使用できます。

Exchange の IRM を構成する用意ができている場合:

- Exchange Online については、「[Exchange Online: IRM 構成](../deploy-use/configure-office365.md#exchange-online-irm-configuration)」を参照してください。

- Exchange On-Premises については、「[Azure Rights Management コネクタをデプロイする](../deploy-use/deploy-rms-connector.md)」を参照してください。


## <a name="sharepoint-online-and-sharepoint-server"></a>SharePoint Online と SharePoint Server

SharePoint Online または SharePoint Server を使用するとき、Information Rights Management (IRM) でドキュメントを保護できます。 この構成では、管理者がリストやライブラリを保護できます。ユーザーがドキュメントをチェックアウトしたときに、指定した情報保護ポリシーに従って許可されたユーザーのみがファイルを表示および使用できるようにダウンロードされたファイルが保護されます。 たとえば、ファイルが読み取り専用のときに、テキストのコピーを無効にし、ローカル コピーの保存やファイルの印刷を防止することができます。

SharePoint のリストとライブラリについては、情報保護は常にエンド ユーザーではなく管理者によって構成されます。 アクセス許可はサイト レベルで設定します。そのようなアクセス許可は、既定では、そのサイトのリストまたはライブラリにより継承されます。 SharePoint Online を使用する場合、ユーザーは OneDrive for Business ライブラリの IRM 保護も構成できます。

さらに細かく制御するには、サイトのリストまたはライブラリを構成し、親からアクセス許可を継承することを停止できます。 その後、そのレベル (リストまたはライブラリ) で IRM アクセス許可を構成できます。構成後、アクセス許可は "固有のアクセス許可" と呼ばれます。 ただし、アクセス許可は常にコンテナー レベルで設定されます。個々のファイルにアクセス許可を設定することはできません。 

最初に SharePoint の IRM サービスを有効にする必要があります。 次に、ライブラリの IRM アクセス許可を指定します。 SharePoint Online と OneDrive for Business の場合、ユーザーは OneDrive for Business ライブラリに対しても IRM アクセス許可を指定できます。 SharePoint は権限ポリシー テンプレートを使用しませんが、テンプレートに指定できるいくつかの設定と同じ設定を SharePoint の構成で選択できます。

SharePoint Server を使用する場合、Azure Rights Management コネクタをデプロイすることでこの IRM 保護を使用できます。 このコネクタはオンプレミス サーバーと Rights Management クラウド サービスの間のリレーとして機能します。 詳細については、「[Azure Rights Management コネクタをデプロイする](../deploy-use/deploy-rms-connector.md)」を参照してください。

> [!NOTE]
> 現在のところ、SharePoint IRM を使用するとき、いくつかの制限があります。
> 
> - Azure クラシック ポータルで管理する既定のテンプレートまたはカスタム テンプレートは使用できません。 
> 
> - ファイル名拡張子が保護された PDF ファイルのための .PPDF であるファイルはサポートされていません。 ファイル名拡張子が .PDF で、Rights Management がネイティブで保護しているファイルは、Rights Management をネイティブでサポートする PDF リーダーを使用する場合にサポートされます。


IRM 保護を使用するとき、Azure Rights Management サービスは、ドキュメントが SharePoint からダウンロードされる際には使用制限およびデータ暗号化を適用し、ドキュメントが最初に SharePoint で作成される場合、またはライブラリにアップロードされる際には適用しません。 ドキュメントをダウンロードする前に保護する方法については、SharePoint ドキュメントの「[OneDrive for Business および SharePoint Online のデータ暗号化](https://technet.microsoft.com/library/dn905447.aspx)」をご覧ください。

新しい投稿ではありませんが、「[What’s New with Information Rights Management in SharePoint and SharePoint Online](https://blogs.office.com/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/)」 (SharePoint の Information Rights Management と SharePoint Online の新機能) という Office ブログの投稿に追加情報があります。

SharePoint の IRM を構成する用意ができている場合:

- SharePoint Online については、「[SharePoint Online と OneDrive for Business: IRM 構成](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)」を参照してください。

- Sharepoint Server の詳細については、「[Azure Rights Management コネクタをデプロイする](../deploy-use/deploy-rms-connector.md)」を参照してください。


## <a name="next-steps"></a>次のステップ

他のアプリケーションおよびサービスで Azure Information Protection からの Azure Rights Management サービスをサポートする方法については、「[アプリケーションによる Azure Rights Management サービスのサポート](applications-support.md)」をご覧ください。

アプリケーションとサービスの構成など、デプロイを開始する用意ができたら、「[Azure Information Protection デプロイ ロードマップ](/plan-design/deployment-roadmap.md)」を参照してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]