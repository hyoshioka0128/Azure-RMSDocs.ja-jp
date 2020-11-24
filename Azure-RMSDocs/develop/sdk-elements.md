---
title: 開発環境ファイル | Azure RMS
description: このトピックでは、開発環境のファイルと、コンピューター上での相対的なインストール場所について説明します。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: B57AC6F3-733C-42A8-AF83-0E15FBF27C99
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 0b2e741a1ad50c28248bc36fd3895971d429d5f5
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "95570007"
---
# <a name="development-environment-files"></a>開発環境ファイル

このトピックでは、開発環境のファイルと、コンピューター上での相対的なインストール場所について説明します。

Rights Management サービス SDK 2.1 には、次のファイルが含まれています。これらのファイルは、コンピューター上の既定の場所または指定された場所 (%MsipcSDKDir%) にインストールされます。

|ファイル|Path|説明|
|----|----|-----------|
|ReadMe.htm| \ | RMS ヘルプおよび[リリース ノート](release-notes-rtm.md)へのリンクが含まれています。|
|Isvtier5appsigningprivkey.dat|\bin|RMS 対応アプリケーションの開発時に使用するマニフェストを生成するための秘密キーが含まれています。|
|Isvtier5appsigningpubkey.dat|\bin|RMS 対応アプリケーションの開発時に使用するマニフェストを生成するための公開キーが含まれています。|
|Isvtier5appsignsdk_client.xml|\bin|RMS 対応アプリケーションの開発時に使用するマニフェストを生成するために使用します。|
|YourAppName.isv.mcf|\bin|RMS 対応アプリケーションの開発時にマニフェストを生成するために使用できるボイラープレート マニフェスト構成ファイル。|
|Ipcsecproc_isv.dll|\bin\x86|ISV 階層で動作するときに Active Directory Rights Management サービス クライアント 2.1 によって内部的に使用される、x86 アプリケーション用の DLL。|
|Ipcsecproc_ssp_isv.dll|\bin\x86|ISV 階層で動作するときに AD RMS 2.1 によって内部的に使用される、x86 アプリケーション用の DLL。|
|Ipcsecproc_isv.dll|\bin\x64|ISV 階層で動作するときに AD RMS クライアント 2.1 によって内部的に使用される、x64 アプリケーション用の DLL。|
|Ipcsecproc_ssp_isv.dll|\bin\x64|ISV 階層で動作するときに AD RMS クライアント 2.1 によって内部的に使用される、x64 アプリケーション用の DLL。|
|Msipc.h|\inc|RMS SDK 2.1 用のメインのインクルード ファイル。|
|Ipcprot.h|\inc|RMS SDK 2.1 によってエクスポートされたパブリック インターフェイスが含まれています。|
|Ipcbase.h|\inc|RMS SDK 2.1 によってエクスポートされた基本的な型およびヘルパー関数が含まれています。|
|Ipcerror.h|\inc|RMS SDK 2.1 によってエクスポートされたパブリック エラー コードが含まれています。|
|Ipcfile.h|\inc|RMS SDK 2.1 によってエクスポートされた File API インターフェイスが含まれています。|
|Msipc.lib|\lib|RMS SDK 2.1 を使用して x86 アプリケーションを構築するときにリンクするライブラリ。|
|Msipc_s.lib|\lib|x86 アプリケーション用の [IpcInitialize](/previous-versions/windows/desktop/msipc/ipcinitialize) のエントリ ポイントを提供します。|
|Msipc.lib|\lib\x64|RMS SDK 2.1 を使用して x64 アプリケーションを構築するときにリンクするライブラリ。|
|Msipc_s.lib|\lib\x64|x64 アプリケーション用の [IpcInitialize](/previous-versions/windows/desktop/msipc/ipcinitialize) のエントリ ポイントを提供します。|
|Genmanifest.exe|\tools|RMS 対応アプリケーションの開発時に使用するマニフェストを生成します。|