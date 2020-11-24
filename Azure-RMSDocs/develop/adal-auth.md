---
title: ADAL 認証用のアプリの構成 - AIP
description: Azure ADAL 基盤の認証を使用するように Azure Information Protection アプリを構成する手順
keywords: 認証, RMS, ADAL, Informatin Protection,
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 03/13/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev, has-adal-ref
ms.openlocfilehash: 568ed4dee01c59f8808442a4499b8a858f9ebcf5
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "95570358"
---
# <a name="configure-your-app-for-adal-authentication"></a>ADAL 認証用のアプリの構成

このトピックでは、アプリケーションを Azure Active Directory Authentication Library (ADAL) ベースの認証用に構成する手順について説明しています。

## <a name="azure-authentication-setup"></a>Azure 認証のセットアップ

以下のものが必要になります。

- [Microsoft Azure のサブスクリプション](https://azure.microsoft.com/) (無料試用版で十分です)。 詳細については、「[How users sign up for RMS for individuals](../rms-for-individuals.md)」 (ユーザーが個人向け RMS にサインアップする方法) を参照してください。
- Microsoft Azure Rights Management のサブスクリプション (無料の[個人向け RMS](../rms-for-individuals.md) アカウントで十分です)。

> [!NOTE]
> IT 管理者に、Microsoft Azure Rights Management のサブスクリプションがあるかどうかを問い合わせ、以下の手順の実行を依頼します。 組織にサブスクリプションがない場合、IT 管理者に作成してもらいます。 また、IT 管理者は、*Microsoft アカウント* (Hotmail など) ではなく、*職場または学校アカウント* でサブスクライブする必要があります。

Microsoft Azure にサインアップした後:

- 管理者特権を持つアカウントを使用して、組織の [Microsoft Azure の管理ポータル](https://manage.windowsazure.com)にログインします。

![Azure ログイン](../media/AzurePortalLogin.png)

- ポータルの左下にある **[Active Directory]** アプリケーションを参照します。

![Active Directory の選択](../media/AzureADPick.png)

- ディレクトリをまだ作成していない場合は、ポータルの左下隅にある **[新規]** ボタンを選択します。

![[新規] を選択する](../media/AzureNewBtn.png)

- **[Rights Management]** タブを選択し、**[Rights Management のステータス]** が **[アクティブ]**、**[不明]**、または **[許可されていません]** であることを確認します。 ステータスが **[非アクティブ]** の場合は、ポータル中央下部にある **[アクティブ化]** ボタンを選択し、選択を確認します。

![[アクティブ化] を選択する](../media/RMTab.png)

- 次に、ディレクトリを選択して [アプリケーション] を選択し、ディレクトリに新しい *ネイティブ アプリケーション* を作成します。

![[アプリケーション] を選択する](../media/CreateNativeApp.png)

- ポータル中央下部の **[追加]** ボタンを選択します。

![[追加] を選択する](../media/AddAppBtn.png)

- メッセージが表示されたら、**[組織で開発中のアプリケーションを追加]** を選択します。

![[組織で開発中のアプリケーションを追加] の選択](../media/AddAnAppPick.png)

- **[ネイティブ クライアント アプリケーション]** を選択して **[次へ]** ボタンを選択し、アプリケーションの名前を指定します。

![アプリの名前を指定する](../media/TellUsInput.png)

- リダイレクト URI を追加し、[次へ] を選択します。
  リダイレクト URI は、有効な URI で、ディレクトリに対して一意である必要があります。 たとえば、`https://contoso.azurewebsites.net/.auth/login/done` のような URI を使用します。

![リダイレクト URI を追加する](../media/RedirectURI.png)

- ディレクトリでアプリケーションを選択し、**[構成]** を選択します。

![[構成] を選択する](../media/ConfigYourApp.png)

>[!NOTE]
> **[クライアント ID]** と **[リダイレクト URI]** をコピーし、後で RMS クライアントを構成するときのために保存します。

- アプリケーション設定下部で **[他のアプリケーションに対するアクセス許可]** の **[アプリケーションの追加]** ボタンを選択します。

>[!NOTE]
> Windows Azure Active Directory に表示される **[デリゲートされたアクセス許可]** は既定では正しく、オプションは 1 つだけ選択します。そのオプションは **[サインインとユーザー プロファイルの読み取り]** になります。

![[アプリケーションの追加] を選択する](../media/PermissionsToOtherBtn.png)

- **[Microsoft Rights Management]** の隣の [+] ボタンを選択します。

![[+] ボタンの選択](../media/ChoosePlusBtn.png)

- ダイアログの左下隅にあるチェック マークを選択します。

![チェック マークを選択する](../media/choosecheck01.png)

- Azure RMS 用アプリケーションに依存関係を追加する準備ができました。 依存関係を追加するには、**[他のアプリケーションに対するアクセス許可]** で新しい **[Microsoft Rights Management サービス]** エントリを選択し、**[デリゲートされたアクセス許可]** ドロップ ボックスで **[ユーザー用の保護されたコンテンツを作成してアクセスする]** チェック ボックスをオンにします。

![アクセス許可を設定する](../media/AddDependency.png)

- ポータルの下部にある [ **保存** ] アイコンを選択して、アプリケーションを保存し、変更を保持します。

![[保存] を選択する](../media/SaveApplication.png)