---
title: RMS 共有アプリケーションを使用したドキュメントの追跡と取り消し - AIP
description: RMS 共有アプリケーションを使用してドキュメントを保護した後は、保護されたドキュメントのユーザーによる使用状況を追跡できます。 必要に応じて、共有を停止する場合は、これらのドキュメントへのアクセスを取り消すこともできます。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/04/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 61f349ce-bdd2-45c1-acc5-bc83937fb187
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d6d53635a7f86c9ecc27f654885f9d66569f2b1e
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39374241"
---
# <a name="track-and-revoke-your-documents-when-you-use-the-rms-sharing-application"></a>RMS 共有アプリケーションを使用してドキュメントを追跡および取り消す

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*

RMS 共有アプリケーションを使用してドキュメントを保護すると、組織が Active Directory Rights Management サービスではなく Azure Information Protection を使用している場合は、保護されているドキュメントをユーザーがどのように使用しているかを追跡できます。 必要に応じて、共有を停止する場合は、これらのドキュメントへのアクセスを取り消すこともできます。 これを行うには、Windows コンピューター、Mac コンピューター、タブレット、携帯電話からアクセスできる**ドキュメント追跡サイト**を使用します。

このサイトにアクセスしたら、サインインしてドキュメントを追跡します。 [ドキュメント追跡および失効をサポートするサブスクリプション](https://www.microsoft.com/cloud-platform/azure-information-protection-features)が組織にあり、このサブスクリプションのライセンスが割り当てられている場合は、保護したファイルを開こうとしたユーザーおよび成功した (正常に認証された) かどうかを確認できます。 ユーザーがドキュメントへのアクセスを試みるたびに、その時間と場所がわかります。 ただし、まれに、報告された場所が正確でない場合があります。 たとえば、保護されたドキュメントを開くユーザーが VPN 接続を使用している場合、またはそのコンピューターに IPv6 アドレスが割り当てられている場合です。

ドキュメント追跡サイトで実行できる操作は次のとおりです。

- ドキュメントの共有を停止する必要がある場合:**[アクセスの取り消し]** をクリックし、ドキュメントが引き続き使用できる期間を確認して、これまで共有されていたドキュメントへのアクセスを取り消したことをユーザーに通知するかどうかを決定し、カスタマイズしたメッセージを提供します。 ドキュメントの共有を取り消しても共有していたドキュメントが削除されるわけではありませんが、これまでアクセスの権限があったユーザーがそのドキュメントを開くことはできなくなります。

- Excel にエクスポートする場合: **[CSV にエクスポート]** をクリックすると、データを変更したり、独自のビューやグラフを作成したりすることができます。

- 電子メール通知を構成する場合:**[設定]** をクリックして、ドキュメントがアクセスされたときに電子メールを送信するかどうか、および送信方法を選択します。

- 他のユーザーの共有したドキュメントを追跡し、取り消す場合: Azure Information Protection の管理者は、[管理者] アイコンをクリックして、他のユーザーのドキュメントを追跡し、取り消すことができます。 このアイコンは管理者にのみ表示されます。
    
    注: グローバル管理者でもこのアイコンが表示されない場合、ドキュメントが共有されていません。 その場合、https://portal.azurerms.com/#/admin の URL からドキュメント追跡サイトにアクセスします。

- ドキュメント追跡サイトについて質問がある場合、またはフィードバックを提供したい場合:[ヘルプ] アイコンをクリックして、「 [ドキュメント追跡の FAQ](http://go.microsoft.com/fwlink/?LinkId=523977)」にアクセスします。

## <a name="using-office-to-access-the-document-tracking-site"></a>Office を使用したドキュメント追跡サイトへのアクセス

- Office アプリケーション、Word、Excel、PowerPoint の場合:**[ホーム]** タブの **[RMS]** グループで、**[保護ファイルの共有]** をクリックし、**[使用の追跡]** をクリックします。

    ![RMS 共有アプリケーションの使用時に Office アプリケーションから使用状況を追跡する ](../media/ADRMS_MSRMSApp_OfficeToolbarTrackUsage.png)

- Outlook の場合:**[ホーム]** タブの **[RMS]** グループで、**[使用の追跡]** をクリックします。

    ![[RMS 共有アプリケーションの使用時に Outlook から使用状況を追跡する] を選択する ](../media/ADRMS_MSRMSApp_OutlookTrackUsage.png)

これらの RMS のオプションが表示されない場合は、RMS 共有アプリケーションがコンピューターにインストールされていない、最新バージョンがインストールされていない、インストールを完了するためにコンピューターを再起動する必要がある、などの可能性があります。 共有アプリケーションをインストールする方法の詳細については、「[Rights Management 共有アプリケーションをダウンロードしてインストールする](install-sharing-app.md)」を参照してください。

> [!NOTE] 
> [Azure Information Protection クライアント](../rms-client/info-protect-client.md)をインストールした場合、**[保護]** ボタンを使用してドキュメント追跡サイトにアクセスすることもできます。 
> 
> - Office アプリケーションの **[ホーム]** タブの **[保護]** グループで、**[保護]** > **[使用の追跡]** をクリックします。 

### <a name="other-ways-to-track-and-revoke-your-documents"></a>ドキュメントを追跡して取り消すための他の方法
Windows コンピューターで Office アプリケーションを使用してドキュメントを追跡するだけでなく、以下の代替策を使用することもできます。

-   **Web ブラウザーの使用**:この方法は、サポートされているすべてのデバイスで機能します。

-   **エクスプローラーの使用**:この方法は、Windows コンピューターで機能します。

-   **Outlook 電子メール メッセージの使用**:この方法は、Windows コンピューターで機能します。

#### <a name="using-a-web-browser-to-access-the-doc-tracking-site"></a>Web ブラウザーを使用したドキュメント追跡サイトへのアクセス

- サポートされているブラウザーを使用して、 [ドキュメント追跡サイト](http://go.microsoft.com/fwlink/?LinkId=529562)に移動します。

    サポートされているブラウザー:Internet Explorer バージョン 10 以降の使用が推奨されますが、次のいずれかのブラウザーを使用してドキュメント追跡サイトを使用することもできます。

    -   Internet Explorer:バージョン 10 以降

    -   Internet Explorer 9、MS12-037 (Internet Explorer 用の累積的なセキュリティ更新プログラム: 2012 年 6 月 12 日) 以降

    -   Mozilla Firefox:バージョン 12 以降

    -   Apple Safari 5:バージョン 5 以降

    -   Google Chrome:バージョン 18 以降

#### <a name="using-file-explorer-to-access-the-doc-tracking-site"></a>エクスプローラーを使用したドキュメント追跡サイトへのアクセス

- ファイルを右クリックし、**[RMS による保護]** を選択して、**[使用の追跡]** を選択します。

    ![[RMS 共有アプリケーションの使用時に Explorer から使用状況を追跡する] を選択する](../media/ADRMS_MSRMSApp_ExplorerTrackUsage.png)

#### <a name="using-an-outlook-email-message-to-access-the-doc-tracking-site"></a>Outlook 電子メール メッセージを使用したドキュメント追跡サイトへのアクセス

- 電子メール メッセージの **[メッセージ]** タブで、**[RMS]** グループの **[保護ファイルの共有]** をクリックし、**[使用の追跡]** をクリックします。

    ![[RMS 共有アプリケーションの使用時に Outlook から使用状況を追跡する] を選択する](../media/ADRMS_MSRMSApp_OutlookMessageTrackUsage.png)

## <a name="examples-and-other-instructions"></a>例とその他の説明
Rights Management 共有アプリケーションの使用方法の例と操作手順については、Rights Management 共有アプリケーション ユーザー ガイドの次のセクションをご覧ください。

-   [RMS 共有アプリケーションの使用例](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [作業内容](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>参照
[Rights Management 共有アプリケーション ユーザー ガイド](sharing-app-user-guide.md)
