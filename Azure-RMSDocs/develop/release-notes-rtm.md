---
title: リリース ノート
description: SDK 更新の改訂番号とその他の開発者情報。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 10/18/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: CE379738-4E1D-42AD-83F4-F89B70456EBB
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: cb969e8add0c79495cc2cc90e7e92368e42577dc
ms.sourcegitcommit: f0dee92d6668001681b507e82f8aea61f3bfa96e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69894460"
---
# <a name="release-notes"></a>リリース ノート

この記事には、RMS SDK 2.1 のこのリリースとそれ以前のリリースに関する重要な情報が含まれています。

## <a name="april-2019---update"></a>2019年4月-更新
- ファイル API のバグ修正。
- ファイル API が更新され、コンテンツの復号化時に抽出権限ではなく、エクスポート権限がチェックされるようになりました。
- インストーラーを修正して、アップグレード時に新しい PDF v2 プロテクターが確実にインストールされるようにしました。
- テレメトリの変更。 この変更には、C ランタイムライブラリをインストールするインストールパッケージの更新が必要でした。
- サービスバックエンドの認証の変更です。中断を最小限に抑えるには、この SDK バージョンに更新してください

## <a name="october-2017---update"></a>2017 年 10 月の更新

- 環境の初期化と初期化解除のための API が新しく 2 つ追加されました。 詳細については、「[IpcInitializeEnvironment](https://msdn.microsoft.com/library/hh535289.aspx)」と「[IpcUninitializeEnvironment](https://msdn.microsoft.com/library/hh535289.aspx)」を参照してください。
- サポートされるファイルの種類に Visio が加わりました。 詳細については、「 [ファイル API の構成](file-api-configuration.md)」を参照してください。

## <a name="february-2016---sdk-documentation-update"></a>2016 年 2 月 - SDK 文書更新

>[!Note]
> このセクションの機能文書更新は、日付を 2015 年 11 月 12 日とする SDK ダウンロードに適用されます。

- **認証フローの改善** - [Azure Active Directory 認証ライブラリ (ADAL)](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/) 経由の OAuth2 トークン ベース認証を使用します。 このプロセスとその API 拡張機能の詳細については、「[ADAL authentication for your RMS enabled application](how-to-use-adal-authentication.md)」 (RMS 対応アプリケーションの ADAL 認証) を参照してください。

- **ADAL の更新** Microsoft Online サインイン アシスタントではなく、ADAL 認証を使用するようにアプリケーションを更新すると、ユーザーと顧客は以下を利用できるようになります。

  - 多要素認証を使用する
  - コンピューターの管理者特権なしで RMS 2.1 クライアントをインストールする
  - Windows 10 向けアプリケーションの認定

- **Microsoft Online サインイン アシスタント (SIA) と RMS SDK のサポートがなくなります。** サポートの停止後、SIA は 6 か月間使用できます。


## <a name="december-2015-update"></a>2015 年 12 月更新

- 以下を含む一部の領域のパフォーマンスが向上しました。
    - ライセンス専用のサーバーを使用する場合は、プライマリのライセンス サーバーから発行します。
    - ネットワーク接続がない場合に RMS SDK 2.1 が失敗するまでの時間が短縮されています。

- エラー メッセージやトラブルシューティングを向上させる多くの更新があります。
- [サポートされているプラットフォーム](supported-platforms.md)一覧も更新されました。
- 運用前環境の必要性とアプリケーション マニフェストの使用は RMS SDK 2.1 から削除されています。 この開発者向けドキュメント セットのこれらのセクションは削除されており、ドキュメントは全体的に簡素になり、再編成されています。

## <a name="may-2015-update"></a>2015 年 5 月の更新

-   **サービス アプリケーションとクラウド ベースの RMS** - [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx) には 3 つの情報 (対称キー、**AppPrincipalId**、**TenantBposId**) が必要です。 この点についての記事が更新され、この情報の処理に関するガイダンスが用意されました。 この更新については、改訂版の「[方法: クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)」を参照してください。

## <a name="april-2015-update"></a>2015 年 4 月の更新

-   一連の新しい API で**ドキュメント追跡** が可能になりました。 詳細については、「[Tracking Content](tracking-content.md)」 (コンテンツの追跡) を参照してください。
-   **暗号化の種類** – 暗号化パッケージの選択の API レベルでの制御をサポートします。 詳細については、「[Working with encryption](working-with-encryption.md)」 (暗号化の処理) を参照してください。

    **注**  API の **IPC\_LI\_DEPRECATED\_ENCRYPTION\_ALGORITHMS** フラグは非公開となりました。 今後、このフラグを参照しても、アプリケーションでコンパイルされませんが、既にビルドされたアプリケーションではこのフラグを API コード内でプライベートに評価するため、引き続き機能します。 フラグを変更するだけでも、古い非推奨の暗号化アルゴリズムのフラグの機能を利用できます。 詳細については、「[Working with encryption](working-with-encryption.md)」 (暗号化の処理) を参照してください。

-   **サーバー モード アプリケーション**は **IPC\_API\_MODE\_SERVER** の [API モード値](https://msdn.microsoft.com/library/hh535236.aspx) を使用し、アプリケーション マニフェストは不要になりました。 運用 RMS サーバーに対してアプリケーションをテストすることができ、運用環境に切り替えるときに運用のライセンスを取得する必要はありません。 サーバー モード アプリケーションの詳細については、「[アプリケーションの種類](application-types.md)」を参照してください。
-   **ログ**は、ファイルと Event Tracing for Windows メソッドの両方で実装されました。
-   **Windows 7 SP1 または Windows Server 2008 R2 コンピューター**を実行している場合は、「開発者向けの重要な注意事項」の下の記述を参照してください。

## <a name="january-2015-update"></a>2015 年 1 月の更新

-   **保護されたファイル (pfile) のサポート対象サイズの増加** – 1 GB より大きいサイズの pfile がサポートされるようになりました。 pfile の詳細については、「[Support File Formats](supported-file-formats.md)」 (サポートされるファイル形式) を参照してください。
-   **ログの強化による診断の向上** – 確認する必要があるメッセージが**エラー**または**警告**のログ レベルで表示されます。 表示されている例外など、他のすべてのメッセージは**情報**としてログに記録されます。

    詳細情報が失われないようにするために、この方法を選択しました。 これにより、重要なメッセージだけが警告レベルで表示されるようになりました。

-   **会社テンプレートの取得** – ユーザーからのレポートやフィードバックに基づき、テンプレート取得コードが大幅に修正されました。
-   強化されたローカライズの整合性

## <a name="october-2014-update"></a>2014 年 10 月の更新

-   SDK のファイル API のコンポーネントの既定の動作が更新されました。 詳細については、「 [ファイル API の構成](file-api-configuration.md)」を参照してください。
-   新機能の電子メール通知については、開発者向け注意事項の記事「[電子メール通知の有効化](how-to-enable-email-notification.md)」を参照してください。

## <a name="july-2014-update"></a>2014 年 7 月の更新

SDK のファイル API のコンポーネントが拡張され、次の機能が提供されるようになりました。

-   使用する保護機能を識別します。
-   ファイル レベルの粒度で RMS 保護を提供します。

    このリリースで追加された関数:

    **注** - ここに記載されている以外に、ファイル API の拡張機能として、サポートされるデータ型と構造体が追加されました。 このリリースで更新されているすべての記事に、"**暫定的なものであり、変更される可能性があります**" と記載されています。

    -   [IpcfOpenFileOnHandle](https://msdn.microsoft.com/library/dn771751.aspx)
    -   [IpcfOpenFileOnILockBytes](https://msdn.microsoft.com/library/dn771752.aspx)
    -   [IpcfGetFileProperty](https://msdn.microsoft.com/library/dn771749.aspx)
    -   [IpcfLogicalFileRangeToRawFileRange](https://msdn.microsoft.com/library/dn771750.aspx)
    -   [IpcfReadFile](https://msdn.microsoft.com/library/dn771753.aspx)
    -   [IpcfSetEndOfFile](https://msdn.microsoft.com/library/dn771754.aspx)
    -   [IpcfWriteFile](https://msdn.microsoft.com/library/dn771756.aspx)

## <a name="april-2014-update"></a>2014 年 4 月の更新

-   **ファイル API のメモリ使用率** (特に大規模な PFile の場合) が大幅に改善されました。
-   **コンテンツ ID** は、**IPC\_LI\_CONTENT\_ID** プロパティを使用して書き込み可能になりました。 詳細については、「[License property types](https://msdn.microsoft.com/library/hh535287.aspx)」 (ライセンスのプロパティの種類) を参照してください。
-   **運用マニフェストの要件** – RMS 対応のアプリケーション/サービスをサーバー モードで実行する場合には、マニフェストは不要になりました。 詳細については、「[Application types](application-types.md)」 (アプリケーションの種類) を参照してください。
-   **ドキュメントの更新**

    **ベスト プラクティスのテスト** – Azure RMS でテストする前にオンプレミス サーバーを使用する場合のガイダンスを追加しました。 詳細については、「[クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)」を参照してください。

## <a name="important-developer-notes"></a>開発者向けの重要な注意事項

-   **すべてのファイルの種類のネイティブ サポート**

    Rights Management サービス SDK 2.1 のこのリリースでは、あらゆるファイルの種類 (拡張子) のネイティブ サポートを追加できます。 たとえば、拡張子 &lt;ext&gt; (Office 以外および pdf) では、その拡張子の管理者の構成が "NATIVE" の場合、\*.p&lt;ext&gt; が使用されます。

    サポートされているファイルの種類の詳細については、「[ファイル API の構成](file-api-configuration.md)」を参照してください。

-   **Windows 7 SP1 および Windows Server 2008 R2 SP1 コンピューター**に更新プログラム [KB2533623](https://support.microsoft.com/kb/2533623) が適用されていない場合、office ファイルを保護する際に "パラメーターが正しくありません。 エラー コード 0x80070057" というエラーが発生することがあります。 このエラーが表示された場合は、更新プログラムをインストールしてやり直してください。 それでも問題が解決しない場合は、RMS SDK ベータ フィードバック エイリアス(<rmcstbeta@microsoft.com>) にお問い合わせください。

    **注**  2015 年 4 月のリリース時点で、この更新プログラムのインストール プロセスにチェックが追加されました。

     

-   **ファイル API の統合**

    Active Directory Rights Management サービスのファイル API では、ファイル API の追加により次の利点と機能が提供されます。

      - 機密データを自動化された方法で保護することが可能であり、さまざまなファイル形式で使用される Information Rights Management (IRM) の実装の詳細を知る必要はありません。

      - Microsoft Office ファイル、Portable Document Format (PDF) ファイル、および他の一部のファイルの種類は、ネイティブ保護を使用して保護することができます。 ネイティブ保護で保護できるファイルの種類の一覧については、「[ファイル API の構成](file-api-configuration.md)」を参照してください。

      - システム ファイルと Office ファイルを除く、すべてのファイルは、RMS 保護されたファイル形式 (PFile) を使用して保護できます。

    ファイル API は、次の 4 つの新しい関数によって実装されます:[IpcfDecryptFile](https://msdn.microsoft.com/library/dn133058.aspx)、[IpcfEncryptFile](https://msdn.microsoft.com/library/dn133059.aspx)、[IpcfGetSerializedLicenseFromFile](https://msdn.microsoft.com/library/dn133060.aspx)、[IpcfIsFileEncrypted](https://msdn.microsoft.com/library/dn133061.aspx)。

    ファイル API は、Rights Management Service Client 2.1 がクライアント コンピューターにインストールされていること、コンピューターが RMS サーバーに接続されていることを必要とします。 RMS サーバー、RMS クライアント、およびそれらの機能の詳細については、[RMS の IT Pro ドキュメント](https://technet.microsoft.com/library/cc771234(v=ws.10).aspx)に関する TechNet のコンテンツを参照してください。

-   **問題**:ライセンスを最初から作成する場合は、所有権を明示的に許可する必要があります。

    **解決策**:ライセンスを最初から作成する場合は、アプリケーションで [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx) を使用して、ライセンス所有者に**所有者**権限を明示的に追加する必要があります。 詳細については、「[Add explicit owner rights](add-explicit-owner-rights.md)」 (所有権を明示的に追加する) を参照してください。

-   **問題**:アプリケーションでそのハンドルを使用して同じウィンドウに対して [IpcProtectWindow](https://msdn.microsoft.com/library/hh535268.aspx) または [IpcUnprotectWindow](https://msdn.microsoft.com/library/hh535272.aspx) を 2 回呼び出した場合、RMS SDK 2.1 では **HRESULT** でエラーが返されます。

    **解決策**:この問題に対する具体的なガイダンスについては、[IpcProtectWindow](https://msdn.microsoft.com/library/hh535268.aspx) および [IpcUnprotectWindow](https://msdn.microsoft.com/library/hh535272.aspx) の「解説」を参照してください。

-   **問題**:複数のアーキテクチャをビルドする場合は、このガイダンスに従う必要があります。

    **解決策**:Ipcsecproc\*isv.dll を異なるアーキテクチャに使用する場合 (たとえば、64 ビット コンピューターに 64 ビット SDK がインストールされていて、Ipcsecproc\*isv.dll を必要とする 32 ビット コンピューターに 32 ビット SDK を展開しなければならない場合)、32 ビット SDK を別のコンピューターにインストールし、%PROGRAMFILES%\\Microsoft Information Protection And Control フォルダー (既定の場所または SDK のインストール先として選択した任意の場所) から Ipcsecproc\*isv.dll ファイルをコピーする必要があります。

## <a name="frequently-asked-questions"></a>よく寄せられる質問

**Q**: LCID パラメーターを受け取る関数では、既定の言語の動作はどうなるでしょうか。

**A**:既定のロケールには 0 を使用します。 この場合、AD RMS Client 2.1 では、名前と説明を次の順序で検索し、使用可能な最初の値が取得されます。

    1 - User preferred LCID.
    2 - System locale LCID.
    3 - The first available language specified in the Rights Management Server (RMS) template.

名前と説明を取得できない場合、エラーが返されます。 名前と説明は、1 つの LCID に 1 つだけ存在できます。
