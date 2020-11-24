---
title: Azure Information Protection 開発者ガイド
description: 開発者は Azure Information Protection を使用して、すべての種類のファイルを保護および管理することができます。
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 10/11/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a53c2df2-a0a2-4f1f-995b-75ba55e4489b
ms.suite: ems
ms.reviewer: kartikk
ms.custom: has-adal-ref
ms.openlocfilehash: 1ce4499d20da066eddac8d01c29ef1b52ccea250
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "95570214"
---
# <a name="azure-information-protection-developers-guide"></a>Azure Information Protection 開発者ガイド

このガイドでは、Azure Information Protection の Rights Management サービスの拡張、およびサービスとの統合に使用するツールについて説明します。

>現行の Azure Information Protection SDK には、権限管理コンポーネントが含まれています。 分類とラベル付けのコンポーネントは開発中です。

## <a name="service-applications"></a>サービス アプリケーション

サービス アプリケーションは、エンタープライズ コンテンツ管理システム、ビジネス アプリケーション、またはクラウド ベースのビジネス ソリューションからのエクスポートにおいて、情報を保護する機能を提供します。 サービス アプリケーションの例としては、データ損失防止対策 (DLP) および Cloud Application Security (CAS) のアプリケーションが挙げられます。 マイクロソフトが提供するサービス アプリケーション開発向け SDK は、2 つのプログラミング モデルで利用できます。

