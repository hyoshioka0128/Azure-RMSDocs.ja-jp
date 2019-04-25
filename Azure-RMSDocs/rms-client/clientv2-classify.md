---
title: Windows 用 Azure Information Protection の統合されたラベル付けクライアントを使用して分類します。
description: 手順については、Azure Information Protection を使用すると、ドキュメントや電子メールを分類する方法は、Windows 用のラベル付けのクライアントを統合します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: 630959840574c0441719d317dda254242cad3b3d
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60182978"
---
# <a name="user-guide-classify-a-file-or-email-by-using-the-azure-information-protection-unified-labeling-client-for-windows"></a>ユーザー ガイド: Windows 用 Azure Information Protection の統合されたラベル付けクライアントを使用して、ファイルや電子メールを分類します。

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*
>
> *手順:[Azure Information Protection unified Windows 用のラベル付けのクライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

> [!NOTE]
> 次の手順に従って、ドキュメントや電子メールを分類します (保護はしません)。 ドキュメントや電子メールを保護する必要もある場合は、[分類して保護する手順](clientv2-classify-protect.md)を参照してください。 どちらの手順を使用するかわからない場合は、管理者またはヘルプ デスクに確認してください。

次の Office デスクトップ アプリでドキュメントや電子メールを作成または編集している場合、それらを最も簡単な方法で分類できます: **Word**、**Excel**、**PowerPoint**、**Outlook**。 

ただし、**エクスプローラー**を利用してファイルを分類することもできます。 この方法では対応しているファイルの種類が増えます。また、複数のファイルを一度に分類できるので便利です。 

## <a name="using-office-apps-to-classify-your-documents-and-emails"></a>Office アプリを使用してドキュメントや電子メールを分類する

**ホーム**] タブで、[、**感度**リボンのボタンをクリックし、いずれかが構成されているラベルを選択します。 以下に例を示します。

![感度ボタンの例](../media/sensitivity-not-set-callout.png)

または、選択した場合に**バーを表示する**から、**感度**ボタン、Azure Information Protection バーからラベルを選択することができます。 以下に例を示します。

![Azure Information Protection バーの例](../media/info-protect-barv2-not-set-callout.png)

"General"などのラベルを設定する次のように選択します。**全般**します。 現在のドキュメントや電子メールに適用するラベルがわからない場合は、ラベルのツールヒントで、各ラベルの詳細と適用する場合を参照してください。 

ラベルがドキュメントに既に適用され、ラベルを変更する場合は、別のラベルを選択できます。 Azure Information Protection バーを表示して、ラベルが、バーを選択して、最初に表示されていない場合、**ラベルの編集**アイコンは、現在のラベル値の横にあります。

ラベルの手動選択に加え、次の方法でラベルを適用することもできます。

- 管理者が既定のラベルを構成済み。そのまま使用するか、変更することができます。

- 管理者は、機密情報が検出されたときに自動的に設定するラベルを構成します。

- 管理者が構成済みの機密情報が検出されると、および推奨事項に同意するように求められます (とラベルが適用されるキーを押す)、ラベルが推奨されるか、拒否 (推奨されたラベルは適用されません)。

### <a name="exceptions-for-the-sensitivity-button"></a>感度ボタンの例外

##### <a name="dont-see-the-sensitivity-button-in-your-office-apps"></a>Office アプリでの感度ボタンが表示されない場合

- Azure Information Protection の統合されたラベル付けクライアントがない[インストール](install-unifiedlabelingclient-app.md)します。

- 表示されない場合、**感度**リボンのボタンしますが、表示、**保護**代わりにラベルが付いたボタンをクリックする必要があります、Azure Information Protection クライアントのインストールと Azure Information Protection ではありません統一されたラベル付けクライアント。 [詳細情報](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)

##### <a name="is-the-label-that-you-expect-to-see-not-displayed"></a>表示されるはずのラベルが表示されない場合 

- 管理者が新しいラベルを構成したばかりの場合は、すべてのインスタンスの Office アプリを終了してから、開き直します。 この操作で、ラベルの変更が確認されます。

- 自分のアカウントを含まない範囲のポリシーのラベルである可能性があります。 ヘルプ デスクまたは管理者に問い合わせてください。


## <a name="using-file-explorer-to-classify-files"></a>エクスプローラーを使用してファイルを分類する

エクスプローラーを使用すると、1 つのファイル、複数のファイル、またはフォルダーをすばやく分類することができます。 

フォルダーを選択すると、そのフォルダー内のすべてのファイルとサブフォルダーが設定された分類で自動的に選択されます。 ただし、そのフォルダーまたはサブフォルダー内に作成した新しいファイルは、自動的に分類されません。

エクスプローラーを使用してファイルを分類する際に、1 つまたは複数のラベルが淡色表示になっている場合、選択したファイルは保護なしの分類をサポートしません。

管理者ガイドには、保護なしの分類をサポートするファイルの種類の詳細な一覧が含まれています。「[分類のみにサポートされているファイルの種類](clientv2-admin-guide-file-types.md#file-types-supported-for-classification-only)」を参照してください。

### <a name="to-classify-a-file-by-using-file-explorer"></a>エクスプローラーを使用してファイルを分類するには

1. エクスプローラーで、1 つのファイル、複数のファイル、またはフォルダーを選択します。 右クリックして **[分類して保護する]** を選択します。 以下に例を示します。
    
    ![Azure Information Protection を使用する場合のファイル エクスプローラーの右クリック オプション [分類して保護する]](../media/right-click-classify-protect-folder.png)

2. **[分類と保護 - Azure Information Protection]** ダイアログ ボックスで、Office アプリケーションでの操作と同様にラベルを使用し、管理者によって定義されたとおりに分類を設定します。 
    
    選択できるラベルがない場合 (ラベルが淡色表示されている場合): 選択したファイルは分類をサポートしていません。 以下に例を示します。
    
    ![[分類と保護 - Azure Information Protection]** ダイアログ ボックスで使用できるラベルがない](../media/v2info-protect-dialog-labels-dimmed.png)

3. 分類をサポートしていないファイルを選択した場合は、**[閉じる]** をクリックします。 このファイルは保護せずに分類することはできません。
    
    ラベルを選択した場合は、**[適用]** をクリックし、**"作業が終了しました"** というメッセージで結果が示されるまで待ちます。 次に、 **[閉じる]** をクリックします。

選択したラベルを変更する場合は、この手順を繰り返して、別のラベルを選択します。

ファイルを電子メールで送信したり、別の場所に保存した場合にも、指定した分類はファイルに設定されたままです。 

## <a name="other-instructions"></a>その他の手順

Windows 用 Azure Information Protection の統合されたラベル付けクライアント ユーザーからの複数の操作手順を紹介します。

- [目的に合ったトピックをクリックしてください](clientv2-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>管理者向け追加情報

参照してください[機密ラベルの概要](/Office365/SecurityCompliance/sensitivity-labels)します。

