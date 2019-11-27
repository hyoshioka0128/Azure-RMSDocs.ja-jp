---
title: Azure Information Protection ポリシーを構成する - AIP
description: Azure Information Protection クライアント (クラシック) の分類、ラベル付け、保護を構成するには、Azure Information Protection ポリシーを構成する必要があります。
author: cabailey
ms.author: cabailey
ms.date: 11/25/2019
manager: rkarlin
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.subservice: aiplabels
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 498028d071e2af3a908518020b142cc1dea39a4d
ms.sourcegitcommit: 487e681c9683b8adb7ae6fcfb374830bf0e5ad72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2019
ms.locfileid: "74479150"
---
# <a name="configuring-the-azure-information-protection-policy"></a>Azure Information Protection ポリシーの構成

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順: [Windows 用の Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

> [!NOTE]
> Azure Information Protection ポリシーは Azure Information Protection クライアント (クラシック) に適用され、Azure Information Protection の統合されたラベル付けクライアントには適用されません。 これらのクライアントの違いがわからない場合は、 こちらの [FAQ](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client) を参照してください。
> 
> 統一されたラベル付けクライアントの秘密度ラベルとポリシー設定を構成するための情報を探している場合は、Office ドキュメントの「[秘密度ラベルの概要](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels)」を参照してください。

クラシッククライアントの分類、ラベル付け、保護を構成するには、Azure Information Protection ポリシーを構成する必要があります。 このポリシーは、[Azure Information Protection クライアント](https://www.microsoft.com/en-us/download/details.aspx?id=53018)がインストールされたコンピューターにダウンロードされます。

ポリシーにはラベルと設定が含まれています。

- ラベルによってドキュメントや電子メールに分類値を適用し、必要に応じてそのコンテンツを保護することができます。 Azure Information Protection クライアントでは、Office アプリのユーザー向けにこれらのラベルが表示されます。また、エクスプローラーで右クリックしたときにも表示されます。 これらのラベルは、PowerShell と Azure Information Protection スキャナーを使用して適用することもできます。

- この設定で、Azure Information Protection クライアントの既定の動作は変更されます。 たとえば、既定のラベル、すべてのドキュメントと電子メールにラベルが必要かどうか、Office アプリに Azure Information Protection バーを表示するかどうかを選択できます。

## <a name="subscription-support"></a>サブスクリプション サポート

Azure Information Protection では、さまざまなレベルのサブスクリプションをサポートしています。

- Azure Information Protection P2: すべての分類、ラベル付け、保護機能をサポートします。

- Azure Information Protection P1: ほとんどの分類、ラベル付け、保護機能をサポートしますが、自動分類や HYOK はサポートしません。

- Azure Rights Management サービスを含む office 365: 保護をサポートしますが、分類とラベル付けはサポートしません。

Azure Information Protection P2 サブスクリプションが必要なオプションはポータルで確認します。

組織が種類の異なるサブスクリプションを保有している場合、アカウントに使用を許諾されていない機能をユーザーが使用しないようにする必要があります。 Azure Information Protection クライアントはライセンスのチェックと適用を行いません。 一部のユーザーのライセンスには付属しないオプションを構成する場合は、範囲設定されたポリシーやレジストリ設定を使用して、組織がライセンス条件を遵守するようにします。

- **組織が Azure Information Protection P1 と Azure Information Protection P2 の種類が異なるライセンスを保有している場合**: P2 ライセンスを保有しているユーザーは、Azure Information Protection P2 ライセンスが必要なオプションを構成する場合、[範囲設定されたポリシー](configure-policy-scope.md)を 1 つ以上作成して使用します。 Azure Information Protection P2 ライセンスを必要とするオプションがグローバル ポリシーに含まれないようにします。

- **組織が Azure Information Protection のサブスクリプションを保有し、一部のユーザーが Azure Rights Management サービスを含む Office 365 のライセンスのみを保有している場合**: Azure Information Protection のライセンスを保有しないユーザー向けに、コンピューター上のレジストリを編集して、Azure Information Protection ポリシーがダウンロードされないようにします。 手順については、以下のカスタマイズについての管理ガイド、「[Enforce protection-only mode when your organization has a mix of licenses (組織が種類の異なるライセンスを保有している場合の保護のみモードの適用)](./rms-client/client-admin-guide-customizations.md#enforce-protection-only-mode-when-your-organization-has-a-mix-of-licenses)」をご覧ください。

サブスクリプションの詳細については、「[Azure Information Protection にはどのようなサブスクリプションが必要ですか。どのような機能が含まれていますか。](faqs.md#what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included)」を参照してください。

## <a name="signing-in-to-the-azure-portal"></a>Azure Portal にサインインする

Azure Portal にサインインするには、Azure Information Protection を構成して管理します。

- 以下のリンクを使用します。 https://portal.azure.com

- 次のいずれかの[管理者ロール](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)を持つ Azure AD アカウントを使用します。
    
    - **Azure Information Protection 管理者**
    
  - **コンプライアンス管理者**
    
  - **コンプライアンスデータ管理者**
    
  - **セキュリティ管理者**
    
    **セキュリティ閲覧**者 - [Azure Information Protection analytics](reports-aip.md)のみ
    
    **グローバルリーダー** - [Azure Information Protection analytics](reports-aip.md)のみ
    
  - **グローバル管理者**
    
    > [!NOTE] 
    > テナントが統一された[ラベル付けプラットフォーム](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)にある場合、Azure Information Protection 管理者ロール (旧称 "Information Protection administrator")、セキュリティ閲覧者ロール、およびグローバル閲覧者ロールは、Azure portal ではサポートされません。 [詳細情報](configure-policy-migrate-labels.md#administrative-roles-that-support-the-unified-labeling-platform)
    
    Microsoft アカウントは Azure Information Protection を管理できません。

## <a name="to-access-the-azure-information-protection-pane-for-the-first-time"></a>初めて [Azure Information Protection] ウィンドウにアクセスするには

1. Azure ポータルにサインインします。

2. **[+ リソースの作成]** を選択し、Marketplace の検索ボックスに「**Azure Information Protection**」と入力します。 
    
3. 結果一覧から **[Azure Information Protection]** を選択します。 **Azure Information Protection**ウィンドウで、 **[作成]** をクリックします。
    
    > [!TIP] 
    > 必要に応じて、 **[ダッシュボードにピン留めする]** を選択してダッシュボードの **[Azure Information Protection]** タイルを作成し、次にポータルにサインインするときにサービスの参照をスキップできるようにします。
    
    再び **[作成]** をクリックします。

4. サービスに最初に接続するときに自動的に開く **[クイック スタート]** ページが表示されます。 推奨リソースを参照するか、他のメニュー オプションを使用します。 ユーザーが選択できるラベルを構成するには、次の手順に従います。

次に **[Azure Information Protection]** ウィンドウにアクセスしたときに、すべてのユーザーのラベルを表示および構成できるように、 **[ラベル]** オプションが自動的に選択されます。 **[クイック スタート]** ページに戻るには、 **[全般]** メニューから選択します。

## <a name="how-to-configure-the-azure-information-protection-policy"></a>Azure Information Protection ポリシーを構成する方法

1. Azure Information Protection 管理者、セキュリティ管理者、またはグローバル管理のいずれかの管理者ロールを使用して、Azure portal にサインインしていることを確認します。 これらの管理者ロールの詳細については、[上記のセクション](#signing-in-to-the-azure-portal)を参照してください。

2. 必要に応じて、**Azure Information Protection** ウィンドウに移動します。たとえば、ハブメニューで **すべてのサービス** をクリックし、フィルター ボックスに「 **Information Protection**の入力を開始します。 結果から **[Azure Information Protection]** を選択します。 
    
    **[Azure Information Protection ラベル]** ウィンドウが自動的に開き、使用可能なラベルを表示および編集できます。 ラベルをポリシーに追加または削除して、すべてのユーザーまたは選択したユーザーに対して利用可能にしたり、どのユーザーに対しても利用不可にしたりできます。

3. ポリシーを表示および編集するには、メニュー オプションから **[ポリシー]** を選択します。 すべてのユーザーが取得するポリシーを表示および編集するには、 **[グローバル]** ポリシーを選択します。 選択したユーザー用のカスタム ポリシーを作成するには、 **[Add a new policy]\(新しいポリシーの追加\)** を選択します。
    

### <a name="making-changes-to-the-policy"></a>ポリシーに対する変更

任意の数のラベルを作成できます。 ただし、多すぎて正しいラベルを発見して選択する作業が困難になるとき、スコープ ポリシーを作成し、あるユーザーに関連するラベルのみがそのユーザーに表示されるようにします。 保護を適用するラベルには 500 という上限があります。

Azure Information Protection ウィンドウで変更を行った場合は、 **[保存]** をクリックして変更を保存するか、 **[破棄]** をクリックして最後に保存した設定に戻します。 ポリシーに変更を保存したり、ポリシーに追加されたラベルを変更したりすると、それらの変更は自動的に発行されます。 独立した公開オプションはありません。

Azure Information Protection クライアントは、サポート対象の Office アプリケーションの起動時に常に変更の有無を確認し、変更があった場合は該当する最新の Azure Information Protection ポリシーに変更をダウンロードします。 ポリシーをクライアントに更新するトリガーには、他に次のものがあります。

- ファイルまたはフォルダーを分類して保護するための右クリック。

- ラベル付けおよび保護のための [PowerShell コマンドレット](./rms-client/client-admin-guide-powershell.md) (Get-AIPFileStatus、Set-AIPFileClassification、および Set-AIPFileLabel) の実行。

- 24 時間ごと。

- [Azure Information Protection スキャナー](deploy-aip-scanner.md)の場合: サービスが開始されたとき (ポリシーが 1 時間前よりも古い場合) と、操作中の 1 時間ごと。


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

- 電子メールでは、この情報は x ヘッダーに格納されます: **msip_labels: MSIP_Label_\<GUID > _Enabled = True** 

- Word 文書 (.doc および .docx)、Excel スプレッドシート (.xls および .xlsx)、PowerPoint プレゼンテーション (.ppt および .pptx)、および PDF ドキュメントの場合、このメタデータは、次のカスタムプロパティに格納されます: **MSIP_Label_\<GUID > _Enabled = True**

電子メールの場合は、電子メールの送信時にラベル情報が保存されます。 ドキュメントについては、ファイルの保存時にラベル情報が保存されます。 

ラベルの GUID を特定するには、Azure Information Protection ポリシーを表示または構成するときに、Azure portal の**ラベル**ペインで [ラベル ID] の値を見つけます。 ファイルにラベルが適用されている場合、[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) PowerShell コマンドレットを実行して GUID (MainLabelId または SubLabelId) を特定することもできます。 ラベルにサブラベルがある場合、親ラベルではなく、サブラベルの GUID だけを常に指定してください。

## <a name="next-steps"></a>次の手順

Azure Information Protection ポリシーをカスタマイズする方法や、ユーザーに対して結果の動作を表示する方法の例については、次のチュートリアルをご覧ください。

- [Azure Information Protection ポリシーを編集して新しいラベルを作成する](infoprotect-quick-start-tutorial.md)

- [Configure Azure Information Protection policy settings that work together (連携させる Azure Information Protection のポリシー設定を構成する)](infoprotect-settings-tutorial.md)

ポリシーの実行方法を確認するには、「 [Azure Information Protection の中央レポート](reports-aip.md)」を参照してください。

