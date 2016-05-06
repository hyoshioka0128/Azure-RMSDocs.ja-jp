---
# required metadata

title: iOS および OS X のセットアップ |Azure RMS
description: iOS および OS X アプリケーションは RMS SDK 4.2 を使用して、AAD RM リソースを使用することでそのアプリケーション内で統合情報保護を有効にできます。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 23f64fc8-d0f3-49ee-8d8a-b34ef26878a7

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿# iOS および OS X のセットアップ

iOS および OS X アプリケーションは Microsoft Rights Management SDK 4.2 を使用して、Azure Active Directory Rights Management (AAD RM) を使用することでそのアプリケーション内で統合情報保護を有効にできます。

このトピックでは、独自の新しいアプリを作成するために環境をセットアップする方法について説明します。

**注**  この SDK は iPod Touch をサポートしていません。


-   [必要条件](#prerequisites)
-   [省略可能](#optional)
-   [開発環境の構成](#configuring_your_development_environment)
-   [参照](#see_also)

## 必要条件

開発システムでは、次のソフトウェアをお勧めします。

-   OS X は、すべての iOS 開発に必要です。
-   Xcode バージョン 6.0 以降

    Xcode は、[Mac App Store](https://developer.apple.com/technologies/mac/) で入手できます。

-   iOS および OS X 用 MS RMS SDK 4.2 パッケージ。詳細については、「[概要](get-started.md)」を参照してください。

    この SDK は、iOS 7.0 および OS X 10.8 以降を対象とする開発に使用できます。

-   認証ライブラリ: [Azure AD Authentication Library (ADAL)](https://msdn.microsoft.com/en-us/library/jj573266.aspx) を使用することをお勧めします。 ただし、OAuth 2.0 をサポートしている他の認証ライブラリも使用できます。

    詳細については、「[ADAL for iOS (iOS 用の ADAL)](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios)」または「[ADAL for OS X (OS X 用の ADAL)](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/tree/OSXUniversal)」を参照してください。

「[What's new (新機能)](release-notes.md)」トピックで、API の更新情報、リリース ノート、およびよく寄せられる質問 (FAQ) をお読みください。

## 省略可能

UI ライブラリは、独自のカスタム UI 作成を望まない開発者のために、使用操作と保護操作用の再利用可能な UI を提供します。「[UI Library and Sample app for iOS (iOS 用の UI ライブラリとサンプル アプリ](https://github.com/AzureAD/rms-sdk-ui-for-ios)」参照。

## 開発環境の構成

-   新しいプロジェクトを作成するために、**[ファイル]** メニューの **[新規作成]** をクリックし、**[プロジェクト]** をクリックします。
-   **[Single View Application (単一枠ビュー アプリケーション)]** を選択します。

    ![](../media/iOS-Project.png)

-   新しいプロジェクトの名前および識別子を入力します。

    ![](../media/iOS-project-options.png)

-   **[次へ]** をクリックして、プロジェクトの場所を選択します。
-   iOS フレームワークの **MSRightsManagement** フレームワークを追加するために、.framework フォルダーを SDK のインストール フォルダーから**プロジェクト ナビゲーター**の **Frameworks** セクションにドラッグします。

    ![](../media/ios-add-dependencies-01a.png)

-   **[Create groups for any added folders (追加されたすべてのフォルダーのグループを作成する)]** オプション ボタンをクリックし、**[Copy items into destination group's folder (if needed) (出力先グループのフォルダーに項目をコピーする (必要な場合))]** チェック ボックスをオフにします。

    この操作により、コピーを作成する代わりに、SDK のインストール フォルダーへの参照を保持します。

    ![](../media/iOS-create-groups.png)

-   リソース バンドルの MS RMS SDK 4.2 を追加するために、MSRightsManagementResources.bundle ファイルを MSRightsManagement.framework/Resources フォルダーからプロジェクト ナビゲーターの **Frameworks** セクションにドラッグします。

    ![](../media/iOS-add-resource-bundle-02a.png)

-   フレームワークをコピーしたときと同様に、**[Create groups for any added folders (追加されたすべてのフォルダーのグループを作成する)]** オプション ボタンを選択し、**[Copy items into destination group's folder (if needed) (出力先グループのフォルダーに項目をコピーする (必要な場合))]** チェック ボックスをオフにします。
-   SDK は、**CoreData**、**MessageUI**、**SystemConfiguration**、**Libresolv**、**Security** などの他のフレームワークに依存しています。 これらのフレームワークを追加するために、ターゲットの **[サマリー]** ウィンドウの **[Linked Frameworks and Libraries (リンク フレームワークとライブラリ)]** セクションに移動して、フレームワークを追加するセクションを展開します。

    **UIKit** と **Foundation** フレームワークが必要ですが、通常は既定で表示されます。

    ![](../media/iOS-add-libraries.png)

-   ターゲットの **[ビルド設定]** の **[Other Linker Flags (その他のリンカー フラグ)]** に **- ObjC** フラグを追加します。

    ![](../media/iOS-linker-flags.png)

-   これで、**プロジェクト ナビゲーター**はこのツリーのようになります。

    ![](../media/iOS-verify-setup-01a.png)

-   新しい独自の iOS/OS X アプリを作成する準備が整いました。

### 参照

* [作業開始](get-started.md)

* [新機能](release-notes.md)

* [Developer terms and concepts (開発者の用語と概念)](core-concepts.md)

* [iOS / OS X API Reference (iOS / OS X API リファレンス)](/rights-management/sdk/4.2/api/ios/ios)

 

 





<!--HONumber=Apr16_HO3-->

