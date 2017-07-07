---
title: "Windows Phone のセットアップ | Azure RMS"
description: "Windows Phone アプリケーションは Microsoft Rights Management SDK 4.2 を使用して、そのアプリケーション内で統合情報保護を有効にできます。"
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e25a446e-b977-4736-9c65-7711171fb0e1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 1ec4ccc3c20b821023d32cec33147660feb575f8
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2017
---
# <a name="windows-phone-setup"></a>Windows Phone のセットアップ


Windows Phone アプリケーションは Microsoft Rights Management SDK 4.2 を使用して、Azure Active Directory Rights Management (AAD RM) を使用することでそのアプリケーション内で統合情報保護を有効にできます。

このトピックでは、独自の新しいアプリを作成するために環境をセットアップする方法について説明します。

-   [必要条件](#prerequisites)
-   [開発環境の構成](#configuring-your-development-environment)
-   [関連項目](#see-also)

## <a name="prerequisites"></a>必要条件


開発システムには、以下のソフトウェアが必要です。

-   [Windows 8.1](http://windows.microsoft.com/en-US/windows-8/meet) オペレーティング システム
-   [Windows Phone 8.1 の開発ツール (SDK)](http://dev.windowsphone.com/en-us/downloadsdk)
-   Microsoft [Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview) 以降または Visual Studio Express 2012 (Windows Phone SDK 8.0/8.1 に付属)
-   Windows Phone 向け MS RMS SDK 4.2 パッケージ 詳細については、「[作業開始](get-started.md)」を参照してください。
-   認証ライブラリ: [Azure AD Authentication Library](https://msdn.microsoft.com/en-us/library/jj573266.aspx) または他の使用可能な認証ライブラリを使用することをお勧めします。

「[新機能](release-notes.md)」のトピックで、API の更新情報、デバイスと環境情報、リリース ノート、よく寄せられる質問 (FAQ) をお読みください。

[Windows Phone の開発](https://msdn.microsoft.com/en-us/library/windowsphone/develop/ff402535.aspx)の詳細については、Windows Phone デベロッパー センターでご確認ください。

## <a name="configuring-your-development-environment"></a>開発環境の構成


-   *Visual Studio* を開きます。
-   **[ファイル]** をクリックします。 **[ファイル]** メニューの **[新規作成]** をクリックし、**[プロジェクト]** をクリックします。
-   **[新しいプロジェクト]** ダイアログ ボックスで、**[Visual C\#]**、**[空のアプリケーション (Windows Phone)]** の順に選択し、**[OK]** をクリックします。

    ![新規プロジェクトの作成](../media/wpsetup-newproj.png)

-   ソリューション エクスプローラーでプロジェクトを右クリックし、**[参照の追加]** を選択して **[参照の追加]** ダイアログ ボックスを開きます。

    ![参照の追加](../media/wpsetup-addref.png)

-   **[参照の追加]** ダイアログ ボックスの左下で **[参照]** をクリックし、パッケージを解凍したフォルダー内にある *Microsoft.RightsManagment.dll* ファイルを選択します。
-   **管理対象アプリ** - 管理対象アプリを構築するには、この参照を追加する必要があります。**[Windows 8.1]**-&gt;**[拡張機能]** を選択し、**[Windows Visual C++ Runtime Package for Windows]** のチェック ボックスをオンにしてください。

    ![拡張機能の追加](../media/wpsetup-refmngr.png)

-   **機能を追加する** - アプリケーションで SDK を使用するには、[インターネット (クライアントとサーバー)] 機能が必要です。 この機能をアプリに追加するには、*Package.appxmanifest* ファイルをプロジェクトで開き、**[機能]** タブに移動して追加します。

これで、独自の Windows Phone アプリを作成する準備が整いました。

### <a name="see-also"></a>関連項目

[作業開始](get-started.md)

[新機能](release-notes.md)

[コア概念](core-concepts.md)

[Windows Phone の開発](https://msdn.microsoft.com/en-us/library/windowsphone/develop/ff402535.aspx)

[Windows API リファレンス](https://msdn.microsoft.com/library/dn891914.aspx)

[Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview)

[Windows Phone SDK](http://dev.windowsphone.com/en-us/downloadsdk)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]