---
title: Azure Information Protection SDK 2.1 開発者ガイド |Microsoft Docs
description: Rights Management Services SDK 2.1 を使用した開発に関するいくつかの重要な開発シナリオと一般情報に関するガイダンスを紹介します。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 01/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5A9F04FD-0FCD-482F-8671-36FE93B783B0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev, has-adal-ref
ms.openlocfilehash: 76516086a4d2963dfa6b3aa293d0c49a28285c09
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "95570694"
---
# <a name="rights-management-services-sdk-21-developer-guidance"></a>Rights Management Services SDK 2.1 開発者ガイド

このセクションでは、いくつかの重要な開発シナリオについて説明し、この SDK による開発に関する基本情報を提供します。 このセクションのシナリオは Rights Management サービス SDK 2.1 のこのリリースに固有のシナリオであり、将来のリリースで変更される可能性があります。
- [方法: ADAL 認証の使用](how-to-use-adal-authentication.md) - Azure Active Directory Authentication Library (ADAL) を利用し、アプリに対して Azure RMS で認証を実行する。
- [方法: 明示的な所有者権限を追加](add-explicit-owner-rights.md) する-アプリケーションでは、最初からライセンスを作成するときに、"所有者" 権限を明示的に追加する必要があります ([Ipccreatelicensefromscratch](/previous-versions/windows/desktop/msipc/ipccreatelicensefromscratch))。
- [方法: 権限保護対応アプリケーションのデバッグ](debugging-applications-that-use-ad-rms.md) - このトピックでは、アプリケーションをデバッグし、Windows イベント ログを使用する方法について説明します。
- [方法: 顧客のテナントへのアプリのデプロイ](how-to-deploy-app.md) - Azure AD の開発テナントから Azure AD の運用テナントにアプリをデプロイする手順の概要を説明します。
- [方法: ドキュメント追跡の有効化と取り消し](tracking-content.md) - このトピックでは、コンテンツのドキュメント追跡機能を導入する方法について、その基礎を説明し、また、メタデータ更新のサンプル コードとアプリの **[使用の追跡]** ボタンを作成するためのサンプルコードを紹介します。
- [方法: 電子メール通知の有効化](how-to-enable-email-notification.md) - 電子メール通知を使用すると、保護されたコンテンツがアクセスされたときに、そのコンテンツの所有者に通知することができます。
- [方法: クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md) - このトピックでは、Azure Rights Management を使用するようにサービス アプリケーションをセットアップする手順について説明します。
- [方法: RMS サーバーのインストールと構成](how-to-install-and-configure-an-rms-server.md) - このトピックでは、権限保護対応アプリケーションをテストするために、RMS サーバーまたは Azure RMS に接続する手順について説明します。
- [方法: API セキュリティ モードの設定](setting-the-api-security-mode-api-mode.md) - [IpcSetGlobalProperty](/previous-versions/windows/desktop/msipc/ipcsetglobalproperty) 関数を使用して、File API アプリケーションをどのセキュリティ モードで実行するかを選択できます。
- [方法: 暗号化設定の操作](working-with-encryption.md) - このトピックでは、Microsoft の暗号化パッケージとその使い方を示すいくつかのコード スニペットを紹介します。
- 「[Application types (アプリケーションの種類)](application-types.md)」- このトピックでは、権限保護対応として作成できるアプリケーションの種類について説明します。
- [File API configuration (File API の構成)](file-api-configuration.md) - File API の動作は、レジストリの設定を使用して構成できます。
- [Security guidelines (セキュリティのガイドライン)](security-guidelines.md) - アプリケーション開発者に、AIP エコシステム内で有効な位置付けと方向を示しています。
- [サポートされるファイル形式](supported-file-formats.md) - File API は、ネイティブ形式と Pfile 形式をサポートしています。
- [サポートされているプラットフォーム](supported-platforms.md): このトピックでは、RMS SDK 2.1 でサポートされているクライアントとサーバー プラットフォームを識別します。
- [使用制限について](understanding-usage-restrictions.md) - すべての RMS 対応アプリケーションは、このトピックに記載されている定数で定義されている使用制限を適用する必要があります。

 
## <a name="related-topics"></a>関連トピック
* [概要](ad-rms-overview.md)