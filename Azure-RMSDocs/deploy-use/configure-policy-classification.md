---
title: "Azure Information Protection ラベルの条件を構成する"
description: "ラベルの条件を構成するときに、ドキュメントまたは電子メールにラベルを自動的に割り当てることができます。 または、自分が推奨するラベルを選択するようにユーザーに求めることもできます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
ms.openlocfilehash: aa41d4f34f0ed43682f9ba426ec18204457980c3
ms.sourcegitcommit: 2f1936753adf8d2fbea780d0a3878afa621daab5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/18/2017
---
# <a name="how-to-configure-conditions-for-automatic-and-recommended-classification-for-azure-information-protection"></a>Azure Information Protection 用の自動および推奨分類の条件を構成する方法

>*適用対象: Azure Information Protection*

ラベルの条件を構成するときに、ドキュメントまたは電子メールにラベルを自動的に割り当てることができます。 または、自分が推奨するラベルを選択するようにユーザーに求めることもできます。 

- 自動分類は、Word、Excel、および PowerPoint でファイルが保存されるときと、Outlook で電子メールが送信されるときに適用されます。 既に手動でラベル付けされているファイルに対して自動分類を使用することはできません。
 
- 推奨分類は、Word、Excel、および PowerPoint でファイルが保存されるときに適用されます。

条件を構成するときには、**クレジット カード番号**や**米国社会保障番号 (SSN)** などの定義済みのパターンを使用できます。 または、自動分類の条件として、ユーザー指定の文字列またはパターンを定義することもできます。 これらの条件は、ドキュメントや電子メールの本文とヘッダーおよびフッターに適用されます。 条件の詳細については、[次の手順](#to-configure-recommended-or-automatic-classification-for-a-label)の手順 5 をご覧ください。

複数のラベルへの適用時の複数条件の評価方法:

1. ラベルは、ポリシーに指定した位置に従って評価の順序が決まります。先頭に配置されたラベルが最下位 (秘密度が最も低い) になり、最後に配置されたラベルが最上位 (秘密度が最も高い) ものになります。

2. 最も秘密度の高いラベルが適用されます。
 
3. 最後のサブラベルが適用されます。

> [!TIP]
>最良のユーザー エクスペリエンスとビジネスの継続性を確保するために、自動分類ではなく、ユーザーが推奨する分類から始めることをお勧めします。 この構成の場合、ユーザーは、ラベル付けまたは保護操作を受け入れるか、それらの提案が自分のドキュメントまたは電子メール メッセージに適していない場合は無効にすることを選択できます。

ラベルを推奨される操作として適用するように条件を構成したときのプロンプトの例を、カスタム ポリシー ヒントと共に示します。

![Azure Information Protection の検出と推奨事項](../media/info-protect-recommend-calloutsv2.png)

この例では、ユーザーは **[今すぐ変更]** をクリックして推奨されたラベルを適用するか、**[閉じる]** を選択することでその推奨を無効にできます。

## <a name="to-configure-recommended-or-automatic-classification-for-a-label"></a>ラベルの推奨または自動分類を構成するには

1. [Azure Portal](https://portal.azure.com) にサインインしていない場合は、新しいブラウザー ウィンドウを開き、セキュリティ管理者または全体管理者としてサインインします。次に、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. 構成するラベルがすべてのユーザーに適用される場合は、**[Azure Information Protection - グローバル ポリシー]** ブレードのままにします。
    
    構成するラベルが[スコープ付きポリシー](configure-policy-scope.md)内にあり、選択したユーザーだけに適用される場合は、**[ポリシー]** メニューから **[スコープ付きポリシー]** を選びます。 その後、**[Azure Information Protection - スコープ付きポリシー]** ブレードからスコープ付きポリシーを選びます。

3. **[Azure Information Protection - グローバル ポリシー]** ブレードまたは **[ポリシー: \<名前>]** ブレードで、構成するラベルを選びます。 

4. **[ラベル]** ブレードで、**[Configure conditions for automatically applying this label]** (このラベルに自動的に適用する条件を構成する) セクションの **[新しい条件の追加]** をクリックします。

5. **[条件]** ブレードで、定義済みの条件を使用する場合は **[情報の種類]** を、独自の条件を指定する場合は **[カスタム]** を選択します。
    - **[情報の種類]** を選択した場合: 使用可能な条件の一覧から選択し、最小出現回数と、出現で出現回数に一意の値を含めるかどうかを選択します。
        
        情報の種類では、Office 365 データ損失防止 (DLP) の機密情報の種類とパターン検出が使われます。 多くの共通の機密情報の種類から選ぶことができ、これらの一部は異なるリージョンに固有です。 詳しくは、Office ドキュメントの「[What the sensitive information types look for](https://support.office.com/article/What-the-sensitive-information-types-look-for-fd505979-76be-4d9f-b459-abef3fc9e86b)」(検索される機密情報の種類) をご覧ください。 
        
        Azure Portal から選択できる情報の種類の一覧は、定期的に更新され、Office DLP の新しいデータが追加されます。 ただし、ルール パッケージとして定義され、Office 365 セキュリティ/コンプライアンス センターにアップロードされたユーザー設定の機密情報の種類は、一覧から除外されます。 
        
        Azure Information Protection は、選択された情報の種類を評価するとき、Office DLP 信頼レベルの設定を使わず、最も低い信頼度に従って一致させます。
    
    - **[カスタム]** を選択した場合: 一致させる名前とフレーズを指定します。引用符と特殊文字は除外する必要があります。 次に、正規表現として一致させるかどうか、大文字と小文字を区別するかどうか、最小出現回数、出現で出現回数に一意の値を含めるどうかを選択します。
        
        正規表現では、Office 365 の正規表現パターンが使用されます。 詳しくは、Office ドキュメントの「[Defining regular expression based matches](https://technet.microsoft.com/library/jj674702(v=exchg.150).aspx#Anchor_2)」(正規表現に基づく一致の定義) をご覧ください。
        
6. **[最小出現回数]** と **[一意の値のみを含む出現回数をカウント]** を変更する必要があるかどうかを決定し、**[保存]** を選択します。 
    
    出現オプションの例: 社会保障番号の情報タイプを選択し、最小出現回数として 2 を設定したときに、ドキュメントに同じ社会保障番号が 2 回記載されていたとします。**[一意の値のみを含む出現回数をカウント]** を **[オン]** に設定した場合、条件は満たされません。 このオプションを **[オフ]** に設定した場合、条件は満たされます。

7. **[ラベル]** ブレードで、次のように構成し、**[保存]** をクリックします。
    
    - 自動分類または推奨分類を選択します。**[Select how this label is applied: automatically or recommended to user]** (ラベルの適用方法を選択してください: 自動またはユーザーに推奨) で、**[自動]** または **[推奨]** を選択します。
    
    - ユーザー プロンプトまたはポリシー ヒント用のテキストを指定します。既定のテキストを維持するか、独自の文字列を指定します。

8. ユーザーが変更を使用できるようにするには、最初の **[Azure Information Protection]** ブレードで **[公開]** をクリックします。

## <a name="next-steps"></a>次のステップ

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


