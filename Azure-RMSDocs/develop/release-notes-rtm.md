---
title: リリース ノート
description: Microsoft Rights Management Service SDK version 2.1 2019 年10月以前の更新プログラムのリリースノートを参照してください。
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
ms.custom: dev, has-adal-ref
ms.openlocfilehash: f8b0aa99b4a18f1e2b9d0c9b3ddedf2d745b3e19
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "95570631"
---
# <a name="release-notes"></a>リリース ノート

この記事には、RMS SDK 2.1 のこのリリースとそれ以前のリリースに関する重要な情報が含まれています。

## <a name="october-2019---update"></a>2019年10月-更新

- 状況によっては、対称キー認証を使用しても、Azure RMS によるユーザーの認証に失敗し、コンテンツの保護と復号化を防ぐことができます。
- 以前に保護され、保護されていない一部の PDF ドキュメントが現在保護されているかどうかを確認しようとすると、RMS クライアントがクラッシュする場合があります。
- 特別なポートで構成されている AD RMS サーバーに DNS リダイレクトを使用すると、正しく機能しません。

## <a name="september-2019---update"></a>2019年9月-更新

- 他のいくつかの RMS クライアントメソッドと同時に初期化メソッドを呼び出そうとしたときに発生する可能性のあるデッドロックを修正しました。
- パスワードで保護された Office ファイルが RMS で保護されているかどうかを判断する際の問題を修正します。
-   特別な目的のライセンスのライセンス検証を更新します。
- PDF プロテクターを更新します。
- その他のバグの修正。
- C ランタイムライブラリに対して静的にリンクするように更新します。

## <a name="april-2019---update"></a>2019年4月-更新
- ファイル API のバグ修正。
- ファイル API が更新され、コンテンツの復号化時に抽出権限ではなく、エクスポート権限がチェックされるようになりました。
- インストーラーを修正して、アップグレード時に新しい PDF v2 プロテクターが確実にインストールされるようにしました。
- テレメトリの変更。 この変更には、C ランタイムライブラリをインストールするインストールパッケージの更新が必要でした。
- サービスバックエンドの認証の変更 **です。アプリケーションで対称キー認証を使用する場合は、この SDK バージョンに更新して中断を最小限に抑えるようにしてください。**
- VC 15.9 のサポート


## <a name="october-2017---update"></a>2017 年 10 月の更新

- 環境の初期化と初期化解除のための API が新しく 2 つ追加されました。 詳細については、「[IpcInitializeEnvironment](/previous-versions/windows/desktop/msipc/microsoft-information-protection-and-control-client-functions)」と「[IpcUninitializeEnvironment](/previous-versions/windows/desktop/msipc/microsoft-information-protection-and-control-client-functions)」を参照してください。
- サポートされるファイルの種類に Visio が加わりました。 詳細については、「 [ファイル API の構成](file-api-configuration.md)」を参照してください。

## <a name="february-2016---sdk-documentation-update"></a>2016 年 2 月 - SDK 文書更新

>[!Note]
> このセクションの機能文書更新は、日付を 2015 年 11 月 12 日とする SDK ダウンロードに適用されます。

- **認証フローの改善** - [Azure Active Directory 認証ライブラリ (ADAL)](/azure/active-directory/azuread-dev/active-directory-authentication-libraries) 経由の OAuth2 トークン ベース認証を使用します。 このプロセスとその API 拡張機能の詳細については、「[ADAL authentication for your RMS enabled application](how-to-use-adal-authentication.md)」 (RMS 対応アプリケーションの ADAL 認証) を参照してください。

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

-   **サービスアプリとクラウドベースの RMS**  - [IPC \_資格情報の \_ 対称 \_ キー](/previous-versions/windows/desktop/msipc/ipc-credential-symmetric-key)には、対称キー、 **AppPrincipalId**、 **tenantbposid)** という3つの情報が必要です。 この点についての記事が更新され、この情報の処理に関するガイダンスが用意されました。 この更新については、改訂版の「[方法: クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)」を参照してください。

## <a name="april-2015-update"></a>2015 年 4 月の更新

-   一連の新しい API で **ドキュメント追跡** が可能になりました。 詳細については、「[Tracking Content](tracking-content.md)」 (コンテンツの追跡) を参照してください。
-   **暗号化の種類** – 暗号化パッケージの選択の API レベルでの制御をサポートします。 詳細については、「 [暗号化の](working-with-encryption.md)使用」を参照してください。

    **メモ**   API の **IPC \_ LI \_ 非推奨の \_ 暗号化 \_ アルゴリズム** フラグは公開されなくなります。 今後、このフラグを参照しても、アプリケーションでコンパイルされませんが、既にビルドされたアプリケーションではこのフラグを API コード内でプライベートに評価するため、引き続き機能します。 フラグを変更するだけでも、古い非推奨の暗号化アルゴリズムのフラグの機能を利用できます。 詳細については、「 [暗号化の](working-with-encryption.md)使用」を参照してください。

