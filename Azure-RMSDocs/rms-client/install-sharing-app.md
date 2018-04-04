---
title: RMS 共有アプリケーションのダウンロードとインストール - AIP
description: Windows 用 RMS 共有アプリケーションを対話形式でインストールし、他のユーザーとドキュメントを安全に共有できるようにするための手順です。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 6c9fe3e28cb44812a6f3a5830546128975522b5f
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="download-and-install-the-rights-management-sharing-application"></a>Rights Management 共有アプリケーションをダウンロードしてインストールする

>*適用対象: Active Directory Rights Management サービス[、Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*

> [!IMPORTANT]
> **サポートの終了通知**: Windows 用 Rights Management 共有アプリケーションは [Azure Information Protection クライアント](aip-client.md)に置き換えられます。 この古いアプリケーションのサポートは、2019 年 1 月 31 日に停止されます。

RMS 共有アプリケーションをインストールするのにローカル管理者である必要はありません。 ただし、ローカル管理者ではなく、かつ Office 2010 を使用している場合は、いくつか制限があります。 詳細については、このページの「[ローカル管理者ではなく、かつ Office 2010 を使用している場合](#if-you-are-not-a-local-administrator-and-use-office-2010)」を参照してください。

## <a name="to-download-and-install-the-rights-management-sharing-application"></a>Rights Management 共有アプリケーションをダウンロードしてインストールするには

1.  Microsoft Web サイトの [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) ページに移動します。

2.  **[コンピューター]** セクションで、 **Windows 用 RMS アプリケーション** のアイコンをクリックして、Microsoft Rights Management 共有アプリケーションをインストールする **Setup.exe** ファイルを保存します。

3.  ダウンロードされた Setup.exe ファイルをダブルクリックします。 続行を確認するメッセージが表示されたら、**[はい]** をクリックします。

4.  **[Microsoft RMS のセットアップ]** ページで、**[次へ]** をクリックし、インストールが完了するまで待機します。

    > [!NOTE]
    > RMS 共有アプリケーションには、Microsoft .NET Framework のバージョン 4.0 以上が必要です。 これがインストールされているかどうかがセットアップで確認され、インストールされていない場合は、インストールするためのリンクを含むメッセージが表示されます。

5.  インストールが完了したら、**[再起動]** をクリックして、コンピューターを再起動し、インストールを完了します。 または、**[閉じる]** をクリックして、後でコンピューターを再起動し、インストールを完了します。

これで、ファイルの保護を開始したり、他のユーザーが保護しているファイルを読み取ったりする準備ができました。

## <a name="if-you-are-not-a-local-administrator-and-use-office-2010"></a>ローカル管理者ではなく、かつ Office 2010 を使用している場合
コンピューターへのサインイン時にローカルの管理者権限を持っておらず、かつセットアップ時に Office 2010 がインストールされていることが検出される場合、この構成では一部のシナリオがうまくいかないことを示す警告メッセージが表示されます。 シナリオは次のとおりです。

-   組織で、オンプレミス版の Rights Management ではなく、Azure Information Protection から Azure Rights Management サービスを使用する場合

    -   Office の Information Rights Management (IRM) の機能は利用できません。 たとえば、メールの **[転送不可]** オプションや、Word と Excel の **[ファイル]** メニューから設定できる **[アクセスの制限]** アクセス許可は利用できません。 リボンの [保護ファイルの共有] オプションやエクスプローラーの右クリック オプションを使用できます。

-   組織で、Azure Information Protection から Azure Rights Management サービスではなく、オンプレミス版の Rights Management を使用する場合

    -   Azure Rights Management サービスを使用している他の組織のユーザーから送信された、保護されたドキュメントを読み取ることはできません。

ローカル管理者でなくとも、Office 365 または Office 2013 を使用している場合は、このメッセージが表示されません。これらのシナリオはサポートされています。

このような既知の制限はありますが、インストールを続行できます。 また、インストールを中止することもできます。その場合、手順 3. で Setup.exe を実行するときに **[管理者として実行]** オプションを使用して再実行するか、管理者にインストールしてもらうように依頼できます。 管理者は、インストールが自動的に行われるように[このインストールをスクリプト化](sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application)できます。

## <a name="examples-and-other-instructions"></a>例とその他の説明
Rights Management 共有アプリケーションの使用方法の例と操作手順については、Rights Management 共有アプリケーション ユーザー ガイドの次のセクションをご覧ください。

-   [RMS 共有アプリケーションの使用例](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [作業内容](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>参照
[Rights Management 共有アプリケーション ユーザー ガイド](sharing-app-user-guide.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
