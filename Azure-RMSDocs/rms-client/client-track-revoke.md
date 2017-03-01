---
title: "ドキュメントの追跡と取り消し - Azure Information Protection"
description: "ドキュメントを保護した後は、保護されたドキュメントのユーザーによる使用状況を追跡できます。 ドキュメントが読まれる必要がなくなった場合は、必要に応じて、これらのドキュメントへのアクセスを取り消すこともできます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 37ab2f78f1ba2f3803ad1aafd011e530ef204acb
ms.lasthandoff: 02/24/2017


---

# <a name="track-and-revoke-your-documents-when-you-use-azure-information-protection"></a>Azure Information Protection を使用してドキュメントを追跡および取り消す

>*適用対象: Azure Information Protection、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*

Azure Information Protection を使用してドキュメントを保護した後は、保護されたドキュメントのユーザーによる使用状況を追跡できます。 ドキュメントが読まれる必要がなくなった場合は、必要に応じて、ドキュメントへのアクセスを取り消すこともできます。 これを行うには、Windows コンピューター、Mac コンピューター、タブレット、携帯電話からアクセスできる**ドキュメント追跡サイト**を使用します。

このサイトにアクセスしたら、サインインしてドキュメントを追跡します。 [ドキュメント追跡および失効をサポートするサブスクリプション](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)が組織にあり、このサブスクリプションのライセンスが割り当てられている場合は、保護したファイルを開こうとしたユーザーおよび成功した (正常に認証された) かどうかを確認できます。 また、ユーザーがドキュメントへのアクセスを試みるたびに、その時間と場所がわかります。 さらに

-   ドキュメントの共有を停止する必要がある場合:[ **アクセスの取り消し**] をクリックし、ドキュメントが引き続き使用できる期間を確認して、これまで共有されていたドキュメントへのアクセスを取り消したことをユーザーに通知するかどうかを決定し、カスタマイズしたメッセージを提供します。 ドキュメントへのアクセスを取り消しても、共有していたドキュメントが削除されるわけではありませんが、承認ユーザーはドキュメントを開けなくなります。
    
    ![ドキュメント追跡サイトの [アクセスの取り消し] アイコン](../media/tracking-site-revoke-access-icon.png)

-   Excel にエクスポートする場合: **[CSV にエクスポート]** をクリックすると、データを変更したり、独自のビューやグラフを作成したりすることができます。
    
    ![ドキュメント追跡サイトの [CSV にエクスポート] アイコン](../media/tracking-site-export-icon.png)

-   電子メール通知を構成する場合: **[設定]** をクリックして、ドキュメントがアクセスされたときに電子メールを送信するかどうか、および送信方法を選択します。
    
    ![ドキュメント追跡サイトの [CSV にエクスポート] アイコン](../media/tracking-site-settings-email.png)

- 他のユーザーの共有したドキュメントを追跡し、取り消す場合: Azure Information Protection の管理者は、[管理者] アイコンをクリックして、他のユーザーの保護されたドキュメントを追跡し、取り消すことができます。 このアイコンは管理者にのみ表示されます。
    
    ![ドキュメント追跡サイトの [管理者] アイコン](../media/tracking-site-admin-icon.png)

保護されたドキュメントを追跡するには、ドキュメント追跡サイトに登録する必要があります。 登録するには、エクスプローラーまたは Office アプリを使用します。

## <a name="using-office-to-track-or-revoke-the-document"></a>Office を使用したドキュメントの追跡または取り消し

Office アプリケーション、Word、Excel、PowerPoint、Outlook の場合: 

1. 追跡または取り消し対象の保護されたドキュメントを開きます。

2. **[ホーム]** タブの **[保護]** グループで **[保護]** > **[追跡と取り消し]** をクリックします。

    ![使用の追跡オプション](../media/track-usage-callout.png)

Office アプリケーションでこれらのオプションが表示されない場合は、Azure Information Protection クライアントがコンピューターにインストールされていない、Office アプリケーションを再起動する必要がある、インストールを完了するためにコンピューターを再起動する必要がある、などの可能性があります。 Azure Information Protection クライアントのインストール方法の詳細については、「[Azure Information Protection クライアントをダウンロードしてインストールする](install-client-app.md)」を参照してください。

## <a name="using-file-explorer-to-track-or-revoke-the-document"></a>エクスプローラーを使用したドキュメントの追跡または取り消し

1. 保護されたファイルを右クリックし、**[分類して保護する]** を選択します。

2. **[分類と保護 - Azure Information Protection]** ダイアログ ボックスから、**[追跡と取り消し]** を選択します。

    ![[分類と保護 - Azure Information Protection] ダイアログ ボックスの [追跡と取り消し] アイコン](../media/track-and-revoke.png)


### <a name="using-a-web-browser-track-and-revoke-documents-that-you-have-registered"></a>Web ブラウザーを使用した登録ドキュメントの追跡と取り消し

Office アプリまたはエクスプローラーを使用して保護されたドキュメントを登録すると、サポートされる Web ブラウザーを使用してそのドキュメントの追跡および取り消しを行うことができます。

- Windows PC、Mac コンピューター、またはモバイル デバイスで[ドキュメント追跡サイト](https://go.microsoft.com/fwlink/?LinkId=529562)にアクセスします。

    **サポートされているブラウザー**: Internet Explorer バージョン 10 以降の使用が推奨されますが、次のいずれかのブラウザーを使用してドキュメント追跡サイトを使用することもできます。

    -   Internet Explorer:バージョン 10 以降

    -   Internet Explorer 9、MS12-037 (Internet Explorer 用の累積的なセキュリティ更新プログラム: 2012 年 6 月 12 日) 以降

    -   Mozilla Firefox:バージョン 12 以降

    -   Apple Safari 5:バージョン 5 以降

    -   Google Chrome:バージョン 18 以降


## <a name="other-instructions"></a>その他の手順
他の操作手順については、Azure Information Protection ユーザー ガイドを参照してください。

- [作業内容](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