-   **サーバー モード アプリケーション** は **IPC\_API\_MODE\_SERVER** の [API モード値](/previous-versions/windows/desktop/msipc/api-mode-values) を使用し、アプリケーション マニフェストは不要になりました。 運用 RMS サーバーに対してアプリケーションをテストすることができ、運用環境に切り替えるときに運用のライセンスを取得する必要はありません。 サーバーモードアプリケーションの詳細については、「 [アプリケーションの種類](application-types.md)」を参照してください。
-   **ログ** は、ファイルと Event Tracing for Windows メソッドの両方で実装されました。
-   **Windows 7 SP1 または Windows Server 2008 R2 コンピューター** を実行している場合は、「開発者向けの重要な注意事項」の下の記述を参照してください。

## <a name="january-2015-update"></a>2015 年 1 月の更新

-   **保護されたファイル (pfile) のサポート対象サイズの増加** – 1 GB より大きいサイズの pfile がサポートされるようになりました。 pfile の詳細については、「[Support File Formats](supported-file-formats.md)」 (サポートされるファイル形式) を参照してください。
-   **ログの強化による診断の向上** – 確認する必要があるメッセージが **エラー** または **警告** のログ レベルで表示されます。 まだ表示されている例外も含め、他のすべてのメッセージは **情報** としてログに記録されます。

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

    **メモ**  -ここに記載されていない、その他のデータ型と構造体については、ファイル API 拡張機能用に追加されています。 このリリースで更新されているすべての記事に、"**暫定的なものであり、変更される可能性があります**" と記載されています。

    -   [IpcfOpenFileOnHandle](/previous-versions/windows/desktop/msipc/ipcfopenfileonhandle)
    -   [IpcfOpenFileOnILockBytes](/previous-versions/windows/desktop/msipc/ipcfopenfileonilockbytes)
    -   [IpcfGetFileProperty](/previous-versions/windows/desktop/msipc/ipcfgetfileproperty)
    -   [IpcfLogicalFileRangeToRawFileRange](/previous-versions/windows/desktop/msipc/ipcflogicalfilerangetorawfilerange)
    -   [IpcfReadFile](/previous-versions/windows/desktop/msipc/ipcfreadfile)
    -   [IpcfSetEndOfFile](/previous-versions/windows/desktop/msipc/ipcfsetendoffile)
    -   [IpcfWriteFile](/previous-versions/windows/desktop/msipc/ipcfwritefile)

## <a name="april-2014-update"></a>2014 年 4 月の更新

-   **ファイル API のメモリ使用率** (特に大規模な PFile の場合) が大幅に改善されました。
-   **コンテンツ id** は、 **IPC \_ LI \_ content \_ id** プロパティを使用して書き込み可能になりました。 詳細については、「[License property types](/previous-versions/windows/desktop/msipc/license-property-types)」 (ライセンスのプロパティの種類) を参照してください。
-   **運用マニフェストの要件** – RMS 対応のアプリケーション/サービスをサーバー モードで実行する場合には、マニフェストは不要になりました。 詳細については、「 [アプリケーションの種類](application-types.md)」を参照してください。
-   **ドキュメントの更新**

    **ベスト プラクティスのテスト** – Azure RMS でテストする前にオンプレミス サーバーを使用する場合のガイダンスを追加しました。 詳細については、「[クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)」を参照してください。

## <a name="important-developer-notes"></a>開発者向けの重要な注意事項

-   **すべてのファイルの種類のネイティブ サポート**

    Rights Management サービス SDK 2.1 のこのリリースでは、あらゆるファイルの種類 (拡張子) のネイティブ サポートを追加できます。 たとえば、拡張子 &lt;ext&gt; (Office 以外および pdf) では、その拡張子の管理者の構成が "NATIVE" の場合、\*.p&lt;ext&gt; が使用されます。

    サポートされているファイルの種類の詳細については、「 [ファイル API の構成](file-api-configuration.md)」を参照してください。

