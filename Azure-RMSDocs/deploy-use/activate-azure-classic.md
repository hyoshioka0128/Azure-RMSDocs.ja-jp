---
# required metadata

title: Azure クラシック ポータルから Azure Rights Management をアクティブ化する方法 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 9b0a0227-88ce-44b8-ba3f-31eeaab27ff7

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Azure クラシック ポータルから Azure Rights Management をアクティブ化する方法

Azure ポータルにアクセスできる場合は、次の手順を使用してください。 たとえば、Enterprise Mobility Suite のサブスクリプションがある場合などです。

> [!TIP]
> [Azure RMS をアクティブ化する方法](https://channel9.msdn.com/series/pit-stop-enterprise-mobility-suite/activate-azure-rms)に関する 2 分間のビデオをご覧ください。

1.  Azure アカウントにサインアップした後、[Azure クラシック ポータルにサインイン](http://go.microsoft.com/fwlink/p/?LinkID=275081)します。

2.  左ペインで、[ **ACTIVE DIRECTORY**] をクリックします。

3.  [ **Active Directory** ] ページで、[ **RIGHTS MANAGEMENT**] をクリックします。

4.  [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] で管理するディレクトリを選択し、**[アクティブ化]** をクリックして、操作を確定します。

    > [!NOTE]
    > アクティブ化エラーが表示される場合、サービス プランまたは製品バージョンが [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] に対応していないことが考えられます。
    >
    > [Azure RMS をサポートするクラウド サブスクリプション](../get-started/requirements-subscriptions.md)に関するページの情報を基に、RMS のサポートを確認してください。 この問題でサポートが必要な場合は、 [askipteam](mailto:askipteam?subject=I%20cannot%20activate%20RMS)宛てに電子メール メッセージを送信してください。

これで、[ **Rights Management のステータス** ] に [ **アクティブ** ] と表示され、[ **アクティブ化** ] オプションが [ **非アクティブ化**] に置き換えられます。

## Azure クラシック ポータルでの Rights Management のステータス値および説明
[ **アクティブ** ] ステータス (Rights Management サービスが有効化され、使用できる状態にあることを示す) の他に、[ **非アクティブ**]、[ **利用不可**]、または [ **許可されていません**] が表示される場合もあります。

|ステータス値|説明|
|----------------|---------------|
|**アクティブ**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] は有効になっていて、使用できる状態にあります。|
|**非アクティブ**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] は、無効になっているので、組織がファイルを保護できるようにするにはアクティブ化する必要があります。|
|**利用不可**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] サービスはダウンしています。 後でもう一度やり直してください。|
|**許可されていません**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] サービスのステータスを表示する権限がありません。 たとえば、アカウントがロックアウトされているか、または選択したテナントのグローバル管理者になっていません。|

## 次のステップ
「[Azure Rights Management をアクティブにする](activate-service.md)」に戻ります。

<!--HONumber=Apr16_HO3-->

