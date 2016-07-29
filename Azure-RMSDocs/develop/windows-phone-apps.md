---
title: "Windows Phone のセットアップ | Azure RMS"
description: "Windows Phone アプリケーションは Microsoft Rights Management SDK 4.2 を使用して、そのアプリケーション内で統合情報保護を有効にできます。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e25a446e-b977-4736-9c65-7711171fb0e1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 79397c82d9478cbd55630a376fe2d12f3873ebc4
ms.openlocfilehash: 1728a094dfaa869ae490e86d10ffe5ebcf4bfa5d


---

# Windows Phone のセットアップ


Windows Phone アプリケーションは Microsoft Rights Management SDK 4.2 を使用して、Azure Active Directory Rights Management (AAD RM) を使用することでそのアプリケーション内で統合情報保護を有効にできます。

このトピックでは、独自の新しいアプリを作成するために環境をセットアップする方法について説明します。

-   [必要条件](#prerequisites)
-   [開発環境の構成](#configuring-your-development-environment)
-   [参照](#see-also)

## 必要条件


開発システムには、以下のソフトウェアが必要です。

-   [Windows 8.1](http://windows.microsoft.com/en-US/windows-8/meet) オペレーティング システム
-   [Windows Phone 8.1 の開発ツール (SDK)](http://dev.windowsphone.com/en-us/downloadsdk)
-   Microsoft [Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview) 以降または Visual Studio Express 2012 (Windows Phone SDK 8.0/8.1 に付属)
-   Windows Phone 向け MS RMS SDK 4.2 パッケージ 詳細については、「[作業開始](get-started.md)」を参照してください。
-   認証ライブラリ: [Azure AD Authentication Library](https://msdn.microsoft.com/en-us/library/jj573266.aspx) または他の使用可能な認証ライブラリを使用することをお勧めします。

「[新機能](release-notes.md)」のトピックで、API の更新情報、デバイスと環境情報、リリース ノート、よく寄せられる質問 (FAQ) をお読みください。

[Windows Phone の開発](https://msdn.microsoft.com/en-us/library/windowsphone/develop/ff402535.aspx)の詳細については、Windows Phone デベロッパー センターでご確認ください。

## 開発環境の構成


-   *Visual Studio* を開きます。
-   **[ファイル]** をクリックします。 **[ファイル]** メニューの **[新規作成]** をクリックし、**[プロジェクト]** をクリックします。
-   **[新しいプロジェクト]** ダイアログ ボックスで、**[Visual C\#]**、**[空のアプリケーション (Windows Phone)]** の順に選択し、**[OK]** をクリックします。

    ![新規プロジェクトの作成](../media/wpsetup-newproj.png)

-   ソリューション エクスプローラーでプロジェクトを右クリックし、**[参照の追加]** を選択して **[参照の追加]** ダイアログ ボックスを開きます。

    ![参照の追加](../media/wpsetup-addref.png)

-   **[参照の追加]** ダイアログ ボックスの左下で **[参照]** をクリックし、パッケージを解凍したフォルダー内にある *Microsoft.RightsManagment.dll* ファイルを選択します。
-   **管理対象アプリ** - 管理対象アプリを構築するには、**[Windows 8.1]**-&gt;**[拡張機能]** を選択し、**[Windows Visual C++ Runtime Package for Windows]** チェック ボックスをオンにして、この参照を追加する必要があります。

    ![拡張機能の追加](../media/wpsetup-refmngr.png)

-   **機能を追加する** - アプリケーションで SDK を使用するには、[インターネット (クライアントとサーバー)] 機能が必要です。 この機能をアプリに追加するには、*Package.appxmanifest* ファイルをプロジェクトで開き、**[機能]** タブに移動して追加します。

これで、独自の Windows Phone アプリを作成する準備が整いました。

### 参照

[作業開始](get-started.md)

[新機能](release-notes.md)

[コア概念](core-concepts.md)

[Windows Phone の開発](https://msdn.microsoft.com/en-us/library/windowsphone/develop/ff402535.aspx)

[Windows API リファレンス](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement)

[Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview)

[Windows Phone SDK](http://dev.windowsphone.com/en-us/downloadsdk)

 

 






<!--HONumber=Jul16_HO4-->


