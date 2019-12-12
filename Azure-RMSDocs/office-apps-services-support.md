---
title: Office のアプリとサービスが AIP から Azure RMS をサポートするしくみ
description: Word や Outlook などのエンド ユーザー Office アプリケーションと Exchange や SharePoint などの Office サービスで AIP から Azure Rights Management サービスを使用し、組織のデータを保護するしくみ。
author: cabailey
ms.author: cabailey
manager: rkarlin
ms.date: 11/04/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 279fc1cd21486115fc270456d28d0d2598d8d271
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73559839"
---
# <a name="how-office-applications-and-services-support-azure-rights-management"></a>Office のアプリケーションとサービスが Azure Rights Management をサポートするしくみ 

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

エンド ユーザー Office アプリケーションと Office サービスで Azure Information Protection から Azure Rights Management サービスを使用し、組織のデータを保護できます。 これらの Office アプリケーションは Word、Excel、PowerPoint、および Outlook です。 Office サービスは Exchange および SharePoint です。 Azure Rights Management サービスをサポートする Office 構成では、多くの場合、**IRM (Information Rights Management)** という用語が使用されます。

## <a name="office-applications-word-excel-powerpoint-outlook"></a>Office アプリケーション:Word、Excel、PowerPoint、Outlook
これらのアプリケーションは Azure Rights Management をネイティブでサポートし、ユーザーは保存済みのドキュメントまたは送信する電子メール メッセージに保護を適用できます。 ユーザーは[テンプレート](configure-policy-templates.md)を適用して保護を適用できます。 あるいは、Word、Excel、PowerPoint の場合、アクセス、権限、使用制限にカスタマイズ設定を選択できます。

たとえば、組織内の人だけがアクセスできるように Word 文書を設定できます。 あるいは、Excel スプレッドシートを編集可能にしたり、読み取り専用にしたり、印刷禁止にするかどうかを制御できます。 時間が重要なファイルの場合、ファイルにアクセスできなくなる有効期限を構成できます。 この構成はユーザーが直接行うか、保護テンプレートを適用して行うことができます。 Outlook の場合、ユーザーは、 **[転送不可]** オプションを選択して、データの漏えいを防ぐこともできます。

Office アプリを構成する準備ができている場合は、「 [office アプリ: クライアントの構成](configure-office-apps.md)」を参照してください。

## <a name="exchange-online-and-exchange-server"></a>Exchange Online と Exchange Server
Exchange Online または Exchange Server を使用すると、Azure Information Protection のオプションを構成できます。 この構成では、Exchange は次の保護ソリューションを提供します。

-   **Exchange ActiveSync IRM** 。モバイル デバイスで、保護された電子メール メッセージを保護および使用することができます。

-   **Outlook on the web** の電子メール保護サポート。Outlook クライアントと同様に実装されます。 この構成では、ユーザーは保護テンプレートまたはオプションを使用することでメール メッセージを保護できます。 ユーザーは、自分に送信された保護メールのメッセージを読み、利用できます。

