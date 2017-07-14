---
title: "ドキュメントの追跡と取り消し - Azure Information Protection"
description: "ドキュメントを保護した後は、保護されたドキュメントのユーザーによる使用状況を追跡できます。 ドキュメントが読まれる必要がなくなった場合は、必要に応じて、これらのドキュメントへのアクセスを取り消すこともできます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 79c02795ca10ff875744f3b6c90cebd582cb8c3e
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2017
---
# Azure Information Protection を使用してドキュメントを追跡および取り消す
<a id="track-and-revoke-your-documents-when-you-use-azure-information-protection" class="xliff"></a>

>*適用対象: Azure Information Protection、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*

Azure Information Protection を使用してドキュメントを保護した後は、保護されたドキュメントのユーザーによる使用状況を追跡できます。 ドキュメントが読まれる必要がなくなった場合は、必要に応じて、ドキュメントへのアクセスを取り消すこともできます。 これを行うには、Windows コンピューター、Mac コンピューター、タブレット、携帯電話からアクセスできる**ドキュメント追跡サイト**を使用します。

このサイトにアクセスしたら、サインインしてドキュメントを追跡します。 [ドキュメント追跡および失効をサポートするサブスクリプション](https://www.microsoft.com/cloud-platform/azure-information-protection-features)が組織にあり、このサブスクリプションのライセンスが割り当てられている場合は、保護したファイルを開こうとしたユーザーおよび成功した (正常に認証された) かどうかを確認できます。 また、ユーザーがドキュメントへのアクセスを試みるたびに、その時間と場所がわかります。 さらに

- ドキュメントの共有を停止する必要がある場合: 
    
    - **[アクセスの取り消し]** をクリックして、ドキュメントを引き続き利用できる期間を指定し、これまでドキュメントを共有していた相手にアクセスの取り消しを知らせるかどうかを指定し、カスタマイズしたメッセージを入力します。 ドキュメントへのアクセスを取り消しても、共有していたドキュメントが削除されるわけではありませんが、承認ユーザーはドキュメントを開けなくなります。
        
        ![ドキュメント追跡サイトの [アクセスの取り消し] アイコン](../media/tracking-site-revoke-access-icon.png)
        
- Excel にエクスポートする場合: 
    
    - **[CSV にエクスポート]** をクリックすると、データを変更して独自のビューとグラフを作成できるようになります。
         
        ![ドキュメント追跡サイトの [CSV にエクスポート] アイコン](../media/tracking-site-export-icon.png)
         
- 電子メール通知を構成する場合: 
     
    - **[設定]** をクリックし、ドキュメントへのアクセスがあれば電子メールで知らせるかどうかやその方法を選択します。
        
        ![ドキュメント追跡サイトの [CSV にエクスポート] アイコン](../media/tracking-site-settings-email.png)

- 他のユーザーの共有したドキュメントを追跡し、アクセスを取り消す場合:
    
    - Azure Information Protection の管理者は、[管理者] アイコンをクリックして、他のユーザーの保護されたドキュメントを追跡し、そのアクセスを取り消すことができます。 このアイコンは管理者にのみ表示されます。
        
        ![ドキュメント追跡サイトの [管理者] アイコン](../media/tracking-site-admin-icon.png)

管理者でない場合は、自分が保護したドキュメントのみを追跡してアクセスを取り消すことができます。 ドキュメント追跡サイトを使用して、保護した電子メールを追跡することはできません。

> [!NOTE] 
> 管理者がドキュメント追跡サイトのプライバシー管理を構成した場合は、自分が追跡しているドキュメントに組織内のユーザーがいつアクセスしたのかを知ることができない場合があります。 管理者はすべてのユーザーまたは一部のユーザーを除外できます。 ただし、管理者でなくても、追跡しているドキュメントへのアクセスを取り消すことはいつでもできます。

自分が保護したドキュメントを追跡するには、Windows コンピューターを使用してドキュメント追跡サイトに登録する必要があります。 登録するには、エクスプローラーまたは Office アプリを使用します。

## Office を使用したドキュメントの追跡または取り消し
<a id="using-office-to-track-or-revoke-the-document" class="xliff"></a>

Office アプリケーション、Word、Excel、PowerPoint、Outlook の場合: 

1. 追跡または取り消し対象の保護されたドキュメントを開きます。

2. **[ホーム]** タブの **[保護]** グループで **[保護]** > **[追跡と取り消し]** をクリックします。

    ![使用の追跡オプション](../media/track-usage-callout.png)

Office アプリケーションでこれらのオプションが表示されない場合は、Azure Information Protection クライアントがコンピューターにインストールされていない、Office アプリケーションを再起動する必要がある、インストールを完了するためにコンピューターを再起動する必要がある、などの可能性があります。 Azure Information Protection クライアントのインストール方法の詳細については、「[Azure Information Protection クライアントをダウンロードしてインストールする](install-client-app.md)」を参照してください。

## エクスプローラーを使用したドキュメントの追跡または取り消し
<a id="using-file-explorer-to-track-or-revoke-the-document" class="xliff"></a>

1. 保護されたファイルを右クリックし、**[分類して保護する]** を選択します。

2. **[分類と保護 - Azure Information Protection]** ダイアログ ボックスから、**[追跡と取り消し]** を選択します。

    ![[分類と保護 - Azure Information Protection] ダイアログ ボックスの [追跡と取り消し] アイコン](../media/track-and-revoke.png)


### Web ブラウザーを使用した登録ドキュメントの追跡と取り消し
<a id="using-a-web-browser-to-track-and-revoke-documents-that-you-have-registered" class="xliff"></a>

Office アプリまたはエクスプローラーを使用して保護されたドキュメントを登録すると、サポートされる Web ブラウザーを使用してそのドキュメントの追跡および取り消しを行うことができます。

- Windows PC、Mac コンピューター、またはモバイル デバイスで[ドキュメント追跡サイト](https://go.microsoft.com/fwlink/?LinkId=529562)にアクセスします。

    **サポートされているブラウザー**: Internet Explorer バージョン 10 以降の使用が推奨されますが、次のいずれかのブラウザーを使用してドキュメント追跡サイトを使用することもできます。

    -   Internet Explorer:バージョン 10 以降

    -   Internet Explorer 9、MS12-037 (Internet Explorer 用の累積的なセキュリティ更新プログラム: 2012 年 6 月 12 日) 以降

    -   Mozilla Firefox:バージョン 12 以降

    -   Apple Safari 5:バージョン 5 以降

    -   Google Chrome:バージョン 18 以降


## その他の手順
<a id="other-instructions" class="xliff"></a>
他の操作手順については、Azure Information Protection ユーザー ガイドを参照してください。

- [作業内容](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]