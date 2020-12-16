---
title: Azure Information Protection クライアント - インストールと構成
description: Windows コンピューターとモバイルデバイスに Azure Information Protection クライアントを展開する方法に関する管理者向けの情報。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/16/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: b1a19ae7-db26-40da-9e21-6620af3d0b02
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 2da5d348f497a74e88c0bf11da023be6e3cb0152
ms.sourcegitcommit: efeb486e49c3e370d7fd8244687cd3de77cd8462
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/16/2020
ms.locfileid: "97583542"
---
# <a name="azure-information-protection-client-installation-and-configuration-for-clients"></a>Azure Information Protection クライアント: クライアントのインストールと構成

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連**: [AIP のラベル付けクライアントと従来のクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE]
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection のクラシック クライアント** と **ラベル管理** は、**2021 年 3 月 31 日** をもって **非推奨** になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

AIP 統合ラベルクライアントは、ユーザーが Office リボンから直接ドキュメントに簡単にラベルを付けて保護できる Office アドインをインストールするため、すべての Windows コンピューターで推奨されます。 

クライアントは次の機能も提供します。

- 組み込みの保護サービス (Azure Rights Management) でサポートされていないファイルの種類のラベル付けと保護。
- Office アプリで開くことができない保護されたファイルのビューアー。 IOS と Android にも同様のビューアーがあります。
- 保護されたファイルへのアクセスを追跡および取り消すための機能。

Office 2010 を実行しているコンピューターでは、Azure Information Protection クライアントが Azure Information Protection サービスに対して認証を行う必要があります。 詳細については、「 [AIP For Windows And Office versions in extended support](known-issues.md#aip-for-windows-and-office-versions-in-extended-support)」を参照してください。
## <a name="the-azure-information-protection-client-for-windows-installation-and-configuration"></a>Windows 用 Azure Information Protection クライアント: インストールと構成

Windows 用のクライアントのエンタープライズインストールおよび構成については、 [Azure Information Protection 統合されたラベル付けクライアント管理者ガイド](./rms-client/clientv2-admin-guide.md)を参照してください。

これらのクライアントを1台のコンピューターに簡単にインストールしてテストする場合は、「 [Azure Information Protection の統合ラベル付けクライアントをダウンロードしてインストール](./rms-client/install-unifiedlabelingclient-app.md)する」を参照してください。

**従来のクライアントのみ**: クラシッククライアントがインストールされている場合は、代わりに次のリンクを使用します。

- [Azure Information Protection クライアント管理者ガイド](./rms-client/client-admin-guide.md)
- [Azure Information Protection クライアントをダウンロードしてインストール](./rms-client/install-client-app.md)します。

## <a name="the-azure-information-protection-app-for-ios-and-android-installation-and-management"></a>IOS および Android 用の Azure Information Protection アプリ: インストールと管理

IOS および Android 用の Azure Information Protection アプリビューアーをインストールするには、[ [Microsoft Azure Information Protection] ページ](https://go.microsoft.com/fwlink/?LinkId=303970)のリンクを使用します。 構成は必要ありません。

> [!NOTE]
> Mac コンピューターの場合、このページのリンクから RMS 共有アプリをダウンロードします。 これらのコンピューターは Azure Information Protection クライアントをサポートしていません。

### <a name="integration-with-intune"></a>Intune との統合

Azure Information Protection viewer アプリは Microsoft Intune アプリソフトウェア開発キットを使用するため、iOS デバイスと Android デバイスが Intune に登録されている場合は、次のデバイス用の Azure Information Protection ビューアーアプリを展開して管理できます。

1. [Intune に Azure Information Protection アプリを追加する](/intune/apps/apps-add)

2. 次のオプションの一方または両方を実行します。

    - アプリを[ユーザーに割り当てて](/intune/apps/apps-deploy)デプロイする

    - [アプリ保護ポリシー](/intune/apps/app-protection-policies)を使用してアプリを管理する

Azure Information Protection アプリを Intune に追加するときの追加情報:

- IOS の場合: Intune からアプリを検索して追加します。

- Android の場合: アプリを追加するときに、次の **Appstore URL** を使用します。

    ```md
    https://play.google.com/store/apps/details?id=com.microsoft.ipviewer
    ```

Android デバイス用のアプリ保護ポリシーに対して Azure Information Protection アプリを構成すると、保護されたテキスト、イメージ、および PDF ドキュメントを開くだけでなく、このアプリではオーディオ ファイルとビデオ ファイルを開くこともできます。 詳細については、「[Azure Information Protection アプリでメディア ファイルを表示する](/intune/fundamentals/end-user-mam-apps-android#view-media-files-with-the-azure-information-protection-app)」を参照してください。

## <a name="next-steps"></a>次のステップ

Azure Information Protection クライアントをインストールして構成した後、ドキュメントや電子メールを保護するために使用できるさまざまな使用権限をクライアントが解釈する方法について、詳細を確認する必要がある場合があります。 詳細については、「 [Azure Information Management の使用権限を構成する](configure-usage-rights.md)」を参照してください。
