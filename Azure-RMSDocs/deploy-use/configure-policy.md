---
title: Azure Information Protection ポリシーを構成する
description: 分類、ラベル付け、および保護を構成するには、Azure Information Protection ポリシーを構成する必要があります。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/02/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 2b3d0d3f5f49d02ba738ffd900d3d54b5390443a
ms.sourcegitcommit: 949bf02d5d12bef8e26d89ad5d6a0d5cc7826135
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/02/2018
ms.locfileid: "39473833"
---
# <a name="configuring-the-azure-information-protection-policy"></a>Azure Information Protection ポリシーの構成

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

分類、ラベル付け、および保護を構成するには、Azure Information Protection ポリシーを構成する必要があります。 このポリシーは、[Azure Information Protection クライアント](https://www.microsoft.com/en-us/download/details.aspx?id=53018)がインストールされたコンピューターにダウンロードされます。

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

- **組織が Azure Information Protection のサブスクリプションを保有し、一部のユーザーが Azure Rights Management サービスを含む Office 365 のライセンスのみを保有している場合**: Azure Information Protection のライセンスを保有しないユーザー向けに、コンピューター上のレジストリを編集して、Azure Information Protection ポリシーがダウンロードされないようにします。 手順については、以下のカスタマイズについての管理ガイド、「[Enforce protection-only mode when your organization has a mix of licenses (組織が種類の異なるライセンスを保有している場合の保護のみモードの適用)](../rms-client/client-admin-guide-customizations.md#enforce-protection-only-mode-when-your-organization-has-a-mix-of-licenses)」をご覧ください。

サブスクリプションの詳細については、「[Azure Information Protection にはどのようなサブスクリプションが必要ですか。どのような機能が含まれていますか。](../faqs.md#what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included)」を参照してください。

## <a name="signing-in-to-the-azure-portal"></a>Azure Portal にサインインする

Azure Portal にサインインするには、Azure Information Protection を構成して管理します。

- 以下のリンクを使用します。https://portal.azure.com

- 次のいずれかの[管理者ロール](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)を持つアカウントを使用します。
    
    - **Information Protection 管理者**

    - **セキュリティ管理者**

    - **グローバル管理者/会社の管理者**


## <a name="to-access-the-azure-information-protection-blade-for-the-first-time"></a>初めて [Azure Information Protection] ブレードにアクセスするには

1. Azure ポータルにサインインします。

2. ハブ メニューで **[リソースの作成]** を選択し、Marketplace の検索ボックスに **Azure Information Protection** と入力します。 
    
3. 結果一覧から **[Azure Information Protection]** を選択します。 **[Azure Information Protection]** ブレードで **[作成]** をクリックします。
    
    > [!TIP] 
    > 必要に応じて、**[ダッシュボードにピン留めする]** を選択してダッシュボードの **[Azure Information Protection]** タイルを作成し、次にポータルにサインインするときにサービスの参照をスキップできるようにします。
    
    再び **[作成]** をクリックします。

4. サービスに最初に接続するときに自動的に開く **[クイック スタート]** ページが表示されます。 推奨リソースを参照するか、他のメニュー オプションを使用します。 ユーザーが選択できるラベルを構成するには、次の手順に従います。

次に **[Azure Information Protection]** ブレードにアクセスすると、すべてのユーザーのラベルを表示および構成できるように、**[ラベル]** オプションが自動的に選択されます。 **[クイック スタート]** ページに戻るには、**[全般]** メニューから選択します。

## <a name="how-to-configure-the-azure-information-protection-policy"></a>Azure Information Protection ポリシーを構成する方法

1. 次のいずれかの管理者ロール (Information Protection 管理者、セキュリティ管理者、またはグローバル管理者) を使用して、Azure Portal にサインインしていることを確認します。 これらの管理者ロールの詳細については、[上記のセクション](#signing-in-to-the-azure-portal)を参照してください。

2. 必要に応じて、**[Azure Information Protection]** ブレードに移動します。たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information Protection**」と入力します。 結果から **[Azure Information Protection]** を選択します。 
    
    **[Azure Information Protection - ラベル]** ブレードが自動的に開き、使用可能なラベルを表示、編集できます。 ラベルをポリシーに追加または削除して、すべてのユーザーまたは選択したユーザーに対して利用可能にしたり、どのユーザーに対しても利用不可にしたりできます。

3. ポリシーを表示および編集するには、メニュー オプションから **[ポリシー]** を選択します。 すべてのユーザーが取得するポリシーを表示および編集するには、**[グローバル]** ポリシーを選択します。 選択したユーザー用のカスタム ポリシーを作成するには、**[Add a new policy]\(新しいポリシーの追加\)** を選択します。
    

### <a name="overview-of-the-policy"></a>ポリシーの概要

Azure Information Protection ポリシーには、構成可能な次の要素があります。
    
- 含めるラベル。管理者とユーザーは、ラベルを使用してドキュメントや電子メールを分類できます (また、必要に応じて保護できます)。

- ユーザーの Office アプリケーションで、Information Protection バーに表示されるタイトルとツールヒント。

- ドキュメントと電子メールを分類するための開始点となる既定のラベルを設定するオプション。

- ユーザーがドキュメントの保存と電子メールの送信を行ったときに分類を実行するオプション。

- ユーザーが元のレベルよりも低い秘密度レベルのラベルを選択したときに、理由を示すことをユーザーに要求するオプション。

- 添付ファイルに基づいて、電子メール メッセージに自動的にラベルを付けるオプション。

- Office アプリケーションで Information Protection バーが表示されるかどうかを制御するオプション。

- Outlook に [Do Not Forward]\(転送不可\) ボタンを表示するかどうかを制御するオプション。

- ユーザーがドキュメントに独自のアクセス許可を指定できるようにするオプション。

- ユーザーにカスタム ヘルプ リンクを提供するオプション。

Azure Information Protection には[既定ポリシー](configure-policy-default.md)があり、5 つの主要なラベルが含まれています。 これらのうちの 2 つのラベルには、必要なときにサブカテゴリを提供するためのサブラベルが含まれています。 サブラベルのラベルを構成するときに、ユーザーはメインのラベルを選択することはできませんが、サブラベルをいずれか 1 つ選択する必要があります。

Azure Information Protection ラベルは、最下位の分類である個人データから、最上位の分類である非常に機密性の高い社外秘データまで、組織が通常作成して保存するあらゆるデータで使用できます。 

これらの既定のラベルは、そのまま使用する、カスタマイズする、または削除することができ、新しいラベルを作成することもできます。 詳細については、次のセクションのリンクを使用すると、関連するオプションとそのオプションを構成する方法を確認することができます。

任意の数のラベルを作成できます。 ただし、多すぎて正しいラベルを発見して選択する作業が困難になるとき、スコープ ポリシーを作成し、あるユーザーに関連するラベルのみがそのユーザーに表示されるようにします。 保護を適用するラベルには 500 という上限があります。

[Azure Information Protection] ブレードで変更を行ったら、**[保存]** をクリックして変更を保存します。または、**[破棄]** をクリックして、最後に保存した設定に戻します。 ポリシーに変更を保存した場合、またはポリシーに追加されるラベルに変更を加えた場合、それらの変更は自動的に公開されます。 独立した公開オプションはありません。

Azure Information Protection クライアントは、サポート対象の Office アプリケーションの起動時に常に変更の有無を確認し、変更があった場合は該当する最新の Azure Information Protection ポリシーに変更をダウンロードします。 ポリシーをクライアントに更新するトリガーには、他に次のものがあります。

- ファイルまたはフォルダーを分類して保護するための右クリック。

- ラベル付けおよび保護のための [PowerShell コマンドレット](../rms-client/client-admin-guide-powershell.md) (Get-AIPFileStatus、Set-AIPFileClassification、および Set-AIPFileLabel) の実行。

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

## <a name="next-steps"></a>次の手順

既定のポリシーをカスタマイズする方法や、Office アプリケーションで結果の動作を確認する方法の例については、「[Azure Information Protection のクイック スタート チュートリアル](../infoprotect-quick-start-tutorial.md)」をご覧ください。

