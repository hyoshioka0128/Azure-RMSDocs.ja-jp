---
title: "新機能とリリース ノート | Azure RMS"
description: "重要な変更点と、この新しいバージョンの RMS SDK の機能について説明します。"
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4fa1c686-b00b-4734-9abb-141ce582a6af
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: acd6dc2190996787b5354407bbaedec921a5b48c
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="whats-new-and-release-notes"></a>新機能とリリース ノート

## <a name="whats-new"></a>新機能
Microsoft Rights Management SDK 4.2 では、RMS アプリケーションが一段と簡素化され、柔軟性が向上しています。 このトピックでは、このバージョンの RMS SDK の重要な変更点と機能の概要を示します。

### <a name="new-for-june-2016"></a>2016 年 6 月の新機能

- **先進認証のサポート** - Active Directory Authentication Library (ADAL) ベースのサインインが RMS 対応アプリに導入されます。 これによって利用可能になるサインイン機能としては、多要素認証 (MFA)、SAML ベースのサードパーティ ID プロバイダーと RMS クライアント アプリケーションの組み合わせ、スマート カードや証明書をベースとする認証などがあります。また、RMS 対応アプリで基本認証プロトコルを使用する必要がなくなります。
- **ドキュメント追跡のサポート** -開発するアプリの中でドキュメントを保護するときに、ドキュメント追跡を有効化できるようになりました。
- パフォーマンスの向上
- バグの修正


### <a name="december-2015-update"></a>2015 年 12 月の更新

このリリースでは、デバイス用の RMS SDK はバージョン 4.2 であり、以下の機能が追加されています。

