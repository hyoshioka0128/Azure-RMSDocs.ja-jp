---
title: "Azure Information Protection ポリシーを構成する"
description: "分類、ラベル付け、および保護を構成するには、Azure Information Protection ポリシーを構成する必要があります。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/25/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: b04c7881f982b33094107b6de33920a83b17b960
ms.sourcegitcommit: a7cdf911088fdf663e43894484530ea15150284f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2017
---
# <a name="configuring-the-azure-information-protection-policy"></a>Azure Information Protection ポリシーの構成

>*適用対象: Azure Information Protection*

分類、ラベル付け、および保護を構成するには、Azure Information Protection ポリシーを構成する必要があります。 このポリシーは、[Azure Information Protection クライアント](https://www.microsoft.com/en-us/download/details.aspx?id=53018)がインストールされたコンピューターにダウンロードされます。

## <a name="subscription-support"></a>サブスクリプション サポート

Azure Information Protection では、さまざまなレベルのサブスクリプションをサポートしています。

- Azure Information Protection P2: すべての分類、ラベル付け、保護機能をサポートします。

- Azure Information Protection P1: ほとんどの分類、ラベル付け、保護機能をサポートしますが、自動分類や HYOK はサポートしません。

- Azure Rights Management サービスを含む office 365: 保護をサポートしますが、分類とラベル付けはサポートしません。

Azure Information Protection P2 サブスクリプションが必要なオプションはポータルで確認します。

組織が種類の異なるサブスクリプションを保有している場合、アカウントに使用を許諾されていない機能をユーザーが使用しないようにする必要があります。 Azure Information Protection クライアントはライセンスのチェックと適用を行いません。 一部のユーザーのライセンスには付属しないオプションを構成する場合は、範囲設定されたポリシーやレジストリ設定を使用して、組織がライセンス条件を遵守するようにします。

- **組織が Azure Information Protection P1 と Azure Information Protection P2 の種類が異なるライセンスを保有している場合**: P2 ライセンスを保有しているユーザーは、Azure Information Protection P2 ライセンスが必要なオプションを構成する場合、[範囲設定されたポリシー](configure-policy-scope.md)を 1 つ以上作成して使用します。 Azure Information Protection P2 ライセンスを必要とするオプションがグローバル ポリシーに含まれないようにします。

- **組織が Azure Information Protection のサブスクリプションを保有し、一部のユーザーが Azure Rights Management サービスを含む Office 365 のライセンスのみを保有している場合**: Azure Information Protection のライセンスを保有しないユーザー向けに、コンピューター上のレジストリを編集して、Azure Information Protection ポリシーがダウンロードされないようにします。 手順については、以下のカスタマイズについての管理ガイド、「[Enforce protection-only mode when your organization has a mix of licenses (組織が種類の異なるライセンスを保有している場合の保護のみモードの適用)](../rms-client/client-admin-guide-customizations.md#enforce-protection-only-mode-when-your-organization-has-a-mix-of-licenses)」をご覧ください。

サブスクリプションの詳細については、「[Azure Information Protection にはどのようなサブスクリプションが必要ですか。どのような機能が含まれていますか。](../get-started/faqs.md#what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included)」を参照してください。

## <a name="to-access-the-azure-information-protection-blade-for-the-first-time"></a>初めて [Azure Information Protection] ブレードにアクセスするには

1. テナントの全体管理者またはセキュリティ管理者として [Azure Portal](https://portal.azure.com) にサインインします。

2. ハブ メニューで、**[新規]** をクリックし、**[MARKETPLACE]** リストから **[セキュリティ + ID]** を選択します。 
    
3. **[セキュリティ + ID]** ブレードで、**[おすすめアプリ]** リストから **[Azure Information Protection]** を選びます。 次に、**[Azure Information Protection]** ブレードで **[作成]** をクリックします。
    
    テナントの **[Azure Information Protection]** ブレードが作成され、次にポータルにサインインするときに、ハブの **[その他のサービス]** リストからサービスを選択できるようになります。 
    
    > [!TIP] 
    > **[ダッシュボードにピン留めする]** を選択してダッシュボードの **[Azure Information Protection]** タイルを作成し、次にポータルにサインインするときにサービスの参照をスキップできるようにします。

4. サービスに最初に接続するときに自動的に開く **[クイック スタート]** ページが表示されます。 推奨リソースを参照するか、他のメニュー オプションを使用します。 ユーザーが選択できるラベルを構成するには、次の手順に従います。

次に **[Azure Information Protection]** ブレードにアクセスすると、すべてのユーザーのラベルを構成できるように、**[ポリシー]** > **[グローバル ポリシー]** オプションが自動的に選択されます。 **[クイック スタート]** ページに戻るには、**[全般]** メニューから選択します。

## <a name="how-to-configure-the-azure-information-protection-policy"></a>Azure Information Protection ポリシーを構成する方法

1. セキュリティ管理者またはグローバル管理者として [Azure Portal](https://portal.azure.com) にサインインしていることを確認します。

2. 必要に応じて、**[Azure Information Protection]** ブレードに移動します。たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information Protection**」と入力します。 結果から **[Azure Information Protection]** を選択します。 
    
    **[Azure Information Protection - グローバル ポリシー]** ブレードが自動的に開き、すべてのユーザーが取得するグローバル ポリシーを表示、編集できます。 
    
    Azure Information Protection ポリシーには、構成可能な次の要素があります。
    
    - 管理者とユーザーがドキュメントと電子メールを分類するために使用できるラベル。
    
    - ユーザーの Office アプリケーションで、Information Protection バーに表示されるタイトルとツールヒント。
    
    - ユーザーがドキュメントの保存と電子メールの送信を行ったときに分類を実行するオプション。
    
    - ドキュメントと電子メールを分類するための開始点となる既定のラベルを設定するオプション。
    
    - ユーザーが元のレベルよりも低い秘密度レベルのラベルを選択したときに、理由を示すことをユーザーに要求するオプション。
    
    - 添付ファイルに基づいて、電子メール メッセージに自動的にラベルを付けるオプション。
    
    - ユーザーにカスタム ヘルプ リンクを提供するオプション。

Azure Information Protection には[既定ポリシー](configure-policy-default.md)があり、5 つの主要なラベルが含まれています。 これらのうちの 2 つのラベルには、必要なときにサブカテゴリを提供するためのサブラベルが含まれています。 サブラベルのラベルを構成するときに、ユーザーはメインのラベルを選択することはできませんが、サブラベルのいずれか 1 つを選択する必要があります。

Azure Information Protection ラベルは、最下位の分類である個人データから、最上位の分類である非常に機密性の高い社外秘データまで、組織が通常作成して保存するあらゆるデータで使用できます。 

これらの既定のラベルは、そのまま使用する、カスタマイズする、または削除することができ、新しいラベルを作成することもできます。 詳細については、次のセクションのリンクを使用すると、関連するオプションとそのオプションを構成する方法を確認することができます。

任意の数のラベルを作成できます。 ただし、多すぎて正しいラベルを発見して選択する作業が困難になるとき、スコープ ポリシーを作成し、あるユーザーに関連するラベルのみがそのユーザーに表示されるようにします。 保護を適用するラベルには 500 という上限があります。

[Azure Information Protection] ブレードで変更を行ったら、**[保存]** をクリックして変更を保存します。または、**[破棄]** をクリックして、最後に保存した設定に戻します。

目的の変更が終わったら、**[公開]** をクリックします。 

Azure Information Protection クライアントは、サポート対象の Office アプリケーションの起動時に常に変更の有無を確認し、変更があった場合は該当する最新の Azure Information Protection ポリシーに変更をダウンロードします。 ポリシーをクライアントに更新するトリガーには、他に次のものがあります。

- ファイルまたはフォルダーを分類して保護するための右クリック。

- ラベル付けおよび保護のための [PowerShell コマンドレット](../rms-client/client-admin-guide-powershell.md) (Get-AIPFileStatus、Set-AIPFileClassification、および Set-AIPFileLabel) の実行。

- 24 時間ごと。

- [Azure Information Protection スキャナー](deploy-aip-scanner.md)の場合: サービスの開始時と 1 時間ごと。


>[!NOTE]
>クライアントがポリシーをダウンロードしてから完全に機能するまで、数分間待機します。 待機時間はポリシーの構成のサイズや複雑さ、ネットワークの接続などの要素によって異なります。 ラベルの動作の結果が最新の変更と一致しない場合は、15 分待ってから再度お試しください。

### <a name="configuring-your-organizations-policy"></a>組織のポリシーの構成

次の情報を使用して、Azure Information Protection ポリシーを構成します。

- [Information Protection の既定のポリシー](configure-policy-default.md)

- [ポリシー設定を構成する方法](configure-policy-settings.md)

- [新しいラベルを作成する方法](configure-policy-new-label.md)

- [ラベルを削除または順序変更する方法](configure-policy-delete-reorder.md)

- [既存のラベルを変更またはカスタマイズする方法](configure-policy-change-label.md)

- [保護用ラベルの構成方法](configure-policy-protection.md)

- [視覚的なマーキングを適用するようにラベルを構成する方法](configure-policy-markings.md)

- [自動および推奨分類の条件を構成する方法](configure-policy-classification.md)

- [スコープ ポリシーを使用して特定のユーザーのポリシーを構成する方法](configure-policy-scope.md)

- [テンプレートを構成および管理する方法](configure-policy-templates.md)

- [異なる言語のラベルを構成する方法](configure-policy-languages.md)

## <a name="next-steps"></a>次のステップ

既定のポリシーをカスタマイズする方法や、Office アプリケーションで結果の動作を確認する方法の例については、「[Azure Information Protection のクイック スタート チュートリアル](../get-started/infoprotect-quick-start-tutorial.md)」をご覧ください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
