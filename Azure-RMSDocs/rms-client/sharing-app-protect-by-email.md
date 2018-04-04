---
title: 保護ファイルを RMS 共有アプリケーションで共有する - AIP
description: 安全に電子メールでドキュメントを共有するための手順です。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4c1cd1d3-78dd-4f90-8b37-dcc9205a6736
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 71bc303aaadf6856cce2f63db0acf5280fbe172b
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="protect-a-file-that-you-share-by-email-by-using-the-rights-management-sharing-application"></a>Rights Management 共有アプリケーションを使用して、電子メールで共有するファイルを保護する

>*適用対象: Active Directory Rights Management サービス[、Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*

電子メールで共有しているファイルを保護すると、元のファイルの新しいバージョンが作成されます。 元のファイルは保護されない状態のままになり、新しいバージョンは保護されて、送信する電子メールに自動的に添付されます。

場合によっては (Microsoft Word、Excel、PowerPoint で作成されたファイル)、RMS 共有アプリケーションは電子メール メッセージに添付する 2 つのバージョンのファイルを作成します。 2 番目のバージョンのファイルは **.ppdf** というファイル名拡張子で、ファイルの PDF シャドウ コピーです。 このバージョンのファイルを使用すると、受信者は、作成に使われたものと同じアプリケーションがインストールされていなくても、常にファイルを読み取ることができます。 受信者が電子メールをモバイル デバイスで読んでいて、添付ファイルを表示したいときに、このようなことはよくあります。 ファイルを開くために必要なものは、RMS 共有アプリケーションだけです。 その場合、受信者は添付ファイルを読むことはできますが、Rights Management サービスをサポートするアプリケーションを使用してもう 1 つのバージョンのファイルを開くまでは、添付ファイルを変更することはできません。

Azure Information Protection を使用している場合は、共有によって保護されているファイルを追跡できます。

-   保護された添付ファイルをだれかが開こうとするときに、電子メールを受け取るオプションを選択します。 ファイルにアクセスされるたびに、ファイルを開こうとしたユーザー、試みられた日時、および試みが成功したか (正常に認証された) 失敗したかが通知されます。

-   ドキュメント追跡サイトを使用します。 ドキュメント追跡サイトでファイルへのアクセスを取り消すことにより、ファイルの共有を停止することもできます。 詳細については、「[RMS 共有アプリケーションを使用してドキュメントを追跡および取り消す](sharing-app-track-revoke.md)」を参照してください。

## <a name="using-outlook-to-protect-a-file-that-you-share-by-email"></a>Outlook の使用:電子メールで共有するファイルを保護するには

1.  電子メール メッセージを作成してファイルを添付します。 次に、**[RMS]** グループの **[メッセージ]** タブで、**[保護ファイルの共有]** をクリックし、もう一度 **[保護ファイルの共有]** をクリックします。

    ![RMS 共有アプリケーション用 Outlook アドイン](../media/ADRMS_MSRMSApp_SP_OutlookToolbar.png)

    このボタンが表示されない場合は、RMS 共有アプリケーションがコンピューターにインストールされていない、最新バージョンがインストールされていない、インストールを完了するためにコンピューターを再起動する必要がある、などの可能性があります。 共有アプリケーションをインストールする方法の詳細については、「[Rights Management 共有アプリケーションをダウンロードしてインストールする](install-sharing-app.md)」を参照してください。

2.  [[share protected] (保護ファイルの共有) ダイアログ ボックス](sharing-app-dialog-box.md)でこのファイルに必要なオプションを指定し、**[Send Now]** (今すぐ送信) をクリックします。

### <a name="other-ways-to-protect-a-file-that-you-share-by-email"></a>電子メールで共有するファイルを保護する他の方法
Outlook を使用して保護されたファイルを共有する以外に、以下の方法を使用することもできます。

-   エクスプローラーから:この方法はすべてのファイルに対して使用できます。

-   Office アプリケーションから: この方法は、Office アドインを使用することによって RMS 共有アプリケーションがサポートするアプリケーションで機能するため、リボンに **[RMS]** グループが表示されます。

#### <a name="using-file-explorer-or-an-office-application-to-protect-a-file-that-you-share-by-email"></a>エクスプローラーまたは Office アプリケーションの使用:電子メールで共有するファイルを保護するには

1.  以下のいずれかのオプションを使用します。

    -   エクスプローラーの場合: ファイルを右クリックし、**[RMS による保護]** を選択して、**[Share Protected]** (保護ファイルの共有) を選択します。

        ![[保護ファイルの共有] メニュー オプション](../media/ADRMS_MSRMSApp_ShareProtectedMenu.png)

    -   Office アプリケーション、Word、Excel、PowerPoint の場合:まず、ファイルを保存してあることを確認します。 次に、**[ホーム]** タブの **[RMS]** で、**[保護ファイルの共有]** をクリックし、もう一度 **[保護ファイルの共有]** をクリックします。

        ![Office ツールバー アドイン](../media/ADRMS_MSRMSApp_SP_OfficeToolbar.png)

    これらの保護用オプションが表示されない場合は、RMS 共有アプリケーションがコンピューターにインストールされていない、最新バージョンがインストールされていない、インストールを完了するためにコンピューターを再起動する必要がある、などの可能性があります。 共有アプリケーションをインストールする方法の詳細については、「[Rights Management 共有アプリケーションをダウンロードしてインストールする](install-sharing-app.md)」を参照してください。

2.  [[share protected] (保護ファイルの共有) ダイアログ ボックス](sharing-app-dialog-box.md)でこのファイルに必要なオプションを指定し、**[送信]** をクリックします。

3.  すぐにファイルが保護されていることを示すダイアログ ボックスが表示される場合があります。その後、添付ファイルは Microsoft RMS で保護されていて表示するにはサインインする必要があることを受信者に伝える、自動的に作成される電子メール メッセージが表示されます。 受信者がサインインへのリンクをクリックすると、受信者が保護された添付ファイルを開くことができることを確認するための手順とリンクが表示されます。

    例:

    ![Azure Information Protection の電子メール メッセージ](../media/ADRMS_MSRMSApp_EmailMessage.PNG)

    詳細: [自動的に作成される .ppdf ファイルとは](sharing-app-dialog-box.md#whats-the-ppdf-file-thats-automatically-created)

4.  省略可能:この電子メール メッセージの内容は自由に変更できます。 たとえば、メッセージの件名またはテキストを追加または変更できます。

    > [!WARNING]
    > この電子メール メッセージのユーザーを追加または削除できますが、それによって **[保護ファイルの共有]** ダイアログ ボックスで指定した添付ファイルのアクセス許可が変わることはありません。 アクセス許可を変更するには、たとえば、新しいユーザーにファイルを開くアクセス許可を付与し、保存したり送信したりしないで電子メール メッセージを閉じてから、手順 1 に戻ります。

5.  電子メール メッセージを送信します。

## <a name="examples-and-other-instructions"></a>例とその他の説明
Rights Management 共有アプリケーションの使用方法の例と操作手順については、Rights Management 共有アプリケーション ユーザー ガイドの次のセクションをご覧ください。

-   [RMS 共有アプリケーションの使用例](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [作業内容](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>参照
[Rights Management 共有アプリケーション ユーザー ガイド](sharing-app-user-guide.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]