-   ドキュメント追跡 (IOS/OS X および Android オペレーティング システムでは RMS オンラインのみ)

    iOS/OS X の場合の詳細および使用ガイダンスについては、追跡情報、および [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx) での追加のドキュメント追跡登録メソッドを提供する、[MSLicenseMetadata](https://msdn.microsoft.com/library/mt573683.aspx) クラスを参照してください。 Android 用の同様の機能も [LicenseMetadata](https://msdn.microsoft.com/library/mt573675.aspx) および [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) に追加されています。

    ドキュメント追跡機能の詳細については、「[方法: ドキュメント追跡を使用する](how-to-use-document-tracking.md)」を参照してください。

-   Android API の非同期バージョンに相当する一連の同期メソッド。

    [CustomProtectedInputStream.create 同期メソッド](https://msdn.microsoft.com/library/mt631362.aspx)

    [CustomProtectedOutputStream.create 同期メソッド](https://msdn.microsoft.com/library/mt631363.aspx)

    [ProtectedFileInputStream.create 同期メソッド](https://msdn.microsoft.com/library/mt631375.aspx)

    [ProtectedFileOutputStream.create 同期メソッド](https://msdn.microsoft.com/library/mt631376.aspx)

    [TemplateDescriptor.getTemplates 同期メソッド](https://msdn.microsoft.com/library/mt631380.aspx)

    [UserPolicy.acquire 同期メソッド](https://msdn.microsoft.com/library/mt631384.aspx)

    [UserPolicy.create (PolicyDescriptor…) 同期メソッド**](https://msdn.microsoft.com/library/mt631385.aspx)

    [UserPolicy.create (TempalteDescriptor…) 同期メソッド](https://msdn.microsoft.com/library/mt631386.aspx)

-   Android API に新しい [ProtectedBuffer](https://msdn.microsoft.com/library/mt631369.aspx) クラスを追加します。
-   エラー メッセージやトラブルシューティングを向上させる更新プログラム
-   暗号化操作の重要なパフォーマンスの向上

### <a name="july-2015-update---adds-support-for-linux--c-development"></a>2015 年 7 月の更新 – Linux / C++ による開発のサポートを追加

このリリースでは、以下が追加されています。

-   Linux プラットフォーム向けの RMS SDK 4.1

    詳細については、「[作業開始](get-started.md)」を参照してください。

### <a name="may-2015-update---adds-logging-control"></a>2015 年 5 月の更新 – ログの制御を追加

このリリースでは、以下のサポートが追加されています。

-   iOS

    アプリケーションの暗号化および復号化を独立して、並列的に実行できます。

    詳細については、「[MSProtector](https://msdn.microsoft.com/library/mt210993.aspx)」を参照してください。

    ログ レベルの制御の設定が可能になりました。

    詳細については、「[How to: Enable error and performance logging](enabling-logging.md)」 (方法: エラーとパフォーマンスのログを有効にする) を参照してください。

    キャッシュ クリアのサポートが追加されました。

    詳細については、「[MSProtection:resetStateWithCompletionBlock](https://msdn.microsoft.com/library/mt210991.aspx)」を参照してください。

### <a name="february-2015-update---adds-windows-store-application-support"></a>2015 年 2 月の更新 – Windows ストア アプリケーションのサポートを追加

このリリースでは、Windows ストア アプリケーションのサポートを追加し、RMS SDK 4.1 の Windows Phone、Android、および iOS/OS X 版リリースにそれぞれ同等の機能を提供しています。

### <a name="january-2015-update---adds-winphone-platform-support"></a>2015 年 1 月の更新 – WinPhone プラットフォームのサポートを追加

このリリースでは、Windows Phone オペレーティング システムのサポートを追加し、RMS SDK 4.1 の Android 版および iOS/OS X 版リリースにそれぞれ同等の機能を提供しています。

### <a name="october-2014-update---upgrade-to-microsoft-rms-sdk-41"></a>2014 年 10 月の更新 – Microsoft RMS SDK 4.1 にアップグレード

RMS SDK のバージョン 4.1 のリリースでは、Google Android と Apple iOS/OS X に以下の新機能が追加されています。

-   *ユーザーの同意*を処理するための Android および iOS/OS SDK API 拡張により、SDK の動作をユーザーが確認できるようになりました。 現在、サポートされている同意タイプは、ドキュメント追跡、および不明な AD RMS サービス URL へのアクセスです。

    詳細については、Android API バージョンの [ConsentCallback インターフェイス](https://msdn.microsoft.com/library/dn833503.aspx)を例として参照してください。

-   iOS 8 および OS X 10.10 (Yosemite) がサポートされるようになりました。 Xcode 6 で必要ないくつかのプロパティ名も変更されました。

    たとえば、MSUserPolicy.name が [MSUserPolicy.policyName](https://msdn.microsoft.com/library/dn790799.aspx) に変更されました。

## <a name="release-notes"></a>リリース ノート

このセクションでは、開発者が知っておくと便利な、Microsoft Rights Management SDK 4.x API の現在および以前のリリースに関する情報をまとめています。

**AD RMS SDK 4.1 – iOS/OS X および Android プラットフォームのグローバル公開リリース**

-   **AD RMS のサポート** – 新しい AD RMS サーバーのモバイル デバイス拡張機能により、IT 管理者はモバイル デバイスで RMS 対応アプリケーションを使用できます。
-   **オフラインで使用** – エンドユーザーが RMS 保護されたデータにオフラインでアクセスできます。
-   **認証の分離** - 独自に開発した認証ライブラリを Azure RMS と AD RMS に使用できます (推奨される [Azure AD 認証ライブラリ (ADAL)](https://MSDN.Microsoft.Com/library/jj573266.aspx) を使用することもできます)。
-   **UI の分離** – 開発者は、RMS 保護されたドキュメントを保護および使用するためのユーザー インターフェイスを構築できます。
-   **再設計された API** – RMS の一貫性のある動作により、開発者は最低限の労力で API のシンプルかつ透過的な暗号化および暗号化解除を利用できます。

**すべてのプラットフォームに共通**

-   RMS SDK 4.x API は*スレッド セーフ*ではありません。

**Android**

-   Amazon® Kindle デバイスで .ptxt の添付ファイルを表示するサンプル アプリケーションを使用する際に、表示する前に、まずファイルをダウンロードする必要があります。

    **ソリューション** – これは既知の問題であり、今後対応する予定です。

-   複数のインスタンスが許可されていると、SDK を使用するアプリケーションがクラッシュすることがあります。

    **ソリューション** – アプリケーションが Android API への複数インスタンスの呼び出しを許可しないようにします。

-   [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx).write(byte\[\] array, int offset, int length) メソッドを使用するときに、長さが *array.length* の値と異なっていると、後で SDK を使用してコンテンツを使用することができません。

    **ソリューション** – これは既知の問題です。 対策としては、*byte \[\]* 配列に渡す長さの値は常に length パラメーターと同じにするか、[ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx).write(byte\[\] array) メソッドを使用します。

**iOS および OS X**

-   iOS および OS X 用 SDK をサポートするポルトガル語の言語仕様は&2; つありますが、 バグがあるため、現在 1 番目の言語仕様のローカライズは完全にはサポートしていません。 このバグにより、ポルトガル語は完全にはサポートされていません。 テキストの大部分は翻訳されますが、UI は翻訳されません。

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

    - [MSProtectedData.protectedDataWithProtectedFile](https://msdn.microsoft.com/library/dn758351.aspx)
    - [MSCustomProtectedData.customProtectedDataWithPolicy](https://msdn.microsoft.com/library/dn758315.aspx)



**注**  MDI アプリケーションは、iOS API ではサポートされていません。

## <a name="frequently-asked-questions"></a>よく寄せられる質問

**すべてのプラットフォーム**

**Q**: 保護ワークフローに**カスタム アクセス許可**の選択 UI が表示されません。 これはなぜでしょうか。

**A** – これは既知の問題であり、今後対応する予定です。

**Q**: SDK およびサンプル アプリケーションを試すために新しい組織のテナントを取得するにはどうすればよいですか。

**A**: Azure AD RMS のテスト組織の資格情報を要求するには、<rmcstbeta@microsoft.com> に電子メールを送信してください。

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

**OS X**

**Q**: サンプル アプリケーションのフレームワークは Xcode 5 に対応していますが、Xcode 4.6 でも使用できますか。

**A**: OS X SDK は Xcode 4.6 以降のみ、および OS X 10.8 以降で動作します。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]