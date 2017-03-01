---
title: "Azure クラシック ポータルで Azure RMS をアクティブ化する - AIP"
description: "Azure Portal にアクセスできる場合に、Azure Rights Management サービスをアクティブ化する手順です。 たとえば、Enterprise Mobility Suite のサブスクリプションまたは Azure Information Protection Premium のサブスクリプションがある場合です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 9b0a0227-88ce-44b8-ba3f-31eeaab27ff7
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 444d74c957ec6e243858fcddfaac36951c257a9d
ms.lasthandoff: 02/24/2017


---

# <a name="how-to-activate-azure-rights-management-from-the-azure-classic-portal"></a>Azure クラシック ポータルから Azure Rights Management をアクティブ化する方法

>*適用対象: Azure Information Protection*


Azure Portal にアクセスできる場合は、次の手順を使用してください。 たとえば、Enterprise Mobility Suite のサブスクリプションまたは Azure Information Protection Premium のサブスクリプションがある場合です。

> [!TIP]
> [Azure RMS をアクティブ化する方法](https://channel9.msdn.com/series/pit-stop-enterprise-mobility-suite/activate-azure-rms)に関する 2 分間のビデオをご覧ください。

1.  Azure アカウントにサインアップした後、[Azure クラシック ポータルにサインイン](http://go.microsoft.com/fwlink/p/?LinkID=275081)します。 Azure Rights Management を含むサブスクリプションの取得に使用したアカウントなどのグローバル管理者アカウントを使用します。

2.  左ペインで、[ **ACTIVE DIRECTORY**] をクリックします。

3.  [ **Active Directory** ] ページで、[ **RIGHTS MANAGEMENT**] をクリックします。

4.  [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] で管理するディレクトリを選択し、**[アクティブ化]** をクリックして、操作を確定します。

    > [!NOTE]
    >アクティブ化でエラーが発生する場合、サービス プランまたは製品バージョンが Azure Information Protection の Azure Rights Management サービスを含んでいないことが考えられます。
    >
    >Azure Rights Management サービスをアクティブ化するには、[Azure Information Protection Premium プラン](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing)を取得するか、[Rights Management を含む Office 365 プラン](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)を取得する必要があります。 この問題でサポートが必要な場合は、 [askipteam](mailto:askipteam?subject=I%20cannot%20activate%20RMS)宛てに電子メール メッセージを送信してください。


これで、[ **Rights Management のステータス** ] に [ **アクティブ** ] と表示され、[ **アクティブ化** ] オプションが [ **非アクティブ化**] に置き換えられます。

## <a name="rights-management-status-values-and-descriptions-in-the-azure-classic-portal"></a>Azure クラシック ポータルでの Rights Management のステータス値および説明
[ **アクティブ** ] ステータス (Rights Management サービスが有効化され、使用できる状態にあることを示す) の他に、[ **非アクティブ**]、[ **利用不可**]、または [ **許可されていません**] が表示される場合もあります。

|ステータス値|説明|
|----------------|---------------|
|**アクティブ**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] は有効化され、使用できる様態にあります。|
|**非アクティブ**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] は、無効になっているので、組織がファイルを保護できるようにするにはアクティブ化する必要があります。|
|**利用不可**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] サービスはダウンしています。 後でもう一度やり直してください。|
|**許可されていません**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] サービスのステータスを表示する権限がありません。 たとえば、アカウントがロックアウトされているか、または選択したテナントのグローバル管理者になっていません。|

## <a name="next-steps"></a>次のステップ
「[Azure Rights Management をアクティブにする](activate-service.md)」に戻ります。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
