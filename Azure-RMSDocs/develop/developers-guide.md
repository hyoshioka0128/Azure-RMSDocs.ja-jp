---
title: "開発者ガイド |Azure RMS"
description: "開発者ツールの使用の概要, SDK, 追加のライブラリ, コード例。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a22e6bd0-8ce8-45b4-9a32-273126ab831e
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: 5010096d11524eb4f48fafcc6b2a5d85f48c8fe9


---

# 開発者ガイド

## 概要 ##
このガイドでは、Rights Management SDK のスイートと、サポートされているすべてのプラットフォームの増え続けているツール セットおよびコード サンプルについて説明します。 

## ソフトウェア開発キット ##
次の表で概説する 3 つの世代の RMS SDK をご利用いただけるようになりました。

| SDK | 説明 |
|------|---------|
| [RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) | Android、iOS、Mac OS X、Windows Phone/RT、および Linux/C++ のデバイス アプリで Microsoft Rights Management サービスを使用して情報を保護できるようにするための、軽量な開発エクスペリエンスを提供する次世代のシンプルなツール セット。 |
| [RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) | Windows デスクトップ アプリケーションの開発者およびサーバー ベースのソリューション プロバイダーのための強力な SDK オファリングです。その製品の著作権を管理できるようにします。|
|[AD RMS SDK](https://msdn.microsoft.com/library/cc530379(v=vs.85).aspx)|**注** - AD RMS SDK は Msdrm.dll でクライアントによって公開される機能を活用し、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows 7、Windows Server 2008、および Windows Vista で使用できます。 今後のバージョンでは変更されるか、利用できなくなる場合もあります。 代わりに、Msdrm.dll でクライアントによって公開される機能を活用する、Microsoft Rights Management サービス SDK 2.1 を使用してください。|
|[AD RMS スクリプト API](https://msdn.microsoft.com/en-us/library/bb968797(v=vs.85).aspx)| AD RMS インストールを管理するスクリプトを作成するために使用|

## コード サンプルとツール
マイクロソフトが提供するこの一連の RMS コード サンプルと開発者サポート ツールは、すべてのサポートされているオペレーティング システム (Android、iOS/OS X、Windows Phone、および Windows Desktop) に対応しています。また、そのサポートされている SDK との互換性を維持するために定期的に更新されます。

### Android

以下は、[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) および 4.x SDK 以降のバージョンでサポートされている Android で実行されます。

- 標準 UI ですぐに使用を開始してご自分のアプリで再利用できる GitHub の [UI ライブラリおよびサンプル アプリ](https://github.com/AzureAD/rms-sdk-ui-for-android)。
- RMS SDK に慣れるための重要な開発シナリオを表す Java による[ Android の使用シナリオ](https://msdn.microsoft.com/en-us/library/dn758246(v=vs.85).aspx)。 Microsoft によって保護されたファイル形式の使用例、カスタムの保護されたファイル形式の使用例、カスタムの UI コントロールの使用例などがあります。

### iOS / OS X

以下は、[RMS SDK 4.2](active-directory-rights-management-services-multi-platform-thin-client-sdk-portal.md) および 4.x SDK 以降のバージョンでサポートされている iOS / OS X で実行されます。

- RMS SDK に慣れるための重要な開発シナリオを表す Objective C による[ iOS / OS X の使用シナリオ](https://msdn.microsoft.com/en-us/library/dn758307(v=vs.85).aspx)。 Microsoft によって保護されたファイル形式の使用例、カスタムの保護されたファイル形式の使用例、カスタムの UI コントロールの使用例などがあります。
- 標準 UI ですぐに使用を開始してご自分のアプリで再利用できる GitHub の [UI ライブラリおよびサンプル アプリ](https://github.com/AzureAD/rms-sdk-ui-for-ios)。 **iOS でのみ**サポートされています。

### Windows デスクトップ

以下は、[RMS SDK 2.1](microsoft-information-protection-and-control-client-portal.md) および 2.x SDK 以降のバージョンでサポートされている Windows デスクトップで実行されます。

- 「[Read PFILE protected PDF (PFILE で保護された PDF の読み取り)](https://blogs.msdn.microsoft.com/rms/2015/11/09/reading-a-pfile-protected-pdf/)」は、RMS 開発者のコーナー ブログで紹介されているシンプルなコード例です。MSIPC ファイル API を使用して、PFILE で保護された PDF ドキュメントを解読して開きます。
- [IpcManagedAPI](https://github.com/Azure-Samples/active-directory-dotnet-rms) は、管理対象のアプリケーションの RMS 対応を簡単にする RMS SDK 2.1 の .NET (c#) 表現です。
- [IPCNotepad](https://code.msdn.microsoft.com/ipcnotepad-sample-f67dae80) は、RMS 対応のサンプル アプリケーションです。各 RMS 対応アプリケーションで制限付きコンテンツを保護および使用するときに実行する必要がある基本的な手順が分かります。
- [IpcDlp](https://github.com/Azure-Samples/active-directory-dotnet-rms) は、RMS 対応のデータ漏えい保護 (DLP) サンプル アプリケーションです。DLP RMS 対応アプリケーションで制限付きコンテンツを保護および使用するために FILE API を使用して実行する必要がある基本的な手順が分かります。
- [IpcAzureApp](https://github.com/Azure-Samples/active-directory-dotnet-rms) は、Azure Blob Storage のデータを保護するために Azure アプリケーションで RMS SDK を使用する方法をデモンストレーションするサンプルです。
- [RmsDocumentInspector](https://github.com/Azure-Samples/active-directory-dotnet-rms) は、コンテンツ ID やユーザー権限などの、RMS で保護されているファイルに関する情報を得られるツールです。
- [RmsFileWatcher](https://github.com/Azure-Samples/active-directory-dotnet-rms) は、ファイル システムのディレクトリを監視し、すべての変更 (ファイルの追加や変更) に RMS 保護ポリシーを適用する Windows アプリケーションを構築する方法を示すサンプルです。

### Windows ストアおよび Phone

- [Windows ストアの UI ライブラリ](https://github.com/AzureAD/rms-sdk-ui-for-windowsstore) - Windows ストア アプリケーション用の Microsoft RMS SDK v4.1 の UI ライブラリです。 このライブラリは省略可能です。開発者は Microsoft RMS SDK v4.1 を使用して独自の UI を構築する際に選択できます。

- [Windows Phone の UI ライブラリ](https://github.com/AzureAD/rms-sdk-ui-for-winphone) - Windows Phone アプリケーション用の Microsoft RMS SDK v4.1 の UI ライブラリです。 このライブラリは省略可能です。開発者は Microsoft RMS SDK v4.1 を使用して独自の UI を構築する際に選択できます。

- [サンプル アプリケーション](https://github.com/Azure-Samples/active-directory-dotnet-rms-windowsstore) - Windows ストア アプリケーション用 Microsoft RMS SDK v4.1 のサンプルには、プラットフォームの基本的なドキュメントの使用例が提供されています。



<!--HONumber=Sep16_HO5-->


