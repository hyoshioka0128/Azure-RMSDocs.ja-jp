---
title: Azure Information Protection ポリシーに対するラベルの追加または削除 - AIP
description: すべてのユーザー用のグローバル ポリシーまたはユーザーのサブセット用のスコープ ポリシーに Azure Information Protection ラベルを追加または削除します。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/06/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0546cc11-67a5-4194-8c54-f3ac8ce9ebe1
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 327d8902ecb7abab96b8ff7d05eb6b845eef2199
ms.sourcegitcommit: 3b50727cb50a612b12f248a5d18b00175aa775f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/08/2020
ms.locfileid: "75742898"
---
# <a name="add-or-remove-a-label-to-or-from-an-azure-information-protection-policy"></a>Azure Information Protection ポリシーにラベルを追加または削除する

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順: [Windows 用の Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*


Azure Information Protection ラベルを作成したら、ユーザーが使用できるようにラベルをポリシーに追加できます。 ラベルがすべてのユーザーに対するものである場合は、ラベルをグローバル ポリシーに追加します。 ラベルがユーザーのサブセットに対するものである場合は、ラベルをスコープ ポリシーに追加します。 ラベルは 1 つのポリシーにのみ追加できます。 

サブラベルを追加するには、親ラベルが同じポリシーまたはグローバル ポリシーにある必要があります。 サブラベルを追加するとき、メイン ラベルの設定は継承されません。 ポリシーでサブラベルを割り当てられているユーザーの場合、メイン ラベルは名前と色の表示コンテナーとしてのみサポートされます。 このシナリオでは、メイン ラベルの他の構成設定は、視覚的なマーキング、保護、および条件に対してサポートされません。 それらを構成することはできますが、メイン ラベルでのそれらの設定は、サブラベルを含まないポリシー内にメイン ラベルがあるユーザーに対してのみサポートされます。

既にポリシー内にあるラベルは、ポリシーから削除できます。 このアクションでは、ラベルは削除されません。 別のポリシーで利用可能なままになります。

ラベルをまだ作成していない場合は、「[Azure Information Protection の新しいラベルを作成する方法](configure-policy-new-label.md)」をご覧ください。

ラベルがユーザーのサブセットに適用されるようにスコープ ポリシーを作成する必要がある場合は、「[スコープ ポリシーを使用して特定のユーザーの Azure Information Protection ポリシーを構成する方法](configure-policy-scope.md)」をご覧ください。

## <a name="to-add-or-remove-a-label-to-or-from-a-policy"></a>ポリシーにラベルを追加または削除するには

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、 **[Azure Information Protection]** ペインに移動します。
    
    たとえば、リソース、サービス、ドキュメントの検索ボックスで、「**情報**の入力を開始し、 **[Azure Information Protection]** を選択します。

2. **分類** > **ポリシー**  メニューオプションから:  **Azure Information Protection** - **ポリシー**  ウィンドウで、追加 または 削除 のラベルをすべてのユーザーに適用する場合は **グローバル** を選択します。

    追加または削除するラベルがユーザーのサブセットに適用される場合は、代わりにスコープ ポリシーを選択します。

3. **[ポリシー]** ウィンドウで、 **[ラベルの追加または削除]** を選択します。

4. **[ポリシー: ラベルの追加または削除]** ウィンドウで、既にポリシーに含まれている場合はチェックボックスがオンになっているすべてのラベルと、**ポリシー**列の対応するポリシー名が表示されます。
     
    サブラベルはインデントされて表示されます。 スコープ ポリシーでは、グローバル ポリシーから継承されているラベルは利用不可として表示されます。
    
    次の 1 つ以上のアクションを実行し、 **[OK]** をクリックします。
    
    - ラベルを追加するには、そのラベルを選択すると、オンになったチェックボックスが追加されます。
    
    - ラベルを削除するには、そのチェック ボックスをオフにします。
  
5. 変更を保存するには、 **[保存]** をクリックします。
   
    変更内容はユーザーとサービスに対して自動的に利用可能になります。 独立した公開オプションはなくなりました。


## <a name="next-steps"></a>次の手順

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。
