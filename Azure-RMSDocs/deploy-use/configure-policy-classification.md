---
title: "Azure Information Protection ラベルの条件を構成する"
description: "ラベルの条件を構成するときに、ドキュメントまたは電子メールにラベルを自動的に割り当てることができます。 または、自分が推奨するラベルを選択するようにユーザーに求めることもできます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
ms.openlocfilehash: 1c37f1b05126b8e8d9a5e64f033c503f27a8a1fc
ms.sourcegitcommit: a8140a7215c8704f34c247f602e1f12eb7b49aa2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2017
---
# <a name="how-to-configure-conditions-for-automatic-and-recommended-classification-for-azure-information-protection"></a>Azure Information Protection 用の自動および推奨分類の条件を構成する方法

>*適用対象: Azure Information Protection*

ラベルの条件を構成するときに、ドキュメントまたは電子メールにラベルを自動的に割り当てることができます。 または、自分が推奨するラベルを選択するようにユーザーに求めることもできます。 

これらの条件を構成するときには、**クレジット カード番号**や**米国社会保障番号 (SSN)** などの定義済みのパターンを使用できます。 または、自動分類の条件として、ユーザー指定の文字列またはパターンを定義することもできます。 これらの条件は、ドキュメントや電子メールの本文とヘッダーおよびフッターに適用されます。 条件の詳細については、[次の手順](#to-configure-recommended-or-automatic-classification-for-a-label)の手順 5 をご覧ください。

最良のユーザー エクスペリエンスとビジネスの継続性を確保するために、自動分類ではなく、ユーザーが推奨する分類から始めることをお勧めします。 この構成の場合、ユーザーは、分類や関連付けられている保護を受け入れるか、それらの提案が自分のドキュメントまたは電子メール メッセージに適していない場合は無効にすることを選択できます。

ラベルを推奨される操作として適用するように条件を構成したときのプロンプトの例を、カスタム ポリシー ヒントと共に示します。

![Azure Information Protection の検出と推奨事項](../media/info-protect-recommend-calloutsv2.png)

この例では、ユーザーは **[今すぐ変更]** をクリックして推奨されたラベルを適用するか、**[閉じる]** を選択することでその推奨を無効にできます。

> [!IMPORTANT]
>自動分類とユーザー定義のアクセス許可にはラベルを構成しないでください。 ユーザー定義のアクセス許可オプションは、アクセス許可を与える人をユーザーが指定できるという[保護設定](configure-policy-protection.md)となります。
>
>自動分類とユーザー定義のアクセス許可にラベルを構成すると、条件に対してコンテンツがチェックされ、ユーザー定義のアクセス許可設定は適用されません。 推奨されている分類とユーザー定義のアクセス許可を使用できます。

## <a name="how-automatic-or-recommended-labels-are-applied"></a>自動ラベルと推奨ラベルが適用されるしくみ

**Azure Information Protection クライアントの一般公開バージョンの場合:**

- 自動分類は、Word、Excel、PowerPoint でドキュメントが保存されるときと、Outlook で電子メールが送信されるときに適用されます。 
    
    以前に手動でラベルが付けられているか、以前に上位の分類で自動的にラベルが付けられているドキュメントと電子メールには自動分類を使用できません。 

- 推奨分類は、Word、Excel、および PowerPoint でドキュメントが保存されるときに適用されます。 Outlook の場合、推奨分類を使用できません。
    
    上位の分類の有無に関係なく、以前にラベルが付けられたドキュメントには推奨分類を使用できます。 


**Azure Information Protection クライアントの最新プレビュー バージョンの場合:**

- 自動分類は、Word、Excel、PowerPoint、Outlook に適用されます。 ドキュメントに対して、自動分類は[バックグラウンドで継続的に](#more-information-about-running-continuously)実行されます。 Outlook の場合、電子メールを送信すると、自動分類が実行されます。 
    
    以前に手動でラベルが付けられているか、以前に上位の分類で自動的にラベルが付けられているドキュメントには自動分類を使用できません。 例外は、OverrideLabel パラメーターをオンに設定して Azure Information Protection スキャナーを使用する場合です。

- 推奨分類は、Word、Excel、PowerPoint に適用されます。 これらのドキュメントに対して、推奨分類は[バックグラウンドで継続的に](#more-information-about-running-continuously)実行されます。 Outlook の場合、推奨分類を使用できません。
    
    上位の分類の有無に関係なく、以前にラベルが付けられたドキュメントには推奨分類を使用できます。 

#### <a name="more-information-about-running-continuously"></a>継続的実行に関する詳細

Azure Information Protection クライアントの現行プレビュー版は、ドキュメントに指定された条件規則を定期的にチェックします。 この動作により、SharePoint Online に格納されているドキュメントの自動分類/保護と推奨分類/保護が有効になります。 条件規則が既に実行されているため、大きなファイルもすばやく保存されます。 

条件規則がユーザーの入力と同時にリアルタイムで実行されることはありません。 ドキュメントが変更された場合、バックグラウンド タスクとして定期的に実行されます。 

### <a name="how-multiple-conditions-are-evaluated-when-they-apply-to-more-than-one-label"></a>複数のラベルに適用するときの複数の条件の評価方法

Azure Information Protection クライアントと現行プレビュー クライアントの一般公開バージョンの場合:

1. ラベルは、ポリシーに指定した位置に従って評価の順序が決まります。先頭に配置されたラベルが最下位 (秘密度が最も低い) になり、最後に配置されたラベルが最上位 (秘密度が最も高い) ものになります。

2. 最も秘密度の高いラベルが適用されます。
 
3. 最後のサブラベルが適用されます。


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

[Azure Information Protection スキャナー](deploy-aip-scanner.md)のデプロイについて検討します。このスキャナーは自動分類規則を利用し、ネットワーク共有やオンプレミス ファイル ストアのファイルを検出、分類、保護できます。  

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

