---
title: "Azure Rights Management 保護を準備する - AIP"
description: "組織がドキュメントや電子メールを保護できるように、Azure Rights Management サービスを使用するためのすべての準備ができていることを確認します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/24/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: afbca2d6-32a7-4bda-8aaf-9f93f5da5abc
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 11ebd66a1ae05535814af159523bd49b7921d46d
ms.openlocfilehash: fc80a4a65bd5fae1b8604c316a4e2354bbe8c8be
ms.lasthandoff: 02/25/2017


---

# <a name="preparing-for-azure-information-protection"></a>Azure Information Protection の準備

>*適用対象: Azure Information Protection、Office 365*

組織の Azure Information Protection をデプロイする前に、次の内容が準備されていることを確認します。

-   手動で作成するか、または Active Directory ドメイン サービス (AD DS) から自動的に作成および同期される、クラウド内のユーザー アカウントおよびグループ。

    オンプレミスのアカウントとグループを同期するとき、すべての属性を同期する必要はありません。 Azure Information Protection によって使用される Azure Rights Management サービス用に同期する必要がある属性の一覧については、Azure Active Directory のドキュメントの [Azure RMS に関するセクション](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms)をご覧ください。 デプロイが容易なので [Azure AD Connect](/active-directory/active-directory-aadconnectsync-whatis) を使用してオンプレミスのディレクトリを Azure Active Directory と接続することをお勧めしますが、同じ結果が得られる他のディレクトリ同期方法を使ってもかまいません。

-   Azure Information Protection で使用する、クラウドでのメールが有効なグループ。 組み込みのグループ、または保護されたドキュメントと電子メールを使用するユーザーを含む手動で作成したグループにすることができます。

    Exchange Online がある場合は、Exchange 管理センターを使用して、メールが有効なグループを作成し使用することができます。 AD DS があり、Azure AD と同期している場合は、セキュリティ グループまたは配布グループであるメールが有効なグループを作成して使用できます。

### <a name="group-membership-caching"></a>グループ メンバーシップのキャッシュ

パフォーマンス上の理由から、グループ メンバーシップは Azure Rights Management サービスによってキャッシュされます。 これは、グループ メンバーシップの変更内容が有効になるまで最長で 3 時間かかる場合があり、この期間は変わる可能性があることを意味します。 変更を加えるとき、または[カスタム テンプレート](../deploy-use/configure-custom-templates.md)の構成などの Azure Rights Management サービスの構成でグループを使用する場合や、[スーパー ユーザー機能](../deploy-use/configure-super-users.md)でグループを使用する場合にテストを行う際にはこの遅延を考慮してください。 

## <a name="activate-the-rights-management-service-for-data-protection"></a>データ保護のための Rights Management サービスのアクティブ化
ドキュメントや電子メールの保護を開始する準備ができたら、このテクノロジを有効にする Rights Management サービスをアクティブにします。 詳細については、「[Rights Management をアクティブにする](../deploy-use/activate-service.md)」を参照してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



