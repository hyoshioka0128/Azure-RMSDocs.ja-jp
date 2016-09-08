---
title: "Office アプリケーションおよびサービス | Azure RMS"
description: "エンドユーザー Office アプリケーション (Word、Excel、PowerPoint、Outlook など) と Office サービス (Exchange、SharePoint など) で Microsoft Azure Rights Management を使用して、組織のデータを保護できます。"
author: cabailey
manager: mbaldwin
ms.date: 06/30/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 388e67cd-c16f-4fa0-a7bb-ffe0def2be81
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: 93dde9494a430526ebd26e1d5123ad44901ffcbb


---


# Office アプリケーションおよびサービス

>*適用対象: Azure Rights Management、Office 365*

エンド ユーザー Office アプリケーション (Word、Excel、PowerPoint、Outlook など) と Office サービス (Exchange、SharePoint など) で Microsoft Azure Rights Management を使用して、組織のデータを保護できます。

## Office アプリケーション:Word、Excel、PowerPoint、Outlook
これらのアプリケーションでは、Information Rights Management (IRM) を使用することで Rights Management がネイティブでサポートされ、ユーザーは保存済みドキュメントまたは送信される電子メール メッセージに保護を適用できます。 ユーザーは、テンプレートを適用するか、Word、Excel、PowerPoint の場合にはアクセス、権限、および使用制限の細かくカスタマイズされた設定を選択できます。 

たとえば、ユーザーは、組織内のユーザーのみがアクセスできるように Word 文書を構成することも、Excel スプレッドシートの編集の可否、読み取り専用への制限、印刷防止などを制御することもできます。 時間が重要なファイルの場合、ファイルにアクセスできなくなる有効期限を (ユーザーが直接またはテンプレートの適用により) 構成できます。 Outlook の場合、ユーザーは、テンプレートを選択できるだけでなく、[**転送不可**] オプションを選択して、データの漏えいを防ぐこともできます。

## Exchange Online と Exchange Server
Exchange Online または Exchange Server を使用する場合、追加の情報保護ソリューションを提供する Information Rights Management (IRM) 統合を使用できます。

-   **Exchange ActiveSync IRM** 。モバイル デバイスで、保護された電子メール メッセージを保護および使用することができます。

-   **Outlook Web App**用の RMS のサポート。これは、Outlook クライアントと同様に実装されるので、ユーザーは、テンプレートを使用するか個別のオプションを指定して電子メール メッセージを保護したり、自分に送信された保護された電子メール メッセージを読んで使用したりできます。

