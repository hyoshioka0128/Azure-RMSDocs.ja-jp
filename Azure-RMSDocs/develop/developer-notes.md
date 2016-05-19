---
# required metadata

title: 開発者向け注意事項 | Azure RMS
description: このトピックでは、いくつかの重要な開発シナリオの具体的なガイダンスについて説明します。 
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 65c2f3d1-0852-41fa-a95a-53dcec787680

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿# 開発者向け注意事項

このセクションでは、いくつかの重要な開発シナリオの具体的なガイダンスについて説明します。 このセクションのシナリオは Rights Management サービス SDK 2.1 のこのリリースに固有のシナリオであり、将来のリリースで変更される可能性があります。

- [明示的な所有者権限の追加](add-explicit-owner-rights.md) - アプリケーションでは、最初からライセンスを作成するときに、&quot;所有者&quot; 権限を明示的に追加する必要があります ([IpcCreateLicenseFromScratch](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch))。
- [Common error conditions and solutions (一般的なエラー状況とソリューション)](common-error-conditions-and-solutions.md) - RMS SDK 2.1 開発者ツールを使用するときに発生する可能性のある最も一般的なエラー メッセージ。
- [Enabling email notification (電子メール通知の有効化)](how-to-enable-email-notification.md) - 電子メール通知を使用すると、保護されたコンテンツがアクセスされたときに、そのコンテンツの所有者に通知することができます。
- [File API configuration (File API の構成)](file-api-configuration.md) - File API の動作は、レジストリの設定を使用して構成できます。
- [IPCHelloWorld - an example application (IPCHelloWorld - サンプル アプリケーション)](how-to-build-your-first-application.md) - このトピックには、権限保護に対応するサンプル アプリケーションを作成する手順が含まれています。
- [API のセキュリティ モードの設定](setting-the-api-security-mode-api-mode.md) - [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) 関数を使用して、File API アプリケーションをどのセキュリティ モードで実行するかを選択できます。
- [サポートされるファイル形式](supported-file-formats.md) - File API は、ネイティブ形式と Pfile 形式をサポートしています。
- [コンテンツの追跡](tracking-content.md) - このトピックでは、RMS SDK 2.1 で保護されたコンテンツのドキュメント追跡を実装するための基本的なガイダンスを提供します。
- [Working with encryption (暗号化の操作)](working-with-encryption.md) - このトピックでは、Microsoft の暗号化パッケージとその使い方を示すいくつかのコード スニペットを紹介します。

 

## 関連項目 ##
* [概要](ad-rms-overview.md)
* [使用方法](how-to-use-msipc.md)
 

 


<!--HONumber=Apr16_HO3-->


