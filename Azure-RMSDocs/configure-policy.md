---
title: Azure Information Protection ポリシーを構成する - AIP
description: 分類、ラベル付け、および保護を構成するには、Azure Information Protection ポリシーを構成する必要があります。
author: cabailey
ms.author: cabailey
ms.date: 05/29/2019
manager: barbkess
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 53847787fa79782c2bf8e6ce2b6b032e439d1547
ms.sourcegitcommit: e366a19300be4165da05ec7ee592f883c467bb51
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2019
ms.locfileid: "66269722"
---
# <a name="configuring-the-azure-information-protection-policy"></a>Azure Information Protection ポリシーの構成

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順:[Windows 用 Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

分類、ラベル付け、および保護を構成するには、Azure Information Protection ポリシーを構成する必要があります。 このポリシーは、[Azure Information Protection クライアント](https://www.microsoft.com/en-us/download/details.aspx?id=53018)がインストールされたコンピューターにダウンロードされます。

ポリシーにはラベルと設定が含まれています。

- ラベルによってドキュメントや電子メールに分類値を適用し、必要に応じてそのコンテンツを保護することができます。 Azure Information Protection クライアントでは、Office アプリのユーザー向けにこれらのラベルが表示されます。また、エクスプローラーで右クリックしたときにも表示されます。 これらのラベルは、PowerShell と Azure Information Protection スキャナーを使用して適用することもできます。

- この設定で、Azure Information Protection クライアントの既定の動作は変更されます。 たとえば、既定のラベル、すべてのドキュメントと電子メールにラベルが必要かどうか、Office アプリに Azure Information Protection バーを表示するかどうかを選択できます。

## <a name="subscription-support"></a>サブスクリプション サポート

Azure Information Protection では、さまざまなレベルのサブスクリプションをサポートしています。

- Azure Information Protection P2:すべての分類、ラベル付け、保護機能がサポートされます。

- Azure Information Protection P1:ほとんどの分類、ラベル付け、保護機能がサポートされますが、自動分類や HYOK はサポートされません。

- Azure Rights Management サービスを含む office 365:保護はサポートされますが、分類とラベル付けはサポートされません。

Azure Information Protection P2 サブスクリプションが必要なオプションはポータルで確認します。

組織が種類の異なるサブスクリプションを保有している場合、アカウントに使用を許諾されていない機能をユーザーが使用しないようにする必要があります。 Azure Information Protection クライアントはライセンスのチェックと適用を行いません。 一部のユーザーのライセンスには付属しないオプションを構成する場合は、範囲設定されたポリシーやレジストリ設定を使用して、組織がライセンス条件を遵守するようにします。

- **Azure Information Protection P1 ライセンスと Azure Information Protection P2 ライセンスの両方を組織が保有している場合**:P2 ライセンスを保有しているユーザーは、Azure Information Protection P2 ライセンスが必要なオプションを構成する場合、[範囲設定されたポリシー](configure-policy-scope.md)を 1 つ以上作成して使用します。 Azure Information Protection P2 ライセンスを必要とするオプションがグローバル ポリシーに含まれないようにします。

- **組織が Azure Information Protection のサブスクリプションを保有し、一部のユーザーが Azure Rights Management サービスを含む Office 365 のライセンスのみを保有している場合**:Azure Information Protection のライセンスを保有しないユーザー向けに、コンピューター上のレジストリを編集して、Azure Information Protection ポリシーがダウンロードされないようにします。 手順については、管理ガイドで以下のカスタマイズについての説明をご覧ください:「[組織が種類の異なるライセンスを保有している場合の保護のみモードの適用](./rms-client/client-admin-guide-customizations.md#enforce-protection-only-mode-when-your-organization-has-a-mix-of-licenses)」。

サブスクリプションの詳細については、「[Azure Information Protection にはどのようなサブスクリプションが必要ですか。どのような機能が含まれていますか。](faqs.md#what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included)」を参照してください。

## <a name="signing-in-to-the-azure-portal"></a>Azure Portal にサインインする

Azure Portal にサインインするには、Azure Information Protection を構成して管理します。

- 以下のリンクを使用します。 https://portal.azure.com

- 次のいずれかの[管理者ロール](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)を持つアカウントを使用します。
    
    - **Azure Information Protection 管理者**
    
    - **セキュリティ閲覧者** ([Azure Information Protection 分析](reports-aip.md)のみ)
    
  - **コンプライアンス管理者**
    
  - **セキュリティ管理者**
    
  - **グローバル管理者**
    
    > [!NOTE] 
    > 統合のラベル付けのストアに、テナントが移行された場合、Azure Information Protection 管理者 (旧称「Information Protection 管理者」) はサポートされていません。 [詳細情報](configure-policy-migrate-labels.md#important-information-about-administrative-roles)


## <a name="to-access-the-azure-information-protection-blade-for-the-first-time"></a>初めて [Azure Information Protection] ブレードにアクセスするには

1. Azure ポータルにサインインします。

2. ハブ メニューで **[リソースの作成]** を選択し、Marketplace の検索ボックスに **Azure Information Protection** と入力します。 
    
3. 結果一覧から **[Azure Information Protection]** を選択します。 **[Azure Information Protection]** ブレードで **[作成]** をクリックします。
    
    > [!TIP] 
    > 必要に応じて、 **[ダッシュボードにピン留めする]** を選択してダッシュボードの **[Azure Information Protection]** タイルを作成し、次にポータルにサインインするときにサービスの参照をスキップできるようにします。
    
    再び **[作成]** をクリックします。

4. サービスに最初に接続するときに自動的に開く **[クイック スタート]** ページが表示されます。 推奨リソースを参照するか、他のメニュー オプションを使用します。 ユーザーが選択できるラベルを構成するには、次の手順に従います。

次に **[Azure Information Protection]** ブレードにアクセスすると、すべてのユーザーのラベルを表示および構成できるように、 **[ラベル]** オプションが自動的に選択されます。 **[クイック スタート]** ページに戻るには、 **[全般]** メニューから選択します。

## <a name="how-to-configure-the-azure-information-protection-policy"></a>Azure Information Protection ポリシーを構成する方法

1. 次のいずれかの管理者ロールを使用して、Azure portal にサインインしていることを確認します:Azure Information Protection 管理者、セキュリティ管理者、またはグローバル管理します。 これらの管理者ロールの詳細については、[上記のセクション](#signing-in-to-the-azure-portal)を参照してください。

2. 必要に応じて、 **[Azure Information Protection]** ブレードに移動します。たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information Protection**」と入力します。 結果から **[Azure Information Protection]** を選択します。 
    
    **[Azure Information Protection - ラベル]** ブレードが自動的に開き、使用可能なラベルを表示、編集できます。 ラベルをポリシーに追加または削除して、すべてのユーザーまたは選択したユーザーに対して利用可能にしたり、どのユーザーに対しても利用不可にしたりできます。

3. ポリシーを表示および編集するには、メニュー オプションから **[ポリシー]** を選択します。 すべてのユーザーが取得するポリシーを表示および編集するには、 **[グローバル]** ポリシーを選択します。 選択したユーザー用のカスタム ポリシーを作成するには、 **[Add a new policy]\(新しいポリシーの追加\)** を選択します。
    

### <a name="making-changes-to-the-policy"></a>ポリシーに対する変更

任意の数のラベルを作成できます。 ただし、多すぎて正しいラベルを発見して選択する作業が困難になるとき、スコープ ポリシーを作成し、あるユーザーに関連するラベルのみがそのユーザーに表示されるようにします。 保護を適用するラベルには 500 という上限があります。

[Azure Information Protection] ブレードで変更を行ったら、 **[保存]** をクリックして変更を保存します。または、 **[破棄]** をクリックして、最後に保存した設定に戻します。 ポリシーでは、変更を保存するか、ポリシーに追加されるラベルを変更すると、ときに、これらの変更が自動的に発行します。 独立した公開オプションはありません。

Azure Information Protection クライアントは、サポート対象の Office アプリケーションの起動時に常に変更の有無を確認し、変更があった場合は該当する最新の Azure Information Protection ポリシーに変更をダウンロードします。 ポリシーをクライアントに更新するトリガーには、他に次のものがあります。

- ファイルまたはフォルダーを分類して保護するための右クリック。

- ラベル付けおよび保護のための [PowerShell コマンドレット](./rms-client/client-admin-guide-powershell.md) (Get-AIPFileStatus、Set-AIPFileClassification、および Set-AIPFileLabel) の実行。

- 24 時間ごと。

- [Azure Information Protection スキャナー](deploy-aip-scanner.md)の場合:サービスが開始されたとき (ポリシーが 1 時間前よりも古い場合) と、操作中の 1 時間ごと。


>[!NOTE]
>クライアントがポリシーをダウンロードしてから完全に機能するまで、数分間待機します。 待機時間はポリシーの構成のサイズや複雑さ、ネットワークの接続などの要素によって異なります。 ラベルの動作の結果が最新の変更と一致しない場合は、15 分待ってから再度お試しください。

### <a name="configuring-your-organizations-policy"></a>組織のポリシーの構成

次の情報を使用して、Azure Information Protection ポリシーを構成します。

- [Information Protection の既定のポリシー](configure-policy-default.md)

- [ポリシー設定を構成する方法](configure-policy-settings.md)

- [新しいラベルを作成する方法](configure-policy-new-label.md)

- [ラベルを追加または削除する方法](configure-policy-add-remove-label.md)
 
- [ラベルを削除または順序変更する方法](configure-policy-delete-reorder.md)

- [既存のラベルを変更またはカスタマイズする方法](configure-policy-change-label.md)

- [保護用ラベルの構成方法](configure-policy-protection.md)

- [視覚的なマーキングを適用するようにラベルを構成する方法](configure-policy-markings.md)

- [自動および推奨分類の条件を構成する方法](configure-policy-classification.md)

- [スコープ ポリシーを使用して特定のユーザーのポリシーを構成する方法](configure-policy-scope.md)

- [テンプレートを構成および管理する方法](configure-policy-templates.md)

- [異なる言語のラベルを構成する方法](configure-policy-languages.md)

- [Azure Information Protection ラベルを Office 365 に移行する方法](configure-policy-migrate-labels.md)

## <a name="label-information-stored-in-emails-and-documents"></a>メールやドキュメントに格納されるラベル情報

ドキュメントまたはメールにラベルが適用されるとき、実際には、アプリケーションとサービスがそのラベルを読み取れるように、メタデータにラベルが格納されています。

- メールでは、この情報は **msip_labels: MSIP_Label_\<GUID>_Enabled=True;** の X ヘッダーに格納されます 

- Word 文書 (.doc、.docx)、Excel スプレッドシート (.xls、.xlsx)、PowerPoint プレゼンテーション (.ppt、.pptx)、PDF ドキュメントの場合、このメタデータは次のカスタム プロパティに格納されます:**MSIP_Label_\<GUID>_Enabled=True** に格納されます。  

メールの電子メールが送信されるときに、ラベル情報が格納されます。 ドキュメントについては、ファイルを保存するときに、ラベル情報が格納されます。 

ラベルの GUID を特定するには、Azure Information Protection ポリシーを表示または構成するときに、Azure portal の **[ラベル]** ブレード上の [ラベル ID] の値を見つけます。 ファイルにラベルが適用されている場合、[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) PowerShell コマンドレットを実行して GUID (MainLabelId または SubLabelId) を特定することもできます。 ラベルにサブラベルがある場合、親ラベルではなく、サブラベルの GUID だけを常に指定してください。

## <a name="next-steps"></a>次の手順

Azure Information Protection ポリシーをカスタマイズする方法や、ユーザーに対して結果の動作を表示する方法の例については、次のチュートリアルをご覧ください。

- [Azure Information Protection ポリシーを編集して新しいラベルを作成する](infoprotect-quick-start-tutorial.md)

- [連携させる Azure Information Protection のポリシー設定を構成する](infoprotect-settings-tutorial.md)

ポリシーの実行方法を確認するには、[Azure Information Protection 向けのレポート作成](reports-aip.md)に関する記事を参照してください。