-   Outlook クライアントの**保護ルール** 。管理者が構成し、RMS テンプレートを特定受信者向けの電子メール メッセージに自動的に適用されます。 たとえば、社内電子メールが法務部門に送信されるときに、法務部門の所属者のみが読むことが可能で、ただし転送できないようにすることができます。 送信前に電子メール メッセージに保護が適用されたことがユーザーに表示され、既定では、ユーザーは不要と判断した場合にそれを削除できます。 電子メールは送信される前に暗号化されます。 詳細については、Exchange ライブラリの「[Outlook の保護ルール](https://technet.microsoft.com/library/dd638178%28v=exchg.150%29.aspx)」および「[Outlook 保護ルールを作成する](https://technet.microsoft.com/library/dd638196%28v=exchg.150%29.aspx)」を参照してください。

-   **トランスポート ルール** 。管理者が構成し、送信者、受信者、メッセージの件名、および内容などのプロパティを基にして電子メール メッセージに RMS テンプレートを自動的に適用します。 これらは、概念的に保護ルールと似ていますが、ユーザーが保護を削除することはできず、Outlook Web Access とモバイル デバイスによって送信される電子メールに適用され、クライアントから送信される前に電子メール メッセージを暗号化しません。 詳細については、Exchange ライブラリの「[トランスポート保護ルールを作成する](https://technet.microsoft.com/library/dd302432.aspx)」を参照してください。

-   **データ損失防止 (DLP) ポリシー** 。このポリシーは、電子メール メッセージにフィルターを適用するための条件のセットを含み、機密コンテンツ (個人情報やクレジット カード情報など) のデータの損失を防ぐために役立つ操作を実行します。 ポリシーのヒントを使用すると、機密データが検出されたときに、電子メール メッセージ内の情報を基にして、情報保護の適用が必要な可能性があることをユーザーに警告することができます。 詳細については、Exchange ライブラリの「[データ損失防止](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx)」を参照してください。

-   **Office 365 メッセージ暗号化** 。トランスポート ルールを使用して暗号化された電子メールを社外のユーザーに送信し、Outlook Web App に似たブラウザーのインターフェイスで電子メールを読み取ります。 会社の暗号化された電子メールの免責事項のテキストとヘッダーのテキストをカスタマイズすることが可能で、会社のロゴを追加することもできます。 詳細については、Office Web サイトの「[Office 365 Message Encryption](https://office.microsoft.com/o365-message-encryption-FX104179182.aspx)」を参照してください。

Exchange Server を使用する場合は、オンプレミス サーバーと RMS クラウド サービスの間のリレーとして機能する RMS コネクタを配置することで、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] と情報保護機能を使用できます。 詳細については、「[Azure Rights Management コネクタをデプロイする](../deploy-use/deploy-rms-connector.md)」を参照してください。

## SharePoint Online と SharePoint Server
SharePoint Online または SharePoint Server を使用する場合に Information Rights Management (IRM) 統合を使用すると、管理者がリストやライブラリを保護し、ユーザーがドキュメントをチェックアウトしたときに、指定した情報保護ポリシーに従って許可されたユーザーのみがファイルを表示および使用できるようにファイルが保護されます。 たとえば、ファイルが読み取り専用のときに、テキストのコピーを無効にし、ローカル コピーの保存やファイルの印刷を防止することができます。

リストとライブラリについては、情報保護は常にエンド ユーザーではなく管理者によって適用されます。 また、個別のファイルではなくコンテナー内のすべてのドキュメントのリストまたはライブラリのレベルで適用されます。  SharePoint Online を使用する場合、ユーザーは OneDrive for Business ライブラリにも IRM を適用できます。

最初に SharePoint の IRM サービスを有効にする必要があります。 次に、ライブラリに対して Information Rights Management を指定します。 SharePoint Online と OneDrive for Business の場合、ユーザーは OneDrive for Business ライブラリに対しても Information Rights Management を指定できます。 SharePoint は権限ポリシー テンプレートを使用しませんが、SharePoint にはテンプレートで指定できる設定とほとんど同じでユーザーが選択できる構成設定があります。

SharePoint Server を使用する場合は、オンプレミス サーバーと RMS クラウド サービスの間のリレーとして機能する RMS コネクタを配置することで、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] と情報保護機能を使用できます。 詳細については、「[Azure Rights Management コネクタをデプロイする](../deploy-use/deploy-rms-connector.md)」を参照してください。

> [!NOTE]
> 現在のところ、SharePoint で IRM を使用する場合、いくつかの制限があります。
> 
> -   Azure クラシック ポータルで管理する既定のテンプレートまたはカスタム テンプレートは使用できません。
> -   ファイル名拡張子が保護された PDF ファイルのための .PPDF であるファイルはサポートされていません。 ファイル名拡張子が .PDF で、RMS がネイティブで保護しているファイルは、RMS をネイティブでサポートする PDF リーダーを使用する場合にサポートされます。
> -   モバイル デバイスの Office では RMS がまだサポートされていないため、RMS で保護されているファイルを表示するにはこれらのデバイスでブラウザーを使用する必要があり、ファイルは読み取り専用です。

Azure RMS は、ドキュメントが SharePoint からダウンロードされる際には使用制限およびデータ暗号化を適用し、ドキュメントが最初に SharePoint で作成される場合、またはライブラリにアップロードされる際には適用しません。 ドキュメントをダウンロードする前に保護する方法については、SharePoint ドキュメントの「 [OneDrive for Business および SharePoint Online のデータ暗号化](https://technet.microsoft.com/library/dn905447.aspx) 」を参照してください。

SharePoint での Azure RMS の使用について詳しくは、Office のブログの次の投稿を参照してください: [SharePoint および SharePoint Online における Information Rights Management の新機能](http://blogs.office.com/2012/11/09/whats-new-with-information-rights-management-in-sharepoint-and-sharepoint-online/)

## 次のステップ

「[アプリケーションで Azure Rights Management をサポートする方法](applications-support.md)」を参照して、他のアプリケーションおよびサービスで Azure Rights Management をサポートする方法について確認してください。


<!--HONumber=Aug16_HO4-->