-   **Windows 7 SP1 および Windows Server 2008 R2 SP1 コンピューター** に更新プログラム [KB2533623](https://support.microsoft.com/kb/2533623) が適用されていない場合、office ファイルを保護する際に "パラメーターが正しくありません。 エラー コード 0x80070057" というエラーが発生することがあります。 このエラーが表示された場合は、更新プログラムをインストールしてやり直してください。 それでも問題が解決しない場合は、RMS SDK ベータ フィードバック エイリアス(<rmcstbeta@microsoft.com>) にお問い合わせください。

    **メモ**   2015年4月のリリースの時点で、この KB のインストールプロセスにチェックが追加されています。



-   **ファイル API の統合**

    Active Directory Rights Management サービスのファイル API では、ファイル API の追加により次の利点と機能が提供されます。

      - 機密データを自動化された方法で保護することが可能であり、さまざまなファイル形式で使用される Information Rights Management (IRM) の実装の詳細を知る必要はありません。

      - Microsoft Office ファイル、Portable Document Format (PDF) ファイル、および他の一部のファイルの種類は、ネイティブ保護を使用して保護することができます。 ネイティブ保護で保護できるファイルの種類の完全な一覧については、「 [ファイル API の構成](file-api-configuration.md)」を参照してください。

      - システム ファイルと Office ファイルを除く、すべてのファイルは、RMS 保護されたファイル形式 (PFile) を使用して保護できます。

    ファイル API は、[IpcfDecryptFile](/previous-versions/windows/desktop/msipc/ipcfdecryptfile)、[IpcfEncryptFile](/previous-versions/windows/desktop/msipc/ipcfencryptfile)、[IpcfGetSerializedLicenseFromFile](/previous-versions/windows/desktop/msipc/ipcfgetserializedlicensefromfile)、[IpcfIsFileEncrypted](/previous-versions/windows/desktop/msipc/ipcfisfileencrypted) という 4 つの新機能を介して実装されます。

    ファイル API は、Rights Management Service Client 2.1 がクライアント コンピューターにインストールされていること、コンピューターが RMS サーバーに接続されていることを必要とします。 RMS サーバー、RMS クライアント、およびそれらの機能の詳細については、[RMS の IT Pro ドキュメント](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771234(v=ws.10))に関する TechNet のコンテンツを参照してください。

-   **問題**: ライセンスを最初から作成する場合は、所有権を明示的に許可する必要があります。

    **ソリューション**: ライセンスを最初から作成する場合は、アプリケーションで [IpcCreateLicenseFromScratch](/previous-versions/windows/desktop/msipc/ipccreatelicensefromscratch) を使用して、ライセンス所有者に **所有者** 権限を明示的に追加する必要があります。 詳細については、「 [明示的な所有者権限の追加](add-explicit-owner-rights.md)」を参照してください。

-   **問題点**: アプリケーションがハンドルを使用して同じウィンドウに対して [IpcProtectWindow](/previous-versions/windows/desktop/msipc/ipcprotectwindow) または [IpcUnprotectWindow](/previous-versions/windows/desktop/msipc/ipcunprotectwindow) を2回呼び出す場合、RMS SDK 2.1 は **HRESULT** でエラーを返します。

    **解決方法**: 詳細については、 [IpcProtectWindow](/previous-versions/windows/desktop/msipc/ipcprotectwindow) と [IpcUnprotectWindow](/previous-versions/windows/desktop/msipc/ipcunprotectwindow)の「解説」を参照してください。

-   **問題**: 複数のアーキテクチャをビルドする場合は、このガイダンスに従う必要があります。

    **解決方法**: ipcsecprocisv.dll を別のアーキテクチャで使用する場合 \* (たとえば、64ビットコンピューターに64ビット SDK をインストールしたが、ipcsecprocisv.dll を必要とする32ビットコンピューターにを展開する場合など \* )、32ビット SDK を別のコンピューターにインストールし、 \* "% PROGRAMFILES% \\ Microsoft Information Protection と Control" フォルダー (既定の場所または SDK のインストール先として選択した場所) から、ipcsecprocisv.dll ファイルをそこにコピーする必要があります。

## <a name="frequently-asked-questions"></a>よく寄せられる質問

**Q**: LCID パラメーターを受け取る関数では、既定の言語の動作はどうなるでしょうか。

**A**: 既定のロケールには 0 を使用します。 この場合、AD RMS Client 2.1 では、名前と説明を次の順序で検索し、使用可能な最初の値が取得されます。

1. ユーザーの優先 LCID。
2. システムロケール LCID。
3. Rights Management サーバー (RMS) テンプレートで指定されている最初の使用可能な言語。

名前と説明を取得できない場合、エラーが返されます。 名前と説明は、1 つの LCID に 1 つだけ存在できます。