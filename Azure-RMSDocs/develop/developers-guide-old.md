---
title: "開発者ガイド |Azure RMS"
description: "開発者ツールの使用の概要, SDK, 追加のライブラリ, コード例。"
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 11/15/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a22e6bd0-8ce8-45b4-9a32-273126ab831e
audience: developer
ms.reviewer: kartikk
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 329dce4c8bb5a6de3ecb7bbd7e734b4acbf339c9
ms.openlocfilehash: bbf266512a80ece05253cbfab7b9ab40505f3f67


---

# <a name="developers-guide"></a>開発者ガイド

## <a name="overview"></a>概要 ##
このガイドでは、サポート対象のすべてのプラットフォーム用の豊富なツールおよびコード サンプル、Rights Management SDK、および PowerShell 管理ツールの概要を示します。

[**コード サンプルとツール**](#code-samples-and-tools) - サポート対象のすべてのオペレーティング システム (Android、iOS/OS X、Windows クライアントおよびスマートフォン) に対応しています。

[**PowerShell ガイダンス**](#powershell-guidance) - Rights Management の管理と一括保護の両方を対象としています。

[**ソフトウェア開発キット**](#software-development-kits) - Android や iOS などのモバイル デバイス オペレーティング システムをサポートするとともに、Windows クライアントを広範にサポートしています。


---

## <a name="code-samples-and-tools"></a>コード サンプルとツール

マイクロソフトが提供するこの一連の RMS コード サンプルと開発者サポート ツールは、すべてのサポートされているオペレーティング システム (Android、iOS/OS X、Windows Phone、および Windows Desktop) に対応しています。また、そのサポートされている SDK との互換性を維持するために定期的に更新されます。

### <a name="android"></a>Android

以下は、[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) および 4.x SDK 以降のバージョンでサポートされている Android で実行されます。

- 標準 UI ですぐに使用を開始してご自分のアプリで再利用できる GitHub の [UI ライブラリおよびサンプル アプリ](https://github.com/AzureAD/rms-sdk-ui-for-android)。
- RMS SDK に慣れるための重要な開発シナリオを表す Java による[ Android の使用シナリオ](https://msdn.microsoft.com/en-us/library/dn758246(v=vs.85).aspx)。 Microsoft によって保護されたファイル形式の使用例、カスタムの保護されたファイル形式の使用例、カスタムの UI コントロールの使用例などがあります。

### <a name="ios-os-x"></a>iOS / OS X

以下は、[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) および 4.x SDK 以降のバージョンでサポートされている iOS / OS X で実行されます。

- RMS SDK に慣れるための重要な開発シナリオを表す Objective C による[ iOS / OS X の使用シナリオ](https://msdn.microsoft.com/en-us/library/dn758307(v=vs.85).aspx)。 Microsoft によって保護されたファイル形式の使用例、カスタムの保護されたファイル形式の使用例、カスタムの UI コントロールの使用例などがあります。
- 標準 UI ですぐに使用を開始してご自分のアプリで再利用できる GitHub の [UI ライブラリおよびサンプル アプリ](https://github.com/AzureAD/rms-sdk-ui-for-ios)。 **iOS でのみ**サポートされています。

### <a name="windows-desktop"></a>Windows デスクトップ

以下は、[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) および 2.x SDK 以降のバージョンでサポートされている Windows デスクトップで実行されます。

- 「[Read PFILE protected PDF (PFILE で保護された PDF の読み取り)](https://blogs.msdn.microsoft.com/rms/2015/11/09/reading-a-pfile-protected-pdf/)」は、RMS 開発者のコーナー ブログで紹介されているシンプルなコード例です。MSIPC ファイル API を使用して、PFILE で保護された PDF ドキュメントを解読して開きます。
- [IpcManagedAPI](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcManagedAPI) は、管理対象のアプリケーションの RMS 対応を簡単にする RMS SDK 2.1 の .NET (c#) 表現です。
- [IPCNotepad](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcNotepad) は、RMS 対応のサンプル アプリケーションです。各 RMS 対応アプリケーションで制限付きコンテンツを保護および使用するときに実行する必要がある基本的な手順が分かります。
- [IpcDlp](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcDlpApp) は、RMS 対応のデータ漏えい保護 (DLP) サンプル アプリケーションです。DLP RMS 対応アプリケーションで制限付きコンテンツを保護および使用するために FILE API を使用して実行する必要がある基本的な手順が分かります。
- [IpcAzureApp](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcAzureApp) は、Azure Blob Storage のデータを保護するために Azure アプリケーションで RMS SDK を使用する方法をデモンストレーションするサンプルです。
- [RmsDocumentInspector](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/RmsDocumentInspector) は、コンテンツ ID やユーザー権限などの、RMS で保護されているファイルに関する情報を得られるツールです。
- [RmsFileWatcher](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/RmsFileWatcher) は、ファイル システムのディレクトリを監視し、すべての変更 (ファイルの追加や変更) に RMS 保護ポリシーを適用する Windows アプリケーションを構築する方法を示すサンプルです。

### <a name="windows-store-and-phone"></a>Windows ストアおよび Phone

- [Windows ストアの UI ライブラリ](https://github.com/AzureAD/rms-sdk-ui-for-windowsstore) - Windows ストア アプリケーション用の Microsoft RMS SDK v4.1 の UI ライブラリです。 このライブラリは省略可能です。開発者は Microsoft RMS SDK v4.1 を使用して独自の UI を構築する際に選択できます。

- [Windows Phone の UI ライブラリ](https://github.com/AzureAD/rms-sdk-ui-for-winphone) - Windows Phone アプリケーション用の Microsoft RMS SDK v4.1 の UI ライブラリです。 このライブラリは省略可能です。開発者は Microsoft RMS SDK v4.1 を使用して独自の UI を構築する際に選択できます。

- [サンプル アプリケーション](https://github.com/Azure-Samples/active-directory-dotnet-rms-windowsstore) - Windows ストア アプリケーション用 Microsoft RMS SDK v4.1 のサンプルには、プラットフォームの基本的なドキュメントの使用例が提供されています。

---

## <a name="powershell-guidance"></a>PowerShell ガイド
Rights Management の管理と一括保護の両方の PowerShell コマンドレットが用意されています。

[Azure Rights Management コマンドレット](https://msdn.microsoft.com/library/azure/dn629398.aspx)を使用すると、コマンド ラインから Azure RMS を管理できます。 PowerShell コマンドレットで自動化が可能になりますが、信頼性が高く反復的なプロセスをサポートしているので、管理者の作業も軽減されます。 また、一部の Azure RMS の高度な構成と操作には Azure PowerShell が必要です。

[RMS 保護コマンドレット](https://msdn.microsoft.com/library/azure/mt433195.aspx)は、Azure Information Protection の Azure Rights Management (Azure RMS) のデータ保護、または Active Directory Rights Management サービス (AD RMS) と併用できます。また、これらの Rights Management デプロイの他の PowerShell モジュールを補完できます。 これらの RMS 保護コマンドレットを使用して、任意のファイルの種類について複数のファイルの保護と保護解除を一括して実行できます。

---

## <a name="software-development-kits"></a>ソフトウェア開発キット


次の表で概説する 3 つの世代の RMS SDK をご利用いただけるようになりました。

| SDK | 説明 |
|------|---------|
| [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) | Android、iOS、Mac OS X、Windows Phone/RT、および Linux/C++ のデバイス アプリで Microsoft Rights Management サービスを使用して情報を保護できるようにするための、軽量な開発エクスペリエンスを提供する次世代のシンプルなツール セット。 |
| [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) | Windows デスクトップ アプリケーションの開発者およびサーバー ベースのソリューション プロバイダーのための強力な SDK オファリングです。その製品の著作権を管理できるようにします。|
|[AD RMS SDK](https://msdn.microsoft.com/library/cc530379.aspx)|**注** - AD RMS SDK は Msdrm.dll でクライアントによって公開される機能を活用し、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7、Windows Server 2008、および Windows Vista で使用できます。 今後のバージョンでは変更されるか、利用できなくなる場合もあります。 代わりに、Msdrm.dll でクライアントによって公開される機能を活用する、Microsoft Rights Management サービス SDK 2.1 を使用してください。|
|[AD RMS スクリプト API](https://msdn.microsoft.com/en-us/library/bb968797.aspx)| AD RMS インストールを管理するスクリプトを作成するために使用|



<!--HONumber=Nov16_HO3-->


