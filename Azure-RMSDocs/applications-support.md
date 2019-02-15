---
title: アプリが AIP から Azure Rights Management をサポートするしくみ
description: 幅広く使用されているエンド ユーザー アプリケーション (Office アプリケーション、Word、Excel、PowerPoint、Outlook など) およびサービス (Exchange、SharePoint など) で、Azure Information Protection の Azure Rights Management を使用して組織の文書や電子メールを保護する方法について説明します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 01/02/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2cdc7bde-4044-4021-b887-11476f99afd9
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 56584fbff799780a86f93546997a342faa29592f
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2019
ms.locfileid: "56258387"
---
# <a name="how-applications-support-the-azure-rights-management-service"></a>アプリケーションによる Azure Rights Management サービスのサポート

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

以下では、幅広く使用されているエンド ユーザー アプリケーションとサービスが組織の文書や電子メールを保護するために、Azure Information Protection の Azure Rights Management をどのように使用するかを説明します。 アプリケーションには、Word、Excel、PowerPoint、Outlook があります。 サービスには Exchange や SharePoint があります。

> [!NOTE]
> Azure Rights Management サービスをサポートするアプリケーションおよびバージョンを確認するには、「[Azure Rights Management データ保護をサポートするアプリケーション](./requirements-applications.md)」をご覧ください。

管理者がポリシーを構成している場合、Azure Rights Management サービスによって保護が自動で実行される場合があります。 たとえば、SharePoint ライブラリや Exchange トランスポート ルールなどがこれに該当します。 それ以外の場合、エンド エーザーは自分のアプリケーションから自分で保護を適用する必要があります。 たとえば、ユーザーは保護を適用するように構成されている分類ラベルを選択するか、テンプレートを選択するか、特定のオプションを選択します。 ユーザーによる保護の適用は、ユーザーが共有するファイルを保護していて、選択したユーザーまたは組織外のユーザーにアクセスや使用を制限する場合に一般的です。

テンプレートを使用すると、ユーザー (およびポリシーを構成する管理者) が、簡単に正しいレベルの保護を適用し、組織内のユーザーにアクセスを制限することができます。 Azure Rights Management サービスには、2 つの既定のテンプレートが付属していますが、カスタム テンプレートを作成すると、ユーザーと管理者が個別のオプションを指定する時間を減らすことができます。 テンプレートの詳細については、「[Azure Information Protection のテンプレートを構成して管理する](configure-policy-templates.md)」を参照してください。

ユーザーが保護を自分で適用する必要がある場合は、必ずユーザーに指示を与え、適用の方法とタイミングに関するガイダンスを提供してください。 ユーザーが使用するアプリケーションとバージョン、用途について具体的に指示してください。 また、ビジネスに適切な保護を適用するタイミングと方法について指示してください。 詳細については、「[ユーザーに Azure Rights Management でファイルを保護するためのヘルプを提供する](help-users.md)」を参照してください。

Azure Information Protection から Azure Rights Management サービス用にこれらのアプリケーションを構成する方法の詳細については、「[Azure Rights Management 用にアプリケーションを構成する](configure-applications.md)」を参照してください。

検索サービスは、さまざまな方法で Rights Management と統合できます。 次に例を示します。 

- Exchange Online と Exchange Server は、サービス側インデックス作成を使用して、ユーザーの保護された電子メールが検索結果に自動的に表示されようにします。 

- SharePoint Online と SharePoint Server は Rights Management 保護をダウンロード時にのみファイルに適用します。 この実装は、SharePoint のインデックス作成と検索結果がこのドキュメント保護ソリューションによる影響を受けないことを意味します。 ただし、ドキュメントを SharePoint に保存し、検索結果で返されないようにしたい場合は、SharePoint にアップロードする前にドキュメントを保護します。

- Windows デスクトップ検索はデバイスの異なるユーザー間で共有インデックスを使用するので、保護されたドキュメント内のデータを保護するため、保護されたファイルのインデックスを作成しません。 つまり、検索結果には保護されたファイルが含まれませんが、PC にサインインまたは接続する他のユーザーの検索結果に、機密データを含むファイルが表示されないことが保証されます。 

## <a name="next-steps"></a>次の手順

次の各アプリケーションとサービスで Azure Rights Management サービスをサポートする方法について説明します。

-   [Office アプリケーションおよびサービス](office-apps-services-support.md)

-   [Windows Server を実行し、ファイル分類インフラストラクチャ (FCI) を使用するファイル サーバー](file-server-support.md)

-   [RMS API をサポートするその他のアプリケーション](api-support.md)

