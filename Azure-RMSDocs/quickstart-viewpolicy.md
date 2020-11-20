---
title: クイック スタート - Azure portal で Azure Information Protection (AIP) を表示する
description: 組織で初めて Azure Information Protection (AIP) を使用する場合は、このクイック スタートから開始して、サービスを Azure portal に追加し、保護サービスがアクティブになっていることを確認して、ラベルとポリシー設定を公開します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/19/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: b0128abb8d75418596459ac142a49dbbfa06b646
ms.sourcegitcommit: df6ee1aca02e089e3a72006ecf0747f14213979c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2020
ms.locfileid: "94503623"
---
# <a name="quickstart-get-started-with-azure-information-protection-in-the-azure-portal"></a>クイック スタート:Azure portal で Azure Information Protection の使用を開始する

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順:[Windows 用 Azure Information Protection クラシック クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

このクイック スタートでは、Azure portal に Azure Information Protection を追加し、この保護サービスがアクティブ化されていることを確認し、ラベルがまだ用意されていなければ既定のラベルを作成し、Azure Information Protection クライアント (クラシック) のポリシー設定を表示します。

**必要な時間:** このクイック スタートは 10 分もかからずに終了できます。

## <a name="prerequisites"></a>前提条件

このクイック スタートを完了するには、次のものが必要です。

- [**Azure portal**](https://portal.azure.com/) アカウントへのアクセス。

- [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/) を含むサブスクリプション。

    このようないずれかのサブスクリプションがない場合は、組織用の[無料](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)アカウントを作成できます。

Azure Information Protection を使用するための必要条件の完全な一覧については、「[Azure Information Protection の要件](requirements.md)」をご覧ください。

## <a name="add-azure-information-protection-to-the-azure-portal"></a>Azure portal に Azure Information Protection を追加する

[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/) を含むサブスクリプションをお持ちの場合でも、Azure portal で AIP が自動的に使用できるようにはなりません。

次の手順を実行して、Azure portal に AIP を追加してください。

1. テナントのグローバル管理者アカウントを使用して、[Azure Portal](https://portal.azure.com) にサインインします。

    グローバル管理者でない場合は、次のリンクを使用して別のロールにします:「[Azure portal にサインインする](configure-policy.md#signing-in-to-the-azure-portal)」

1. **[+ リソースの作成]** を選択します。 Marketplace の検索ボックスに「**Azure Information Protection**」と入力して、それを選択します。 [Azure Information Protection] ページで、 **[作成]** を選択し、もう一度 **[作成]** を選択します。

    :::image type="content" source="media/gifs/quickstart-add-aip-to-portal.gif" alt-text="Azure portal に Azure Information Protection を追加する":::

    > [!TIP]
    > この手順を初めて実行する場合は、ペインの名前の横に **[ダッシュボードにピン留めする]** ![[ダッシュボードにピン留めする] アイコン](media/qs-tutor/pin-to-dashboard.png "ダッシュボードにピン留めするアイコン") アイコンが表示されます。 選択すると、ダッシュボード上にタイルを作成して、次回から直接移動できるようになります。

## <a name="confirm-that-the-protection-service-is-activated"></a>保護サービスがアクティブになっていることを確認する

保護サービスは、新しいお客様に対して自動的にアクティブ化されるようになりました。 次の操作を行い、アクティブになっていることを今すぐ、または後で確認してください。

1. **[Azure Information Protection]** ペインで、 **[管理]**  >  **[保護のアクティブ化]** を選択します。

1. テナントの保護がアクティブになっているかどうかを確認します。 次に例を示します。

    :::image type="content" source="media/qs-tutor/confirm-activation.PNG" alt-text="AIP のアクティブ化を確認する":::

    どの時点でも、保護がアクティブになっておらず、アクティブにする必要がある場合は、 **[アクティブ化]** ![AIP のアクティブ化](media/qs-tutor/activate.png "AIP のアクティブ化") を選択します。 アクティブ化が完了すると、情報バーに **[Activation finished successfully]\(アクティブ化が正常に完了しました\)** と表示されます。

## <a name="create-and-publish-labels"></a>ラベルの作成と公開

お客様の組織に既にラベルが存在している場合があります。これは、お客様のテナント用のラベルが自動的に作成されていたため、または、Office 365 セキュリティ & コンプライアンス センター、Microsoft セキュリティ センター、または Microsoft コンプライアンス センターのラベルが存在するためです。 では、始めましょう。

1. **[分類]** の下で、 **[ラベル]** を選択します。

    既定のラベルが既に作成されている場合があります。 次の図は、Azure Information Protection により既定で作成されるラベルを示しています。

    :::image type="content" source="media/info-protect-defaultlabels.png" alt-text="Azure Information Protection の既定のラベル":::

    **既定のラベル、またはいずれのラベルも表示されない場合**:

    既定のラベル、またはいずれのラベルも表示されない場合は、 **[既定のラベルの生成]** を選択し、クラシック クライアントで使用するために作成します。

    グリッドの上に **[既定のラベルの生成]** ボタンが表示されない場合は、 **[管理]** の下で **[統合ラベル付け]** を選択します。 [統合ラベル付け] の状態が **[アクティブ化されていません]** になっている場合は、 **[アクティブ化]** を選択してから、 **[分類]**  >  **[ラベル]** ペインに戻ります。

    > [!NOTE]
    > 統合ラベル付けクライアントの場合、ラベルは Microsoft M365 で管理されます。 詳細については、[機密ラベルの暗号化を使用したコンテンツへのアクセスの制限](/microsoft-365/compliance/encryption-sensitivity-labels)に関する記事をご覧ください。
    >

1. Azure portal でラベルを公開し、Azure Information Protection クラシック クライアントで使用できるようにします。

    1. **[グローバル]** ポリシーを開きます。 **[分類]** の下で、 **[ポリシー]**  >  **[グローバル]** の順に選択します。

    1. **[ラベルの追加または削除]** を選択します。

    1. **[ポリシー: ラベルの追加または削除]** ペインで、すべてのラベルを選択し、 **[OK]** を選択します。

    1. **[ポリシー:グローバル] ペイン** に戻り、 **[保存]** ![保存](media/qs-tutor/save-icon.png "[保存]") ボタンを選択します。

        プロンプトで **[OK]** をクリックして、加えた変更を公開します。

## <a name="view-your-labels"></a>ラベルを表示する

次は、ラベルについて詳しく見てみましょう。

**[グローバル]** ポリシーをまだ開いている場合は、右上にある **[X]** をクリックしてペインを閉じてください。 **[分類]** の下で、 **[ラベル]** を選択します。

Azure Information Protection の既定の分類ラベルは次のとおりです。

- **個人用**
- **全般**
- **社外秘**
- **極秘**

既定で、一部のラベルには既に視覚的なマーキングが構成されています。 これらの視覚的なマーキングには、フッター、ヘッダー、透かしなどがあります。 他のラベルにも保護が構成されています。

ラベルを選択して参照すると、そのラベルの詳細な構成が表示されます。

> [!TIP]
> **[極秘]** ラベルを展開すると、分類にサブカテゴリがある例を確認できます。
>

## <a name="view-your-policy-settings"></a>ポリシー設定を表示する

Azure portal から初めて Azure Information Protection サービスに接続すると、Azure Information Protection クライアントによって使用される既定のポリシー設定が常に自動的に作成されます。

- **クラシック クライアント。** クラシック クライアントに対して、ラベルとポリシー設定の両方がクライアントの Azure Information Protection ポリシー内にダウンロードされます。

- **統合ラベル付けクライアント。** 統合ラベル付けクライアントに対しては、ラベルのみがクライアントにダウンロードされます。 Office 365 コンプライアンス & セキュリティ センター、Microsoft 365 コンプライアンス センター、または Microsoft 365 セキュリティ センターからポリシー設定がダウンロードされます。 Azure portal の代わりに、これらの管理センターを使ってラベルとラベルのポリシーを編集します。

    詳細については、Microsoft 365 のドキュメントに含まれる「[秘密度ラベルの詳細](/microsoft-365/compliance/sensitivity-labels)」を参照してください。

**クラシック クライアントの手順:**

クラシック クライアント用の Azure Information Protection の既定のポリシー設定を表示するには:

1. **[分類]** の下で、 **[ポリシー]**  >  **[グローバル]** の順に選択して、お客様のテナントに対して作成された既定の Azure Information Protection ポリシー設定を表示します。

1. **[表示する設定を構成して、Information Protection のエンド ユーザーに適用する]** セクションで、ラベルの後にポリシー設定が表示されます。 たとえば、既定のラベル セットはなく、ドキュメントと電子メールはラベルが必須ではなく、ユーザーがラベルを変更するときに理由を示す必要はありません。

    :::image type="content" source="media/defaultsettings-aip.png" alt-text="Azure Information Protection ポリシーのグローバル設定":::

1. これで、ポータルで開いたすべてのペインを閉じることができます。

## <a name="next-steps"></a>次のステップ

次のステップは、クラシック クライアントと統合ラベル付けクライアントのどちらを使用するかによって異なります。 これらのクライアントの違いがわからない場合は、 こちらの [FAQ](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients) を参照してください。

**クラシック クライアントを使用している場合:**

- 次の手順として、以下のチュートリアルが役に立つ場合があります。[Azure Information Protection のポリシーの編集と新しいラベルの作成](infoprotect-quick-start-tutorial.md)。

- また、Azure Information Protection ポリシーのすべての要素を構成するための詳しい手順については、「[Azure Information Protection ポリシーの構成](configure-policy.md)」をご覧ください。

**統合ラベル付けクライアントを使用している場合:**

詳細については、Microsoft 365 のコンプライアンスに関するドキュメントの[「機密ラベルの詳細](/microsoft-365/compliance/sensitivity-labels)」を参照してください。