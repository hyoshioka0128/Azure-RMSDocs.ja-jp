---
title: クイック スタート チュートリアルの手順 1 - AIP
description: Azure Information Protection を簡単に試すためのチュートリアルの手順 1 - 保護サービスの有効化。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
ms.openlocfilehash: cfeed994bb23469694e906132e175aabf925290e
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="step-1-activate-protection"></a>手順 1: 保護の有効化します
 
>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
>テナントの Azure Rights Management サービスがアクティブになっている場合でも、この手順を行ってアクティブ化の状態を確認します。 この手順には、手順 2 の準備として、Azure Portal へのサインインと、Azure Information Protection ブレードの作成が含まれます。

Azure Rights Management サービスをアクティブ化すると、組織の最も機密性の高いドキュメントや電子メールを保護できます。 また、他のユーザーと共有するときに、これらの保護されたドキュメントがどのように使用されるかを追跡することもできます。 

保護をアクティブ化するには、さまざまな方法があります。 PowerShell と管理ポータルを使用することができます。 ただし、このチュートリアルでは、Azure Portal を使い、そこでユーザーのラベルの構成も行います。 

## <a name="to-activate-the-azure-rights-management-service"></a>Azure Rights Management サービスをアクティブにするには

1. テナントのグローバル管理者アカウントを使用して、[Azure Portal](https://portal.azure.com) にサインインします。 
    
    グローバル管理者でない場合は、**Information Protection 管理者**または**セキュリティ管理者**のいずれかの[管理者ロール](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)を使用できます。

2. ハブ メニューで、**[リソースの作成]** をクリックして、**[MARKETPLACE]** リストから **[セキュリティ + ID]** を選択します。 
    
3.  **[セキュリティ + ID]** ブレードで、**[おすすめアプリ]** リストから **[Azure Information Protection]** を選びます。 次に、**[Azure Information Protection]** ブレードで **[作成]** をクリックします。
    
    このアクションでは **[Azure Information Protection]** ブレードが作成され、次にポータルにサインインするときに、ハブの **[すべてのサービス]** リストからサービスを選択できるようになります。 
    
    > [!TIP] 
    > **[ダッシュボードにピン留めする]** を選択してダッシュボードの **[Azure Information Protection]** タイルを作成し、次にポータルにサインインするときにサービスの参照をスキップできるようにします。

4. サービスに最初に接続するときに自動的に開く **[クイック スタート]** ページに関する情報を確認します。 後でここに戻ることができます。 このチュートリアルでは、**[Protection activation]\(保護のアクティブ化\)** を選択します。 

5. Azure Rights Management サービスがテナントでアクティブかどうかを確認できます。 
    
    - サービスがアクティブの場合、次の確認情報が表示されます。
        
        ![Azure RMS での Azure Information Protection の状態](../media/info-protect-azurerms-activated.png)
        
    - サービスがアクティブでない場合は、状態情報でそのことが示され、アクティブ化するオプションが表示されます。
        
        ![Azure RMS での Azure Information Protection の状態](../media/info-protect-azurerms-deactivated.png)

6. サービスがアクティブになっていない場合は、**[アクティブ化]** を選びます。 

    アクティブ化が完了すると、情報バーに **[Activation finished successfully]\(アクティブ化が正常に完了しました\)** と表示されます。

これで、このチュートリアルを完了するための最初の手順に必要な操作は終わりました。 これで手順 2 に進むことができます。

|必要な詳細情報|追加情報|
|--------------------------------|--------------------------|
|Rights Management のアクティブ化について|[Azure Rights Management をアクティブにする](../deploy-use/activate-service.md)|


>[!div class="step-by-step"]
[&#171; 概要](infoprotect-quick-start-tutorial.md)
[手順 2 &#187;](infoprotect-tutorial-step2.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
