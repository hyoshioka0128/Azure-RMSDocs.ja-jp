---
# required metadata

title: 新機能とリリース ノート | Azure RMS
description: 重要な変更点と、この新しいバージョンの RMS SDK の機能について説明します。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 4fa1c686-b00b-4734-9abb-141ce582a6af
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 新機能とリリース ノート

## 新機能
Microsoft Rights Management SDK 4.2 では、RMS アプリケーションが一段と簡素化され、柔軟性が向上しています。 このトピックでは、重要な変更点と、この新しいバージョンの RMS SDK の機能について説明します。

-   [2015 年 12 月の更新の新しい点](#new_for_our_december_2015_update)
-   [2015 年 7 月の更新 – Linux / C++ による開発のサポートを追加](#july_2015_update_-_adds_support_for_linux___c___development)
-   [2015 年 5 月の更新 – ログの制御を追加](#may_2015_update_-_adds_logging_control)
-   [2015 年 2 月の更新 – Windows ストア アプリケーションのサポートを追加](#february_2015_update_-_adds_windows_store_application_support)
-   [2015 年 1 月の更新 – WinPhone プラットフォームのサポートを追加](#january_2015_update_-_adds_winphone_platform_support)
-   [2014 年 10 月の更新 – Microsoft RMS SDK 4.1 にアップグレード](#october_2014_update_-_upgrade_to_microsoft_rms_sdk_4.1)
-   [リリース ノート](#release-notes)
-   [よく寄せられる質問](#frequently_asked_questions)

### 2015 年 12 月の更新の新しい点

このリリースでは、デバイス用の RMS SDK はバージョン 4.2 であり、以下の機能が追加されています。

-   ドキュメント追跡 (IOS/OS X および Android オペレーティング システムでは RMS オンラインのみ)

    iOS/OS X の場合の詳細および使用ガイダンスについては、情報を追跡し、追加ドキュメントの登録を追跡するメソッドを提供する [**MSUserPolicy**](/rights-management/sdk/4.2/api/iOS/iOS#msipcthin2_msuserpolicy_interface_objc) の [**MSLicenseMetadata**](/rights-management/sdk/4.2/api/iOS/mslicensemetadata#msipcthin2_mslicensemetadata_class_objc) クラスを参照してください。 Android 用にも [**LicenseMetadata**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_licensemetadata_interface_java) および [**UserPolicy**](/rights-management/sdk/4.2/api/android/userpolicy) と同様の機能が追加されています。

    ドキュメント追跡機能の詳細については、「[**How to: Use document tracking**](how-to-use-document-tracking.md)」 (方法: ドキュメント追跡を使用する) を参照してください。

-   Android API の非同期バージョンに相当する一連の同期メソッド。

    [**CustomProtectedInputStream.create 同期メソッド**](/rights-management/sdk/4.2/api/android/customprotectedinputstream#msipcthin2_customprotectedinputstream_create_synchronous_method_java)

    [**CustomProtectedOutputStream.create 同期メソッド**](/rights-management/sdk/4.2/api/android/customprotectedoutputstream#msipcthin2_customprotectedoutputstream_create_synchronous_method)

    [**ProtectedFileInputStream.create 同期メソッド**](/rights-management/sdk/4.2/api/android/protectedfileinputstream#msipcthin2_protectedfileinputstream_create_synchronous_method)

    [**ProtectedFileOutputStream.create 同期メソッド**](/rights-management/sdk/4.2/api/android/customprotectedoutputstream#msipcthin2_customprotectedoutputstream_create_synchronous_method)

    [**TemplateDescriptor.getTemplates 同期メソッド**](/rights-management/sdk/4.2/api/android/templatedescriptor#msipcthin2_templatedescriptor_gettemplates_synchronous_method_java)

    [**UserPolicy.acquire 同期メソッド**](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_acquire_synchronous_method_java)

    [**UserPolicy.create (PolicyDescriptor...) 同期メソッド**](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_create_policydescriptor_______synchronous_method_java)

    [**UserPolicy.create (TempalteDescriptor…) 同期メソッド**](/rights-management/sdk/4.2/api/android/userpolicy#msipcthin2_userpolicy_create_templatedescriptor_______synchronous_method_java)

-   Android API に新しい [**ProtectedBuffer**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_protectedbuffer_class) クラスを追加
-   エラー メッセージやトラブルシューティングを向上させる更新プログラム
-   暗号化操作の重要なパフォーマンスの向上

### 2015 年 7 月の更新 – Linux / C++ による開発のサポートを追加

このリリースでは、以下が追加されています。

-   Linux プラットフォーム向けの RMS SDK 4.1

    詳細については、「[作業開始](get-started.md)」を参照してください。

### 2015 年 5 月の更新 – ログの制御を追加

このリリースでは、以下のサポートが追加されています。

-   iOS

    アプリケーションの暗号化および復号化を独立して、並列的に実行できます。

    詳細については、「[**MSProtector**](/rights-management/sdk/4.2/api/iOS/iOS#msipcthin2_msprotector_class_objc)」を参照してください。

    ログ レベルの制御の設定が可能になりました。

    詳細については、「[How to: Enable error and performance logging](enabling-logging.md)」 (方法: エラーとパフォーマンスのログを有効にする) を参照してください。

    キャッシュ クリアのサポートが追加されました。

    詳細については、「[**MSProtection:resetStateWithCompletionBlock**](/rights-management/sdk/4.2/api/iOS/msprotection#msipcthin2_msprotection_resetstatewithcompletionblock_method_objc)」を参照してください。

### 2015 年 2 月の更新 – Windows ストア アプリケーションのサポートを追加

このリリースでは、Windows ストア アプリケーションのサポートを追加し、RMS SDK 4.1 の Windows Phone、Android、および iOS/OS X 版リリースにそれぞれ同等の機能を提供しています。

### 2015 年 1 月の更新 – WinPhone プラットフォームのサポートを追加

このリリースでは、Windows Phone オペレーティング システムのサポートを追加し、RMS SDK 4.1 の Android 版および iOS/OS X 版リリースにそれぞれ同等の機能を提供しています。

## 2014 年 10 月の更新 – Microsoft RMS SDK 4.1 にアップグレード

RMS SDK のバージョン 4.1 のリリースでは、Google Android と Apple iOS/OS X に以下の新機能が追加されています。

-   *ユーザーの同意*を処理するための Android および iOS/OS SDK API 拡張により、SDK の動作をユーザーが確認できるようになりました。 現在、サポートされている同意タイプは、ドキュメント追跡、および不明な AD RMS サービス URL へのアクセスです。

    詳細については、Android API バージョンの [**ConsentCallback インターフェイス**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_consentcallback_interface_java) を例として参照してください。

-   iOS 8 および OS X 10.10 (Yosemite) がサポートされるようになりました。 Xcode 6 で必要ないくつかのプロパティ名も変更されました。

    たとえば、MSUserPolicy.name が [**MSUserPolicy.policyName**](/rights-management/sdk/4.2/api/iOS/msuserpolicy#msipcthin2_msuserpolicy_name_property_objc) に変更されました。

## リリース ノート

このセクションでは、開発者が知っておくと便利な、Microsoft Rights Management SDK 4.x API の現在および以前のリリースに関する情報をまとめています。

**AD RMS SDK 4.1 – iOS/OS X および Android プラットフォームのグローバル公開リリース**

-   **AD RMS のサポート** – 新しい AD RMS サーバーのモバイル デバイス拡張機能により、IT 管理者はモバイル デバイスで RMS 対応アプリケーションを使用できます。
-   **オフラインで使用** – エンドユーザーが RMS 保護されたデータにオフラインでアクセスできます。
-   **認証の分離** – 開発者は、独自の認証ライブラリ (または推奨される [Azure AD 認証ライブラリ (ADAL)](https://MSDN.Microsoft.Com/en-us/library/jj573266.aspx)) を Azure RMS と AD RMS に使用できます。
-   **UI の分離** – 開発者は、RMS 保護されたドキュメントを保護および使用するためのユーザー インターフェイスを構築できます。
-   **再設計された API** – RMS の一貫性のある動作により、開発者は最低限の労力で API のシンプルかつ透過的な暗号化および暗号化解除を利用できます。

**すべてのプラットフォームに共通**

-   RMS SDK 4.x API は*スレッド セーフ*ではありません。

**Android**

-   Amazon® Kindle デバイスで .ptxt の添付ファイルを表示するサンプル アプリケーションを使用する際に、表示する前に、まずファイルをダウンロードする必要があります。

    **ソリューション** – これは既知の問題であり、今後対応する予定です。

-   複数のインスタンスが許可されていると、SDK を使用するアプリケーションがクラッシュすることがあります。

    **ソリューション** – アプリケーションが Android API への複数インスタンスの呼び出しを許可しないようにします。

-   [**ProtectedFileOutputStream**](/rights-management/sdk/4.2/api/android/protectedfileoutputstream#msipcthin2_protectedfileoutputstream_class_java)**.write(byte\[\] array, int offset, int length)** メソッドを *array.length* の値と異なるサイズで使用すると、その後 SDK でそのコンテンツを使用できません。

    **ソリューション** – これは既知の問題です。 この現象を軽減するには、**byte \[\]** 配列に length パラメーターと同じ長さの値を渡すか、[**ProtectedFileOutputStream**](/rights-management/sdk/4.2/api/android/protectedfileoutputstream#msipcthin2_protectedfileoutputstream_class_java)**.write(byte\[\] array)** メソッドを使用します。

**iOS および OS X**

-   iOS および OS X 用 SDK をサポートするポルトガル語の言語仕様は 2 つありますが、 バグがあるため、現在 1 番目の言語仕様のローカライズは完全にはサポートしていません。 このバグにより、ポルトガル語は完全にはサポートされていません。 テキストの大部分は翻訳されますが、UI は翻訳されません。

    1. ポルトガル語

    2. ポルトガル語 (ポルトガル)

**iOS のみ**

-   RMS SDK 4.x では、ネットワーク アクティビティのインジケーターは表示されません。

    Apple のヒューマン インターフェイス ガイドラインによると、これは iOS の既知の省略可能な動作です。

**OS X のみ**

-   RMS SDK 4.x では、ネットワーク アクティビティのインジケーターは表示されません。

    Apple のヒューマン インターフェイス ガイドラインによると、これは OS X の既知の省略可能な動作です。

-   **ソリューション** – マルチ ドキュメント インターフェイス (MDI) アプリケーションを作成する場合には、次のガイダンスに従って OS X SDK を使用します。

    次のメソッドは同時に実行しないでください。 実行の完了を監視するには、説明に従って完了ブロック アプローチを使用します。

    - [**protectedDataWithProtectedFile**](/rights-management/sdk/4.2/api/iOS/msprotecteddata#msipcthin2_msprotecteddata_protecteddatawithprotectedfile_completionblock_method_objc)
    - [**customProtectedDataWithPolicy**](/rights-management/sdk/4.2/api/iOS/mscustomprotecteddata#msipcthin2_mscustomprotecteddata_customprotecteddatawithpolicy_protecteddata_contentstartposition_contentsize_completionblock_method_objc)



**注**  MDI アプリケーションは、iOS API ではサポートされていません。

## よく寄せられる質問

**すべてのプラットフォーム**

**Q**: 保護ワークフローに**カスタム アクセス許可**の選択 UI が表示されません。 これはなぜでしょうか。

**A** – これは既知の問題であり、今後対応する予定です。

**Q**: SDK およびサンプル アプリケーションを試すために新しい組織のテナントを取得するにはどうすればよいですか。

**A**: Azure AD RMS のテスト組織の資格情報を要求するには、<rmcstbeta@microsoft.com> まで電子メールを送信してください。

**Q**: ドキュメントにテスト階層についての説明が見当たりません。 これはなぜでしょうか。

**A**: 新しい AD RMS SDK にはテスト階層の概念はなく、 常に運用階層を使用します。

**Q**: RMS SDK バージョン 2.1 では、情報保護を実装するアプリケーションごとに生成済みマニフェストが必要ですが、バージョン 4.0 以降でも同じでしょうか。

**A**: いいえ、マニフェストは Rights Management SDK バージョン 3.0 以降では不要です。

**Android**

**Q**: SDK はどの開発環境でテストされていますか。

**A**: Google API 15 以降を使用した Eclipse Juno です。

**Q**: UI スレッドから操作を取り消すメソッド cancel() を呼び出すことはできますか。
**A**: cancel() は、ネットワーク接続を中止する可能性があるため、非 UI スレッドから を呼び出す必要があります。

**iOS**

**Q**: SDK の開発はどのプラットフォームで検証されましたか。

**A**: iOS 7 以降を使用した Xcode 5.0 です。

**Q**: 操作に対して cancel() メソッドを呼び出しましたが、まだ操作が完了したことを示す通知が届きます。 これはなぜでしょうか。

**A**: すべての操作が取り消し可能なわけではなく、取り消し操作は可能な限りにおいて実行されます。

**OS x**

**Q**: サンプル アプリケーションのフレームワークは Xcode 5 に対応していますが、Xcode 4.6 でも使用できますか。

**A**: OS X SDK は Xcode 4.6 以降のみ、および OS X 10.8 以降で動作します。

 

 


<!--HONumber=Apr16_HO4-->