-   Outlook クライアントの**保護ルール**。保護テンプレートおよびオプションが特定受信者のメール メッセージに自動的に適用されるように管理者が構成します。 たとえば、社内電子メールが法務部門に送信されるときに、法務部門の所属者のみが読むことが可能で、ただし転送できないようにすることができます。 送信前に電子メール メッセージに保護が適用されたことがユーザーに表示され、既定では、ユーザーは不要と判断した場合にこの保護を削除できます。 電子メールは送信される前に暗号化されます。 詳細については、Exchange ライブラリの「 [Outlook 保護ルール](https://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx) 」と「 [Outlook 保護ルールの作成](https://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx) 」を参照してください。

-   **メール フロー ルール**。保護テンプレートまたはオプションがメール メッセージに自動的に適用されるように管理者が構成します。 ルールの基盤は送信者、受信者、メッセージの件名、内容などのプロパティになります。 ルールは概念上、保護ルールに似ていますが、ユーザーは保護を削除できません。これは、保護がクライアントではなく Exchange サービスによって設定されるためです。 保護がサービスによって設定されるので、ユーザーがどのようなデバイスまたはオペレーティング システムを使用していても関係ありません。 詳細については、Exchange オンプレミスに関する「[Exchange Online のメール フロー ルール (トランスポート ルール)](/exchange/security-and-compliance/mail-flow-rules/mail-flow-rules)」および「[トランスポート保護ルールを作成する](https://technet.microsoft.com/library/dd302432.aspx)」を参照してください。

-   **データ損失防止 (DLP) ポリシー**。このポリシーは、メール メッセージにフィルターを適用するための条件のセットを含み、機密コンテンツのデータの損失を防ぐために役立つ操作を実行します。 指定できるアクションの 1 つは、保護テンプレートまたはオプションの 1 つを指定することで、保護として暗号化を適用することです。 ポリシーのヒントを使用すると、機密データが検出されたときに、保護の適用が必要な可能性があることをユーザーに警告できます。 詳細については、Exchange Online ドキュメントの「[データ損失防止](/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention)」を参照してください。

-   **Office 365 Message Encryption** では、保護されているメール メッセージと保護されている Office ドキュメントを添付ファイルとして、あらゆるデバイスであらゆるメール アドレスに送信できます。 Azure AD を使用しないユーザー アカウントの場合、インターネットがあれば、ソーシャル ID プロバイダーやワンタイム パスコードを利用できます。 詳細については、Office 365 ドキュメントの「[Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection](/microsoft-365/compliance/set-up-new-message-encryption-capabilities)」 (Azure Information Protection 上に構築される新しい Office 365 メッセージの暗号化機能の設定) を参照してください。 この構成に関連する追加情報については、「[Office 365 Message Encryption](https://docs.microsoft.com/microsoft-365/compliance/ome)」を参照してください。

オンプレミスで Exchange を使用している場合、Azure Rights Management コネクタを展開し、IRM 機能と Azure Rights Management サービスを利用できます。 このコネクタはオンプレミス サーバーと Azure Rights Management サービスの間のリレーとして機能します。

保護テンプレートの詳細については、「[Azure Information Protection のテンプレートを構成して管理する](configure-policy-templates.md)」を参照してください。

メールを保護するためのメール オプションの詳細については、「[電子メールの [転送不可] オプション](configure-usage-rights.md#do-not-forward-option-for-emails)」および「[電子メールの暗号化のみオプション](configure-usage-rights.md#encrypt-only-option-for-emails)」を参照してください。

メールの保護するために Exchange を構成する準備ができたら、次を参照します。

- Exchange Online については、「[Exchange Online: IRM 構成](configure-office365.md#exchangeonline-irm-configuration)」を参照してください。

- Exchange On-Premises については、「[Azure Rights Management コネクタをデプロイする](deploy-rms-connector.md)」を参照してください。


## <a name="sharepoint-online-and-sharepoint-server"></a>SharePoint Online と SharePoint Server

SharePoint Online または SharePoint Server を使用するとき、SharePoint IRM (Information Rights Management) でドキュメントを保護できます。 この機能では、管理者がリストやライブラリを保護できます。ユーザーが文書をチェックアウトしたときに、指定した情報保護ポリシーに従って許可されたユーザーのみがファイルを表示および使用できるようにダウンロードされたファイルが保護されます。 たとえば、ファイルが読み取り専用のときに、テキストのコピーを無効にし、ローカル コピーの保存やファイルの印刷を防止することができます。

Word、PowerPoint、Excel、PDF ドキュメントがこの SharePoint IRM 保護に対応しています。 既定では、保護はドキュメントをダウンロードした人に限定されます。 この既定を変更するには、 **[グループの保護を許可します]** という名前の構成オプションを使用します。これは、指定したグループに保護を拡張します。 たとえば、ライブラリ内のドキュメントを編集するアクセス許可を持つグループを指定して、同じユーザーのグループが、どのユーザーがドキュメントをダウンロードしたかに関係なく、SharePoint の外部でドキュメントを編集できるようにすることができます。 または、SharePoint でアクセス許可を付与されていないグループ内のユーザーが、SharePoint の外部でドキュメントにアクセスする必要がある場合に、このグループを指定できます。 SharePoint のリストとライブラリについては、この保護は常にエンド ユーザーではなく管理者によって構成されます。 アクセス許可はサイト レベルで設定します。そのようなアクセス許可は、既定では、そのサイトのリストまたはライブラリにより継承されます。 SharePoint Online を使用する場合、ユーザーは OneDrive for Business ライブラリの IRM 保護も構成できます。

さらに細かく制御するには、サイトのリストまたはライブラリを構成し、親からアクセス許可を継承することを停止できます。 その後、そのレベル (リストまたはライブラリ) で IRM アクセス許可を構成できます。構成後、アクセス許可は "固有のアクセス許可" と呼ばれます。 ただし、アクセス許可は常にコンテナー レベルで設定されます。個々のファイルにアクセス許可を設定することはできません。 

最初に SharePoint の IRM サービスを有効にする必要があります。 次に、ライブラリの IRM アクセス許可を指定します。 SharePoint Online と OneDrive for Business の場合、ユーザーは OneDrive for Business ライブラリに対しても IRM アクセス許可を指定できます。 SharePoint は権限ポリシー テンプレートを使用しませんが、テンプレートに指定できるいくつかの設定と同じ設定を SharePoint の構成で選択できます。

SharePoint Server を使用する場合、Azure Rights Management コネクタをデプロイすることでこの IRM 保護を使用できます。 このコネクタはオンプレミス サーバーと Rights Management クラウド サービスの間のリレーとして機能します。 詳細については、「[Azure Rights Management コネクタをデプロイする](deploy-rms-connector.md)」を参照してください。

> [!NOTE]
> SharePoint IRM を使用する場合、いくつかの制限があります。
> 
> - Azure Portal で管理する既定のテンプレートまたはカスタム保護テンプレートを使用できません。 
> 
> - ファイル名拡張子が保護された PDF ファイルのための .ppdf であるファイルはサポートされていません。 保護された PDF ドキュメントの表示について詳しくは、「[Microsoft Information Protection の保護された PDF リーダー](./rms-client/protected-pdf-readers.md)」をご覧ください。
> 
> - 複数のユーザーが同時にドキュメントを編集する共同編集はサポートされていません。 IRM で保護されたライブラリ内のドキュメントを編集するには、まずドキュメントをチェック アウトしてダウンロードし、Office アプリケーションで編集する必要があります。 そのため、一度に編集できるのは 1 人のみです。

IRM で保護されていないライブラリの場合、SharePoint または OneDrive にアップロードするファイルを保護すると、次のファイルは使用できません。共同作成、web 用 Office、検索、ドキュメントプレビュー、サムネイル、電子情報開示、データ損失防止 (DLP)).

> [!TIP]
> SharePoint IRM を使用する代わりに、機密ラベルを使用して、 [sharepoint と OneDrive (パブリックプレビュー) で暗号化を適用し、Office ファイルの機密ラベルを有効に](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files)することを検討してください。

SharePoint IRM 保護を使用する場合、Azure Rights Management サービスは、ドキュメントが SharePoint からダウンロードされる際には使用制限およびデータ暗号化を適用し、ドキュメントが最初に SharePoint で作成される場合、またはライブラリにアップロードされる際には適用しません。 ドキュメントをダウンロードする前に保護する方法については、SharePoint ドキュメントの「[OneDrive for Business および SharePoint Online のデータ暗号化](https://technet.microsoft.com/library/dn905447.aspx)」をご覧ください。

新しい投稿ではありませんが、「[What’s New with Information Rights Management in SharePoint and SharePoint Online](https://www.microsoft.com/en-us/microsoft-365/blog/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/)」 (SharePoint の Information Rights Management と SharePoint Online の新機能) という Office 365 ブログの投稿に追加情報があります。

今後の変更については、「 [SharePoint のセキュリティ、管理、および移行に対する更新](https://techcommunity.microsoft.com/t5/Microsoft-SharePoint-Blog/Updates-to-SharePoint-security-administration-and-migration/ba-p/549585)」を参照してください。

SharePoint の IRM を構成する用意ができている場合:

- SharePoint Online については、「[SharePoint Online と OneDrive for Business: IRM 構成](configure-office365.md#sharepointonline-and-onedrive-for-business-irm-configuration)」を参照してください。

- Sharepoint Server の詳細については、「[Azure Rights Management コネクタをデプロイする](deploy-rms-connector.md)」を参照してください。


## <a name="next-steps"></a>次のステップ

Office 365 をお持ちの場合、「[Office 365 のファイル保護ソリューション](/office365/enterprise/microsoft-cloud-it-architecture-resources#BKMK_O365fileprotect)」をご覧になることをお勧めします。Office 365 のファイルを保護するための推奨機能を説明しています。

他のアプリケーションおよびサービスで Azure Information Protection からの Azure Rights Management サービスをサポートする方法については、「[アプリケーションによる Azure Rights Management サービスのサポート](applications-support.md)」をご覧ください。

アプリケーションとサービスの構成など、デプロイを開始する用意ができたら、「[Azure Information Protection デプロイ ロードマップ](deployment-roadmap.md)」を参照してください。
