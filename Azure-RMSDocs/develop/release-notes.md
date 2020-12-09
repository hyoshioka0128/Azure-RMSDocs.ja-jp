---
title: Rights Management Services SDK v4. x のリリースノート
description: Microsoft Rights Management Service SDK v4. x 2017 年7月およびそれ以前のリリースの新機能とリリースノートを参照してください。
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 12/11/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4fa1c686-b00b-4734-9abb-141ce582a6af
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.custom: has-adal-ref
ms.openlocfilehash: 65e7e70d6cd144905c37d0c20c05f5841f310c42
ms.sourcegitcommit: 03fef7cf0a7687962bfd3f0cd221541520f4a317
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96862515"
---
# <a name="whats-new-and-release-notes"></a>新機能とリリース ノート

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

## <a name="whats-new"></a>新機能

このトピックでは、この新しいバージョンの RMS SDK v4. x における重要な変更点と機能について説明します。

-   [2017 年 7 月の新機能](#new-for-july-2017)
-   [2016 年 10 月の更新](#october-2016-update)
-   [2016 年 6 月の更新](#june-2016-update)
-   [2015 年 12 月更新](#december-2015-update)
-   [2015 年 7 月の更新 - Linux / C++ による開発のサポートを追加](#july-2015-update---adds-support-for-linux--c-development)
-   [2015年5月の更新-ログの制御を追加](#may-2015-update---adds-logging-control)
-   [2015 年 2 月の更新 - Windows ストア アプリケーションのサポートを追加](#february-2015-update---adds-windows-store-application-support)
-   [2015 年 1 月の更新 - WinPhone プラットフォームのサポートを追加](#january-2015-update---adds-winphone-platform-support)
-   [2014 年 10 月の更新 - Microsoft RMS SDK 4.1 にアップグレード](#october-2014-update---upgrade-to-microsoft-rms-sdk-41)
-   [リリース ノート](#release-notes)
-   [よく寄せられる質問](#frequently-asked-questions)

### <a name="new-for-july-2017"></a>2017 年 7 月の新機能

7 月リリースの更新で SDK が改訂され、4.2.5 になりました。

- Android SDK: Android SDK で、**ログ記録レベルをその場で設定 (オンザフライ設定)** できるようになりました。 詳細については、「[方法: エラーとパフォーマンスのログを有効にする](/information-protection/develop/enabling-logging)」を参照してください。
- iOS SDK では、ログ記録レベルを設定できません。
- SDK は、NULL アクセス トークンに対してエラーを返すようになりました。

### <a name="october-2016-update"></a>2016 年 10 月の更新

- バックエンド バグをいくつか修正。
- Apple iOS/OSX SDK のビットコードを有効化。

### <a name="june-2016-update"></a>2016 年 6 月の更新

- **先進認証のサポート** - Active Directory Authentication Library (ADAL) ベースのサインインを RMS 対応アプリに導入。 これによって利用可能になるサインイン機能としては、Multi-Factor Authentication (MFA)、SAML ベースのサードパーティ ID プロバイダーと RMS クライアント アプリケーションの組み合わせ、スマート カードや証明書をベースとする認証などがあります。また、RMS 対応アプリで基本認証プロトコルを使用する必要がなくなります。
- **ドキュメント追跡のサポート** - 開発するアプリの中でドキュメントを保護するときに、ドキュメント追跡を有効化できるようになりました。
- パフォーマンスの向上
- バグの修正

### <a name="december-2015-update"></a>2015 年 12 月更新

このリリースでは、デバイス用の RMS SDK はバージョン 4.2 であり、以下の機能が追加されています。

-   ドキュメント追跡 (iOS/OS X および Android オペレーティング システムでは RMS オンラインのみ)

    iOS/OS X の場合の詳細と使用方法については、[MSLicenseMetadata](/previous-versions/windows/desktop/msipcthin2/mslicensemetadata-class-objc) クラスを参照してください。追跡情報と [MSUserPolicy](/previous-versions/windows/desktop/msipcthin2/msuserpolicy-interface-objc) での追加の文書追跡登録メソッドを提供します。 Android 用の同様の機能も [LicenseMetadata](/previous-versions/windows/desktop/msipcthin2/licensemetadata-interface-java) および [UserPolicy](/previous-versions/windows/desktop/msipcthin2/userpolicy-class-java) に追加されています。

    ドキュメント追跡機能の詳細については、「[方法: ドキュメント追跡を使用する](how-to-use-document-tracking.md)」を参照してください。

-   Android API の非同期バージョンに相当する一連の同期メソッド。

    [CustomProtectedInputStream.create 同期メソッド](/previous-versions/windows/desktop/msipcthin2/customprotectedinputstream-create-synchronous-method-java)

    [CustomProtectedOutputStream.create 同期メソッド](/previous-versions/windows/desktop/msipcthin2/customprotectedoutputstream-create-synchronous-method)

    [ProtectedFileInputStream.create 同期メソッド](/previous-versions/windows/desktop/msipcthin2/protectedfileinputstream-create-synchronous-method)

    [ProtectedFileOutputStream.create 同期メソッド](/previous-versions/windows/desktop/msipcthin2/protectedfileoutputstream-create-synchronous-method-java)

    [TemplateDescriptor.getTemplates 同期メソッド](/previous-versions/windows/desktop/msipcthin2/templatedescriptor-gettemplates-synchronous-method-java)

    [UserPolicy.acquire 同期メソッド](/previous-versions/windows/desktop/msipcthin2/userpolicy-acquire-synchronous-method-java)

    [UserPolicy.create (PolicyDescriptor…) 同期メソッド**](/previous-versions/windows/desktop/msipcthin2/userpolicy-create-policydescriptor-------synchronous-method-java)

    [UserPolicy.create (TempalteDescriptor…) 同期メソッド](/previous-versions/windows/desktop/msipcthin2/userpolicy-create-templatedescriptor-------synchronous-method-java)

-   Android API に新しい [ProtectedBuffer](/previous-versions/windows/desktop/msipcthin2/protectedbuffer-class) クラスを追加します。
-   エラー メッセージやトラブルシューティングを向上させる更新プログラム
-   暗号化操作の重要なパフォーマンスの向上

### <a name="july-2015-update---adds-support-for-linux--c-development"></a>2015 年 7 月の更新 - Linux / C++ による開発のサポートを追加

このリリースでは、以下の更新が追加されています。

-   Linux プラットフォーム向けの RMS SDK 4.1

    詳細については、「[作業開始](get-started.md)」を参照してください。

### <a name="may-2015-update---adds-logging-control"></a>2015 年 5 月の更新 - ログの制御を追加

このリリースでは、以下の更新のサポートが追加されています。

-   iOS

    アプリケーションの暗号化および復号化を独立して、並列的に実行できます。

    詳細については、「[MSProtector](/previous-versions/windows/desktop/msipcthin2/msprotector-class-objc)」を参照してください。

    ログ レベルの制御の設定が可能になりました。

    詳細については、「[方法: エラーとパフォーマンスのログを有効にする](enabling-logging.md)」を参照してください。

    キャッシュ クリアのサポートが追加されました。

    詳細については、「[MSProtection:resetStateWithCompletionBlock](/previous-versions/windows/desktop/msipcthin2/msprotection-resetstatewithcompletionblock-method-objc)」を参照してください。

### <a name="february-2015-update---adds-windows-store-application-support"></a>2015 年 2 月の更新 - Windows ストア アプリケーションのサポートを追加

このリリースでは、Windows ストア アプリケーションのサポートを追加し、RMS SDK 4.1 の Windows Phone、Android、iOS/OS X 版リリースにそれぞれ同等の機能を提供しています。

### <a name="january-2015-update---adds-winphone-platform-support"></a>2015 年 1 月の更新 - WinPhone プラットフォームのサポートを追加

このリリースでは、Windows Phone オペレーティング システムのサポートを追加し、RMS SDK 4.1 の Android 版および iOS/OS X 版リリースにそれぞれ同等の機能を提供しています。

### <a name="october-2014-update---upgrade-to-microsoft-rms-sdk-41"></a>2014 年 10 月の更新 - Microsoft RMS SDK 4.1 にアップグレード

RMS SDK のバージョン 4.1 のリリースでは、Google Android と Apple iOS/OS X に以下の新機能が追加されています。

-   *ユーザーの同意* を処理するための Android および iOS/OS SDK API 拡張により、SDK の動作をユーザーが確認できるようになりました。 現在、サポートされている同意タイプは、ドキュメント追跡、および不明な AD RMS サービス URL へのアクセスです。

    詳細については、Android API バージョンの [ConsentCallback インターフェイス](/previous-versions/windows/desktop/msipcthin2/consentcallback-interface-java)を例として参照してください。

-   iOS 8 および OS X 10.10 (Yosemite) がサポートされるようになりました。 Xcode 6 で必要ないくつかのプロパティ名も変更されました。

    たとえば、MSUserPolicy.name が [MSUserPolicy.policyName](/previous-versions/windows/desktop/msipcthin2/msuserpolicy-name-property-objc) に変更されました。

## <a name="release-notes"></a>リリース ノート

このセクションでは、開発者が知っておくと便利な、Microsoft Rights Management SDK 4.x API の現在および以前のリリースに関する情報をまとめています。

**AD RMS SDK 4.1 - iOS/OS X および Android プラットフォームのグローバル公開リリース**

-   **AD RMS のサポート** - 新しい AD RMS サーバーのモバイル デバイス拡張機能により、IT 管理者はモバイル デバイスで RMS 対応アプリケーションを使用できます。
-   **オフラインで使用** - エンドユーザーが RMS 保護されたデータにオフラインでアクセスできます。
-   **認証の分離** - 独自に開発した認証ライブラリを Azure RMS と AD RMS に使用できます (推奨される [Azure AD 認証ライブラリ (ADAL)](/previous-versions/azure/jj573266(v=azure.100)) を使用することもできます)。
-   **UI の分離** - 開発者は、RMS 保護されたドキュメントを保護および使用するためのユーザー インターフェイスを構築できます。
-   **再設計された API** - 暗号化/復号化の API が単純でわかりやすくなりました。RMS の動作と操作方法に一貫性があり、労力が最小限に抑えられます。

**すべてのプラットフォームに共通**

-   RMS SDK 4.x API は *スレッド セーフ* ではありません。

**Android**

-   Amazon® Kindle デバイスで .ptxt の添付ファイルを表示するサンプル アプリケーションを使用する際に、表示する前に、まずファイルをダウンロードする必要があります。

    **解決策** -これは既知の問題であり、解決されない可能性が1つあります。 代わりに、 [Microsoft INFORMATION PROTECTION SDK](/information-protection/develop/) を調査することをお勧めします。

-   複数のインスタンスが許可されていると、SDK を使用するアプリケーションがクラッシュすることがあります。

    **解決方法** - アプリケーションが Android API への複数インスタンスの呼び出しを許可しないようにします。

-   [Protectedfileoutputstream .write](/previous-versions/windows/desktop/msipcthin2/protectedfileoutputstream-class-java)(byte \[ \] array, int offset, int length) メソッドを使用する場合、*配列* の長さの値とは別の長さであるため、SDK を使用して後でコンテンツを使用することはできません。

    **解決方法** - これは既知の問題です。 これを軽減するには、長さのパラメーターと同じ長さの値を持つ *バイト \[ \]* 配列を常に渡すか、 [protectedfileoutputstream .write](/previous-versions/windows/desktop/msipcthin2/protectedfileoutputstream-class-java)(バイト \[ \] 配列) メソッドを使用します。

**iOS および OS X**

-   iOS および OS X 用 SDK をサポートするポルトガル語の言語仕様は 2 つありますが、 バグがあるため、現在のところ、最初の言語仕様のローカライズは完全にサポートしていません。 このバグにより、ポルトガル語は完全にはサポートされていません。 テキストの大部分は翻訳されていますが、UI は翻訳されていません。

    1. ポルトガル語

    2. ポルトガル語 (ポルトガル)

**iOS のみ**

-   RMS SDK 4.x では、ネットワーク アクティビティのインジケーターは表示されません。

    Apple のヒューマン インターフェイス ガイドラインによると、これは iOS の既知の省略可能な動作です。

**OS X のみ**

-   RMS SDK 4.x では、ネットワーク アクティビティのインジケーターは表示されません。

    Apple のヒューマン インターフェイス ガイドラインによると、これは OS X の既知の省略可能な動作です。

-   **ソリューション** - マルチ ドキュメント インターフェイス (MDI) アプリケーションを作成する場合には、次のガイダンスに従って OS X SDK を使用します。

    次のメソッドは同時に実行しないでください。 実行の完了を監視するには、説明に従って完了ブロック アプローチを使用します。

    - [MSProtectedData.protectedDataWithProtectedFile](/previous-versions/windows/desktop/msipcthin2/msprotecteddata-protecteddatawithprotectedfile-completionblock-method-objc)
    - [MSCustomProtectedData.customProtectedDataWithPolicy](/previous-versions/windows/desktop/msipcthin2/mscustomprotecteddata-customprotecteddatawithpolicy-protecteddata-contentstartposition-contentsize-completionblock-method-objc)



**注**  MDI アプリケーションは、iOS API ではサポートされていません。

## <a name="frequently-asked-questions"></a>よく寄せられる質問

**すべてのプラットフォーム**

**Q**: 保護ワークフローに **カスタム アクセス許可** の選択 UI が表示されません。 なぜでしょうか。

**A**: これは既知の問題であり、今後対応する予定です。

**Q**: SDK およびサンプル アプリケーションを試すために新しい組織のテナントを取得するにはどうすればよいですか。

**A**: Azure AD RMS のテスト組織の資格情報を要求するには、<rmcstbeta@microsoft.com> に電子メールを送信してください。

**Q**: ドキュメントにテスト階層についての説明が見当たりません。 なぜでしょうか。

**A**: 新しい AD RMS SDK にはテスト階層の概念はなく、 常に運用階層を使用します。

**Q**: RMS SDK バージョン 2.1 では、情報保護を実装するアプリケーションごとに生成済みマニフェストが必要です。 SDK バージョン 4.0 以降でも同じでしょうか。

**A**: いいえ、マニフェストは Rights Management SDK バージョン 3.0 以降では不要です。

**Android**

**Q**: SDK はどの開発環境でテストされていますか。

**A**: Google API 15 以降を使用した Eclipse Juno です。

**Q**: UI スレッドから操作を取り消すメソッド cancel() を呼び出すことはできますか。
**A**: cancel() は、ネットワーク接続を中止する可能性があるため、非 UI スレッドから cancel() を呼び出す必要があります。

**iOS**

**Q**: SDK の開発はどのプラットフォームで検証されましたか。

**A**: iOS 7 以降を使用した Xcode 5.0 です。

**Q**: 操作に対して cancel() メソッドを呼び出しましたが、まだ操作が完了したことを示す通知が届きます。 なぜでしょうか。

**A**: すべての操作が取り消し可能なわけではなく、取り消し操作は可能な限りにおいて実行されます。

**OS x**

**Q**: サンプル アプリケーションのフレームワークは Xcode 5 に対応していますが、Xcode 4.6 でも使用できますか。

**A**: OS X SDK は Xcode 4.6 以降のみ、および OS X 10.8 以降で動作します。
