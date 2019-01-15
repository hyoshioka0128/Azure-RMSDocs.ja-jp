---
title: クイック スタート - Azure portal で Azure Information Protection の使用を開始する - AIP
description: 組織で初めて Azure Information Protection を使用する場合は、このクイック スタートから開始して、サービスを Azure portal に追加し、保護サービスがアクティブ化されていることを確認して、ポリシーを表示します。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/15/2018
ms.topic: quickstart
ms.service: information-protection
ms.openlocfilehash: c890d6acf2557093441a175bc8ed8657e8d1d9da
ms.sourcegitcommit: bc082cffaa698b89b28aef7034290553c26f667b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2018
ms.locfileid: "53411815"
---
# <a name="quickstart-get-started-with-azure-information-protection-in-the-azure-portal"></a>クイック スタート:Azure portal で Azure Information Protection の使用を開始する

このクイック スタートでは、Azure Information Protection を Azure portal に追加し、保護サービスがアクティブ化されていることを確認して、組織の既定のポリシーを表示します。 

このクイック スタートは 5 分で完了します。

## <a name="prerequisites"></a>必要条件

このクイック スタートを完了するには、次の要件があります。

- Azure Information Protection プラン 1 またはプラン 2 を含むサブスクリプション。
    
    このようないずれかのサブスクリプションがない場合は、組織用の[無料](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)アカウントを作成できます。

Azure Information Protection を使用するための必要条件の完全な一覧については、「[Azure Information Protection の要件](requirements.md)」をご覧ください。

## <a name="add-azure-information-protection-to-the-azure-portal"></a>Azure portal に Azure Information Protection を追加する

Azure Information Protection は、Azure portal で自動的に使用可能になるわけではありません。 このサービスを追加する必要があります。

1. テナントのグローバル管理者アカウントを使用して、[Azure Portal](https://portal.azure.com) にサインインします。 
    
    グローバル管理者でない場合は、次のリンクを使用して別のロールにします:「[Azure portal にサインインする](configure-policy.md#signing-in-to-the-azure-portal)」

2. ハブ メニューで **[リソースの作成]** を選択し、Marketplace の検索ボックスに **Azure Information Protection** と入力します。 
    
3. 結果一覧から **[Azure Information Protection]** を選択します。 次に、**[Azure Information Protection]** ブレードで **[作成]** をクリックします。
    
    > [!TIP] 
    > 必要に応じて、**[ダッシュボードにピン留めする]** を選択してダッシュボードの **[Azure Information Protection]** タイルを作成し、次にポータルにサインインするときにサービスの参照をスキップできるようにします。
    
    再び **[作成]** をクリックします。

## <a name="confirm-the-protection-service-is-activated"></a>保護サービスがアクティブ化されていることを確認する

保護サービスは新しいテナントに対しては自動的にアクティブ化されますが、手動でアクティブ化する必要がないことを確認することをお勧めします。 

1. **[Azure Information Protection]** ブレードで、**[管理]** > **[保護のアクティブ化]** を選択します。

2. テナントの保護がアクティブかどうかを確認します。 
    
    - 保護がアクティブの場合、次の確認情報が表示されます。
        
        ![Azure RMS での Azure Information Protection の状態](./media/info-protect-azurerms-activated.png)
        
    - 保護がアクティブでない場合は、状態情報でそのことが示され、アクティブ化するオプションが表示されます。
        
        ![Azure RMS での Azure Information Protection の状態](./media/info-protect-azurerms-deactivated.png)

3. 保護がアクティブになっていない場合は、**[アクティブ化]** を選択します。 

    アクティブ化が完了すると、情報バーに **[Activation finished successfully]\(アクティブ化が正常に完了しました\)** と表示されます。

## <a name="view-your-organizations-default-policy---labels-and-policy-settings"></a>組織の既定のポリシーを表示する - ラベルとポリシー設定

Azure portal を使用して Azure Information Protection サービスに初めて接続すると、テナントの既定のポリシーが作成されます。 既定のポリシーには、そのまま使用可能な、またはカスタマイズ可能なラベルと設定が含まれています。

1. **[分類]** > **[ポリシー]** > **[グローバル]** を選択して、テナントに対して作成された既定の Azure Information Protection ポリシーを表示します。
    
2. 表示されるラベルをよく理解しておいてください。
    
    - 分類用のラベル:**[個人用]**、**[公開]**、**[全般]**、**[社外秘]**、**[非常に機密性の高い社外秘]**。 最後の 2 つのラベルを展開するとサブラベルが表示されます。これは、分類にサブカテゴリを設定できることを示す例となります。
    
    - 既定の構成では、一部のラベルには視覚的なマーキングが構成されていることに注意してください。 視覚的なマーカーとは、フッター、ヘッダー、および透かしです。 既定のポリシーによっては、一部のラベルに保護が設定されていることもあります。 次に例を示します。 
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - 既定ポリシー](./media/info-protect-policy-default-labelsv2.png)
    
3. ラベルの後、**[表示する設定を構成して、Information Protection のエンド ユーザーに適用する]** セクションに、ポリシー設定の一部も表示されます。 たとえば、既定のラベル セットはなく、ドキュメントと電子メールはラベルが必須ではなく、ユーザーがラベルを変更するときに理由を示す必要はありません。
    
    ![Azure Information Protection クイック スタート チュートリアル手順 3 - 既定ポリシー](./media/info-protect-policy-default-settings-quickstart.png) 

4. 表示しているのはラベルと設定のみであるため、開いたブレードを閉じてもかまいません。

## <a name="next-steps"></a>次の手順

ラベルとポリシー設定を Azure portal で確認したので、次のことに関するチュートリアルが次の手順として役立ちます:[Azure Information Protection のポリシーの編集と新しいラベルの作成](infoprotect-quick-start-tutorial.md)。

また、Azure Information Protection ポリシーのすべての要素を構成するための詳しい手順については、「[Azure Information Protection ポリシーの構成](configure-policy.md)」をご覧ください。
