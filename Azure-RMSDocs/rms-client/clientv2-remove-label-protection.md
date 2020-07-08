---
title: Azure Information Protection 統合ラベル付けクライアントを使用してラベルを削除する
description: Azure Information Protection 統合ラベル付けクライアントを使用して、ファイルと電子メールから機密ラベルと保護を削除する方法について説明します。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 06/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ''
ms.subservice: v2client
ms.suite: ems
ms.custom: user
ms.openlocfilehash: c24b67911e4968ffaaa5c4b639917b96197d1b54
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86047390"
---
# <a name="user-guide-remove-labels-and-protection-from-files-and-emails-that-have-been-labeled-by-azure-information-protection"></a>ユーザーガイド: Azure Information Protection によってラベル付けされたファイルと電子メールからラベルと保護を削除する

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8*
>
> **Windows 7 と Office 2010 向けに拡張された Microsoft サポートをご利用のお客様は、これらのバージョンの Azure Information Protection サポートを受けることもできます。詳細については、サポート担当者にお問い合わせください。*
>
> *手順: [Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Azure Information Protection 統合クライアントが[コンピューターにインストール](install-client-app.md)されている場合は、ファイルと電子メールから機密ラベルと保護を削除できます。

削除する感度ラベルが保護を適用するように構成されている場合、この操作によってファイルから保護も削除されます。 ラベルを削除する理由を記録するためにメッセージが表示されることがあります。

> [!IMPORTANT]
> 保護を削除するファイルの所有者であるか、保護を削除するアクセス許可 (**抽出**または**フル コントロール**の Rights Management アクセス許可) を付与されている必要があります。

別のラベルまたは別の保護設定セットを選択する場合、ラベルまたは保護を削除する必要はありません。 代わりに、新しいラベルを選択し、必要に応じて、エクスプローラーを使用してカスタムアクセス許可を定義できます。 

Office のデスクトップ アプリ (**Word**、**Excel**、**PowerPoint**、**Outlook**) で Office ドキュメントや電子メールを作成または編集している場合、ラベルと保護を削除できます。 

また、**エクスプローラー**を使用して分類と保護の削除を行うこともできます。エクスプローラーは、その他のファイルの種類をサポートしています。複数のファイルからラベルと保護を一度に削除する場合に便利な方法です。

## <a name="using-office-apps-to-remove-labels-and-protection-from-documents-and-emails"></a>Office アプリを使用してドキュメントと電子メールからラベルと保護を削除する

[**ホーム**] タブで、リボンの [**感度**] ボタンを選択し、現在選択されているラベルをクリアします。

または、[**感度**] ボタンから [**バーの表示**] を選択した場合は、Azure Information Protection バーから [**ラベルの削除**] アイコンを選択できます。

![Azure Information Protection バー - [ラベルの削除]](../media/v2delete-label.png)

[**ラベルの削除**] アイコンがすぐに使用できない場合は、まず [**ラベルの編集**] アイコンを選択します。

![Azure Information Protection バー - [ラベルの編集]](../media/v2edit-label.png)

[**ラベルの削除**] アイコンが表示されない場合は、すべてのドキュメントと電子メールにラベルが付いている必要があるため、管理者はこのオプションを使用できません。

## <a name="using-file-explorer-to-remove-labels-and-protection-from-files"></a>エクスプローラーを使用してファイルからラベルと保護を削除する

エクスプローラーを使用すると、1 つのファイル、複数のファイル、またはフォルダーからラベルと保護をすばやく削除することができます。 フォルダーを選択すると、そのフォルダー内のすべてのファイルとサブフォルダーが自動的に選択されます。 

1. エクスプローラーで、1 つのファイル、複数のファイル、またはフォルダーを選択します。 右クリックして **[分類して保護する]** を選択します。

2. ラベルを削除するには: **[分類と保護 - Azure Information Protection]** ダイアログ ボックスで、**[ラベルの削除]** をクリックします。 保護を適用するようにラベルが構成されていた場合、その保護は自動的に削除されます。

3. 1 つのアプリケーションからカスタムの保護を削除するには: **[分類と保護 - Azure Information Protection]** ダイアログ ボックスで、**[Protect with custom permissions]**(カスタム アクセス許可で保護) オプションをオフにします。 

4. 複数のファイルからカスタムの保護を削除するには: **[分類と保護 - Azure Information Protection]** ダイアログ ボックスで、**[Remove custom permissions]** (カスタム アクセス許可の削除) をクリックします。

5. **[適用]** をクリックし、**"作業が終了しました"** というメッセージで結果が示されるまで待ちます。 次に、**[閉じる]** をクリックします。


## <a name="other-instructions"></a>その他の手順
他の操作手順については、Azure Information Protection ユーザー ガイドを参照してください。

- [実行する操作](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>管理者向け追加情報    

「[秘密度ラベルについ](/microsoft-365/compliance/sensitivity-labels)て」を参照してください。

