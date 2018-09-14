---
title: クイック スタート チュートリアルの手順 1 - AIP
description: Azure Information Protection を簡単に試すためのチュートリアルの手順 1 - 保護サービスの有効化。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/28/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
ms.openlocfilehash: 82a3f71a4c1bb99fc4d0af74f49dd43a706cb132
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2018
ms.locfileid: "44147697"
---
# <a name="step-1-activate-protection"></a>手順 1: 保護の有効化します
 
>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
>テナントの保護がアクティブになっている場合でも、この手順を行ってアクティブ化の状態を確認します。 この手順には、手順 2 の準備として、Azure Portal へのサインインと、Azure Information Protection ブレードの作成が含まれます。

Azure Information Protection に対して保護をアクティブ化すると、組織の最も機密性の高いドキュメントや電子メールを保護できます。 また、他のユーザーと共有するときに、これらの保護されたドキュメントがどのように使用されるかを追跡することもできます。 

保護をアクティブ化するには、さまざまな方法があります。 PowerShell と管理ポータルを使用することができます。 ただし、このチュートリアルでは、Azure Portal を使い、そこでユーザーのラベルの構成も行います。 

## <a name="to-activate-protection"></a>保護をアクティブにするには

1. テナントのグローバル管理者アカウントを使用して、[Azure Portal](https://portal.azure.com) にサインインします。 
    
    グローバル管理者でない場合は、**Information Protection 管理者**または**セキュリティ管理者**のいずれかの[管理者ロール](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)を使用できます。

2. ハブ メニューで **[リソースの作成]** を選択し、Marketplace の検索ボックスに **Azure Information Protection** と入力します。 
    
3. 結果一覧から **[Azure Information Protection]** を選択します。 **[Azure Information Protection]** ブレードで **[作成]** をクリックします。
    
    > [!TIP] 
    > 必要に応じて、**[ダッシュボードにピン留めする]** を選択してダッシュボードの **[Azure Information Protection]** タイルを作成し、次にポータルにサインインするときにサービスの参照をスキップできるようにします。
    
    再び **[作成]** をクリックします。

4. サービスに最初に接続するときに自動的に開く **[クイック スタート]** ページに関する情報を確認します。 後でここに戻ることができます。 このチュートリアルでは、**[管理]** > **[保護のアクティブ化]** を選択します。 

5. これで、テナントの保護がアクティブかどうかが表示されます。 
    
    - 保護がアクティブの場合、次の確認情報が表示されます。
        
        ![Azure RMS での Azure Information Protection の状態](./media/info-protect-azurerms-activated.png)
        
    - 保護がアクティブでない場合は、状態情報でそのことが示され、アクティブ化するオプションが表示されます。
        
        ![Azure RMS での Azure Information Protection の状態](./media/info-protect-azurerms-deactivated.png)

6. 保護がアクティブになっていない場合は、**[アクティブ化]** を選択します。 

    アクティブ化が完了すると、情報バーに **[Activation finished successfully]\(アクティブ化が正常に完了しました\)** と表示されます。

これで、このチュートリアルを完了するための最初の手順に必要な操作は終わりました。 これで手順 2 に進むことができます。

|必要な詳細情報|追加情報|
|--------------------------------|--------------------------|
|保護のアクティブ化について|[Azure Rights Management をアクティブにする](activate-service.md)|


>[!div class="step-by-step"]
[&#171; 概要](infoprotect-quick-start-tutorial.md)
[手順 2 &#187;](infoprotect-tutorial-step2.md)

