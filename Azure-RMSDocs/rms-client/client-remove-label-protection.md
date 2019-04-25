---
title: Azure Information Protection ラベルを削除する
description: Azure Information Protection でラベルが適用されたファイル、または Rights Management で保護されているファイルから、分類ラベルと保護を削除する手順について説明します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ''
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 031bfb196e7f896b49e96d4b94574b43e11a8fe8
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60183244"
---
# <a name="user-guide-remove-labels-and-protection-from-files-and-emails-that-have-been-labeled-by-azure-information-protection-or-protected-by-rights-management"></a>ユーザー ガイド: Azure Information Protection でラベルが適用されたファイル、または Rights Management で保護されているファイルから、ラベルと保護を削除する

>*適用対象: Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*
>
> *手順:[Windows 用の azure Information Protection クライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

[コンピューターに Azure Information Protection クライアントをインストールする](install-client-app.md)と、ファイルと電子メールから分類ラベルと保護を削除することができます。

削除対象のラベルが保護を適用するように構成されている場合、この操作でもファイルから保護が削除されます。 ラベルを削除する理由を記録するためにメッセージが表示されることがあります。

> [!IMPORTANT]
> 保護を削除するファイルの所有者であるか、保護を削除するアクセス許可 (**抽出**または**フル コントロール**の Rights Management アクセス許可) を付与されている必要があります。

別のラベルまたは別の保護設定セットを選択する場合、ラベルまたは保護を削除する必要はありません。 その代わり、新しいラベルを選択し、必要に応じて、カスタム アクセス許可を定義できます (管理者がこの設定を許可している場合)。 

次の Office デスクトップ アプリで Office ドキュメントや電子メールを作成または編集している場合、ラベルと保護を削除できます: **Word**、**Excel**、**PowerPoint**、**Outlook**。 

また、**エクスプローラー**を使用して分類と保護の削除を行うこともできます。エクスプローラーは、その他のファイルの種類をサポートしています。複数のファイルからラベルと保護を一度に削除する場合に便利な方法です。

## <a name="using-office-apps-to-remove-labels-and-protection-from-documents-and-emails"></a>Office アプリを使用してドキュメントと電子メールからラベルと保護を削除する

Information Protection バーの **[ラベルの削除]** アイコンをクリックします。

![Azure Information Protection バー - [ラベルの削除]](../media/delete-label.png)

**[ラベルの削除]** アイコンを使用できない場合は、まず **[ラベルの編集]** アイコンをクリックします。

![Azure Information Protection バー - [ラベルの編集]](../media/edit-label.png)

まだ表示されない場合、**ラベルの削除**アイコン、管理者によりすべてのドキュメントと電子メールはラベルがある必要なために、このオプションを使用することです。

> [!NOTE]
> お使いの Office アプリでこの Information Protection バーが表示されない場合:
>
> - リボンに **[保護]** ボタンが表示されている場合: **[保護]** を選択してから、次のように **[バーの表示]** を選択します。
> 
> - Azure Information Protection クライアントが[インストール](install-client-app.md)されていないか、クライアントが[保護のみモード](client-protection-only-mode.md)で実行されている可能性があります。

## <a name="using-file-explorer-to-remove-labels-and-protection-from-files"></a>エクスプローラーを使用してファイルからラベルと保護を削除する

エクスプローラーを使用すると、1 つのファイル、複数のファイル、またはフォルダーからラベルと保護をすばやく削除することができます。 フォルダーを選択すると、そのフォルダー内のすべてのファイルとサブフォルダーが自動的に選択されます。 

1. エクスプローラーで、1 つのファイル、複数のファイル、またはフォルダーを選択します。 右クリックして **[分類して保護する]** を選択します。

2. ユーザーを削除するには: **[分類と保護 - Azure Information Protection]** ダイアログ ボックスで、**[ラベルの削除]** をクリックします。 保護を適用するようにラベルが構成されていた場合、その保護は自動的に削除されます。

3. 1 つのファイルからカスタム保護を削除するには: **[分類と保護 - Azure Information Protection]** ダイアログ ボックスで、**[カスタム アクセス許可で保護する]** オプションをオフにします。 
    
    **[カスタム アクセス許可で保護する]** オプションが表示されない場合、管理者はお客様がこのオプションを使用することを許可していません。
    
4. 複数のファイルからカスタム保護を削除するには: **[分類と保護 - Azure Information Protection]** ダイアログ ボックスで、**[カスタム アクセス許可の削除]** をクリックします。
    
    **[カスタム アクセス許可の削除]** オプションが表示されない場合、管理者はお客様がこのオプションを使用することを許可していません。

5. **[適用]** をクリックし、**"作業が終了しました"** というメッセージで結果が示されるまで待ちます。 次に、 **[閉じる]** をクリックします。


## <a name="other-instructions"></a>その他の手順
他の操作手順については、Azure Information Protection ユーザー ガイドを参照してください。

- [目的に合ったトピックをクリックしてください](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>管理者向け追加情報    
**[Make the custom permissions option available to users]\(ユーザーがカスタム アクセス許可オプションを使用できるようにする\)** のポリシー設定を有効にする構成手順については、「[Azure Information Protection のポリシー設定を構成する](../configure-policy-settings.md)」を参照してください。

その他の構成手順: [Azure Information Protection ポリシーの構成](../configure-policy.md)

