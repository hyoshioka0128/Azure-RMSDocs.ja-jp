---
title: Azure Information Protection 統合ラベル付けクライアントを使用してラベルを削除する
description: Azure Information Protection 統合ラベル付けクライアントを使用して、ファイルと電子メールから機密ラベルと保護を削除する手順。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ''
ms.suite: ems
ms.openlocfilehash: 1d7d712c43c3fcc13d3dfaebf0b0bcb110f40354
ms.sourcegitcommit: 7992e1dc791d6d919036f7aa98bcdd21a6c32ad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68428033"
---
# <a name="user-guide-remove-labels-and-protection-from-files-and-emails-that-have-been-labeled-by-azure-information-protection"></a>ユーザー ガイド: Azure Information Protection によってラベル付けされたファイルと電子メールからラベルと保護を削除する

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*
>
> *手順:[Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection 統合クライアントが[コンピューターにインストール](install-client-app.md)されている場合は、ファイルと電子メールから機密ラベルと保護を削除できます。

削除する感度ラベルが保護を適用するように構成されている場合、この操作によってファイルから保護も削除されます。 ラベルを削除する理由を記録するためにメッセージが表示されることがあります。

> [!IMPORTANT]
> 保護を削除するファイルの所有者であるか、保護を削除するアクセス許可 (**抽出**または**フル コントロール**の Rights Management アクセス許可) を付与されている必要があります。

別のラベルまたは別の保護設定セットを選択する場合、ラベルまたは保護を削除する必要はありません。 代わりに、新しいラベルを選択し、必要に応じて、エクスプローラーを使用してカスタムアクセス許可を定義できます。 

次の Office デスクトップ アプリで Office ドキュメントや電子メールを作成または編集している場合、ラベルと保護を削除できます: **Word**、**Excel**、**PowerPoint**、**Outlook**。 

また、**エクスプローラー**を使用して分類と保護の削除を行うこともできます。エクスプローラーは、その他のファイルの種類をサポートしています。複数のファイルからラベルと保護を一度に削除する場合に便利な方法です。

## <a name="using-office-apps-to-remove-labels-and-protection-from-documents-and-emails"></a>Office アプリを使用してドキュメントと電子メールからラベルと保護を削除する

**[ホーム]** タブで、リボンの **[感度]** ボタンを選択し、現在選択されているラベルをクリアします。

または、 **[感度]** ボタンから **[バーの表示]** を選択した場合は、Azure Information Protection バーから **[ラベルの削除]** アイコンを選択できます。

![Azure Information Protection バー - [ラベルの削除]](../media/v2delete-label.png)

**[ラベルの削除]** アイコンがすぐに使用できない場合は、まず **[ラベルの編集]** アイコンを選択します。

![Azure Information Protection バー - [ラベルの編集]](../media/v2edit-label.png)

**[ラベルの削除]** アイコンが表示されない場合は、すべてのドキュメントと電子メールにラベルが付いている必要があるため、管理者はこのオプションを使用できません。

## <a name="using-file-explorer-to-remove-labels-and-protection-from-files"></a>エクスプローラーを使用してファイルからラベルと保護を削除する

エクスプローラーを使用すると、1 つのファイル、複数のファイル、またはフォルダーからラベルと保護をすばやく削除することができます。 フォルダーを選択すると、そのフォルダー内のすべてのファイルとサブフォルダーが自動的に選択されます。 

1. エクスプローラーで、1 つのファイル、複数のファイル、またはフォルダーを選択します。 右クリックして **[分類して保護する]** を選択します。

2. ユーザーを削除するには: **[分類と保護 - Azure Information Protection]** ダイアログ ボックスで、 **[ラベルの削除]** をクリックします。 保護を適用するようにラベルが構成されていた場合、その保護は自動的に削除されます。

3. 1 つのファイルからカスタム保護を削除するには: **[分類と保護 - Azure Information Protection]** ダイアログ ボックスで、 **[カスタム アクセス許可で保護する]** オプションをオフにします。 

4. 複数のファイルからカスタム保護を削除するには: **[分類と保護 - Azure Information Protection]** ダイアログ ボックスで、 **[カスタム アクセス許可の削除]** をクリックします。

5. **[適用]** をクリックし、 **"作業が終了しました"** というメッセージで結果が示されるまで待ちます。 次に、 **[閉じる]** をクリックします。


## <a name="other-instructions"></a>その他の手順
他の操作手順については、Azure Information Protection ユーザー ガイドを参照してください。

- [目的に合ったトピックをクリックしてください](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>管理者向け追加情報    

「[秘密度ラベルの概要」を](/Office365/SecurityCompliance/sensitivity-labels)参照してください。

