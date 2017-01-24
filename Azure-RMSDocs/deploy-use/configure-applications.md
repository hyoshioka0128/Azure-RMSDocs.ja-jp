---
title: "Azure Rights Management サービスのアプリケーションを構成する | Azure Information Protection"
description: "Azure Information Protection 用の Azure Rights Management 保護サービスをサポートするように、管理者がアプリケーションとサービスを構成する手順について説明します。 たとえば、Word 2013 や Word 2010 などの Office アプリケーション、および Exchange Online (トランスポート ルール、データ損失の防止、転送禁止、およびメッセージの暗号化) や SharePoint Online (保護されたライブラリ) などのサービスが含まれます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/05/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ea09cbc5-b98b-444e-8b60-5bc3cb199c36
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 3c54f0c2f3fcbd312bb3ade521e5dd7f4a12eb85


---

# <a name="configuring-applications-for-azure-rights-management"></a>Azure Rights Management 用にアプリケーションを構成する

>*適用対象: Azure Information Protection、Office 365*

> [!NOTE]
> ここでは、Azure Information Protection をデプロイした IT 管理者やコンサルタント向けの情報を紹介しています。 特定のアプリケーション用の Rights Management 機能の使用方法、または権利保護されたファイルを開く方法に関するユーザー向けヘルプや情報をお探しの場合は、アプリケーションに付属しているヘルプとガイダンスを使用してください。
>
> たとえば、Office アプリケーションの場合、[ヘルプ] アイコンをクリックし、「 **Rights Management** 」や「 **IRM**」などの検索語句を入力します。 Windows 用の RMS 共有アプリケーションの場合は、「[Rights Management 共有アプリケーション ユーザー ガイド](../rms-client/sharing-app-user-guide.md)」を参照してください。

組織に Azure Information Protection をデプロイしたら、次の情報を使用して、Azure Information Protection からの Azure Rights Management サービスをサポートするようにアプリケーションとサービスを構成します。 これらの構成には、Word 2013 や Word 2010、および Exchange Online (トランスポート ルール、データ損失の防止、転送禁止、およびメッセージの暗号化) や SharePoint Online (保護されたライブラリ) などのサービスが含まれます。 これらのアプリケーションおよびサービスで Rights Management をサポートする方法については、「[アプリケーションによる Azure Rights Management サービスのサポート](../understand-explore/applications-support.md)」を参照してください。

> [!IMPORTANT]
> サポートされているアプリケーションおよびその他の要件については、「[Azure Rights Management の要件](../get-started/requirements-azure-rms.md)」を参照してください。

-   [Office 365: クライアントとオンライン サービスの構成](configure-office365.md)

    -   [Exchange Online: IRM 構成](configure-office365.md#exchange-online-irm-configuration)

    -   [SharePoint Online と OneDrive for Business: IRM 構成](configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration)

- [Office アプリケーション: クライアントの構成](configure-office-apps.md)

    -   [Office 2016 と Office 2013](configure-office-apps.md#office-2016-and-office-2013)

    -   [Office 2010](configure-office-apps.md#office-2010)

-   [Rights Management 共有アプリケーション: クライアントでのインストールと構成](configure-sharing-app.md)

    -   [Windows 用 RMS 共有アプリケーション: インストールと構成](configure-sharing-app.md#the-rms-sharing-application-for-windows-installation-and-configuration)

    -   [モバイル プラットフォーム用 RMS 共有アプリケーション: インストールと管理](configure-sharing-app.md#the-rms-sharing-application-for-mobile-platforms-installation-and-management)


Exchange Server や SharePoint Server などのオンプレミス サーバーを構成する場合は、「[Azure Rights Management コネクタをデプロイする](deploy-rms-connector.md)」を参照してください。

> [!TIP]
> Azure Rights Management サービスを使用するように構成されたアプリケーションの概要レベルの例とスクリーンショットについては、「[Azure RMS の動作: 管理者およびユーザーに対する表示](../understand-explore/what-admins-users-see.md)」を参照してください。


これらのアプリケーションおよびサービスに加えて、Rights Management API をサポートする他のアプリケーションがあります。 このカテゴリには、Rights Management SDK を使用して社内で作成された基幹業務アプリケーション、および Rights Management SDK を使用して作成されたソフトウェア ベンダー製アプリケーションが含まれます。 これらのアプリケーションについては、アプリケーション付属の手順を参照してください。

## <a name="next-steps"></a>次のステップ
Azure Rights Management サービスをサポートするためにアプリケーションを構成したら、[Azure Information Protection のデプロイ ロードマップ](../plan-design/deployment-roadmap.md)を使用して、Azure Information Protection をユーザーおよび管理者にロールアウトする前に行う他の構成手順があるかどうかを確認します。 他の手順を実行する必要がない場合は、次の操作に関する情報が役に立ちます。

- [Azure Rights Management サービスの検証](verify.md)

- [Azure Rights Management サービスを利用したファイルの保護でユーザーを支援するヘルプ](help-users.md)

- [Azure Rights Management サービスをログに記録して分析する](log-analyze-usage.md)

- [Azure Information Protection テナント キーに対する操作](operations-tenant-key.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]




<!--HONumber=Jan17_HO4-->


