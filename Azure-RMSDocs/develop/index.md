---
title: "RMS 開発者ガイド |Azure RMS"
description: "Rights Management SDK の&3; つの世代をご利用いただけるようになりました。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: azure
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0510ead4-2fe7-4269-885b-fe16bcc69888
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: c408d7a8f068e2de6616534a58161a86482a2a9c
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="rms-developers-guide"></a>RMS 開発者ガイド

## <a name="overview"></a>概要 ##
Rights Management SDK は、**Microsoft Rights Management SDK 4.2** (Android、iOS/OS X、Windows デバイスと Linux 用)、**Microsoft Rights Management SDK 2.1** (Windows デスクトップ クライアント用)、**AD RMS SDK** (置き換えられました) の 3 つの世代をご利用いただけるようになりました。

## <a name="software-development-kits"></a>ソフトウェア開発キット ##
| SDK | 説明 |
|------|---------|
| [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) | Android、iOS、Mac OS X、Windows Phone/RT、および Linux/C++ のデバイス アプリで Microsoft Rights Management サービスを使用して情報を保護できるようにするための、軽量な開発エクスペリエンスを提供する次世代のシンプルなツール セット。 |
| [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) | Windows デスクトップ アプリケーションの開発者およびサーバー ベースのソリューション プロバイダーのための強力な SDK オファリングです。その製品の著作権を管理できるようにします。|
|[AD RMS SDK]()|**注** - AD RMS SDK は Msdrm.dll でクライアントによって公開される機能を活用し、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7、Windows Server 2008、および Windows Vista で使用できます。 今後のバージョンでは変更されるか、利用できなくなる場合もあります。 代わりに、Msdrm.dll でクライアントによって公開される機能を活用する、Microsoft Rights Management サービス SDK 2.1 を使用してください。|
|[AD RMS スクリプト API]()| AD RMS インストールを管理するスクリプトを作成するために使用|

## <a name="code-samples-and-tools"></a>コード サンプルとツール ##
マイクロソフトが提供するこの一連の RMS コード サンプルと開発者サポート ツールは、すべてのサポートされているオペレーティング システム (Android、iOS/OS X、Windows Phone、および Windows Desktop) に対応しています。また、そのサポートされている SDK との互換性を維持するために定期的に更新されます。

| 項目 | オペレーティング システム | サポートされている SDK バージョン | 説明 |
|------|------------------|------------------------|-------------|
| [PFILE で保護された PDF の読み取り](https://blogs.msdn.microsoft.com/rms/2015/11/09/reading-a-pfile-protected-pdf/) | Windows デスクトップ| [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) および 2.x SDK 以降のバージョン | 「**Read PFILE protected PDF (PFILE で保護された PDF の読み取り)**」は、RMS 開発者のコーナー ブログで紹介されているシンプルなコード例です。MSIPC ファイル API を使用して、PFILE で保護された PDF ドキュメントを解読して開きます。|
| [IpcManagedAPI](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Windows デスクトップ | [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) および 2.x SDK 以降のバージョン | **IpcManagedAPI** は、管理対象のアプリケーションの RMS 対応を簡単にする RMS SDK 2.1 の .NET (c#) 表現です。|
| [IPCNotepad](https://code.msdn.microsoft.com/ipcnotepad-sample-f67dae80) | Windows デスクトップ | [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) および 2.x SDK 以降のバージョン| **IPCNotepad** は、RMS 対応のサンプル アプリケーションです。各 RMS 対応アプリケーションで制限付きコンテンツを保護および使用するときに実行する必要がある基本的な手順が分かります。|
| [IpcDlp](https://github.com/Azure-Samples/active-directory-dotnet-rms)|Windows デスクトップ|[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) および 2.x SDK 以降のバージョン|**IpcDlp** は、RMS 対応のデータ漏えい保護 (DLP) サンプル アプリケーションです。DLP RMS 対応アプリケーションで制限付きコンテンツを保護および使用するために FILE API を使用して実行する必要がある基本的な手順が分かります。|
| [IpcAzureApp](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Windows デスクトップ|[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) および 2.x SDK 以降のバージョン|**IpcAzureApp** は、Azure Blob Storage のデータを保護するために Azure アプリケーションで RMS SDK を使用する方法をデモンストレーションするサンプルです。|
| [RmsDocumentInspector](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Windows デスクトップ|[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) および 2.x SDK 以降のバージョン|**RmsDocumentInspector** は、コンテンツ ID やユーザー権限などの、RMS で保護されているファイルに関する情報を得られるツールです。|
| [RmsFileWatcher](https://github.com/Azure-Samples/active-directory-dotnet-rms) | Windows デスクトップ|[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) および 2.x SDK 以降のバージョン|**RmsFileWatcher** は、ファイル システムのディレクトリを監視し、すべての変更 (ファイルの追加や変更) に RMS 保護ポリシーを適用する Windows アプリケーションを構築する方法を示すサンプルです。|
| [iOS/OS X の使用シナリオ](https://msdn.microsoft.com/library/dn758307(v=vs.85).aspx) |iOS / OS X|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) および 4.x SDK 以降のバージョン|RMS SDK に慣れるための重要な開発シナリオを表す **Objective C** のコード例です。 Microsoft によって保護されたファイル形式の使用例、カスタムの保護されたファイル形式の使用例、カスタムの UI コントロールの使用例などがあります。|
| [UI ライブラリおよびサンプル アプリ](https://github.com/AzureAD/rms-sdk-ui-for-ios) |iOS|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) および 4.x SDK 以降のバージョン|GitHub の **UI ライブラリおよび iOS 用のサンプル アプリ**です。標準 UI をすぐに使いはじめてご自分のアプリで再利用できます。|
| [UI ライブラリおよびサンプル アプリ](https://github.com/AzureAD/rms-sdk-ui-for-android) |Android|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) および 4.x SDK 以降のバージョン|GitHub の **UI ライブラリおよび Android 用のサンプル アプリ**です。標準 UI をすぐに使いはじめてご自分のアプリで再利用できます。|
| [Android の使用シナリオ](https://msdn.microsoft.com/en-us/library/dn758246(v=vs.85).aspx) |Android|[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) および 4.x SDK 以降のバージョン|RMS SDK に慣れるための重要な開発シナリオを表す **Java のコード例**です。 Microsoft によって保護されたファイル形式の使用例、カスタムの保護されたファイル形式の使用例、カスタムの UI コントロールの使用例などがあります。|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]