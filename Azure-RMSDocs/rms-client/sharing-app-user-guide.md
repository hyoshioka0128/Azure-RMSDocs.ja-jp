---
title: "Rights Management 共有アプリケーション ユーザー ガイド | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: eaf6d02c-aa36-4915-856e-49bb71ab1484
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 384a58f32aae8c7d908392e7fd9a1629bc05cdff
ms.openlocfilehash: d3727eb963532e03137aea2140293fa9c5821db2


---

# Rights Management 共有アプリケーション ユーザー ガイド

*適用対象: Active Directory Rights Management サービス、Azure Rights Management、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*

Windows 用 Microsoft Rights Management (RMS) 共有アプリケーションは、重要なドキュメントや画像を、それらを表示してはならないユーザーから保護するために役立ちます。それらを電子メールで送信したり、別のデバイスに保存したりする場合でも同様です。 また、このアプリケーションを使用して、他のユーザーが同じ Rights Management テクノロジを使って保護したファイルを開いて使用することもできます。

必要なのは、Windows 7 Service Pack 1 を実行しているコンピューターのみです。 次に、この無料のアプリケーションをマイクロソフトから [ダウンロードしてインストール](http://go.microsoft.com/fwlink/?LinkId=303970) します。

このガイドで答えられていない質問がある場合は、「 [Windows 用 Microsoft Rights Management 共有アプリケーションの FAQ](http://go.microsoft.com/fwlink/?LinkId=303971)」を参照してください。 このページには、問題が生じた場合のトラブルシューティング情報も含まれています。

## RMS 共有アプリケーションの使用例
ここでは、ファイルを保護するために RMS 共有アプリケーションを使用する方法の例をいくつか示します。

|目的の操作|実行方法|
|----------------|------------------|
|**… 別の組織に勤務していて、信頼できるユーザーと安全に財務情報を共有する**<br /><br />パートナー企業と協力しており、予想売上高を含む Excel スプレッドシートをそのパートナー企業に電子メールで送信したいと考えます。 パートナー企業は数値を表示できるようにしますが、変更はできないようにします。|Excel のリボンの [ **保護ファイルの共有** ] ボタンを使用して、パートナー企業の協力する 2 人のユーザーの電子メール アドレスを入力し、[ **閲覧者 – 表示のみ**] を選択して、[ **送信**] をクリックします。<br /><br />パートナー企業に電子メールが届くと、電子メールで指定された受信者のみがスプレッドシートを表示できますが、保存、編集、印刷、または転送することはできません。<br /><br />ステップ バイ ステップ: [Rights Management 共有アプリケーションを使用して、電子メールで共有するファイルを保護する](sharing-app-protect-by-email.md)。|
|**… iOS デバイスを使用している相手に電子メールで安全にドキュメントを送信する**<br /><br />iOS デバイスで定期的に電子メールを確認していることを知っている同僚に、機密性の高い Word 文書を送信したいと考えます。|エクスプローラーを使用して、ファイルを右クリックし、**[Share Protected (保護ファイルの共有)]** を選択し、 ファイルを添付ファイルとして同僚に送信します。<br /><br />受信者は、iOS デバイスで電子メールを受信します。 受信者は iPad および iPhone 向け Office を持っていないため、電子メールに含まれている共有アプリケーションのダウンロード方法を示すリンクをクリックし、iOS デバイス用のバージョンをインストールしてドキュメントを表示します¹。<br /><br />ステップ バイ ステップ: [Rights Management 共有アプリケーションを使用して、電子メールで共有するファイルを保護する](sharing-app-protect-by-email.md)。|
|**… 保護されたドキュメントを開いたユーザーとそのタイミングを確認し、必要に応じてアクセス権を取り消す**<br /><br />機密の設計ドキュメントを複数のサプライヤー候補と安全に共有したところで、だれがいつどこからそのドキュメントにアクセスしたかを確認したいと考えます。 サプライヤーの 1 社に業務を発注するときに、元のドキュメントへのアクセスを取り消し、ドキュメントを共有したその他のユーザーが読み取れなくなるようにしたいと考えます。|ドキュメントを電子メールで共有した後、 [ドキュメント追跡サイト](http://go.microsoft.com/fwlink/?LinkId=529562) に移動して、だれがいつそのドキュメントにアクセスしたか確認します。 その共有を停止する必要がある場合は、アクセスを取り消すオプションを選択します。<br /><br />ステップ バイ ステップ: [RMS 共有アプリケーションを使用してドキュメントを追跡および取り消す](sharing-app-track-revoke.md)。|
|**… 安全に共有された添付ファイルを含む電子メール メッセージで受信した添付ファイルを読み取ろうとしても、会社が Rights Management を使用していないため、これを読み取ることができない**<br /><br />電子メールの送信者は、これまでにビジネスを行ったことがあるため信頼できるユーザーで、新しいビジネス チャンスに関する情報を送信してきている可能性があると考えます。|電子メール内の手順に従ってリンクをクリックし、Microsoft Rights Management にサインアップします。 Microsoft は、組織に Azure Rights Management が含まれているサブスクリプションがないことを確認し、無料のサインアップ手続きを実行するための電子メールを送信します。新しいアカウントでログインします。 電子メールの 2 番目のリンクをクリックして Rights Management 共有アプリケーションをインストールすると、電子メールの添付ファイルを開いて、新しいビジネス チャンスについて読むことができます。<br /><br />ステップ バイ ステップ: [Rights Management によって保護されたファイルを表示して使用する](sharing-app-view-use-files.md)。|
|**… ノート パソコン上の会社の機密ファイルを保護し、社外のユーザーがアクセスできないようにする**<br /><br />出張が多く、ノート パソコンを使用して、未承認のアクセスに対して保護する必要があるフォルダーのファイルにアクセスして更新しています。|ノート パソコンには RMS 共有アプリケーションがインストールされています。 エクスプローラーを使用して、ファイルをすばやく保護するテンプレートでファイルを保護しています。 ノート パソコンが盗まれたとしても、社外の人物はこれらのドキュメントにアクセスできないので安心です。<br /><br />ステップ バイ ステップ: [Rights Management 共有アプリケーションを使用して、デバイス上のファイルを保護する &#40;インプレースの保護&#41;](sharing-app-protect-in-place.md)。|
¹ PDF レンダリング Powered by Foxit。 Copyright © 2003–2014 by Foxit Corporation.

## 作業内容
> [!NOTE]
> [サポートされているファイルの種類](sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions)や、[エンタープライズ ネットワークにこのアプリケーションをインストールする方法](sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application)など、詳細な技術情報については、「[Rights Management 共有アプリケーション管理者ガイド](sharing-app-admin-guide.md)」を参照してください。

- [共有アプリケーションのダウンロードとインストール](install-sharing-app.md)

- [デバイス上のファイルを保護 (保護済み)](sharing-app-protect-in-place.md)

- [電子メールで共有するファイルを保護する](sharing-app-protect-by-email.md)

- [保護されたファイルに対するアクセス許可を変更する](sharing-app-reprotect-files.md)

- [ドキュメントを追跡および取り消す](sharing-app-track-revoke.md)

- [保護されているファイルの表示と使用](sharing-app-view-use-files.md)

- [ファイルからの保護の削除](sharing-app-remove-protection.md)

- [キーボード ショートカット](sharing-app-keyboard-shortcuts.md)

- [ダイアログ ボックスで設定を指定する](sharing-app-dialog-box.md)






<!--HONumber=Jul16_HO3-->


