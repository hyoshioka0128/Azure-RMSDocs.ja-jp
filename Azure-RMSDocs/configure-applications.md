---
title: Azure Rights Management 用にアプリケーションを構成する - AIP
description: Azure Information Protection 用の Azure Rights Management 保護サービスをサポートするように、管理者がアプリケーションとサービスを構成する手順について説明します。 たとえば、Word 2013 や Word 2010 などの Office アプリケーション、および Exchange Online (トランスポート ルール、データ損失の防止、転送禁止、およびメッセージの暗号化) や SharePoint Online (保護されたライブラリ) などのサービスが含まれます。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/26/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3e4a84fc212c1e998556eec88a896d33d7615f05
ms.sourcegitcommit: 5fdf013fe05b65517b56245e1807875d80be6e70
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2018
ms.locfileid: "39489995"
---
# <a name="configuring-applications-for-azure-rights-management"></a>Azure Rights Management 用にアプリケーションを構成する

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!NOTE]
> ここでは、Azure Information Protection をデプロイした IT 管理者やコンサルタント向けの情報を紹介しています。 特定のアプリケーション用の Rights Management 機能の使用方法、または権利保護されたファイルを開く方法に関するユーザー向けヘルプや情報をお探しの場合は、アプリケーションに付属しているヘルプとガイダンスを使用してください。
>
> たとえば、Office アプリケーションの場合、[ヘルプ] アイコンをクリックし、「 **Rights Management** 」や「 **IRM**」などの検索語句を入力します。 Windows 用 Azure Information Protection クライアントについては、「[Azure Information Protection ユーザー ガイド](./rms-client/client-user-guide.md)」を参照してください。

組織に Azure Information Protection をデプロイしたら、次の情報を使用してアプリケーション、Azure Information Protection クライアント、サービスを構成します。 たとえば、Word 2016、Word 2013、Word 2010 などの Office アプリケーションです。 また、Exchange Online (トランスポート ルール、データ損失の防止、転送禁止、およびメッセージの暗号化) や SharePoint Online (保護されたライブラリ) などのサービスも含まれます。 これらのアプリケーションとサービスで Azure Information Protection からデータ保護サービスをサポートする方法については、「[アプリケーションによる Azure Rights Management サービスのサポート](applications-support.md)」を参照してください。

> [!IMPORTANT]
> サポートされているアプリケーションおよびその他の要件については、「[Azure Rights Management の要件](requirements.md)」を参照してください。

-   [Office 365: クライアントとオンライン サービスの構成](configure-office365.md)

    -   [Exchange Online: IRM 構成](configure-office365.md#exchange-online-irm-configuration)

    -   [SharePoint Online と OneDrive for Business: IRM 構成](configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)

- [Office アプリケーション: クライアントの構成](configure-office-apps.md)

    -   [Office 2016 と Office 2013](configure-office-apps.md#office-2016-and-office-2013)

    -   [Office 2010](configure-office-apps.md#office-2010)

-   [Azure Information Protection クライアント: クライアントのインストールと構成](configure-sharing-app.md)

-   [Rights Management 共有アプリケーション: クライアントでのインストールと構成](configure-sharing-app.md)


Exchange Server や SharePoint Server などのオンプレミス サーバーを構成する場合は、「[Azure Rights Management コネクタをデプロイする](deploy-rms-connector.md)」を参照してください。

これらのアプリケーションおよびサービスに加えて、Rights Management API をサポートする他のアプリケーションがあります。 このカテゴリには、Rights Management SDK を使用して社内で作成された基幹業務アプリケーション、および Rights Management SDK を使用して作成されたソフトウェア ベンダー製アプリケーションが含まれます。 これらのアプリケーションについては、アプリケーション付属の手順を参照してください。

## <a name="next-steps"></a>次の手順
Azure Rights Management サービスをサポートするためにアプリケーションを構成したら、[Azure Information Protection のデプロイ ロードマップ](deployment-roadmap.md)を使用して、Azure Information Protection をユーザーおよび管理者にロールアウトする前に行う他の構成手順があるかどうかを確認します。 他の手順を実行する必要がない場合は、次の操作に関する情報が役に立ちます。

- [Azure Rights Management サービスの検証](verify.md)

- [Azure Rights Management サービスを利用したファイルの保護でユーザーを支援するヘルプ](help-users.md)

- [Azure Rights Management サービスをログに記録して分析する](log-analyze-usage.md)

- [Azure Information Protection テナント キーに対する操作](operations-tenant-key.md)


