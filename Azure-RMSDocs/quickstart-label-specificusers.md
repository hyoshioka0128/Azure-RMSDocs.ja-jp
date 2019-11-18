---
title: クイック スタート - 特定のユーザー向けの新しい Azure Information Protection ラベル - AIP
description: スコープ付きポリシーを使用してユーザーのサブセットに向けたドキュメントや電子メールを分類する新しいラベルを作成および構成します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/28/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: fa0278f0171faee18594ea40f7ac6fee2d238eb9
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559118"
---
# <a name="quickstart-create-a-new-azure-information-protection-label-for-specific-users"></a>クイック スタート:特定のユーザー向けの新しい Azure Information Protection ラベルを作成する

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順:[Windows 用 Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

このクイック スタートでは、ドキュメントや電子メールを分類および保護するために特定のユーザーのみが表示して適用できる、新しい Azure Information Protection ラベルを作成します。

この構成では、スコープ付きポリシーを使用します。

この構成は 10 分未満で完了します。

## <a name="prerequisites"></a>必要条件

このクイック スタートを完了するには、次の要件があります。

1. Azure Information Protection プラン 1 またはプラン 2 を含むサブスクリプション。
    
    このようないずれかのサブスクリプションがない場合は、組織用の[無料](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)アカウントを作成できます。

2. Azure portal に [Azure Information Protection] ペインを追加し、保護サービスがアクティブになっていることを確認した。

    これらの操作に関するサポートが必要な場合は、[Azure portal での作業の開始](quickstart-viewpolicy.md)に関するページをご覧ください。

3. 新しいラベルを表示および適用するユーザーを含む、Azure AD の電子メールが有効なグループ。
    
    適切なグループがない場合は、"**営業チーム**" という名前のグループを作成し、少なくとも 1 人のユーザーを追加します。

4. 新しいラベルをテストする場合:Windows コンピューターに Azure Information Protection クライアント (クラシック) がインストールされている必要があります。 
    
    クラシック クライアントをインストールするには、[Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)に移動し、Azure Information Protection ページから **AzInfoProtection.exe** をダウンロードします。
     
    クラシック クライアントとは別のラベル付けクライアントを使用している場合は、このチュートリアルと同等の手順について Office ドキュメントを参照してください。 たとえば、「[機密ラベルの概要](/microsoft-365/compliance/sensitivity-labels)」です。

Azure Information Protection を使用するための必要条件の完全な一覧については、「[Azure Information Protection の要件](requirements.md)」をご覧ください。
    
## <a name="create-a-new-label"></a>新しいラベルの作成

最初に、新しいラベルを作成します。

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure portal](configure-policy.md#signing-in-to-the-azure-portal) にサインインします。 次に、 **[Azure Information Protection]** ペインに移動します。
    
    たとえば、リソース、サービス、ドキュメントの検索ボックスで次のようにします: 「**Information**」と入力し、 **[Azure Information Protection]** を選択します。
    
    グローバル管理者でない場合は、次のリンクを使用して別のロールにします:「[Azure portal にサインインする](configure-policy.md#signing-in-to-the-azure-portal)」

2. **[分類]**  >  **[ラベル]** メニュー オプションから: **[Azure Information Protection - ラベル]** ペインで、 **[新しいラベルの追加]** をクリックします。

3. **[ラベル]** ペインで、少なくとも以下の項目を指定します。
    
    - **[ラベルの表示名]** :ユーザーに表示されるラベルの名前。これによりコンテンツの分類を識別します。 たとえば、`Sales - Restricted` と指定します。
    
    - **説明**:ユーザーがこの新しいラベルを選択するタイミングを識別するために役立つヒント。 例: `Business data that is restricted to the Sales Team.`

4. **[有効化]** が **[オン]** (既定値) に設定されていることを確認し、 **[保存]** を選択します。

## <a name="add-the-label-to-a-new-scoped-policy"></a>新しいスコープ付きポリシーにラベルを追加する

次に、新しく作成したラベルを新しいスコープ付きポリシーに追加します。

1. **[分類]**  >  **[ポリシー]** メニュー オプションから: **[Azure Information Protection - ポリシー]** ペインで、 **[新しいポリシーの追加]** を選択します。 

2. **[ポリシー]** ペインの **[ポリシー名]** ボックスに、新しく作成したラベルを表示するユーザー グループを識別する名前を入力します。 たとえば、`Sales` のように指定します。

3. **[このポリシーを取得するユーザーまたはグループを選択してください]** オプションを選択します。

4. **[AAD ユーザーとグループ]** ペインで、 **[ユーザー/グループ]** を選択します。 次に、新しい **[ユーザー/グループ]** ペインで、必要条件で特定したグループを検索して選択します。 たとえば、"**営業チーム**" を選択します。 ペインの **[選択]** をクリックし、 **[OK]** をクリックします。

5. **[ポリシー]** ペインに戻り、 **[ラベルの追加または削除]** を選択します。

6. **[ポリシー: ラベルの追加または削除]** ペインで、作成したラベル ("**営業 - 制限付き**" など) を選択し、 **[OK]** を選択します。

7. **[ポリシー]** ペインに戻り、 **[保存]** を選択します。 

これで、指定したグループのメンバーだけに新しいラベルが公開されました。 

## <a name="test-your-new-label"></a>新しいラベルをテストする

このラベルをテストするには、少なくとも 2 台のコンピューターが必要です。Azure Information Protection クライアントでは、同じコンピューターにおける複数のユーザーの操作がサポートされていないためです。

 - 1 台目のコンピューターで、"営業チーム" グループのメンバーとしてサインインします。 Word を開いて、新しいラベルが表示されることを確認します。 Word が既に開いている場合は再起動して、ポリシーの更新を適用します。

- 2 台目のコンピューターで、"営業チーム" グループのメンバー以外のユーザーとしてサインインします。 Word を開いて、新しいラベルが表示されないことを確認します。 前述のとおり、Word が既に開いている場合は再起動します。

## <a name="clean-up-resources"></a>リソースをクリーンアップする

このラベルとスコープ付きポリシーを保持しない場合は、次の手順を実行します。

1. **[分類]**  >  **[ポリシー]** メニュー オプションから: **[Azure Information Protection - ポリシー]** ペインで、作成したスコープ付きポリシーのコンテキスト メニュー ( **...** ) を選択します。 たとえば、"**営業**" を選択します。

2. **[ポリシーの削除]** を選択し、確認を求められたら **[OK]** を選択します。

3. **[分類]**  >  **[ラベル]** メニュー オプションから: **[Azure Information Protection - ラベル]** ペインで、作成したラベルのコンテキスト メニュー ( **...** ) を選択します。  たとえば、"**営業 - 制限付き**" を選択します。

4.  **[このラベルを削除]** を選択し、確認を求められたら **[OK]** を選択します。


## <a name="next-steps"></a>次の手順

このクイック スタートには、特定のユーザー向けの新しいラベルをすばやく作成するための最低限のオプションが含まれています。 詳しい手順については、次の記事をご覧ください。

- [新しいラベルを作成する方法](configure-policy-new-label.md)

- [スコープ ポリシーを使用して特定のユーザーのポリシーを構成する方法](configure-policy-scope.md)

また、"営業チーム" のメンバーだけが開けるようにコンテンツを保護するラベルが必要な場合は、保護を適用するようにラベルを構成する必要があります。 手順については、「[Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)」をご覧ください。

