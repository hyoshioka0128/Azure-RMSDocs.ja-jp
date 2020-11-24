---
title: Windows ストアのセットアップ | Azure RMS
description: Windows ストア アプリケーションは Microsoft Rights Management SDK 4.2 を使用して、そのアプリケーション内で統合情報保護を有効にできます。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 12/10/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2720aa0e-0d37-469f-be99-678bf95a9c51
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 0382a1a97d65938c5d90d10d4e572697558223cc
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "95570734"
---
# <a name="windows-store-setup"></a>Windows ストアのセットアップ

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

Windows ストア アプリケーションは Microsoft Rights Management SDK 4.2 を使用して、Azure Active Directory Rights Management (AAD RM) を使用することでそのアプリケーション内で統合情報保護を有効にできます。

このトピックでは、独自の新しいアプリを作成するために環境をセットアップする方法について説明します。

-   [前提条件](#prerequisites)
-   [省略可能](#optional)
-   [開発環境の構成](#configuring-your-development-environment)
-   [参照](#see-also)

## <a name="prerequisites"></a>前提条件


開発システムには、以下のソフトウェアが必要です。

-   [Windows 8.1](https://windows.microsoft.com/windows-8/meet) オペレーティング システム
-   [Windows 8.1 用 Windows SDK](https://msdn.microsoft.com/windows/desktop/bg162891.aspx)
-   Microsoft [Visual Studio 2012](https://visualstudio.microsoft.com/vs/older-downloads/) 以降、または Visual Studio Express 2012 (Windows 8.0/8.1 用 Windows SDK に付属)
-   Windows ストア アプリケーション用の MS RMS SDK 4.2 パッケージ。 詳細については、「 [はじめ](get-started.md)に」を参照してください。
-   認証ライブラリ: [Azure AD Authentication Library](/previous-versions/azure/jj573266(v=azure.100)) または他の使用可能な認証ライブラリを使用することをお勧めします。

「[新機能](release-notes.md)」のトピックで、API の更新情報、デバイスと環境情報、リリース ノート、よく寄せられる質問 (FAQ) をお読みください。

## <a name="optional"></a>Optional

UI ライブラリは、独自のカスタム UI 作成を望まない開発者のために、使用操作と保護操作用の再利用可能な UI を提供します - [Windows ストア アプリ用の UI ライブラリ](https://github.com/AzureAD/rms-sdk-ui-for-windowsstore)。 Windows ストア アプリのサンプル アプリケーションも提供しています - [Windows ストア用の RMS サンプル アプリケーション](https://github.com/AzureADSamples/rms-samples-for-windowsstore)。

## <a name="configuring-your-development-environment"></a>開発環境の構成


-   Visual Studio を開きます。
-   [**ファイル**] をクリックし、[**新規作成**] をクリックし、[**プロジェクト**] をクリックします。
-   [**新しいプロジェクト**] ダイアログボックスで、 **[Visual \# C** ] をクリックし、[**空のアプリケーション (Windows)** ] をクリックして、[ **OK**] をクリックします。

    ![新しいプロジェクトの作成](../media/winrtsetup-newproj.png)

-   **ソリューション エクスプローラー** でプロジェクトを右クリックし、**[参照の追加]** を選択して **[参照の追加]** ダイアログ ボックスを開きます。

    ![参照の追加](../media/winrtsetup-addref.png)

-   **[参照の追加]** ダイアログ ボックスで **[参照]** をクリックし、SDK パッケージを解凍したフォルダー内にある *Microsoft.RightsManagement.dll* ファイルを選択します。
-   **管理対象アプリ**-管理対象アプリを構築するには、この参照を追加する必要があります。**Windows 8.1** - &gt; **拡張機能** を選択し、[windows **Visual C++ Runtime Package for windows** ] チェックボックスをオンにします

    ![拡張機能の追加](../media/winrtsetup-refmngr.png)

-   **機能を追加する** - アプリケーションで SDK を使用するには、[インターネット (クライアントとサーバー)] 機能が必要です。 この機能をアプリに追加するには、*Package.appxmanifest* ファイルをプロジェクトで開き、**[機能]** タブに移動して追加します。

これで、新しい独自の Windows ストア アプリを作成する準備が整いました。

### <a name="see-also"></a>参照

[作業開始](get-started.md)

[新機能](release-notes.md)

[開発者の用語と概念](core-concepts.md)

[Windows 8](https://windows.microsoft.com/windows-8/meet)

[Visual Studio 2012](https://visualstudio.microsoft.com/vs/older-downloads/)

[Windows API リファレンス](/previous-versions/windows/desktop/msipcthin2/winrt)