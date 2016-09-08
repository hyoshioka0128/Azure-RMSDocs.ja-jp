---
title: "Azure Information Protection ポリシーの構成 | Azure RMS"
description: "分類、ラベル付け、および保護を構成するには、Azure Information Protection ポリシーを構成する必要があります。"
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: da0145444a7d0abb6407ed2ccbb581d4dcdd10d6
ms.openlocfilehash: e5b8054b3b5cb38adf2f5ae1d2f4f399d98f6e23


---

# Azure Information Protection ポリシーの構成

>*適用対象: Azure Information Protection プレビュー*

**[この情報は暫定的なものであり、変更されることがあります。 ]**

分類、ラベル付け、および保護を構成するには、Azure Information Protection ポリシーを構成する必要があります。 このポリシーは、[Azure Information Protection クライアント](https://www.microsoft.com/en-us/download/details.aspx?id=53018)がインストールされたコンピューターにダウンロードされます。

Azure Information Protection のプレビュー リリース中に Azure Information Protection ポリシーを構成するには:

1. [Azure ポータル](https://portal.azure.com)にサインインします。

2. **[Azure Information Protection]** ブレードに移動します。たとえば、ハブ メニューで **[参照]** をクリックし、[フィルター] ボックスに「 **Information Protection**」と入力します。 結果から [**Azure Information Protection**] を選択します。 

    **[Azure Information Protection]** ブレードが表示され、ここで、次の要素を含む Azure Information Protection ポリシーを構成できます。

    - ユーザーの Office アプリケーションで、Information Protection バーに表示されるタイトルとツールヒント。

    - 管理者とユーザーがドキュメントと電子メールを分類するために使用できるラベル。

    - ユーザーがドキュメントの保存と電子メールの送信を行ったときに分類を実行するオプション。

    - ドキュメントと電子メールを分類するための開始点となる既定のラベルを設定するオプション。

    - ユーザーが元のレベルよりも低い秘密度レベルのラベルを選択したときに、理由を示すことをユーザーに要求するオプション。


Azure Information Protection には[既定のポリシー](configure-policy-default.md)が付属しています。このポリシーには、**[個人用]**、**[パブリック]**、**[内部]**、**[機密]**、および **[秘密]**というラベルが含まれています。 これらの既定のラベルは、そのまま使用する、カスタマイズする、または削除することができ、新しいラベルを作成することもできます。

[Azure Information Protection] ブレードで変更を行ったら、**[保存]** をクリックして変更を保存します。または、**[破棄]** をクリックして、最後に保存した設定に戻します。 

目的の変更が終わったら、**[公開]** をクリックします。 

Azure Information Protection クライアントは、サポート対象の Office アプリケーションの起動時に常に変更の有無を確認し、変更があった場合は該当する Azure Information Protection ポリシーに変更をダウンロードします。

## 組織のポリシーの構成

次の情報を使用して、Azure Information Protection ポリシーを構成します。

- [Information Protection の既定のポリシー](configure-policy-default.md)

- [グローバル ポリシー設定を構成する方法](configure-policy-settings.md)

- [新しいラベルを作成する方法](configure-policy-new-label.md)

- [ラベルを削除または順序変更する方法](configure-policy-delete-reorder.md)

- [既存のラベルを変更またはカスタマイズする方法](configure-policy-change-label.md)

- [保護を適用するようにラベルを構成する方法](configure-policy-protection.md)

- [視覚的なマーキングを適用するようにラベルを構成する方法](configure-policy-markings.md)

- [自動および推奨分類の条件を構成する方法](configure-policy-classification.md)

## 次のステップ

既定のポリシーをカスタマイズする方法や、Office アプリケーションで結果の動作を確認する方法の例については、「[Azure Information Protection のクイック スタート チュートリアル](infoprotect-quick-start-tutorial.md)」をご覧ください。




<!--HONumber=Aug16_HO4-->


