---
title: ドキュメントの追跡と取り消し - Azure Information Protection
description: ドキュメントを保護した後は、保護されたドキュメントのユーザーによる使用状況を追跡できます。 ドキュメントが読まれる必要がなくなった場合は、必要に応じて、これらのドキュメントへのアクセスを取り消すこともできます。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/13/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 643c762e-23ca-4b02-bc39-4e3eeb657a1d
ms.subservice: doctrack
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 47cde44d90f1281338e94ad8bbb78cf7e230d0a1
ms.sourcegitcommit: b763a7204421a4c5f946abb7c5cbc06e2883199c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2020
ms.locfileid: "95569910"
---
# <a name="user-guide-track-and-revoke-your-documents-when-you-use-azure-information-protection"></a>ユーザー ガイド: Azure Information Protection を使用してドキュメントを追跡および取り消す

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8*
>
> *手順:[Windows 用 Azure Information Protection クライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Azure Information Protection を使用してドキュメントを保護した後は、保護されたドキュメントのユーザーによる使用状況を追跡できます。 ドキュメントが読まれる必要がなくなった場合は、必要に応じて、ドキュメントへのアクセスを取り消すこともできます。 このような場合は、**ドキュメント追跡サイト** を使用します。 このサイトには、Windows コンピューター、Mac コンピューターだけでなく、タブレットやスマートフォンからもアクセスできます。

このサイトにアクセスしたら、サインインしてドキュメントを追跡します。 [ドキュメント追跡および失効をサポートするサブスクリプション](https://www.microsoft.com/cloud-platform/azure-information-protection-features)が組織にあり、このサブスクリプションのライセンスが割り当てられている場合は、保護したファイルを開こうとしたユーザーおよび成功した (正常に認証された) かどうかを確認できます。 また、ユーザーがドキュメントへのアクセスを試みるたびに、その時間と場所がわかります。 ただし、まれに、報告された場所が正確でない場合があります。 たとえば、保護されたドキュメントを開くユーザーが VPN 接続を使用している場合、またはそのコンピューターに IPv6 アドレスが割り当てられている場合です。

ドキュメント追跡サイトで実行できる操作は次のとおりです。

- ドキュメントの共有を停止する必要がある場合: 
    
    - **[アクセスの取り消し]** をクリックします。 ドキュメントを継続して使用できる期間に注意してください。 カスタマイズされたメッセージを表示して、共有していたドキュメントへのアクセスを取り消すことを他のユーザーに知らせるかどうかを決めます。 ドキュメントへのアクセスを取り消しても、共有していたドキュメントが削除されるわけではありませんが、承認ユーザーはドキュメントを開けなくなります。
        
        ![ドキュメント追跡サイトの [アクセスの取り消し] アイコン](../media/tracking-site-revoke-access-icon.png)
        
- Excel にエクスポートする場合: 
    
    - **[CSV にエクスポート]** をクリックすると、データを変更して独自のビューとグラフを作成できるようになります。
         
        ![ドキュメント追跡サイトの [CSV にエクスポート] アイコン](../media/tracking-site-export-icon.png)
         
- 電子メール通知を構成する場合: 
     
    - **[設定]** をクリックし、ドキュメントへのアクセスがあれば電子メールで知らせるかどうかやその方法を選択します。
        
        ![ドキュメント追跡サイトで電子メール通知を構成する](../media/tracking-site-settings-email.png)

- 他のユーザーの共有したドキュメントを追跡し、アクセスを取り消す場合:
    
    - ユーザーが自分のドキュメントをドキュメント追跡サイトに登録している場合、Azure Information Protection の管理者は、[管理者] アイコンをクリックして、ユーザーの保護されているドキュメントを追跡して取り消すことができます。 このアイコンは管理者にのみ表示されます。
        
        ![ドキュメント追跡サイトの [管理者] アイコン](../media/tracking-site-admin-icon.png)
        
        グローバル管理者でもこのアイコンが表示されない場合、ドキュメントが共有されていません。 その場合、https://portal.azurerms.com/#/admin の URL からドキュメント追跡サイトにアクセスします。

管理者でない場合は、自分が保護したドキュメントのみを追跡してアクセスを取り消すことができます。 ドキュメント追跡サイトを使用して、保護した電子メールを追跡することはできません。

> [!NOTE] 
> 管理者がドキュメント追跡サイトのプライバシー制御を構成している場合は、組織のユーザーが追跡したドキュメントにアクセスした時期がわからないことがあります。管理者は、すべてのユーザーを除外することも、一部のユーザーのみを除外することもできます。 ただし、管理者でなくても、追跡しているドキュメントへのアクセスを取り消すことはいつでもできます。

自分が保護したドキュメントを追跡するには、Windows コンピューターを使用してドキュメント追跡サイトに登録する必要があります。 登録するには、エクスプローラーまたは Office アプリを使用します。

Azure Information Protection クライアントの現在の一般公開バージョンがある場合は、 [set-aipfilelabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel)コマンドレットで *enabletracking* パラメーターを使用するときに、保護されたドキュメントを PowerShell に登録することもできます。

## <a name="using-office-to-track-or-revoke-the-document"></a>Office を使用したドキュメントの追跡または取り消し

Office アプリケーション、Word、Excel、および PowerPoint の場合: 

1. 追跡または取り消し対象の保護されたドキュメントを開きます。

2. [**ホーム**] タブの [**保護**] グループで、[**保護**] [  >  **追跡と取り消し**] をクリックします。

    ![使用の追跡オプション](../media/track-usage-callout.png)
    
    Office アプリケーションでこれらのオプションが表示されない場合は、次のいずれかが理由の可能性があります。
    
    - Azure Information Protection クライアントがコンピューターにインストールされていない。
    
    - Office アプリケーションを再起動する必要がある。
    
    - インストールを完了するには、コンピューターを再起動する必要がある。
    
Azure Information Protection クライアントのインストール方法の詳細については、「[Azure Information Protection クライアントをダウンロードしてインストールする](install-client-app.md)」を参照してください。

## <a name="using-file-explorer-to-track-or-revoke-the-document"></a>エクスプローラーを使用したドキュメントの追跡または取り消し

1. 保護されたファイルを右クリックし、**[分類して保護する]** を選択します。

2. **[分類と保護 - Azure Information Protection]** ダイアログ ボックスから、**[追跡と取り消し]** を選択します。

    ![[分類と保護 - Azure Information Protection] ダイアログ ボックスの [追跡と取り消し] アイコン](../media/track-and-revoke.png)


### <a name="using-a-web-browser-to-track-and-revoke-documents-that-you-have-registered"></a>Web ブラウザーを使用した登録ドキュメントの追跡と取り消し

Office アプリまたはエクスプローラーを使用して保護されたドキュメントを登録すると、サポートされる Web ブラウザーを使用してそのドキュメントの追跡および取り消しを行うことができます。

- Windows PC、Mac コンピューター、またはモバイル デバイスで[ドキュメント追跡サイト](https://go.microsoft.com/fwlink/?LinkId=529562)にアクセスします。

    **サポートされているブラウザー**: バージョン10以上の Internet Explorer を使用することをお勧めしますが、次のいずれかのブラウザーを使用してドキュメント追跡サイトを使用することもできます。

    - Internet Explorer:バージョン 10 以降

    - Internet Explorer 9、MS12-037 (Internet Explorer 用の累積的なセキュリティ更新プログラム: 2012 年 6 月 12 日) 以降

    - Mozilla Firefox:バージョン 12 以降

    - Apple Safari 5:バージョン 5 以降

    - Google Chrome:バージョン 18 以降


## <a name="other-instructions"></a>その他の手順
他の操作手順については、Azure Information Protection ユーザー ガイドを参照してください。

- [目的に合ったトピックをクリックしてください](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>管理者向け追加情報    
[管理者ガイド](client-admin-guide.md)の「[Azure Information Protection のドキュメント追跡の構成と使用](client-admin-guide-document-tracking.md)」をご覧ください。
