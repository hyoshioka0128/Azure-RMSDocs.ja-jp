---
title: "Azure RMS の ADAL 認証を構成する | Azure RMS"
description: "Azure ADAL 基盤の認証を構成する手順について説明します。"
keywords: "認証、RMS、ADAL"
author: bruceperlerms
manager: mbaldwin
ms.date: 06/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 56d0538243af49580f24c701ad5097b30f3059b0
ms.openlocfilehash: 9b912a2a66838dc6e6a3b227bcfe4ac589fe06c1


---

# Azure RMS の ADAL 認証を構成する

このトピックでは、Azure ADAL 基盤の認証を構成する手順について説明します。

## Azure 認証のセットアップ

以下のものが必要です。

- [Microsoft Azure のサブスクリプション](https://azure.microsoft.com/en-us/) (無料試用版で十分です)。 詳細については、「[How users sing up for RMS for individuals (ユーザーが個人向け RMS にサインアップする方法)](../understand-explore/rms-for-individuals-user-sign-up.md)」を参照してください。
- Microsoft Azure Rights Management のサブスクリプション (無料の[個人向け RMS](https://technet.microsoft.com/en-us/library/dn592127.aspx) アカウントで十分です)。

> [!NOTE] 
> IT 管理者に、Microsoft Azure Rights Management のサブスクリプションがあるかどうかを問い合わせ、以下の手順の実行を依頼します。 組織にサブスクリプションがない場合、IT 管理者に作成してもらいます。 また、IT 管理者は、*Microsoft アカウント* (Hotmail など) ではなく、*職場または学校アカウント*でサブスクライブする必要があります。

Microsoft Azure にサインアップした後:

- 管理者特権を持つアカウントを使用して、組織の [Microsoft Azure の管理ポータル](https://manage.windowsazure.com)にログインします。

![Azure にログインする](../media/AzurePortalLogin.png)

- ポータルの左下にある **[Active Directory]** アプリケーションを参照します。

![[Active Directory] を選択する](../media/AzureADPick.png)

- ディレクトリをまだ作成していない場合は、ポータルの左下隅にある **[新規]** ボタンを選択します。

![[新規] を選択する](../media/AzureNewBtn.png)

- **[Rights Management]** タブを選択し、**[Rights Management のステータス]** が **[アクティブ]**、**[不明]**、または **[許可されていません]** であることを確認します。 ステータスが **[非アクティブ]** の場合は、ポータル中央下部にある **[アクティブ化]** ボタンを選択し、選択を確認します。

![[アクティブ化] を選択する](../media/RMTab.png)

- 次に、ディレクトリを選択して [アプリケーション] を選択し、ディレクトリに新しい*ネイティブ アプリケーション*を作成します。

![[アプリケーション] を選択する](../media/CreateNativeApp.png)

- ポータル中央下部の **[追加]** ボタンを選択します。

![[追加] を選択する](../media/AddAppBtn.png)

- メッセージが表示されたら、**[組織で開発中のアプリケーションを追加]** を選択します。

![[組織で開発中のアプリケーションを追加] の選択](../media/AddAnAppPick.png)

- **[ネイティブ クライアント アプリケーション]** を選択して **[次へ]** ボタンを選択し、アプリケーションの名前を指定します。

![アプリの名前を指定する](../media/TellUsInput.png)

- リダイレクト URI を追加し、[次へ] を選択します。
  リダイレクト URI は、有効な URI で、ディレクトリに対して一意である必要があります。 たとえば、`com.mycompany.myapplication://authorize` のような URI を使用します。

![リダイレクト URI を追加する](../media/RedirectURI.png)

- ディレクトリでアプリケーションを選択し、**[構成]** を選択します。

![[構成] を選択する](../media/ConfigYourApp.png)

>[!NOTE] 
> **[クライアント ID]** と **[リダイレクト URI]** をコピーし、後で RMS クライアントを構成するときのために保存します。

- アプリケーション設定下部で **[他のアプリケーションに対するアクセス許可]** の **[アプリケーションの追加]** ボタンを選択します。

>[!NOTE] 
> Windows Azure Active Directory に表示される **[デリゲートされたアクセス許可]** は既定では正しく、オプションは 1 つだけ選択します。そのオプションは **[サインインとユーザー プロファイルの読み取り]** になります。

![[アプリケーションの追加] を選択する](../media/PermissionsToOtherBtn.png)

- この GUID `00000012-0000-0000-c000-000000000000` を **[次で始まる]** 編集ボックスに追加し、チェック ボタンを選択します。

![GUID を追加する](../media/AddGUID.png)

- **[Microsoft Rights Management]** の隣の [+] ボタンを選択します。

![[+] ボタンの選択](../media/ChoosePlusBtn.png)

- ダイアログの左下隅にあるチェック マークを選択します。

![チェック マークを選択する](../media/ChooseCheck.png)

- Azure RMS 用アプリケーションに依存関係を追加する準備ができました。 依存関係を追加するには、**[他のアプリケーションに対するアクセス許可]** で新しい **[Microsoft Rights Management サービス]** エントリを選択し、**[デリゲートされたアクセス許可]** ドロップ ボックスで **[ユーザー用の保護されたコンテンツを作成してアクセスする]** チェック ボックスをオンにします。

![アクセス許可を設定する](../media/AddDependency.png)

- ポータル中央下部の **[保存]** アイコンを選択して、アプリケーションを保存します。

![[保存] を選択する](../media/SaveApplication.png)



<!--HONumber=Jul16_HO3-->


