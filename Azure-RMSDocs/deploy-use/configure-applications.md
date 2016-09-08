---
title: "Azure Rights Management 用にアプリケーションを構成する | Azure RMS"
description: "組織に Azure Rights Management (Azure RMS) をデプロイしたら、次の情報を使用して、Azure RMS をサポートするようにアプリケーションとサービスを構成します。 これらの構成には、Word 2013 や Word 2010、および Exchange Online (トランスポート ルール、データ損失の防止、転送禁止、およびメッセージの暗号化) や SharePoint Online (保護されたライブラリ) などのサービスが含まれます。"
author: cabailey
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: 7e592d99bcd2a143d63b35aa4afb92b1e45cb74a


---

# Azure Rights Management 用にアプリケーションを構成する

>*適用対象: Azure Rights Management、Office 365*

> [!NOTE]
> ここでは、Azure Rights Management をデプロイした IT 管理者やコンサルタント向けの情報を紹介しています。 特定のアプリケーション用の Rights Management の使用方法、または権利保護されたファイルを開く方法に関するユーザー向けヘルプや情報をお探しの場合は、アプリケーションに付属しているヘルプとガイダンスを使用してください。
>
> たとえば、Office アプリケーションの場合、[ヘルプ] アイコンをクリックし、「 **Rights Management** 」や「 **IRM**」などの検索語句を入力します。 Windows 用の RMS 共有アプリケーションの場合は、「[Rights Management 共有アプリケーション ユーザー ガイド](../rms-client/sharing-app-user-guide.md)」を参照してください。

組織に Azure Rights Management (Azure RMS) をデプロイしたら、次の情報を使用して、Azure RMS をサポートするようにアプリケーションとサービスを構成します。 これらの構成には、Word 2013 や Word 2010、および Exchange Online (トランスポート ルール、データ損失の防止、転送禁止、およびメッセージの暗号化) や SharePoint Online (保護されたライブラリ) などのサービスが含まれます。 これらのアプリケーションおよびサービスで Rights Management をサポートする方法については、「[アプリケーションで Azure Rights Management をサポートする方法](../understand-explore/applications-support.md)」を参照してください。

> [!IMPORTANT]
> サポートされているアプリケーションおよびその他の要件については、「[Azure Rights Management の要件](../get-started/requirements-azure-rms.md)」を参照してください。

-   [Office 365: クライアントとオンライン サービスの構成](configure-office365.md)

    -   [Exchange Online: IRM 構成](configure-office365.md#exchange-online-irm-configuration)

    -   [SharePoint Online と OneDrive for Business:IRM 構成](configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)

- [Office アプリケーション: クライアントの構成](configure-office-apps.md)

    -   [Office 2016 と Office 2013:](configure-office-apps.md#office-2016-and-office-2013)

    -   [Office 2010](configure-office-apps.md#office-2010)

-   [Rights Management 共有アプリケーション: クライアントでのインストールと構成](configure-sharing-app.md)

    -   [Windows 用 RMS 共有アプリケーション: インストールと構成](configure-sharing-app.md#the-rms-sharing-application-for-windows-installation-and-configuration)

    -   [モバイル プラットフォーム用 RMS 共有アプリケーション: インストールと管理](configure-sharing-app.md#the-rms-sharing-application-for-mobile-platforms-installation-and-management)


Exchange Server や SharePoint Server などのオンプレミス サーバーを構成する場合は、「[Azure Rights Management コネクタをデプロイする](deploy-rms-connector.md)」を参照してください。

> [!TIP]
> Azure RMS を使用するように構成されたアプリケーションの概要レベルの例とスクリーンショットについては、「[Azure RMS の動作: 管理者およびユーザーに対する表示](../understand-explore/what-admins-users-see.md)」を参照してください。


これらのアプリケーションおよびサービスに加えて、RMS API をサポートする他のアプリケーションがあります。 このカテゴリには、RMS SDK を使用して社内で作成された基幹業務アプリケーション、および RMS SDK を使用して作成されたソフトウェア ベンダー製アプリケーションが含まれます。 これらのアプリケーションについては、アプリケーション付属の手順を参照してください。

## 次のステップ
Azure Rights Management をサポートするためにアプリケーションを構成したら、[Azure Rights Management のデプロイ ロードマップ](../plan-design/deployment-roadmap.md)を使用して、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] をユーザーおよび管理者にロールアウトする前に行う他の構成手順があるかどうかを確認します。 他の手順を実行する必要がない場合は、次の操作に関する情報が役に立ちます。

- [Azure Rights Management を確認する](verify.md)

- [ユーザーに Azure Rights Management でファイルを保護するためのヘルプを提供する](help-users.md)

- [Azure Rights Management をログに記録して分析する](log-analyze-usage.md)

- [Azure Rights Management テナント キーに対する操作](operations-tenant-key.md)





<!--HONumber=Aug16_HO4-->


