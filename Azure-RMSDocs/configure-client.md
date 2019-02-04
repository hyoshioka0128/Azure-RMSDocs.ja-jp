---
title: Azure Information Protection クライアント&colon; インストールと構成
description: Windows コンピューターとモバイル デバイスに Azure Information Protection クライアントをデプロイする場合の管理者向けの情報です。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/17/2019
ms.topic: conceptual
ms.service: information-protection
ms.assetid: b1a19ae7-db26-40da-9e21-6620af3d0b02
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 10fc4c158cd4669b67c28e4968b0a3c4e7b889ad
ms.sourcegitcommit: b1e08bc29d50187532f00dc215ab331e0a7dbebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2019
ms.locfileid: "55146844"
---
# <a name="azure-information-protection-client-installation-and-configuration-for-clients"></a>Azure Information Protection クライアント:クライアントでのインストールと構成

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Rights Management サービスと Azure Information Protection サービスに対して認証を行うには、Office 2010 を実行するコンピューターに Azure Information Protection クライアント (または Rights Management 共有アプリケーション) が必要です。 このクライアントは、Azure Rights Management サービスと Azure Information Protection をサポートするすべての Windows コンピューターと iOS および Android デバイスにも推奨されます。 

Azure Information Protection クライアントと Office アプリケーションを統合するには、Office アドインをインストールします。統合すると、ユーザーはドキュメントと電子メールのラベル付けと保護を Office リボンから簡単に直接実行できるようになります。 また、このクライアントには、Azure Rights Management サービスがネイティブでサポートしていないファイルの種類にラベルと保護を適用する機能、保護されたファイルのビューアー、保護されたファイルの追跡および取り消しをユーザーが行うことができるドキュメント追跡サイトもあります。

## <a name="the-azure-information-protection-client-for-windows-installation-and-configuration"></a>Windows 用 Azure Information Protection クライアント: インストールと構成
企業での Windows 用クライアントのインストールと構成については、「[Azure Information Protection administrator guide](./rms-client/client-admin-guide.md)」(Azure Information Protection 管理者ガイド) を参照してください。

> [!TIP]
> 1 台のコンピューターで Azure Information Protection クライアントをインストールおよびテストする簡単な方法については、「[Azure Information Protection ユーザー ガイド](./rms-client/client-user-guide.md)」の「[Azure Information Protection クライアントをダウンロードしてインストールする](./rms-client/install-client-app.md)」を参照してください。

## <a name="the-azure-information-protection-client-for-ios-and-android-installation-and-management"></a>iOS 用と Android 用の Azure Information Protection クライアント: インストールと管理
これらの一般的なモバイル プラットフォーム用の Azure Information Protection クライアントをインストールするには、[Microsoft Azure Information Protection ページ](https://go.microsoft.com/fwlink/?LinkId=303970)のリンクを使用して関連するアプリをダウンロードできます。 構成は必要ありません。

> [!NOTE]
> Mac コンピューターの場合、このページのリンクでモバイル デバイス用の RMS 共有アプリをダウンロードします。 これらのコンピューターは Azure Information Protection クライアントをサポートしていません。

**Microsoft Intune を所有している場合**: Azure Information Protection アプリは Microsoft Intune App Software Development Kit を使用して構築されているため、Intune で iOS デバイスや Android デバイスを登録していると、これらのデバイス用の Azure Information Protection アプリをデプロイおよび管理できます。

- アプリをデプロイするには、[Azure Information Protection アプリを Intune に追加](/intune/apps-add)し、[ユーザーに割り当て](/intune/apps-deploy)ます。

- アプリを管理するには、Intune の[アプリ保護ポリシー](/intune/app-protection-policies)を使用します。

## <a name="next-steps"></a>次の手順

Azure Information Protection クライアントをインストールして構成したら、ドキュメントおよび電子メールの保護に使用できるさまざまな使用権限がクライアントでどのように解釈されるかを詳しく学習する必要があります。 詳細については、「[Azure Rights Management の使用権限を構成する](configure-usage-rights.md)」を参照してください。
