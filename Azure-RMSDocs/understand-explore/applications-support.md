---
title: "アプリケーションで Azure Rights Management をサポートする方法 | Azure RMS"
description: "幅広く使用されているエンドユーザー アプリケーション (Office アプリケーション、Word、Excel、PowerPoint、Outlook など) およびサービス (Exchange、SharePoint など) で、Microsoft Azure Rights Management を使用して組織のデータの保護を可能にする方法を理解するには、次の情報を参考にしてください。"
author: cabailey
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: df66b53238acecd4173b7d1bc57a611c403ec256


---

# アプリケーションによる Azure Rights Management のサポート

>*適用対象: Azure Rights Management、Office 365*

次の情報は、幅広く使用されているエンド ユーザー アプリケーション (Office アプリケーション、Word、Excel、PowerPoint、Outlook など) およびサービス (Exchange、SharePoint など) が Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] を使用して、組織のデータの保護を可能にする方法を理解する場合に役立ちます。 
> [!NOTE]
> [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) によってサポートされるアプリケーションとバージョンを確認するには、「[Azure Rights Management の要件](../get-started/requirements-azure-rms.md)」を参照してください。

場合によっては、構成するポリシーに従って情報保護が自動的に適用されます。 たとえば、SharePoint ライブラリ、分類されたファイル、Exchange トランスポート ルールなどがこれに該当します。 それ以外の場合は、ユーザーが、テンプレートを選択するか特定のオプションを選択して、アプリケーションから情報保護を自分で適用する必要があります。 たとえば、ユーザーが電子メールでファイルを共有する場合や、選択したユーザーまたは組織外のユーザーにアクセスや使用を制限することでファイルをその場で保護する場合などがこれに該当します。

テンプレートを使用すると、ユーザー (およびポリシーを構成する管理者) が、簡単に正しいレベルの保護を適用し、組織内のユーザーにアクセスを制限することができます。 [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] には、2 つの既定のテンプレートが付属していますが、カスタム テンプレートを作成すると、個別のオプションの指定が必要な回数を減らすことができます。 詳細については、「[Azure Rights Management のカスタム テンプレートを構成する](../deploy-use/configure-custom-templates.md)」を参照してください。

ユーザーが情報保護を自分で適用する必要がある場合は、必ずユーザーに指示を与え、適用の方法とタイミングに関するガイダンスを提供してください。 ユーザーが使用するアプリケーションとバージョンおよびそれらの使用方法に適した指示を提供し、ビジネスに適した方法とタイミングで情報保護を適用するためのガイダンスを提供する必要があります。 詳細については、「[ユーザーに Azure Rights Management でファイルを保護するためのヘルプを提供する](../deploy-use/help-users.md)」を参照してください。

Azure RMS 用にこれらのアプリケーションを構成する方法の詳細については、「[Azure Rights Management 用にアプリケーションを構成する](../deploy-use/configure-applications.md)」を参照してください。

> [!TIP]
> Azure RMS を使用するアプリケーションの例とスクリーンショットについては、「[Azure RMS in action: What administrators and users see (Azure RMS の動作: 管理者およびユーザーに対する表示)](what-admins-users-see.md)」を参照してください。

検索サービスは、さまざまな方法で Rights Management と統合できます。 たとえば、 

- Exchange Online と Exchange Server は、サービス側インデックス作成を使用して、ユーザーの RMS で保護された電子メールが検索結果に自動的に表示されようにします。 

- SharePoint Online と SharePoint Server は、ダウンロード時にのみファイルに RMS 保護を適用します。つまり、SharePoint でのインデックス作成と検索結果は、このドキュメント保護ソリューションによる影響を受けません。 ただし、ドキュメントを SharePoint に保存し、検索結果で返されないようにしたい場合は、SharePoint にアップロードする前に RMS でファイルを保護します。

- Windows デスクトップ検索はデバイスの異なるユーザー間で共有インデックスを使用するので、保護されたドキュメント内のデータを保護するため、RMS で保護されたファイルのインデックスを作成しません。 つまり、検索結果には保護されたファイルは含まれませんが、機密データを含むファイルは PC にサインインまたは接続する他のユーザーに対する検索結果に表示されないことが保証されます。 



## 次のステップ

次の各アプリケーションで Azure RMS をサポートする方法について説明します。

-   [Windows およびモバイル プラットフォーム用の RMS 共有アプリケーション](sharing-app-support.md)

-   [Office アプリケーションおよびサービス](office-apps-services-support.md)

-   [Windows Server を実行するファイル サーバーとファイル分類インフラストラクチャ (FCI) の使用](file-server-support.md)

-   [RMS API をサポートするその他のアプリケーション](api-support.md)




<!--HONumber=Aug16_HO4-->


