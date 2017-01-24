---
title: "Azure Information Protection を使用して保護されたドキュメントを追跡および取り消す | Azure Information Protection"
description: "ドキュメントを保護した後は、保護されたドキュメントのユーザーによる使用状況を追跡できます。 ドキュメントが読まれる必要がなくなった場合は、必要に応じて、これらのドキュメントへのアクセスを取り消すこともできます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 54abc32a6065bb3863cf55b42466250f8fc9c634


---

# <a name="track-and-revoke-your-documents-when-you-use-azure-information-protection"></a>Azure Information Protection を使用してドキュメントを追跡および取り消す

>*適用対象: Azure Information Protection、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*

**[このバージョンのクライアントはプレビュー段階にあり、変更される可能性があります。]**

Azure Information Protection を使用してドキュメントを保護した後は、保護されたドキュメントのユーザーによる使用状況を追跡できます。 ドキュメントが読まれる必要がなくなった場合は、必要に応じて、ドキュメントへのアクセスを取り消すこともできます。 これを行うには、Windows コンピューター、Mac コンピューター、タブレット、携帯電話からアクセスできる**ドキュメント追跡サイト**を使用します。

<div style="padding-top: 56.25%; position: relative; width: 100%;">
<iframe style="position: absolute;top: 0;left: 0;right: 0;bottom: 0;" width="100%" height="100%" src="https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation/player" frameborder="0" allowfullscreen></iframe>
</div>

このサイトにアクセスしたら、サインインしてドキュメントを追跡します。 [ドキュメント追跡および失効をサポートするサブスクリプション](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)が組織にあり、このサブスクリプションのライセンスが割り当てられている場合は、保護したファイルを開こうとしたユーザーおよび成功した (正常に認証された) かどうかを確認できます。 また、ユーザーがドキュメントへのアクセスを試みるたびに、その時間と場所がわかります。 さらに

-   ドキュメントの共有を停止する必要がある場合:[ **アクセスの取り消し**] をクリックし、ドキュメントが引き続き使用できる期間を確認して、これまで共有されていたドキュメントへのアクセスを取り消したことをユーザーに通知するかどうかを決定し、カスタマイズしたメッセージを提供します。 ドキュメントへのアクセスを取り消しても共有していたドキュメントが削除されるわけではありませんが、承認ユーザーはドキュメントを開けなくなります。

-   Excel にエクスポートする場合: **[CSV にエクスポート]** をクリックすると、データを変更したり、独自のビューやグラフを作成したりすることができます。

-   電子メール通知を構成する場合:[ **設定** ] をクリックして、ドキュメントがアクセスされたときに電子メールを送信するかどうか、および送信方法を選択します。

- 他のユーザーの共有したドキュメントを追跡し、取り消す場合: Azure Information Protection の管理者は、[管理者] アイコンをクリックして、他のユーザーの保護されたドキュメントを追跡し、取り消すことができます。 このアイコンは管理者にのみ表示されます。

-   ドキュメント追跡サイトについて質問がある場合、またはフィードバックを提供したい場合:[ヘルプ] アイコンをクリックして、「 [ドキュメント追跡の FAQ](http://go.microsoft.com/fwlink/?LinkId=523977)」にアクセスします。

## <a name="using-office-to-access-the-document-tracking-site"></a>Office を使用したドキュメント追跡サイトへのアクセス

-   Office アプリケーション、Word、Excel、PowerPoint、および Outlook: **[ホーム]** タブの **[保護]** グループで、**[保護]**  >  **[使用の追跡]** をクリックします。

Office アプリケーションでこれらのオプションが表示されない場合は、Azure Information Protection クライアントがコンピューターにインストールされていない、Office アプリケーションを再起動する必要がある、インストールを完了するためにコンピューターを再起動する必要がある、などの可能性があります。 Azure Information Protection クライアントのインストール方法の詳細については、「[Azure Information Protection クライアントをダウンロードしてインストールする](install-client-app.md)」を参照してください。


### <a name="other-ways-to-track-and-revoke-your-documents"></a>ドキュメントを追跡して取り消すための他の方法
Windows コンピューターで Office アプリケーションを使用して保護されたドキュメントを追跡するだけでなく、以下の代替策を使用することもできます。

-   **Web ブラウザーの使用**:この方法は、サポートされているすべてのデバイスで機能します。

-   **エクスプローラーの使用**:この方法は、Windows コンピューターで機能します。

#### <a name="using-a-web-browser-to-access-the-doc-tracking-site"></a>Web ブラウザーを使用したドキュメント追跡サイトへのアクセス

-   サポートされているブラウザーを使用して、 [ドキュメント追跡サイト](https://go.microsoft.com/fwlink/?LinkId=529562)に移動します。

    サポートされているブラウザー:Internet Explorer バージョン 10 以降の使用が推奨されますが、次のいずれかのブラウザーを使用してドキュメント追跡サイトを使用することもできます。

    -   Internet Explorer:バージョン 10 以降

    -   Internet Explorer 9、MS12-037 (Internet Explorer 用の累積的なセキュリティ更新プログラム: 2012 年 6 月 12 日) 以降

    -   Mozilla Firefox:バージョン 12 以降

    -   Apple Safari 5:バージョン 5 以降

    -   Google Chrome:バージョン 18 以降

#### <a name="using-file-explorer-to-access-the-doc-tracking-site"></a>エクスプローラーを使用したドキュメント追跡サイトへのアクセス

-   ファイルを右クリックして **[分類と保護 (プレビュー)]** を選択し、**Azure Information Protection ビューア** で [使用の追跡] アイコンを選択します。


## <a name="other-instructions"></a>その他の手順
操作方法に関する手順については、「Azure Information Protection ユーザー ガイド」の次のセクションを参照してください。

-   [作業内容](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


