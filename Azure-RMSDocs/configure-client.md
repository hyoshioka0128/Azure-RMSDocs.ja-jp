---
title: Azure Information Protection クライアント - インストールと構成
description: Windows コンピューターとモバイルデバイスに Azure Information Protection クライアントを展開する方法に関する管理者向けの情報。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b1a19ae7-db26-40da-9e21-6620af3d0b02
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: f91052c45a3246d3ed63ab9945e09a3dd7ab3789
ms.sourcegitcommit: c20c7f114ae58ed6966785d8772d0bf1c1d39cce
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2019
ms.locfileid: "74935165"
---
# <a name="azure-information-protection-client-installation-and-configuration-for-clients"></a>Azure Information Protection クライアント: クライアントのインストールと構成

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Office 2010 を実行しているコンピューターでは、Azure Information Protection サービスに対して認証を行うために、Azure Information Protection クライアント (クラシック) または Azure Information Protection 統合ラベルクライアントが必要です。

これらの2つのクライアントの違いがわからない場合は、  [Azure Information Protection クライアントと Azure Information Protection の統一されたラベル付けクライアントの違いを](faqs.md#whats-the-difference-between-azure-information-protection-and-microsoft-information-protection)ご覧ください。

これらのクライアントは Office アドインをインストールするため、すべての Windows コンピューターにも推奨されます。これにより、ユーザーは Office リボンから直接ドキュメントや電子メールに簡単にラベルを付けて保護することができます。 また、これらのクライアントは、保護サービス (Azure Rights Management) によってネイティブでサポートされていないファイルの種類のラベル付けと保護、および Office アプリで開くことができない保護されたファイルのビューアーを提供します。 IOS と Android にも同様のビューアーがあります。

また、クラシッククライアントでは、ユーザーが保護したファイルを追跡および取り消すためのドキュメント追跡サイトもサポートしています。

## <a name="the-azure-information-protection-client-for-windows-installation-and-configuration"></a>Windows 用 Azure Information Protection クライアント: インストールと構成

Windows 用のクライアントのエンタープライズインストールおよび構成については、次の管理者ガイドを参照してください。

- 統一されたラベル付けクライアント: Azure Information Protection 統合された[クライアント管理者ガイド](./rms-client/clientv2-admin-guide.md)] (./rms-client/client-admin-guide.md)

- 従来のクライアント: [Azure Information Protection クライアント管理者ガイド](./rms-client/client-admin-guide.md)

ただし、これらのクライアントを1台のコンピューターに簡単にインストールしてテストする場合は、ユーザーガイドの次の手順を参照してください。

- 統一されたラベル付けクライアント: [Azure Information Protection 統合されたラベル付けクライアントをダウンロードしてインストール](./rms-client/install-unifiedlabelingclient-app.md)します。

- 従来のクライアント: [Azure Information Protection クライアントユーザーガイド](./rms-client/client-user-guide.md)から[Azure Information Protection クライアントをダウンロードしてインストール](./rms-client/install-client-app.md)します。

## <a name="the-azure-information-protection-app-for-ios-and-android-installation-and-management"></a>IOS および Android 用の Azure Information Protection アプリ: インストールと管理

IOS および Android 用の Azure Information Protection アプリビューアーをインストールするには、[ [Microsoft Azure Information Protection] ページ](https://go.microsoft.com/fwlink/?LinkId=303970)のリンクを使用します。 構成は必要ありません。

> [!NOTE]
> Mac コンピューターの場合、このページのリンクから RMS 共有アプリをダウンロードします。 これらのコンピューターは Azure Information Protection クライアントをサポートしていません。

### <a name="integration-with-intune"></a>Intune との統合

Azure Information Protection viewer アプリは Microsoft Intune アプリソフトウェア開発キットを使用するため、iOS デバイスと Android デバイスが Intune に登録されている場合は、次のデバイス用の Azure Information Protection ビューアーアプリを展開して管理できます。

1. [Intune に Azure Information Protection アプリを追加する](/intune/apps-add) 

2. 次のオプションの一方または両方を実行します。
    
    - アプリを[ユーザーに割り当てて](/intune/apps-deploy)デプロイする
    
    - [アプリ保護ポリシー](/intune/app-protection-policies)を使用してアプリを管理する

Azure Information Protection アプリを Intune に追加するときの追加情報:

- IOS の場合: Intune からアプリを検索して追加します。

- Android の場合: アプリを追加するときに、次の**Appstore URL**を使用します。
        
        https://play.google.com/store/apps/details?id=com.microsoft.ipviewer

Android デバイス用のアプリ保護ポリシーに対して Azure Information Protection アプリを構成すると、保護されたテキスト、イメージ、および PDF ドキュメントを開くだけでなく、このアプリではオーディオ ファイルとビデオ ファイルを開くこともできます。 詳細については、「[Azure Information Protection アプリでメディア ファイルを表示する](/intune/end-user-mam-apps-android#view-media-files-with-the-azure-information-protection-app)」を参照してください。

## <a name="next-steps"></a>次のステップ

Azure Information Protection クライアントをインストールして構成した後、ドキュメントや電子メールを保護するために使用できるさまざまな使用権限をクライアントが解釈する方法について、詳細を確認する必要がある場合があります。 詳細については、「 [Azure Information Management の使用権限を構成する](configure-usage-rights.md)」を参照してください。
