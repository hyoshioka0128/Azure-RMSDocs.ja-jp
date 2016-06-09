---
# required metadata

title: Windows ストアのセットアップ | Azure RMS
description: Windows Store アプリケーションは Microsoft Rights Management SDK 4.2 を使用して、そのアプリケーション内で統合情報保護を有効にできます。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 2720aa0e-0d37-469f-be99-678bf95a9c51
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Windows ストアのセットアップ

Windows ストア アプリケーションは Microsoft Rights Management SDK 4.2 を使用して、Azure Active Directory Rights Management (AAD RM) を使用することでそのアプリケーション内で統合情報保護を有効にできます。

このトピックでは、独自の新しいアプリを作成するために環境をセットアップする方法について説明します。

-   [必要条件](#prerequisites)
-   [省略可能](#optional)
-   [開発環境の構成](#configuring-your-development-environment)
-   [参照](#see-also)

## 必要条件


開発システムには、以下のソフトウェアが必要です。

-   [Windows 8.1](http://windows.microsoft.com/en-US/windows-8/meet) オペレーティング システム
-   [Windows 8.1 用 Windows SDK](https://msdn.microsoft.com/en-us/windows/desktop/bg162891.aspx)
-   Microsoft [Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview) 以降、または Visual Studio Express 2012 (Windows 8.0/8.1 用 Windows SDK に付属)
-   Windows ストア アプリケーション用の MS RMS SDK 4.2 パッケージ。 詳細については、「[作業開始](get-started.md)」を参照してください。
-   認証ライブラリ: [Azure AD Authentication Library](https://msdn.microsoft.com/en-us/library/jj573266.aspx) または他の使用可能な認証ライブラリを使用することをお勧めします。

[新機能](release-notes.md)に関するトピックで、API の更新情報、デバイスと環境情報、リリース ノート、よく寄せられる質問 (FAQ) をお読みください。

## 省略可能

UI ライブラリは、独自のカスタム UI 作成を望まない開発者のために、使用操作と保護操作用の再利用可能な UI を提供します - [Windows ストア アプリ用の UI ライブラリ](https://github.com/AzureAD/rms-sdk-ui-for-windowsstore)。 Windows ストア アプリのサンプル アプリケーションも提供しています - [Windows ストア用の RMS サンプル アプリケーション](https://github.com/AzureADSamples/rms-samples-for-windowsstore)。

## 開発環境の構成


-   Visual Studio を開きます。
-   **[ファイル]**、**[新規作成]**、**[プロジェクト]** の順にクリックします。
-   **[新しいプロジェクト]** ダイアログ ボックスで、**[Visual C\#]**、**[空のアプリケーション (Windows)]** の順にクリックし、**[OK]** をクリックします。

    ![新規プロジェクトの作成](../media/winrtsetup-newproj.png)

-   **ソリューション エクスプローラー**でプロジェクトを右クリックし、**[参照の追加]** を選択して **[参照の追加]** ダイアログ ボックスを開きます。

    ![参照の追加](../media/winrtsetup-addref.png)

-   **[参照の追加]** ダイアログ ボックスで **[参照]** をクリックし、SDK パッケージを解凍したフォルダー内にある *Microsoft.RightsManagement.dll* ファイルを選択します。
-   **管理対象アプリ** - 管理対象アプリを構築するには、**[Windows 8.1]**-&gt;**[拡張機能]** を選択し、**[Windows Visual C++ Runtime Package for Windows]** チェック ボックスをオンにして、この参照を追加する必要があります。

    ![拡張機能の追加](../media/winrtsetup-refmngr.png)

-   **機能を追加する** - アプリケーションで SDK を使用するには、[インターネット (クライアントとサーバー)] 機能が必要です。 この機能をアプリに追加するには、*Package.appxmanifest* ファイルをプロジェクトで開き、**[機能]** タブに移動して追加します。

これで、新しい独自の Windows ストア アプリを作成する準備が整いました。

### 参照

[作業開始](get-started.md)

[新機能](release-notes.md)

[開発者の用語と概念](core-concepts.md)

[Windows 8](http://windows.microsoft.com/en-US/windows-8/meet)

[Visual Studio 2012](http://www.microsoft.com/visualstudio/eng/products/visual-studio-overview)

[Windows API リファレンス](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement)


<!--HONumber=May16_HO2-->

