---
title: クイック スタート - Azure portal で Azure Information Protection を表示する - AIP
description: 組織で初めて Azure Information Protection を使用する場合は、このクイック スタートから開始して、サービスを Azure portal に追加し、この保護サービスがアクティブ化されていることを確認して、ラベルとポリシー設定を公開します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/01/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: d48061cda0d13ad04dc05dbd5d260a56dec60166
ms.sourcegitcommit: d939dd4191965f68a5e59e13ed612e40bfa28556
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71712568"
---
# <a name="quickstart-get-started-with-azure-information-protection-in-the-azure-portal"></a>クイック スタート:Azure portal で Azure Information Protection の使用を開始する

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

このクイック スタートでは、Azure portal に Azure Information Protection を追加し、この保護サービスがアクティブ化されていることを確認し、ラベルがまだ用意されていなければ既定のラベルを作成し、Azure Information Protection クライアント (クラシック) のポリシー設定を表示します。

このクイック スタートは 10 分もかからずに終了できます。

## <a name="prerequisites"></a>必要条件

このクイック スタートを完了するには、次の要件があります。

- Azure Information Protection プラン 1 またはプラン 2 を含むサブスクリプション。
    
    このようないずれかのサブスクリプションがない場合は、組織用の[無料](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)アカウントを作成できます。

Azure Information Protection を使用するための必要条件の完全な一覧については、「[Azure Information Protection の要件](requirements.md)」をご覧ください。

## <a name="add-azure-information-protection-to-the-azure-portal"></a>Azure portal に Azure Information Protection を追加する

Azure Information Protection は、Azure portal で自動的に使用可能になるわけではありません。 このサービスを追加する必要があります。

