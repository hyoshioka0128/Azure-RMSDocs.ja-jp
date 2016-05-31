---
# required metadata

title: Rights Management 共有アプリケーション&colon; クライアントでのインストールと構成 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: b9af5dc3-73d4-4147-b7ef-f6803b0d5216

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Rights Management 共有アプリケーション: クライアントでのインストールと構成

*適用対象: Azure Rights Management、Office 365*

クライアント コンピューターの Office 2010 で Azure RMS を使用するには、Rights Management (RMS) 共有アプリケーションが必要です。このアプリケーションは Azure RMS をサポートするすべてのコンピューターおよびモバイル デバイスに推奨されます。 RMS 共有アプリケーションにより Office アドインがインストールされて Office アプリケーションが統合されるので、ユーザーは簡単にファイルや電子メールをリボンから直接保護できます。 RMS 共有アプリケーションでは、Azure Rights Management がネイティブでサポートしていないファイルに汎用的な保護を適用することで、すべてのファイルの種類を保護することもできます。また、ドキュメント追跡サイトにより、ユーザーが保護したドキュメントを追跡したり、取り消したりすることもできます。

## Windows 用 RMS 共有アプリケーション: インストールと構成
エンタープライズ デプロイで Windows 用 RMS 共有アプリケーションをインストールして構成する場合は、「[Rights Management 共有アプリケーション管理者ガイド](../rms-client/sharing-app-admin-guide.md)」を参照してください。.

> [!TIP]
> 単一のコンピューターで RMS 共有アプリケーションを簡単にインストールしてテストしたい場合は、「[Rights Management 共有アプリケーション ユーザー ガイド](../rms-client/sharing-app-user-guide.md)」の「[Rights Management 共有アプリケーションをダウンロードしてインストールする](../rms-client/install-sharing-app.md)」を参照してください。.

## モバイル プラットフォーム用 RMS 共有アプリケーション: インストールと管理
モバイル プラットフォームで RMS 共有アプリケーションをインストールするには、 [Microsoft Rights Management ページ](http://go.microsoft.com/fwlink/?LinkId=303970)のリンクを使用して該当するアプリをダウンロードできます。 このアプリで Azure RMS を使用するために構成は必要ありません。

**Microsoft Intune がある場合**: RMS 共有アプリには Microsoft Intune アプリ ソフトウェア開発キットが含まれているため、次のオプションがあります。

-   Intune で登録されているデバイスについては、iOS および Android を実行するデバイス用に RMS 共有アプリをデプロイし、管理できます。 詳細については、Intune のドキュメントの「[Configure and deploy mobile application management policies in the Microsoft Intune console (Microsoft Intune コンソールでモバイル アプリケーション管理ポリシーを構成およびデプロイする)](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)」を参照してください。 手順 2. として、手順に従ってポリシー管理型アプリを発行します。

-   Intune で登録されていないデバイスについては、Android を実行するデバイス用に RMS 共有アプリをデプロイし、管理できます。 詳細については、「[Microsoft Intune でのモバイル アプリ管理ポリシーの作成および展開](/intune/deploy-use/create-and-deploy-mobile-app-management-policies-with-microsoft-intune)」を参照してください。.



<!--HONumber=Apr16_HO4-->


