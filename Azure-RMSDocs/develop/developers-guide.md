---
title: "開発者ガイド - AIP"
description: "開発者は Azure Information Protection を使用して、すべての種類のファイルを保護および管理することができます。"
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 03/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a53c2df2-a0a2-4f1f-995b-75ba55e4489b
ms.suite: ems
ms.reviewer: kartikk
ms.openlocfilehash: 3268b175b2e029c55ec5488a8c4ace8ad92fcb18
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2017
---
# <a name="azure-information-protection-developers-guide"></a>Azure Information Protection 開発者ガイド

このガイドでは、Azure Information Protection の Rights Management サービスの拡張、およびサービスとの統合に使用するツールについて説明します。 このガイドは、Rights Management システムを利用する管理者が、サポートされている広範なプラットフォーム向けにさまざまな種類のアプリケーションを作成できることを目的としています。

>現在 Azure Information Protection SDK には権限管理コンポーネントが含まれており、分類およびラベル付けについては開発中です。

## <a name="service-applications"></a>サービス アプリケーション

サービス アプリケーションは、エンタープライズ コンテンツ管理システム、ビジネス アプリケーション、またはクラウド ベースのビジネス ソリューションからのエクスポートにおいて、情報を保護する機能を提供します。 サービス アプリケーションの例としては、データ損失防止対策 (DLP) および Cloud Application Security (CAS) のアプリケーションが挙げられます。 マイクロソフトが提供するサービス アプリケーション開発向け SDK は、2 つのプログラミング モデルで利用できます。

