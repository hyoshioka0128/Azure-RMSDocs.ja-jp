---
title: "Android のセットアップ | Azure RMS"
description: "Android アプリケーションは Microsoft Rights Management SDK 4.2 を使用して、そのアプリケーション内で統合情報保護を有効にできます。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 986f6932-159b-4791-bd1a-7640a83ee792
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: 72196edd630a1934f2c0b6e755771039fceaa795


---

# Android のセットアップ

Android アプリケーションは Microsoft Rights Management SDK 4.2 を使用して、Azure Active Directory Rights Management (AAD RM) を使用することでそのアプリケーション内で統合情報保護を有効にできます。

このトピックでは、独自の新しいアプリを作成するために環境をセットアップする方法について説明します。

-   [必要条件](#prerequisites)
-   [省略可能](#optional)
-   [開発環境の構成](#configuring-your-development-environment_)
-   [関連項目](#see-also)

## 必要条件

開発システムでは、次のソフトウェアをお勧めします。

-   [Eclipse](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) 開発環境を実行する Windows または OS X オペレーティング システム。
-   このガイドでは、Eclipse Juno 4.2 以降を持つ Eclipse SDK と、既定のインストールを使用していることを前提としています。
-   Java 1.6 以降。
-   [Android Developer Tools (ADT) プラグイン](http://developer.android.com/sdk/installing/index.html)。 注 - インストールを完了するために、Eclipse の再起動を求められる場合があります。

     

-   Android 向け MS RMS SDK 4.2 パッケージ。 詳細については、「[作業開始](get-started.md)」を参照してください。

    この SDK は、Android 4.0.3 (API レベル 15) 以降を対象とする開発に使用できます。

-   認証ライブラリ: [Azure AD Authentication Library (ADAL)](https://msdn.microsoft.com/library/jj573266.aspx) を使用することをお勧めします。 ただし、OAuth 2.0 をサポートしている他の認証ライブラリも使用できます。

    詳細については、「[ADAL for iOS ](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)」 (iOS 用の ADAL) を参照してください。

    **注**  アプリケーションで OAuth 2.0 認証ライブラリとして ADAL ライブラリが使用されない場合は、Android ガイダンス「[Some SecureRandom Thoughts](http://android-developers.blogspot.com/2013/08/some-securerandom-thoughts.html)」 (セキュリティ保護に関するランダムな意見) を参照してください。

     

「[What's new](release-notes.md)」 (新機能) トピックで、API の更新情報、リリース ノート、およびよく寄せられる質問 (FAQ) をお読みください。

## 省略可能

UI ライブラリは、独自のカスタム UI 作成を望まない開発者のために、使用操作と保護操作用の再利用可能な UI を提供します。「[UI Library and Sample app for Android](https://github.com/AzureAD/rms-sdk-ui-for-android)」 (Android 用の UI ライブラリとサンプル アプリ) 参照。

## 開発環境の構成

**注**  MS RMS SDK 4.2 プレビュー リリース: このプレビュー リリースでは、com/microsoft/protection から com/microsoft/rightsmanagment へのパス名の変更を表示するようにスクリーンショットが更新されていません。 テキストは更新されています。

 
-   Eclipse の開発環境を開きます。
-   Android アプリケーション プロジェクトを新規作成するには、**[File]** メニューで **[New]**、**[Project]** の順にクリックし、**[Android Application Project]** を選択します。

    ![新しい Android アプリケーションを作成する](../media/Android-setup-01c.png)

-   アプリケーション名を入力します。 アプリケーション名に基づいて、プロジェクト名とパッケージ名が入力されます。
-   **[Next]** をクリックし、ワークスペースを作成する場所を選択します。

    ![アプリケーション名を入力する](../media/Android-setup-02a.jpg)

-   **[Next]** をクリックし、アプリのアイコンを選択します。

    ![アプリのアイコンを選択する](../media/Android-setup-03.png)

-   **[Next]** をクリックし、**[Blank Activity]** を選択してアクティビティを作成します。

    ![アクティビティを作成する](../media/Android-setup-04.png)

-   **[Next]** をクリックし、アクティビティの名前を指定します。 *MainActivity* は既定の名前のままにし、レイアウト名を *activity\_main* にします。

    ![アクティビティの名前を指定する](../media/Android-setup-05a.jpg)

-   **[Finish]** をクリックします。

    ![作成を終了する](../media/Android-setup-06.jpg)

-   プロジェクトがメイン アクティビティ クラス *MainActivity.java* と共に作成されました。

**SDK の参照**

-   *adrms\_android\_sdk.zip* を展開したフォルダーに移動します。 "SDK > com > microsoft > rightsmanagement" フォルダーで、ファイル *.classpath*、*.project*、および *project.properties* が読み取り専用にマークされていないことを確認します。
-   参照するには、SDK をワークスペースにインポートする必要があります。

    Eclipse で **[File]** をクリックします。 **[File]** メニューの **[Import]** をクリックします。 **[Import]** ダイアログ ボックスで、**[Android / Existing Android Code into Workspace]** を選択します。

    ![ワークスペースにインポートする](../media/Android-setup-07.png)

-   **[Next]** をクリックします。 *adrms\_android\_sdk.zip* を展開したフォルダーに移動して選択します。 SDK が **com.microsoft.rightsmanagement** として一覧に表示されます。

    ![フォルダーに移動して選択する](../media/Android-setup-08c.jpg)

-   **[Finish]** をクリックすると、SDK プロジェクトが、以前に作成したアプリケーションの兄弟として表示されます。

    ![SDK プロジェクトがアプリケーションの兄弟として表示される](../media/Android-setup-09.jpg)

-   **プロジェクト** アイコンを右クリックし、プロジェクトのプロパティを表示します。
-   **[Android]** タブに移動します。
-   **[Add]** をクリックして、ワークスペースから *com.microsoft.rightsmanagement* ライブラリを選択します。

    ![ライブラリを追加する](../media/Android-setup-10b.jpg)

-   **[OK]**をクリックします。

    MS RMS SDK 4.2 は AAD RM に接続するため、アプリケーションに **INTERNET** および **ACCESS\_NETWORK\_STATE** が許可されている必要があります。 これを行うには、プロジェクトのルートで *AndroidManifest.xml* ファイルを開きます。

    アクセス許可を追加するには、**[Add]** をクリックして、**[Uses Permissions]** を選択します。

    ![アクセス許可を追加する](../media/Android-setup-11d.jpg)

-   マニフェストを検証するには、テキスト エディターのビューでマニフェストを表示します。 次の行が表示されていることを確認してください。


    <uses-sdk      android:minSdkVersion="15"      android:targetSdkVersion="19"/> <uses-permission android:name="android.permission.INTERNET"/> <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/> <uses-permission/>


**注**  SDK では *android.support.v4* が使用されます。

-   新しい独自の Android アプリを作成する準備が整いました。

### 関連項目

[作業開始](get-started.md)

[新機能](release-notes.md)

[開発者の用語と概念](core-concepts.md)

[Android API リファレンス](android-namespaces.md)

 

 



<!--HONumber=Aug16_HO4-->


