---
title: "Rights Management 共有アプリケーション&colon; クライアントでのインストールと構成 | Azure Information Protection"
description: "Rights Management (RMS) 共有アプリケーションの Windows コンピューターおよびモバイルデバイスへのデプロイに関する管理者向けの情報です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b9af5dc3-73d4-4147-b7ef-f6803b0d5216
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: f96641355da46eee85a828a6e5e417282883bac7


---

# <a name="rights-management-sharing-application-installation-and-configuration-for-clients"></a>Rights Management 共有アプリケーション: クライアントでのインストールと構成

>*適用対象: Azure Information Protection、Office 365*

Rights Management (RMS) 共有アプリケーションは、Azure Rights Management サービスと Office 2010 を使用するクライアント コンピューターに必要です。また、Azure Information Protection からの Azure Rights Management サービスをサポートするすべてのコンピューターとモバイル デバイスに推奨されます。 RMS 共有アプリケーションにより Office アドインがインストールされて Office アプリケーションが統合されるので、ユーザーは簡単にファイルや電子メールをリボンから直接保護できます。 RMS 共有アプリケーションでは、Azure Rights Management サービスがネイティブでサポートしていないファイルに汎用的な保護を適用することで、すべてのファイルの種類を保護することもできます。また、ドキュメント追跡サイトにより、ユーザーが保護したドキュメントを追跡したり、取り消したりすることもできます。

## <a name="the-rms-sharing-application-for-windows-installation-and-configuration"></a>Windows 用 RMS 共有アプリケーション: インストールと構成
エンタープライズ デプロイで Windows 用 RMS 共有アプリケーションをインストールして構成する場合は、「[Rights Management 共有アプリケーション管理者ガイド](../rms-client/sharing-app-admin-guide.md)」を参照してください。

> [!TIP]
> 単一のコンピューターで RMS 共有アプリケーションを簡単にインストールしてテストしたい場合は、「[Rights Management 共有アプリケーション ユーザー ガイド](../rms-client/sharing-app-user-guide.md)」の「[Rights Management 共有アプリケーションをダウンロードしてインストールする](../rms-client/install-sharing-app.md)」を参照してください。

## <a name="the-rms-sharing-application-for-mobile-platforms-installation-and-management"></a>モバイル プラットフォーム用 RMS 共有アプリケーション: インストールと管理
モバイル プラットフォームで RMS 共有アプリケーションをインストールするには、 [Microsoft Rights Management ページ](http://go.microsoft.com/fwlink/?LinkId=303970)のリンクを使用して該当するアプリをダウンロードできます。 Azure Rights Management サービスとこのアプリを使用するには、構成は必要ありません。

> [!NOTE]
> iOS 用および Android 用の RMS 共有アプリケーションは、Azure Information Protection アプリに置き換わっています。

**Microsoft Intune を所有している場合**: Azure Information Protection アプリには Microsoft Intune App Software Development Kit が含まれているため、Intune で iOS デバイスや Android デバイスを登録していると、これらのデバイス用の Azure Information Protection アプリをデプロイおよび管理できます。 詳細については、Intune のドキュメントの「[Configure and deploy mobile application management policies in the Microsoft Intune console (Microsoft Intune コンソールでモバイル アプリケーション管理ポリシーを構成およびデプロイする)](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)」を参照してください。 手順 2. として、手順に従ってポリシー管理型アプリを発行します。






<!--HONumber=Nov16_HO2-->


