---
title: Azure Rights Management 用にアプリケーションを構成する - AIP
description: Azure Information Protection 用の Azure Rights Management 保護サービスをサポートするように、管理者がアプリケーションとサービスを構成する手順について説明します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/30/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 9deba7b1f62e501d49944410c4347743be3341cf
ms.sourcegitcommit: b763a7204421a4c5f946abb7c5cbc06e2883199c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2020
ms.locfileid: "95569687"
---
# <a name="configuring-applications-for-azure-rights-management"></a>Azure Rights Management 用にアプリケーションを構成する

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!NOTE]
> ここでは、Azure Information Protection をデプロイした IT 管理者やコンサルタント向けの情報を紹介しています。 特定のアプリケーション用の Rights Management 機能の使用方法、または権利保護されたファイルを開く方法に関するユーザー向けヘルプや情報をお探しの場合は、アプリケーションに付属しているヘルプとガイダンスを使用してください。
>
> たとえば、Office アプリケーションの場合、[ヘルプ] アイコンをクリックし、「**Rights Management**」または「**IRM**」などの検索語句を入力します。 Windows 用 Azure Information Protection クライアントについては、「[Azure Information Protection ユーザー ガイド](./rms-client/client-user-guide.md)」を参照してください。

組織に Azure Information Protection をデプロイしたら、次の情報を使用してアプリケーション、Azure Information Protection クライアント、サービスを構成します。 たとえば、Word 2019、Word 2016、Word 2013 などの Office アプリケーションです。 また、Exchange Online (トランスポートルール、データ損失の防止、転送禁止、およびメッセージの暗号化) や Microsoft SharePoint (保護されたライブラリ) などのサービスもあります。 これらのアプリケーションとサービスで Azure Information Protection からデータ保護サービスをサポートする方法については、「[アプリケーションによる Azure Rights Management サービスのサポート](applications-support.md)」を参照してください。

> [!IMPORTANT]
> サポートされているバージョンとその他の要件については、「 [Azure Information Protection の要件](requirements.md)」を参照してください。

-   [Office 365: オンラインサービスの構成](configure-office365.md)

    -   [Exchange Online: IRM の構成](configure-office365.md#exchangeonline-irm-configuration)

    -   [Microsoft 365 の SharePoint と OneDrive: IRM の構成](configure-office365.md#sharepoint-in-microsoft-365-and-onedrive-irm-configuration)

- [Office アプリケーション: クライアントの構成](configure-office-apps.md)

    -   [Office 365 アプリ、Office 2019、Office 2016、および Office 2013](configure-office-apps.md#office365-apps-office-2019-office-2016-and-office-2013)

    -   [Office 2010](configure-office-apps.md#office2010)

-   [Azure Information Protection クライアント: クライアントのインストールと構成](configure-client.md)

Exchange Server や SharePoint Server などのオンプレミスサーバーを構成するには、「 [Azure Rights Management コネクタのデプロイ](deploy-rms-connector.md)」を参照してください。

これらのアプリケーションおよびサービスに加えて、Rights Management API をサポートする他のアプリケーションがあります。 このカテゴリには、Rights Management SDK を使用して社内で作成された基幹業務アプリケーション、および Rights Management SDK を使用して作成されたソフトウェア ベンダー製アプリケーションが含まれます。 これらのアプリケーションについては、アプリケーション付属の手順を参照してください。

## <a name="next-steps"></a>次のステップ
Azure Rights Management サービスをサポートするためにアプリケーションを構成したら、[Azure Information Protection のデプロイ ロードマップ](deployment-roadmap.md)を使用して、Azure Information Protection をユーザーおよび管理者にロールアウトする前に行う他の構成手順があるかどうかを確認します。 他の手順を実行する必要がない場合は、次の操作に関する情報が役に立ちます。

- [Azure Rights Management サービスの検証](verify.md)

- [Azure Rights Management サービスを利用したファイルの保護でユーザーを支援するヘルプ](help-users.md)

- [Azure Rights Management サービスをログに記録して分析する](log-analyze-usage.md)

- [Azure Information Protection テナント キーの操作](operations-tenant-key.md)


