---
title: Azure Information Protection のスコープ ポリシーの構成 - AIP
description: 特定のユーザーに異なる設定とラベルを構成するには、Azure Information Protection のスコープ付きポリシーを構成する必要があります。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/17/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4b134785-0353-4109-8fa7-096d1caa2242
ms.subservice: aiplabels
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 1d7f009ef3405e9622a35a9f9eb8884494122df9
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383076"
---
# <a name="how-to-configure-the-azure-information-protection-policy-for-specific-users-by-using-scoped-policies"></a>スコープ ポリシーを使用して特定のユーザーの Azure Information Protection ポリシーを構成する方法

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***関連**: [Windows 用のクラシッククライアント Azure Information Protection](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)ます。 統一されたラベル付けクライアントについては、Microsoft 365 のドキュメントの「 [秘密度ラベルについて](/microsoft-365/compliance/sensitivity-labels) 」を参照してください。 *

> [!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Azure Information Protection クライアントがインストールされているコンピューターに Azure Information Protection ポリシーがダウンロードされると、すべてのユーザーは、既定のポリシーから設定とラベルを取得するか、グローバル ポリシー用に構成された変更を取得します。 異なる設定やラベルを使用して、特定のユーザーに対してこの構成を補完する場合は、それらのユーザー用に構成された **スコープ付きポリシー** を作成する必要があります。

## <a name="how-scoped-policies-work"></a>スコープ付きポリシーのしくみ

Azure Information Protection クライアントをサポートするアプリケーションの場合、すべてのユーザーは、Information Protection バーに表示されるタイトルとツールヒント、グローバル設定、およびグローバル ラベルを含むグローバル ポリシーを受信します。 特定のユーザーに対してスコープ付きポリシーを構成した場合、それらのユーザーは追加の設定とラベルを受け取ります。 

Azure Information Protection クライアントをサポートする Office デスクトップ アプリケーションに加えて、ラベルも PowerShell および Azure Information Protection スキャナーでサポートされています。 つまり、Powershell コマンドまたはスキャナーを実行するアカウントに対して、スコープ ポリシーを作成し構成することができます。 

スコープ付きポリシーは、ラベルと同様に Azure Portal で順序付けされます。 ユーザーが複数のスコープに対して構成されている場合、ダウンロード前に、そのユーザーの有効なポリシーが計算されます。 ポリシーの順序に従って、最後のポリシー設定が適用されます。 ユーザーに表示されるラベルは、グローバル ポリシーのラベルと、ユーザーが属するスコープ付きポリシーの追加ラベルです。

例外は、テナントからのユーザーがラベル付きのドキュメントまたは電子メールを開く場合に、そのユーザーがラベルのスコープに含まれていない場合です。 このシナリオでは、ユーザーにラベルのセットの名前が表示されますが、ラベルは選択可能なものとして表示されません。  

スコープ付きポリシーは、グローバル ポリシーのラベルと設定を常に継承します。グローバル ポリシーのラベルは、スコープ付きポリシーを作成または編集するときに表示されます。 ただし、スコープ付きポリシーを編集するときに、グローバル ポリシーのラベルを編集することはできません。 ただし、これらの継承されたラベルにサブラベルを追加することはできます。

たとえば、グローバル ポリシーに **Confidential** というラベルがある場合、すべてのユーザーにこのラベルが表示されます。 スコープ ポリシーでこのラベルを削除したり順序を変更したりすることはできません。 ただし、Confidential に新しいサブラベルを追加するマーケティング部門のスコープ付きポリシーを作成して、この部門のユーザーに **Confidential \ Promotions** を表示することができます。 また、Confidential に新しいサブラベルを追加する営業部門の別のスコープ付きポリシーを作成し、この部門のユーザーに **Confidential \ Partners** に表示することもできます。 各サブラベルは異なる設定用に構成することができます。また、サブラベルは各部門のユーザーにのみ表示することができます。

## <a name="configure-a-scoped-policy"></a>スコープポリシーを構成する

1. まだ実行していない場合は、新しいブラウザー ウィンドウを開いて、[Azure Portal にサインインします](configure-policy.md#signing-in-to-the-azure-portal)。 次に、 **[Azure Information Protection]** ペインに移動します。

    たとえば、リソース、サービス、ドキュメントの検索ボックスで次のようにします: 「**Information**」と入力し、 **[Azure Information Protection]** を選択します。

2. [**分類**  >  **ポリシー** ] メニューオプションから: [ **Azure Information Protection-ポリシー** ] ウィンドウで、[**新しいポリシーの追加**] を選択します。 次に、既存のグローバルポリシーを表示する **ポリシー** ウィンドウが表示されます。ここで、新しいスコープ付きポリシーを構成できます。

3. Azure Portal で管理者にのみ表示されるポリシー名と説明を指定します。 名前はテナントに対して一意である必要があります。 次に、[ **このポリシーを取得するユーザー/グループを指定** してください] を選択し、後続のウィンドウで、このポリシーのユーザーとグループを検索して選択します。 このスコープ付きポリシーで構成するラベルと設定は、これらのユーザーにのみ適用されます。
    
    パフォーマンス上の理由から、スコープ付きポリシーのグループ メンバーシップは[キャッシュ](prepare.md#group-membership-caching-by-azure-information-protection)されます。

    > [!NOTE]
    > 最大200のユーザーまたはグループを選択します。 スコープポリシーを取得するために200人以上のユーザーが必要な場合は、新しいグループを作成し、関連するユーザーをそのグループに追加して、ポリシースコープを新しいグループに設定します。 

4. ここで、新しいラベルを追加したり、スコープ ポリシーの設定を構成します。 グローバル ポリシーは常に最初に適用されるため、新しいラベルでグローバル ポリシーを補い、グローバル設定をオーバーライドすることができます。 たとえば、グローバル ポリシーに既定のラベルを指定せず、特定の部門に対して異なるスコープ付きポリシーの異なる既定のラベルを構成します。

    ラベルまたは設定の構成に関するヘルプが必要な場合は、「 [組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy) 」セクションのリンクを使用してください。

6. グローバルポリシーを編集するときと同様に、Azure Information Protection ウィンドウで変更を行うときは、[ **保存** ] をクリックして変更を保存するか、[ **破棄** ] をクリックして最後に保存した設定に戻します。 

7. このスコープポリシーに必要な変更が完了したら、[初期 **Azure Information Protection-ポリシー** ] ウィンドウで、このスコープポリシーが適用する順序であることを確認します。 この手順は、複数のスコープ付きポリシーに対して同じユーザーを選択した場合に重要です。 順序を変更するには、コンテキスト メニュー (**[...]**) を選択し、**[上へ移動]** または **[下へ移動]** を選択します。 

Azure Information Protection クライアントは、サポートされている Office アプリケーションが起動するか、ファイル エクスプローラーが開かれるたびに変更がないかどうかを確認します。 クライアントは、グローバル ポリシー、またはそのユーザーに適用されるスコープ付きポリシーの変更をダウンロードします。

## <a name="next-steps"></a>次のステップ

既定のポリシーをカスタマイズする方法や、Office アプリケーションで結果の動作を確認する方法の例については、[ポリシーの編集と新しいラベルの作成](infoprotect-quick-start-tutorial.md)に関するチュートリアルをご覧ください。