- [C++](https://www.microsoft.com/en-us/download/details.aspx?id=38397)
- [C# マネージ API](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcManagedAPI)

### <a name="examples-of-service-applications"></a>サービス アプリケーションの例

- [IpcDlp](https://github.com/Azure-Samples/active-directory-dotnet-rms) は、RMS 対応の DLP サンプル アプリケーションです。DLP RMS 対応アプリケーションで制限付きコンテンツを保護および使用するために RMS FILE API を使用して実行する必要がある基本的な手順がわかります。
- [IpcAzureApp](https://github.com/Azure-Samples/active-directory-dotnet-rms) は、Azure BLOB ストレージのデータを保護するために Azure アプリケーションで RMS SDK を使用する方法をデモンストレーションするサンプルです。
- [RmsFileWatcher](https://github.com/Azure-Samples/active-directory-dotnet-rms) は、ファイル システムのディレクトリを監視し、すべての変更 (ファイルの追加や変更) に RMS 保護ポリシーを適用する Windows アプリケーションを構築する方法を示すサンプルです。
- [ProtectFilesInDir](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/ProtectFilesInDir) は、ディレクトリを入力として受け取り、そのディレクトリ内のすべてのファイルのみを再帰なしに保護するシンプルなコンソール アプリケーションです。

## <a name="powershell-guides"></a>PowerShell ガイド

これらのスクリプトは通常 Azure Rights Management 管理者によって使用され、サービス アプリケーションの開発とテストに役立ちます。

- [Azure Rights Management コマンドレット](https://msdn.microsoft.com/library/azure/dn629398.aspx)を使用すると、コマンド ラインから Azure RMS を管理できます。 PowerShell コマンドレットで自動化が可能になりますが、信頼性が高く反復的なプロセスをサポートしているので、管理者の作業も軽減されます。 また、一部の Azure RMS の高度な構成と操作には Azure PowerShell が必要です。
- [RMS 保護コマンドレット](https://msdn.microsoft.com/library/azure/mt433195.aspx)は、Azure Information Protection の Azure Rights Management (Azure RMS) のデータ保護、または Active Directory Rights Management サービス (AD RMS) と併用できます。また、これらの Rights Management デプロイの他の PowerShell モジュールを補完できます。 これらの RMS 保護コマンドレットを使用して、任意のファイルの種類について複数のファイルの保護と保護解除を一括して実行できます。

## <a name="user-applications"></a>ユーザー アプリケーション

ユーザー アプリケーションは、RMS SDK 2.1 または RMS SDK 4.2 を使用して作成することができます。
RMS SDK 4.2 は、人気のある OS (iOS および OSX、Android、Linux、Windows) 用の特定の.API をベースとした REST クライアントです。 RMS SDK 2.1 は、Windows ベースのネイティブ アプリケーションの作成に使用されます。

### <a name="user-application-development-guides"></a>ユーザー アプリケーション開発ガイド

- [アプリケーションの開発](developing-your-application.md)
- [アプリケーションのテスト](how-to-set-up-your-test-environment.md)
- [アプリケーションのデプロイ](deploying-your-application.md)

### <a name="user-application-samples"></a>ユーザー アプリケーションのサンプル

- [AzureIP Test](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/AzureIP_Test) は、サンプルのコンソール アプリケーションで、Azure テンプレートまたはアドホック ポリシーを使用してドキュメントを暗号化することができます。
- [IPCNotepad](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/AzureIP_Test) は、RMS 対応のサンプル アプリケーションです。各 RMS 対応アプリケーションで制限付きコンテンツを保護および使用するときに実行する必要がある基本的な手順がわかります。
- [RmsDocumentInspector](https://github.com/Azure-Samples/active-directory-dotnet-rms) は、コンテンツ ID やユーザー権限などの、RMS で保護されているファイルに関する情報を得られるツールです。

## <a name="development-environment-setup"></a>開発環境のセットアップ

次のガイドでは、一般的なツールを使用したアプリケーション開発環境のセットアップ手順を、OS ごとに説明します。

[![iOS および OSX のセットアップ](../media/develop/ios-icon.png)](ios-sdk.md)
[![Android のセットアップ](../media/develop/android-icon.png)](android-sdk.md)
[![Windows Phone のセットアップ](../media/develop/windows-phone-icon.png)](windows-phone-apps.md)
[![Windows サービスのセットアップ](../media/develop/windows-icon.png)](install-the-rms-sdk.md)
[![Linux のセットアップ](../media/develop/linux-icon.png)](linux-setup.md)


## <a name="how-tos"></a>手順ガイド

次の各トピックでは、アプリケーションの実装に関する具体的なガイダンスを提供しています。 サービス アプリケーションは、RMS SDK 2.x. を使用して作成します。 ユーザー アプリケーションは、RMS SDK 4.x. を使用して作成します。 記事のリンクは、アプリケーションの種類、サービス、ユーザー別になっています。

### <a name="general"></a>全般

- [方法: ドキュメント追跡の有効化と取り消し (サービス)](tracking-content.md)
- [クライアントを展開する方法](../rms-client/client-deployment-notes.md)
- [サービス アプリを別のテナントにデプロイする方法] (how-to-deploy-app.md)
- [方法: RMS サーバーをインストールして構成する (サービス)](how-to-install-and-configure-an-rms-server.md)
- [方法: ドキュメント追跡を使用する (ユーザー)](how-to-use-document-tracking.md)
- [Azure Information Protection で対称キーを更新する方法](how-to-renew-symmetric-key.md)

### <a name="security-and-authentication"></a>セキュリティと認証

- [Azure Active Directory ログインを使用するように App Service アプリケーションを構成する方法](https://docs.microsoft.com/en-us/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)
- [方法: Azure Active Directory Authentication (ADAL) 認証の使用](how-to-use-adal-authentication.md)
- [Azure RMS の認証を構成する (サービス)](adal-auth.md)
- [方法: API セキュリティ モードの設定 (サービス)](setting-the-api-security-mode-api-mode.md)
- [アプリケーションの Azure RMS の使用を有効にする (サービス)](how-to-use-file-api-with-aadrm-cloud.md)
- [Azure AD でアプリの登録と RMS の有効化を行う方法 (ユーザー)](authentication-integration.md)

### <a name="configuration-and-performance-management"></a>構成とパフォーマンスの管理

- [方法: 明示的な所有者権限の追加 (サービス)](add-explicit-owner-rights.md)
- [ファイル API の構成 (サービス)](file-api-configuration.md)
- [方法: 組み込み権限の使用 (ユーザー)](built-in-rights-usage-restriction-reference.md)
- [方法: エラーとパフォーマンスのログを有効にする (ユーザー)](enabling-logging.md)

## <a name="videos"></a>ビデオ

Microsoft の Dan Plastina が、[Azure Information Protection の概要](https://www.microsoft.com/cloud-platform/azure-information-protection)を説明します。

これらは、Micorsoft 2016 Ignite カンファレンスのビデオです。

- [組織内の電子メールのセキュリティ](https://myignite.microsoft.com/videos/2787)
- [データを安全に保護し共有するために包括的な ID ベースのソリューションを採用する](https://myignite.microsoft.com/videos/2784)
- [分類、ラベル付け、保護によって永続的なデータ保護が実現されるしくみを説明する](https://myignite.microsoft.com/videos/2786)

## <a name="other-resources"></a>その他のリソース

- [セキュリティのベスト プラクティス ガイド](security-guidelines.md)
- [RMS 開発者のコーナー (ブログ)](https://blogs.msdn.microsoft.com/rms/)
- [Azure Information Protection に関してよく寄せられる質問](https://docs.microsoft.com/en-us/information-protection/get-started/faqs)

### <a name="support-articles"></a>サポート記事

- [サポートされるファイル形式](supported-file-formats.md)
- [サポートされているプラットフォーム](supported-platforms.md)
- [Understanding usage restrictions (使用制限について)](understanding-usage-restrictions.md)

### <a name="api-reference"></a>API reference

- [Windows API リファレンス](https://msdn.microsoft.com/en-us/library/hh535292.aspx)
  - [Windows SDK エラー コード](https://msdn.microsoft.com/library/hh535248.aspx)
- [Windows Phone および Windows ストアの API リファレンス](https://msdn.microsoft.com/library/dn891914.aspx)
- [iOS および OSX の API リファレンス](https://msdn.microsoft.com/en-us/library/dn758306.aspx)
- [Android API リファレンス](https://msdn.microsoft.com/en-us/library/dn758245.aspx)
- [Linux API リファレンス](http://azuread.github.io/rms-sdk-for-cpp/annotated.html)

### <a name="previous-versions"></a>以前のバージョン

- [AD RMS SDK](https://msdn.microsoft.com/en-us/library/cc530379.aspx) は、RMS SDK の最初のバージョンです。
- [AD RMS スクリプト ツール](https://msdn.microsoft.com/en-us/library/bb968797.aspx)は、AD RMS のインストールのための管理ツールです。

### <a name="see-also"></a>関連項目

- [開発者向け用語集](terms.md)
- [Azure Information Protection の用語 - ITPro](../get-started/terminology.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]