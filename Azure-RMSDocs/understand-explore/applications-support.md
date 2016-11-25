---
title: "アプリケーションによる Azure Rights Management サービスのサポート| Azure Information Protection"
description: "幅広く使用されているエンド ユーザー アプリケーション (Office アプリケーション、Word、Excel、PowerPoint、Outlook など) およびサービス (Exchange、SharePoint など) で、Azure Information Protection の Azure Rights Management を使用して組織の文書や電子メールを保護する方法について説明します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: fdb862b0d4f3d0a6b3411b38a314e28b5f1f9edc


---

# <a name="how-applications-support-the-azure-rights-management-service"></a>アプリケーションによる Azure Rights Management サービスのサポート

>*適用対象: Azure Information Protection、Office 365*

以下では、幅広く使用されているエンド ユーザー アプリケーション (Office アプリケーション、Word、Excel、PowerPoint、Outlook など) およびサービス (Exchange、SharePoint など) が組織の文書や電子メールを保護するために、Azure Information Protection の Azure Rights Management をどのように使用するかを説明します。 
> [!NOTE]
> Azure Rights Management サービスをサポートするアプリケーションおよびバージョンを確認するには、「[Azure Rights Management データ保護をサポートするアプリケーション](../get-started/requirements-applications.md)」をご覧ください。

管理者がポリシーを構成している場合、Azure Rights Management サービスによって保護が自動で実行される場合があります。 たとえば、SharePoint ライブラリ、分類されたファイル、Exchange トランスポート ルールなどがこれに該当します。 それ以外の場合は、エンド ユーザーが、テンプレートを選択するか特定のオプションを選択して、アプリケーションから情報保護を自分で適用する必要があります。 たとえば、ユーザーが電子メールでファイルを共有する場合や、選択したユーザーまたは組織外のユーザーにアクセスや使用を制限することでファイルをその場で保護する場合などがこれに該当します。

テンプレートを使用すると、ユーザー (およびポリシーを構成する管理者) が、簡単に正しいレベルの保護を適用し、組織内のユーザーにアクセスを制限することができます。 Azure Rights Management サービスには、2 つの既定のテンプレートが付属していますが、カスタム テンプレートを作成すると、個別のオプションを指定する時間を減らすことができます。 詳細については、「[Azure Rights Management サービスのカスタム テンプレートを構成する](../deploy-use/configure-custom-templates.md)」を参照してください。

ユーザーが情報保護を自分で適用する必要がある場合は、必ずユーザーに指示を与え、適用の方法とタイミングに関するガイダンスを提供してください。 ユーザーが使用するアプリケーションとバージョンおよびそれらの使用方法に適した指示を提供し、ビジネスに適した方法とタイミングで情報保護を適用するためのガイダンスを提供する必要があります。 詳細については、「[ユーザーに Azure Rights Management でファイルを保護するためのヘルプを提供する](../deploy-use/help-users.md)」を参照してください。

Azure Information Protection から Azure Rights Management サービス用にこれらのアプリケーションを構成する方法の詳細については、「[Azure Rights Management 用にアプリケーションを構成する](../deploy-use/configure-applications.md)」を参照してください。

> [!TIP]
> Azure Rights Management サービスを使用するアプリケーションの例とスクリーンショットについては、「[Azure RMS の動作: 管理者およびユーザーに対する表示](what-admins-users-see.md)」を参照してください。

検索サービスは、さまざまな方法で Rights Management と統合できます。 たとえば、 

- Exchange Online と Exchange Server は、サービス側インデックス作成を使用して、ユーザーの RMS で保護された電子メールが検索結果に自動的に表示されようにします。 

- SharePoint Online と SharePoint Server は、ダウンロード時にのみファイルに Rights Management 保護を適用します。つまり、SharePoint でのインデックス作成と検索結果は、この文書保護ソリューションによる影響を受けません。 ただし、ドキュメントを SharePoint に保存し、検索結果で返されないようにしたい場合は、SharePoint にアップロードする前に RMS でファイルを保護します。

- Windows デスクトップ検索はデバイスの異なるユーザー間で共有インデックスを使用するので、保護されたドキュメント内のデータを保護するため、RMS で保護されたファイルのインデックスを作成しません。 つまり、検索結果には保護されたファイルは含まれませんが、機密データを含むファイルは PC にサインインまたは接続する他のユーザーに対する検索結果に表示されないことが保証されます。 



## <a name="next-steps"></a>次のステップ

次の各アプリケーションで Azure Rights Management をサポートする方法について説明します。

-   [Windows およびモバイル プラットフォーム用の RMS 共有アプリケーション](sharing-app-support.md)

-   [Office アプリケーションおよびサービス](office-apps-services-support.md)

-   [Windows Server を実行し、ファイル分類インフラストラクチャ (FCI) を使用するファイル サーバー](file-server-support.md)

-   [RMS API をサポートするその他のアプリケーション](api-support.md)




<!--HONumber=Nov16_HO2-->


