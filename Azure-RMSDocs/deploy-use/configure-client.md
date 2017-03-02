---
title: "Azure Information Protection クライアント&colon; インストールと構成"
description: "Windows コンピューターとモバイル デバイスに Azure Information Protection クライアントをデプロイする場合の管理者向けの情報です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b1a19ae7-db26-40da-9e21-6620af3d0b02
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 39d2fb244be91d7fc655efbdda24e4e268ac1329
ms.lasthandoff: 02/24/2017


---

# <a name="azure-information-protection-client-installation-and-configuration-for-clients"></a>Azure Information Protection クライアント: クライアントのインストールと構成

>*適用対象: Azure Information Protection、Office 365*

Azure Rights Management サービスと Azure Information Protection サービスに対して認証を行うには、Office 2010 を実行するコンピューターに Azure Information Protection クライアント (または Rights Management 共有アプリケーション) が必要です。 このクライアントは、Azure Rights Management サービスと Azure Information Protection をサポートするすべての Windows コンピューターと iOS および Android デバイスにも推奨されます。 

Azure Information Protection クライアントと Office アプリケーションを統合するには、Office アドインをインストールします。統合すると、ユーザーはドキュメントと電子メールのラベル付けと保護を Office リボンから簡単に直接実行できるようになります。 また、このクライアントには、Azure Rights Management サービスがネイティブでサポートしていないファイルの種類にラベルと保護を適用する機能、保護されたファイルのビューアー、保護されたファイルの追跡および取り消しをユーザーが行うことができるドキュメント追跡サイトもあります。

## <a name="the-azure-information-protection-client-for-windows-installation-and-configuration"></a>Windows 用 Azure Information Protection クライアント: インストールと構成
企業での Windows 用クライアントのインストールと構成については、「[Azure Information Protection administrator guide](../rms-client/client-admin-guide.md)」(Azure Information Protection 管理者ガイド) を参照してください。

> [!TIP]
> 1 台のコンピューターで Azure Information Protection クライアントをインストールおよびテストする簡単な方法については、「[Azure Information Protection ユーザー ガイド](../rms-client/client-user-guide.md)」の「[Azure Information Protection クライアントをダウンロードしてインストールする](../rms-client/install-client-app.md)」を参照してください。

## <a name="the-azure-information-protection-client-for-ios-and-android-installation-and-management"></a>iOS および Android 用 Azure Information Protection クライアント: インストールと管理
これらの一般的なモバイル プラットフォーム用の Azure Information Protection クライアントをインストールするには、[Microsoft Azure Information Protection ページ](http://go.microsoft.com/fwlink/?LinkId=303970)のリンクを使用して関連するアプリをダウンロードできます。 構成は必要ありません。

> [!NOTE]
> Mac コンピューターと Windows Phone の場合、このページのリンクでモバイル デバイス用の RMS 共有アプリをダウンロードします。 現在のところ、これらのデバイスは Azure Information Protection クライアントをサポートしていません。

**Microsoft Intune を所有している場合**: Azure Information Protection アプリには Microsoft Intune App Software Development Kit が含まれているため、Intune で iOS デバイスや Android デバイスを登録していると、これらのデバイス用の Azure Information Protection ビューアーをデプロイおよび管理できます。 詳細については、Intune のドキュメントの「[Configure and deploy mobile application management policies in the Microsoft Intune console (Microsoft Intune コンソールでモバイル アプリケーション管理ポリシーを構成およびデプロイする)](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console)」を参照してください。 手順 2. として、手順に従ってポリシー管理型アプリを発行します。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


