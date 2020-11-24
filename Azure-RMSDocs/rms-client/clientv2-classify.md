---
title: Azure Information Protection の統一されたラベル付けクライアントを使用して分類する
description: Azure Information Protection 統合ラベルクライアントを使用して Windows 用にドキュメントと電子メールを分類する方法について説明します。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/03/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 1cb9f1216b8b77b19b8cabb6d884512330221a87
ms.sourcegitcommit: b763a7204421a4c5f946abb7c5cbc06e2883199c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2020
ms.locfileid: "95569887"
---
# <a name="user-guide-classify-a-file-or-email-by-using-the-azure-information-protection-unified-labeling-client-for-windows"></a>ユーザーガイド: Windows 用の Azure Information Protection 統合ラベル付けクライアントを使用してファイルまたは電子メールを分類する

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8*
>
>*Windows 7 または Office 2010 を使用している場合は、「 [AIP For windows And office versions in extended support](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)」を参照してください。*
>
> *手順: [Windows 用の Azure Information Protection 統合ラベル付けクライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

> [!NOTE]
> 次の手順に従って、ドキュメントや電子メールを分類します (保護はしません)。 ドキュメントや電子メールを保護する必要もある場合は、[分類して保護する手順](clientv2-classify-protect.md)を参照してください。 どちらの手順を使用するかわからない場合は、管理者またはヘルプ デスクに確認してください。

Office のデスクトップ アプリ (**Word**、**Excel**、**PowerPoint**、**Outlook**) でドキュメントや電子メールを作成したり編集すると、分類が簡単になります。 

ただし、**エクスプローラー** を利用してファイルを分類することもできます。 この方法では対応しているファイルの種類が増えます。また、複数のファイルを一度に分類できるので便利です。 

## <a name="using-office-apps-to-classify-your-documents-and-emails"></a>Office アプリを使用してドキュメントや電子メールを分類する

[ **ホーム** ] タブで、リボンの [ **感度** ] ボタンを選択し、構成されているラベルのいずれかを選択します。 例:

![感度ボタンの例](../media/sensitivity-not-set-callout.png)

または、[**感度**] ボタンから [**バーの表示**] を選択した場合は、Azure Information Protection バーからラベルを選択できます。 例:

![Azure Information Protection バーの例](../media/info-protect-barv2-not-set-callout.png)

"全般" などのラベルを設定するには、[ **全般**] を選択します。 現在のドキュメントや電子メールに適用するラベルがわからない場合は、ラベルのツールヒントで、各ラベルの詳細と適用する場合を参照してください。 

ラベルがドキュメントに既に適用され、ラベルを変更する場合は、別のラベルを選択できます。 Azure Information Protection バーが表示されていて、選択できるバーにラベルが表示されていない場合は、まず、現在のラベルの値の横にある [ **ラベルの編集** ] アイコンをクリックします。

ラベルの手動選択に加え、次の方法でラベルを適用することもできます。

- 管理者が既定のラベルを構成済み。そのまま使用するか、変更することができます。

- 機密情報が検出されたときに、管理者がラベルを自動的に設定するように構成しました。

- 管理者は、機密情報が検出されたときに推奨ラベルを構成し、推奨事項 (およびラベルが適用されます) を受け入れるか、拒否するかを確認するメッセージが表示されます (推奨ラベルは適用されません)。

### <a name="exceptions-for-the-sensitivity-button"></a>[秘密度] ボタンの例外

##### <a name="dont-see-the-sensitivity-button-in-your-office-apps"></a>Office アプリで [秘密度] ボタンが表示されない場合は、

- Azure Information Protection 統合ラベルクライアントが [インストールさ](install-unifiedlabelingclient-app.md)れていない可能性があります。

- リボンに [ **秘密度** ] ボタンが表示されていない場合でも、ラベル付きの [ **保護** ] ボタンが表示されている場合は、Azure Information Protection クライアント (クラシック) がインストールされており、Azure Information Protection 統一されたラベル付けクライアントではありません。 [詳細情報](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)

##### <a name="is-the-label-that-you-expect-to-see-not-displayed"></a>表示されるはずのラベルが表示されない場合 

- 管理者が新しいラベルを構成したばかりの場合は、すべてのインスタンスの Office アプリを終了してから、開き直します。 この操作で、ラベルの変更が確認されます。

- 自分のアカウントを含まない範囲のポリシーのラベルである可能性があります。 ヘルプ デスクまたは管理者に問い合わせてください。


## <a name="using-file-explorer-to-classify-files"></a>エクスプローラーを使用してファイルを分類する

エクスプローラーを使用すると、1 つのファイル、複数のファイル、またはフォルダーをすばやく分類することができます。 

フォルダーを選択すると、そのフォルダー内のすべてのファイルとサブフォルダーが設定された分類で自動的に選択されます。 ただし、そのフォルダーまたはサブフォルダー内に作成した新しいファイルは、自動的に分類されません。

エクスプローラーを使用してファイルを分類する際に、1 つまたは複数のラベルが淡色表示になっている場合、選択したファイルは保護なしの分類をサポートしません。

管理者ガイドには、保護なしの分類をサポートするファイルの種類の完全なリスト (「[分類のみにサポートされているファイルの種類](clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only)」) が含まれています。

### <a name="to-classify-a-file-by-using-file-explorer"></a>エクスプローラーを使用してファイルを分類するには

1. エクスプローラーで、1 つのファイル、複数のファイル、またはフォルダーを選択します。 右クリックして **[分類して保護する]** を選択します。 次に例を示します。
    
    ![Azure Information Protection を使用する場合のファイル エクスプローラーの右クリック オプション [分類して保護する]](../media/right-click-classify-protect-folder.png)

2. **[分類と保護 - Azure Information Protection]** ダイアログ ボックスで、Office アプリケーションでの操作と同様にラベルを使用し、管理者によって定義されたとおりに分類を設定します。 
    
    選択できるラベルがない場合 (すべてのラベルが淡色表示されている場合): 選択したファイルは分類をサポートしていません。 例:
    
    ![[分類と保護 - Azure Information Protection]** ダイアログ ボックスで使用できるラベルがない](../media/v2info-protect-dialog-labels-dimmed.png)

3. 分類をサポートしていないファイルを選択した場合は、**[閉じる]** をクリックします。 このファイルは保護せずに分類することはできません。
    
    ラベルを選択した場合は、**[適用]** をクリックし、**"作業が終了しました"** というメッセージで結果が示されるまで待ちます。 次に、**[閉じる]** をクリックします。

選択したラベルを変更する場合は、この手順を繰り返して、別のラベルを選択します。

ファイルを電子メールで送信したり、別の場所に保存した場合にも、指定した分類はファイルに設定されたままです。 

## <a name="other-instructions"></a>その他の手順

Windows 用の Azure Information Protection 統合ラベル付けクライアントのユーザーガイドの詳細な手順については、次を参照してください。

- [目的に合ったトピックをクリックしてください](clientv2-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>管理者向け追加情報

「 [秘密度ラベルについ](/microsoft-365/compliance/sensitivity-labels)て」を参照してください。

