---
title: Windows 用 Azure Information Protection の統合されたラベル付けクライアントを使用して機密ラベルを削除します。
description: Azure Information Protection でラベルがファイルから機密ラベルと保護を削除する手順です。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ''
ms.suite: ems
ms.openlocfilehash: 187c36acddb8a6b2e5b1451500640dfd832a8f3f
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60181136"
---
# <a name="user-guide-remove-labels-and-protection-from-files-and-emails-that-have-been-labeled-by-azure-information-protection"></a>ユーザー ガイド: Azure Information Protection でラベル付けするファイルや電子メールからラベルと保護を削除します。

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*
>
> *手順:[Azure Information Protection unified Windows 用のラベル付けのクライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection の統合されたクライアントの場合は[コンピューターにインストールされている](install-client-app.md)ファイルや電子メールから機密ラベルと保護を削除することができます。

保護を適用する構成される機密ラベルを削除すると、この操作により、そのファイルからも保護が削除されます。 ラベルを削除する理由を記録するためにメッセージが表示されることがあります。

> [!IMPORTANT]
> 保護を削除するファイルの所有者であるか、保護を削除するアクセス許可 (**抽出**または**フル コントロール**の Rights Management アクセス許可) を付与されている必要があります。

別のラベルまたは別の保護設定セットを選択する場合、ラベルまたは保護を削除する必要はありません。 代わりに、新しいラベルを選択し、必要に応じて、ファイル エクスプ ローラーを使用してカスタム アクセス許可を定義することができます。 

次の Office デスクトップ アプリで Office ドキュメントや電子メールを作成または編集している場合、ラベルと保護を削除できます: **Word**、**Excel**、**PowerPoint**、**Outlook**。 

また、**エクスプローラー**を使用して分類と保護の削除を行うこともできます。エクスプローラーは、その他のファイルの種類をサポートしています。複数のファイルからラベルと保護を一度に削除する場合に便利な方法です。

## <a name="using-office-apps-to-remove-labels-and-protection-from-documents-and-emails"></a>Office アプリを使用してドキュメントと電子メールからラベルと保護を削除する

**ホーム**] タブで、[、**感度**リボンのボタンをクリックし、現在選択されているラベルをオフにします。

または、選択した場合に**バーを表示する**から、**感度** ボタンを選択できます、**ラベルの削除**Azure Information Protection バーからのアイコン。

![Azure Information Protection バー - [ラベルの削除]](../media/v2delete-label.png)

場合、**ラベルの削除**アイコンはすぐに使用できません、まず選択、**ラベルの編集**アイコン。

![Azure Information Protection バー - [ラベルの編集]](../media/v2edit-label.png)

まだ表示されない場合、**ラベルの削除**アイコン、管理者によりすべてのドキュメントと電子メールはラベルがある必要なために、このオプションを使用することです。

## <a name="using-file-explorer-to-remove-labels-and-protection-from-files"></a>エクスプローラーを使用してファイルからラベルと保護を削除する

エクスプローラーを使用すると、1 つのファイル、複数のファイル、またはフォルダーからラベルと保護をすばやく削除することができます。 フォルダーを選択すると、そのフォルダー内のすべてのファイルとサブフォルダーが自動的に選択されます。 

1. エクスプローラーで、1 つのファイル、複数のファイル、またはフォルダーを選択します。 右クリックして **[分類して保護する]** を選択します。

2. ユーザーを削除するには: **[分類と保護 - Azure Information Protection]** ダイアログ ボックスで、**[ラベルの削除]** をクリックします。 保護を適用するようにラベルが構成されていた場合、その保護は自動的に削除されます。

3. 1 つのファイルからカスタム保護を削除するには: **[分類と保護 - Azure Information Protection]** ダイアログ ボックスで、**[カスタム アクセス許可で保護する]** オプションをオフにします。 

4. 複数のファイルからカスタム保護を削除するには: **[分類と保護 - Azure Information Protection]** ダイアログ ボックスで、**[カスタム アクセス許可の削除]** をクリックします。

5. **[適用]** をクリックし、**"作業が終了しました"** というメッセージで結果が示されるまで待ちます。 次に、 **[閉じる]** をクリックします。


## <a name="other-instructions"></a>その他の手順
他の操作手順については、Azure Information Protection ユーザー ガイドを参照してください。

- [目的に合ったトピックをクリックしてください](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>管理者向け追加情報    

参照してください[機密ラベルの概要](/Office365/SecurityCompliance/sensitivity-labels)します。