1. テナントのグローバル管理者アカウントを使用して、[Azure Portal](https://portal.azure.com) にサインインします。 
    
    グローバル管理者でない場合は、次のリンクを使用して別のロールにします:「[Azure portal にサインインする](configure-policy.md#signing-in-to-the-azure-portal)」

2. ハブ メニューで **[リソースの作成]** を選択し、Marketplace の検索ボックスに **Azure Information Protection** と入力します。 
    
3. 結果一覧から **[Azure Information Protection]** を選択します。 次に、 **[Azure Information Protection]** ブレードで **[作成]** をクリックします。
    
    > [!TIP] 
    > 必要に応じて、 **[ダッシュボードにピン留めする]** を選択してダッシュボードの **[Azure Information Protection]** タイルを作成し、次にポータルにサインインするときにサービスの参照をスキップできるようにします。
    
    再び **[作成]** をクリックします。

## <a name="confirm-the-protection-service-is-activated"></a>保護サービスがアクティブ化されていることを確認する

この保護サービスは、新しいお客様に対しては自動的にアクティブ化されるようになっていますが、手動でアクティブ化する必要がないことを確認しておくことをお勧めします。 

1. **[Azure Information Protection]** ブレードで、 **[管理]**  >  **[保護のアクティブ化]** を選択します。

2. テナントの保護がアクティブかどうかを確認します。 
    
    - 保護がアクティブの場合、次の確認情報が表示されます。
        
        ![Azure RMS での Azure Information Protection の状態 - アクティブ](./media/info-protect-azurerms-activated.png)
        
    - 保護がアクティブでない場合は、状態情報でそのことが示され、アクティブ化するオプションが表示されます。
        
        ![Azure RMS での Azure Information Protection の状態 - 非アクティブ](./media/info-protect-azurerms-deactivated.png)

3. 保護がアクティブになっていない場合は、 **[アクティブ化]** を選択します。 

    アクティブ化が完了すると、情報バーに **[Activation finished successfully]\(アクティブ化が正常に完了しました\)** と表示されます。

## <a name="create-and-publish-labels"></a>ラベルの作成と公開

お客様の組織に既にラベルが存在している場合があります。これは、お客様のテナント用のラベルが自動的に作成されていたため、または、Office 365 セキュリティ & コンプライアンス センター、Microsoft セキュリティ センター、または Microsoft コンプライアンス センターのラベルが存在するためです。 では、始めましょう。

1. **[分類]**  >  **[ラベル]** を選択します。
    
    **[既定のラベルの生成]** オプションが表示される場合は、ラベルはまだ存在していません。
    
     ![Azure Information Protection の既定のラベルなし](./media/info-protect-nodefaultlabels.png)
    
    既定のラベルを生成するこのオプションが表示されない場合は、既にラベルが存在しています。それは、次の図に示すような Azure Information Protection の既定のラベルである可能性があります。
    
    ![Azure Information Protection の既定のラベルあり](./media/info-protect-defaultlabels.png)

2. ラベルが存在しない場合は、 **[既定のラベルの生成]** オプションを選択します。

4. すべてのユーザーに対してラベルを公開するには、 **[分類]**  >  **[ポリシー]**  >  **[グローバル]** で次の操作を行います。
    
    」を参照します。 **[ラベルの追加または削除]** を選択します。
    
    b. **[ポリシー: ラベルの追加または削除]** ブレードで、すべてのラベルを選択し、 **[OK]** を選択します。
    
    c. **[ポリシー:グローバル]** ブレードに戻り、 **[保存]** を選択します。

Azure portal でラベルを公開すると、Azure Information Protection クライアント (クラシック) でそれらを使用できるようになります。

## <a name="view-your-labels"></a>ラベルを表示する

**[分類]**  >  **[ラベル]** を選択し、少し時間を割いて **[Azure Information Protection - ラベル]** ブレードに表示されるラベルをよく理解しておきます。

それが前のセクションの図で示されたラベルに似ていない場合、お客様が使用しているのは Azure Information Protection の既定のラベルではなく、おそらく Office 365 セキュリティ/コンプライアンス センターか、Microsoft 365 セキュリティ センター、または Microsoft 365 コンプライアンス センターで作成されたラベルです。

> [!TIP]
> カスタム ラベルを使用したくない場合は、Azure Information Protection の既定のラベルを代わりに使用してください。 
> - カスタム ラベルを削除すると、[前のセクション](#create-and-publish-labels)で説明したように、 **[ラベル]** ブレードに既定のラベルを生成するオプションが表示されます。 

**[Azure Information Protection - ラベル]** ブレードでは:

- 分類用のラベルは、 **[Personal (個人)]** 、 **[Public (公開)]** 、 **[General (全般)]** 、 **[Confidential (社外秘)]** 、 **[Highly Confidential (非常に機密性の高い社外秘)]** です。 最後の 2 つのラベルを展開するとサブラベルが表示されます。これは、分類にサブカテゴリを設定できることを示す例となります。

- **[マーキング]** 列と **[保護]** 列から、一部のラベルには視覚的なマーカーが構成されていることを確認できます。 視覚的なマーカーとは、フッター、ヘッダー、および透かしです。 一部のラベルには、保護も設定されています。 

次に例を示します。 

![Azure Information Protection の既定のラベルのクイック スタートの概要](./media/info-protect-policy-default-labelsv2.png)

ラベルを選択すると、そのラベル構成の詳細が新しいブレードに表示されます。

## <a name="view-your-policy-settings"></a>ポリシー設定を表示する

Azure portal を使用して Azure Information Protection サービスに初めて接続するときに、Azure Information Protection クライアント (クラシック) によって使用される既定のポリシー設定が常に自動的に作成されます。 クラシック クライアントに対して、ポリシー設定と前述のラベルがクライアントの Azure Information Protection ポリシー内にダウンロードされます。

Azure Information Protection の統合ラベル付けクライアントを使用している場合、このクライアントではこれらのポリシー設定は使用されません。 代わりに、このクライアントには同じラベルがダウンロードされますが、Office 365 コンプライアンス & セキュリティ センター、Microsoft 365 コンプライアンス センター、または Microsoft 365 セキュリティ センターからのものとは異なるポリシー設定がダウンロードされます。 Azure portal の代わりに、これらの管理センターを使ってラベルとラベルのポリシーを編集します。

クラシック クライアント用の Azure Information Protection の既定のポリシー設定を表示するには:

1. **[分類]**  >  **[ポリシー]**  >  **[グローバル]** を選択して、お客様のテナントに対して作成された既定の Azure Information Protection ポリシー設定を表示します。
    
2. **[表示する設定を構成して、Information Protection のエンド ユーザーに適用する]** セクションで、ラベルの後ろにポリシー設定が表示されます。 たとえば、既定のラベル セットはなく、ドキュメントと電子メールはラベルが必須ではなく、ユーザーがラベルを変更するときに理由を示す必要はありません。
    
    ![Azure Information Protection ポリシーのグローバル設定](./media/defaultsettings-aip.png)

3. これで、ポータルで開いたすべてのブレードを閉じることができます。

## <a name="next-steps"></a>次の手順

クラシック クライアントを使用している場合:

- 次の手順として、以下のチュートリアルが役に立つ場合があります。[Azure Information Protection のポリシーの編集と新しいラベルの作成](infoprotect-quick-start-tutorial.md)。
- また、Azure Information Protection ポリシーのすべての要素を構成するための詳しい手順については、「[Azure Information Protection ポリシーの構成](configure-policy.md)」をご覧ください。

統合ラベル付けクライアントを使用している場合:

- Office ドキュメントの「[機密ラベルの概要](/microsoft-365/compliance/sensitivity-labels)」をご覧ください。

これらのクライアントの違いがわからない場合は、 こちらの [FAQ](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client) を参照してください。
