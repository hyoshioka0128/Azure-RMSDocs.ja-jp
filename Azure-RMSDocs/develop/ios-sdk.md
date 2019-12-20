---
title: iOS および OS X のセットアップ |Azure RMS
description: iOS および OS X アプリケーションでは、RMS SDK 4.2 を使用して、AAD RM リソースを使用することにより、そのアプリケーション内で統合情報保護を有効にできます。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b31e5b72-e65e-450a-b1b8-d46e81e9fb34
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: c69e34cce0241a289d75593e4a8a9500f88be433
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "68791448"
---
# <a name="ios-and-os-x-setup"></a>iOS および OS X のセットアップ

iOS および OS X アプリケーションでは、Microsoft Rights Management SDK 4.2 を使用して、Azure Rights Management (Azure RMS) を使用することにより、そのアプリケーション内で統合情報保護を有効にできます。

このトピックでは、独自の新しいアプリを作成するために環境をセットアップする方法について説明します。

**注**  この SDK では iPod Touch はサポートされていません。


-   [必要条件](#prerequisites)
-   [省略可能](#optional)
-   [開発環境の構成](#configuring-your-development-environment)
-   [関連項目](#see-also)

## <a name="prerequisites"></a>必要条件

開発システムでは、次のソフトウェアをお勧めします。

-   OS X は、すべての iOS 開発に必要です。
-   Xcode バージョン 6.0 以降

    Xcode は、[Mac App Store](https://developer.apple.com/technologies/mac/) で入手できます。

-   iOS および OS X 用 MS RMS SDK 4.2 パッケージ。詳しくは、「[作業開始](get-started.md)」をご覧ください。

    この SDK は、iOS 7.0 および OS X 10.8 以降を対象とする開発に使用できます。

-   認証ライブラリ: [Azure AD Authentication Library (ADAL)](https://msdn.microsoft.com/library/jj573266.aspx) を使用することをお勧めします。 ただし、OAuth 2.0 をサポートしている他の認証ライブラリも使用できます。

    詳細については、「[ADAL for iOS (iOS 用の ADAL)](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)」または「[ADAL for OS X (OS X 用の ADAL)](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/tree/OSXUniversal)」を参照してください。

「[What's new (新機能)](release-notes.md)」トピックで、API の更新情報、リリース ノート、およびよく寄せられる質問 (FAQ) をお読みください。

## <a name="optional"></a>オプション

UI ライブラリは、独自のカスタム UI 作成を望まない開発者のために、使用操作と保護操作用の再利用可能な UI を提供します。「[UI Library and Sample app for iOS (iOS 用の UI ライブラリとサンプル アプリ](https://github.com/AzureAD/rms-sdk-ui-for-ios)」参照。

## <a name="configuring-your-development-environment"></a>開発環境の構成

-   新しいプロジェクトを作成するために、 **[ファイル]** メニューの **[新規作成]** をクリックし、 **[プロジェクト]** をクリックします。
-   **[Single View Application (単一枠ビュー アプリケーション)]** を選択します。

    ![新しいプロジェクトの作成](../media/iOS-Project.png)

-   新しいプロジェクトの名前および識別子を入力します。

    ![プロジェクトの命名](../media/iOS-project-options.png)

-   **[次へ]** をクリックして、プロジェクトの場所を選択します。
-   iOS フレームワークの **MSRightsManagement** フレームワークを追加するために、.framework フォルダーを SDK のインストール フォルダーから**プロジェクト ナビゲーター**の **Frameworks** セクションにドラッグします。

    ![場所の設定](../media/ios-add-dependencies-01a.png)

-   **[Create groups for any added folders (追加されたすべてのフォルダーのグループを作成する)]** オプション ボタンをクリックし、 **[Copy items into destination group's folder (if needed) (出力先グループのフォルダーに項目をコピーする (必要な場合))]** チェック ボックスをオフにします。

    この操作により、コピーを作成する代わりに、SDK のインストール フォルダーへの参照を保持します。

    ![SDK のインストール フォルダーへの参照の設定](../media/iOS-create-groups.png)

-   リソース バンドル用の MS RMS SDK 4.2 を追加するには、MSRightsManagementResources.bundle ファイルを MSRightsManagement.framework/Resources フォルダーから Project Navigator の **[Frameworks]\(フレームワーク\)** セクションにドラッグします。

    ![リソース バンドルの追加](../media/iOS-add-resource-bundle-02a.png)

-   フレームワークをコピーしたときと同様に、 **[Create groups for any added folders (追加されたすべてのフォルダーのグループを作成する)]** オプション ボタンを選択し、 **[Copy items into destination group's folder (if needed) (出力先グループのフォルダーに項目をコピーする (必要な場合))]** チェック ボックスをオフにします。
-   SDK は、**CoreData**、**MessageUI**、**SystemConfiguration**、**Libresolv**、**Security** などの他のフレームワークに依存しています。 これらのフレームワークを追加するために、ターゲットの **[サマリー]** ウィンドウの **[Linked Frameworks and Libraries (リンク フレームワークとライブラリ)]** セクションに移動して、フレームワークを追加するセクションを展開します。

    **UIKit** と **Foundation** フレームワークが必要ですが、通常は既定で表示されます。

    ![リソースの追加](../media/iOS-add-libraries.png)

-   ターゲットの **[ビルド設定]** の **[Other Linker Flags (その他のリンカー フラグ)]** に **- ObjC** フラグを追加します。

    ![ビルド設定の追加](../media/iOS-linker-flags.png)

-   これで、**プロジェクト ナビゲーター**はこのツリーのようになります。

    ![プロジェクトの確認](../media/iOS-verify-setup-01a.png)

-   新しい独自の iOS/OS X アプリを作成する準備が整いました。

### <a name="see-also"></a>参照

* [作業開始](get-started.md)

* [新機能](release-notes.md)

* [開発者の用語と概念](core-concepts.md)

* [iOS / OS X API リファレンス](https://msdn.microsoft.com/library/dn758306.aspx)
