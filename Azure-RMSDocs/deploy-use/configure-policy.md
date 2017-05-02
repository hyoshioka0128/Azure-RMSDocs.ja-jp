---
title: "Azure Information Protection ポリシーを構成する"
description: "分類、ラベル付け、および保護を構成するには、Azure Information Protection ポリシーを構成する必要があります。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/25/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 8b6bd6e44fb39c3787e2fe63577c7e7fd9948025
ms.sourcegitcommit: d814d2876cf56e8fff0b107a5e3ec6df2aeda9ae
translationtype: HT
---
# <a name="configuring-azure-information-protection-policy"></a>Azure Information Protection ポリシーの構成

>*適用対象: Azure Information Protection*

分類、ラベル付け、および保護を構成するには、Azure Information Protection ポリシーを構成する必要があります。 このポリシーは、[Azure Information Protection クライアント](https://www.microsoft.com/en-us/download/details.aspx?id=53018)がインストールされたコンピューターにダウンロードされます。

Azure Information Protection ポリシーを構成するには:

1. 新しいブラウザー ウィンドウで、セキュリティ管理者または全体管理者として [Azure Portal](https://portal.azure.com) にサインインします。

2. **[Azure Information Protection]** ブレードに移動します。たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information Protection**」と入力します。 結果から [**Azure Information Protection**] を選択します。 

    **[Azure Information Protection]** ブレードが読み込まれると、**[Policy: Global]** (ポリシー: グローバル) ブレードが自動的に開き、すべてのユーザーが取得するグローバル ポリシーを表示、編集できます。 また、必要に応じて、スコープ ポリシーを追加し、編集することもできます。 Azure Information Protection ポリシーには、構成可能な次の要素があります。

    - 管理者とユーザーがドキュメントと電子メールを分類するために使用できるラベル。

    - ユーザーの Office アプリケーションで、Information Protection バーに表示されるタイトルとツールヒント。

    - ユーザーがドキュメントの保存と電子メールの送信を行ったときに分類を実行するオプション。

    - ドキュメントと電子メールを分類するための開始点となる既定のラベルを設定するオプション。

    - ユーザーが元のレベルよりも低い秘密度レベルのラベルを選択したときに、理由を示すことをユーザーに要求するオプション。

    - 添付ファイルに基づいて、電子メール メッセージに自動的にラベルを付けるオプション。

    - ユーザーにカスタム ヘルプ リンクを提供するオプション。

Azure Information Protection には[既定ポリシー](configure-policy-default.md)があり、5 つの主要なラベルが含まれています。 これらのラベルは、最下位の分類である個人データから、最上位の分類である非常に機密性の高い社外秘データまで、組織が通常作成して保存するあらゆるデータで使用できます。 これらの既定のラベルは、そのまま使用する、カスタマイズする、または削除することができ、新しいラベルを作成することもできます。

[Azure Information Protection] ブレードで変更を行ったら、**[保存]** をクリックして変更を保存します。または、**[破棄]** をクリックして、最後に保存した設定に戻します。 

目的の変更が終わったら、**[公開]** をクリックします。 

Azure Information Protection クライアントは、サポート対象の Office アプリケーションの起動時に常に変更の有無を確認し、変更があった場合は該当する最新の Azure Information Protection ポリシーに変更をダウンロードします。 ポリシーをクライアントに更新するトリガーには、他に次のものがあります。

- ファイルまたはフォルダーを分類して保護するための右クリック。

- ラベル付けおよび保護のための PowerShell コマンドレット (Get-AIPFileStatus および Set-AIPFileLabel) の実行。

- 24 時間ごと。


## <a name="configuring-your-organizations-policy"></a>組織のポリシーの構成

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

## <a name="next-steps"></a>次のステップ

既定のポリシーをカスタマイズする方法や、Office アプリケーションで結果の動作を確認する方法の例については、「[Azure Information Protection のクイック スタート チュートリアル](../get-started/infoprotect-quick-start-tutorial.md)」をご覧ください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
