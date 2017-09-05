---
title: "クイック スタート チュートリアルの手順 1 - AIP"
description: "Azure Information Protection を簡単に試すためのチュートリアルの手順 1 - Azure Rights Management サービスの有効化。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
ms.openlocfilehash: ac28e18573ec1bd8f0a3f1e715a8c8e1b7c2854e
ms.sourcegitcommit: 13e95906c24687eb281d43b403dcd080912c54ec
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2017
---
# <a name="step-1-activate-the-rights-management-service"></a>手順 1.Rights Management サービスの有効化
 
>*適用対象: Azure Information Protection*

> [!NOTE]
>既にテナントの Azure Rights Management サービスをアクティブ化してある場合でも、この手順を行ってアクティブ化の状態を確認します。 この手順には、手順 2 の準備として、Azure Portal へのサインインと、Azure Information Protection ブレードの作成が含まれます。 

Azure Rights Management サービスをアクティブ化すると、組織の最も機密性の高いドキュメントや電子メールを保護し、保護したドキュメントを他のユーザーと共有する際に使用する方法を追跡することができます。 Windows PowerShell の使用や、管理ポータルの使用など、このサービスをアクティブ化するにはさまざまな方法があります。

このチュートリアルでは Azure Portal を使い、そこでユーザーのラベルの構成も行います。 

## <a name="to-activate-the-azure-rights-management-service"></a>Azure Rights Management サービスをアクティブにするには

1. テナントの全体管理者またはセキュリティ管理者として [Azure Portal](https://portal.azure.com) にサインインします。

2. ハブ メニューで、**[新規]** をクリックし、**[MARKETPLACE]** リストから **[セキュリティ + ID]** を選択します。 
    
3.  **[セキュリティ + ID]** ブレードで、**[おすすめアプリ]** リストから **[Azure Information Protection]** を選びます。 次に、**[Azure Information Protection]** ブレードで **[作成]** をクリックします。
    
    **[Azure Information Protection]** ブレードが作成され、次にポータルにサインインするときに、ハブの **[その他のサービス]** リストからサービスを選択できるようになります。 
    
    > [!TIP] 
    > **[ダッシュボードにピン留めする]** を選択してダッシュボードの **[Azure Information Protection]** タイルを作成し、次にポータルにサインインするときにサービスの参照をスキップできるようにします。

4. サービスに最初に接続するときに自動的に開く **[クイック スタート]** ページに関する情報を確認します。 後でここに戻ることができます。 このチュートリアルでは、**[RMS の設定]** を選びます。  

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