- [C++](https://www.microsoft.com/download/details.aspx?id=38397)
- [C# マネージド API](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcManagedAPI)

### <a name="examples-of-service-applications"></a>サービス アプリケーションの例

- [IpcDlp](https://github.com/Azure-Samples/active-directory-dotnet-rms) は、RMS 対応の DLP サンプル アプリケーションです。DLP RMS 対応アプリケーションで制限付きコンテンツを保護および使用するために RMS FILE API を使用して実行する必要がある基本的な手順がわかります。
- [IpcAzureApp](https://github.com/Azure-Samples/active-directory-dotnet-rms) は、Azure BLOB ストレージのデータを保護するために Azure アプリケーションで RMS SDK を使用する方法をデモンストレーションするサンプルです。
- [RmsFileWatcher](https://github.com/Azure-Samples/active-directory-dotnet-rms) は、ファイル システムのディレクトリを監視し、すべての変更 (ファイルの追加や変更) に RMS 保護ポリシーを適用する Windows アプリケーションを構築する方法を示すサンプルです。
- [ProtectFilesInDir](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/ProtectFilesInDir) は、ディレクトリを入力として受け取り、そのディレクトリ内のすべてのファイルのみを再帰なしに保護するシンプルなコンソール アプリケーションです。

## <a name="powershell-guides"></a>PowerShell ガイド

Azure Rights Management 管理者によって使用される、PowerShell コマンドレットはサービス アプリケーションの開発とテストにも役立ちます。 詳しくは、「[Azure Information Protection クライアントでの PowerShell の使用](../rms-client/client-admin-guide-powershell.md)」をご覧ください。

## <a name="user-applications"></a>ユーザー アプリケーション

ユーザー アプリケーションは、RMS SDK 2.1 または RMS SDK 4.2 を使用して作成することができます。
RMS SDK 4.2 は、人気のある OS (iOS および OSX、Android、Linux、Windows) 用の特定の.API をベースとした REST クライアントです。 2.1 バージョンは、Windows ベースのネイティブ アプリケーションの作成に使用されます。

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

[ ![ iOS/OSX セットアップ](../media/develop/ios-icon.png)](ios-sdk.md) 
 [ ![ Android セットアップ](../media/develop/android-icon.png)](android-sdk.md) 
 [ ![ Windows Phone セットアップ](../media/develop/windows-phone-icon.png)](windows-phone-apps.md) 
 [ ![ Windows サービスセットアップ](../media/develop/windows-icon.png)](install-the-rms-sdk.md) 
 [ ![ Linux セットアップ](../media/develop/linux-icon.png)](linux-setup.md)


## <a name="how-tos"></a>方法

次の各トピックでは、アプリケーションの実装に関する具体的なガイダンスを提供しています。 サービス アプリケーションは、RMS SDK 2.x. を使用して作成します。 ユーザー アプリケーションは、RMS SDK 4.x. を使用して作成します。 記事のリンクは、アプリケーションの種類、サービス、ユーザー別になっています。

### <a name="general"></a>全般

- [方法: ドキュメント追跡の有効化と取り消し (サービス)](tracking-content.md)
- [クライアントを展開する方法](../rms-client/client-deployment-notes.md)
- [サービス アプリを別のテナントにデプロイする方法](how-to-deploy-app.md)
- [方法: RMS サーバーをインストールして構成する (サービス)](how-to-install-and-configure-an-rms-server.md)
- [方法: ドキュメント追跡を使用する (ユーザー)](how-to-use-document-tracking.md)
- [Azure Information Protection で対称キーを更新する方法](how-to-renew-symmetric-key.md)

### <a name="security-and-authentication"></a>セキュリティと認証

- [Azure Active Directory ログインを使用するように app service アプリケーションを構成する方法](/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)
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

## <a name="introduction-and-datasheets"></a>概要とデータシート

[Azure Information Protection の概要](https://www.microsoft.com/cloud-platform/azure-information-protection)

## <a name="other-resources"></a>その他のリソース

- [セキュリティのベスト プラクティス ガイド](security-guidelines.md)
- [Azure Information Protection に関してよく寄せられる質問](../faqs.md)

### <a name="support-articles"></a>サポート技術情報

- [サポートされるファイル形式](supported-file-formats.md)
- [サポートされているプラットフォーム](supported-platforms.md)
- [Understanding usage restrictions (使用制限について)](understanding-usage-restrictions.md)

### <a name="message-protocol-and-file-formats"></a>メッセージのプロトコルとファイルの形式

- [クライアント サーバー間のプロトコル](/openspecs/windows_protocols/ms-rmpr/d8ed4b1e-e605-4668-b173-6312cba6977e)
- [権限が管理される電子メール オブジェクトのプロトコル](/openspecs/exchange_server_protocols/ms-oxormms/a121dda4-48f3-41f8-b12f-170f533038bb)
- [複合ファイル バイナリのファイル形式](/openspecs/windows_protocols/ms-cfb/53989ce4-7b05-4f8d-829b-d08d6148375b)

#### <a name="rights-managed-email-message"></a>権限が管理される電子メールのメッセージ

- [.MSG ファイル形式 (パート 1)](/archive/blogs/openspecification/msg-file-format-part-1)
- [.MSG ファイル形式 (パート 2)](/archive/blogs/openspecification/msg-file-format-rights-managed-email-message-part-2)

### <a name="api-reference"></a>API リファレンス

- [Windows API リファレンス](/previous-versions/windows/desktop/msipc/msipc-reference)
  - [Windows SDK エラー コード](/previous-versions/windows/desktop/msipc/error-codes)
- [Windows Phone および Windows ストアの API リファレンス](/previous-versions/windows/desktop/msipcthin2/winrt)
- [iOS および OSX の API リファレンス](/previous-versions/windows/desktop/msipcthin2/ios)
- [Android API リファレンス](/previous-versions/windows/desktop/msipcthin2/android)
- [Linux API リファレンス](https://azuread.github.io/rms-sdk-for-cpp/annotated.html)

### <a name="previous-versions"></a>以前のバージョン

- [AD RMS SDK](/previous-versions/windows/desktop/adrms_sdk/active-directory-rights-management-services-sdk-portal) は、RMS SDK の最初のバージョンです。
- [AD RMS スクリプト ツール](/previous-versions/windows/desktop/adrms_script/adrms-script-portal)は、AD RMS のインストールのための管理ツールです。

### <a name="see-also"></a>関連項目

- [開発者の用語](terms.md)
- [Azure Information Protection の用語 - ITPro](../terminology.md)