---
title: クイック スタート - 特定のユーザー向けの新しい Azure Information Protection ラベル - AIP
description: スコープ付きポリシーを使用してユーザーのサブセットに向けたドキュメントや電子メールを分類する新しいラベルを作成および構成します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/19/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: e706cd2ec04d60b1520839fb76c21105ebf95625
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97386306"
---
# <a name="quickstart-create-a-new-azure-information-protection-label-for-specific-users"></a>クイック スタート:特定のユーザー向けの新しい Azure Information Protection ラベルを作成する

>***適用対象**:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> ***関連する内容**:[Windows 用 Azure Information Protection クラシック クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE]
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure Portal の **Azure Information Protection のクラシック クライアント** と **ラベル管理** は、**2021 年 3 月 31 日** をもって **非推奨** になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

このクイック スタートでは、ドキュメントや電子メールを分類および保護するために特定のユーザーのみが表示して適用できる、新しい Azure Information Protection ラベルを作成します。

この構成では、スコープ付きポリシーを使用します。

**必要な時間**:この構成は 10 分未満で完了します。

## <a name="prerequisites"></a>必要条件

このクイック スタートを完了するには、次の要件があります。

|要件  |説明  |
|---------|---------|
|**サポート サブスクリプション**     |  [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/) を含むサブスクリプションが必要です。 </br></br>このようないずれかのサブスクリプションがない場合は、組織用の[無料](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)アカウントを作成できます。       |
|**Azure portal に AIP が追加されている**    |  Azure portal に [Azure Information Protection] ペインを追加し、保護サービスがアクティブになっていることを確認した。 </br></br>詳細については、「[クイック スタート: 作業の開始](quickstart-viewpolicy.md)に関するページをご覧ください。       |
|**Azure AD のメール受信が有効なグループ**     | 新しいラベルを表示および適用するユーザーが含まれた、Azure AD のメール受信が有効なグループが必要です。 </br></br>適切なグループがない場合は、"**営業チーム**" という名前のグループを作成し、少なくとも 1 人のユーザーを追加します。 |
|**クラシック クライアントがインストールされている**    |   新しいラベルをテストするには、使用するコンピューターにクラシック クライアントをインストールする必要があります。 </br></br>Azure Information Protection クラシック クライアントは、2021 年 3 月に非推奨となる予定です。 AIP クラシック クライアントをデプロイするには、サポート チケットを作成してダウンロード アクセスを取得します。  |
| | |

Azure Information Protection を使用するための必要条件の完全な一覧については、「[Azure Information Protection の要件](requirements.md)」をご覧ください。

## <a name="create-a-new-label"></a>新しいラベルの作成

最初に、新しいラベルを作成します。

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure portal](https://portal.azure.com) にサインインします。 次に、 **[Azure Information Protection]** ペインに移動します。

    たとえば、リソース、サービス、およびドキュメントの検索ボックスで、「**Information**」と入力を開始し、**Azure Information Protection** を選択します。

    グローバル管理者でない場合は、次のリンクを使用して別のロールにします:「[Azure portal にサインインする](configure-policy.md#signing-in-to-the-azure-portal)」

1. **[分類]** の下で、 **[ラベル]** を選択してから、 **[+ 新しいラベルの追加]** をクリックします。

1. **[ラベル]** ペインで、少なくとも以下のフィールドを指定します。

    |フィールド  |[説明]  |
    |---------|---------|
    |**ラベルの表示名**     |    ユーザーに表示されるラベルの名前。これによりコンテンツの分類を識別します。 </br>次に例を示します。「**営業 - 制限付き**」    |
    |**説明**     |   ユーザーがこの新しいラベルを選択するタイミングを識別するために役立つヒント。 </br> 次に例を示します。「**営業チームに制限されたビジネス データ。** 」     |
    | | | 

1. **[有効化]** が **[オン]** (既定値) に設定されていることを確認し、 **[保存]** ![保存](media/qs-tutor/save-icon.png "[保存]") を選択します。

    右上にある **[X]** を選択して、 **[新しいラベル]** ペインを閉じます。

## <a name="add-the-label-to-a-new-scoped-policy"></a>新しいスコープ付きポリシーにラベルを追加する

次に、新しく作成したラベルを新しいスコープ付きポリシーに追加します。

1. もう一度左側の **[分類]** の下で、 **[ポリシー]** を選択してから、 **[新しいポリシーの追加]** をクリックします。

1. **[ポリシー名]** フィールドに、新しいラベルが表示されるユーザーについて説明した、わかりやすい値を入力します。

    たとえば、"**営業**" を選択します。

1. **[このポリシーを取得するユーザーまたはグループを選択してください]** の行を選択して、 **[AAD ユーザーとグループ]** ペインを開きます。

1. **[AAD ユーザーとグループ]** ペインで、必要条件で特定したグループを検索して選択します ("**営業チーム**" など)。

    **[選択]** をクリックしてペインを閉じます。

1. **[ポリシー]** ペインに戻り、 **[ラベルの表示名]** の下にある **[ラベルの追加または削除]** をクリックします。

1. **[ポリシー: ラベルの追加または削除]** ペインで、作成したラベル ("**営業 - 制限付き**" など) を選択し、 **[OK]** を選択します。

1. **[ポリシー]** ペインに戻り、 **[保存]** ![保存](media/qs-tutor/save-icon.png "[保存]") を選択します。

これで、指定したグループのメンバーだけに新しいラベルが公開されました。

## <a name="test-your-new-label"></a>新しいラベルをテストする

このラベルをテストするには、少なくとも 2 台のコンピューターが必要です。Azure Information Protection クライアントでは、同じコンピューターにおける複数のユーザーの操作がサポートされていないためです。

- **1 台目のコンピューターで**、"営業チーム" グループのメンバーとしてサインインします。 Word を開いて、新しいラベルが表示されることを確認します。 Word が既に開いている場合は再起動して、ポリシーの更新を適用します。

- **2 台目のコンピューターで**、"営業チーム" グループのメンバー "*ではない*" ユーザーとしてサインインします。 Word を開いて、新しいラベルが表示されないことを確認します。 前述のとおり、Word が既に開いている場合は再起動します。

## <a name="clean-up-resources"></a>リソースをクリーンアップする

このラベルとスコープ付きポリシーを保持しない場合は、次の手順を実行します。

1. **[分類]**  >  **[ポリシー]** 領域から: **[Azure Information Protection - ポリシー]** ペインで、作成したスコープ付きポリシーのコンテキスト メニュー ( **...** ) を選択します。 たとえば、"**営業**" を選択します。

1. **[ポリシーの削除]** を選択し、確認を求められたら **[OK]** を選択します。

1. **[分類]**  >  **[ラベル]** 領域から: **[Azure Information Protection - ラベル]** ペインで、作成したラベルのコンテキスト メニュー ( **...** ) を選択します。  たとえば、"**営業 - 制限付き**" を選択します。

1. **[このラベルを削除]** を選択し、確認を求められたら **[OK]** を選択します。

## <a name="next-steps"></a>次のステップ

このクイック スタートには、クラシック クライアントを使用して特定のユーザー向けの新しいラベルをすばやく作成するための、最低限のオプションが含まれています。 詳しい手順については、次の記事をご覧ください。

- [新しいラベルを作成する方法](configure-policy-new-label.md)

- [スコープ ポリシーを使用して特定のユーザーのポリシーを構成する方法](configure-policy-scope.md)

また、"営業チーム" のメンバーだけが開けるようにコンテンツを保護するラベルが必要な場合は、保護を適用するようにラベルを構成する必要があります。 手順については、「[Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)」をご覧ください。
