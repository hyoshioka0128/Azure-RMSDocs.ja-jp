---
title: 分類-Azure Information Protection クラシッククライアント
description: Azure Information Protection classic client for Windows を使用するときに、ドキュメントと電子メールを分類する方法について説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/09/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: d65c7690-fab7-4823-845c-8c73903e9c79
ROBOTS: NOINDEX
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 9d2930b7cc5ed01ecb97a59247f0082900d1a606
ms.sourcegitcommit: 78c7ab80be7c292ea4bc62954a4e29c449e97439
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2021
ms.locfileid: "98164166"
---
# <a name="user-guide-classify-a-file-or-email-with-the-azure-information-protection-classic-client"></a>ユーザーガイド: Azure Information Protection クラシッククライアントを使用してファイルまたは電子メールを分類する

>***適用対象**: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8 *
>
>***関連**: [Windows 用のクラシッククライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)ます。 統一されたラベル付けクライアントについては、「 [ユニファイドクライアントユーザーガイド](clientv2-classify.md)」を参照してください。

> [!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure Portal の **Azure Information Protection のクラシック クライアント** と **ラベル管理** は、**2021 年 3 月 31 日** をもって **非推奨** になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

> [!TIP]
> 次の手順に従って、ドキュメントや電子メールを分類します (保護はしません)。 ドキュメントや電子メールを保護する必要もある場合は、[分類して保護する手順](client-classify-protect.md)を参照してください。 どちらの手順を使用するかわからない場合は、管理者またはヘルプ デスクに確認してください。

Office のデスクトップ アプリ (**Word**、**Excel**、**PowerPoint**、**Outlook**) でドキュメントや電子メールを作成したり編集すると、分類が簡単になります。 

ただし、**エクスプローラー** を利用してファイルを分類することもできます。 この方法では対応しているファイルの種類が増えます。また、複数のファイルを一度に分類できるので便利です。 

## <a name="using-office-apps-to-classify-your-documents-and-emails"></a>Office アプリを使用してドキュメントや電子メールを分類する

Azure Information Protection バーを使用して、構成されているラベルを 1 つ選択します。 

たとえば、次の図は、**[秘密度]** が **[未設定]** のため、ドキュメントにまだラベルが設定されていないことを示します。 "General" など、ラベルを設定するには、**[全般]** をクリックします。 現在のドキュメントや電子メールに適用するラベルがわからない場合は、ラベルのツールヒントで、各ラベルの詳細と適用する場合を参照してください。 

![Azure Information Protection バーの例](../media/info-protect-bar-not-set-callout.png)

ラベルがドキュメントに既に適用され、ラベルを変更する場合は、別のラベルを選択できます。 ラベルがバーに表示されない場合は、現在のラベル値の横にある **[ラベルの編集]** アイコンをクリックします。

> [!TIP]
> または、**[ファイル]** タブで **[保護]** ボタンからラベルを選択できます。

ラベルの手動選択に加え、次の方法でラベルを適用することもできます。

- 管理者が既定のラベルを構成済み。そのまま使用するか、変更することができます。

- 機密データが検出された場合に特定のラベルを選択するように推奨するプロンプトを管理者が構成済み。 推奨を受け入れる (ラベルが適用される) か、拒否することができます (推奨されたラベルが適用されない)。

### <a name="exceptions-for-the-azure-information-protection-bar"></a>Azure Information Protection バーの例外 

##### <a name="dont-see-this-information-protection-bar-in-your-office-apps"></a>お使いの Office アプリでこの Information Protection バーが表示されない場合

- Azure Information Protection クライアントが[インストール](install-client-app.md)されていない可能性があります。

- お客様はクライアントをインストールしていますが、管理者がバーを表示しないように設定を構成しています。 代わりに、Office リボンの **[ファイル]** タブで、**[保護]** ボタンからラベルを選択します。 

##### <a name="is-the-label-that-you-expect-to-see-not-displayed-on-the-bar"></a>表示されるはずのラベルがバーに表示されない場合 

- 管理者が新しいラベルを構成したばかりの場合は、すべてのインスタンスの Office アプリを終了してから、開き直します。 この操作で、ラベルの変更が確認されます。

- 自分のアカウントを含まない範囲のポリシーのラベルである可能性があります。 ヘルプ デスクまたは管理者に問い合わせてください。


## <a name="using-file-explorer-to-classify-files"></a>エクスプローラーを使用してファイルを分類する

エクスプローラーを使用すると、1 つのファイル、複数のファイル、またはフォルダーをすばやく分類することができます。 

フォルダーを選択すると、そのフォルダー内のすべてのファイルとサブフォルダーが設定された分類で自動的に選択されます。 ただし、そのフォルダーまたはサブフォルダー内に作成した新しいファイルは、自動的に分類されません。

エクスプローラーを使用してファイルを分類する際に、1 つまたは複数のラベルが淡色表示になっている場合、選択したファイルは保護なしの分類をサポートしません。

管理者ガイドには、保護なしの分類をサポートするファイルの種類の完全なリスト (「[分類のみにサポートされているファイルの種類](client-admin-guide-file-types.md#file-types-supported-for-classification-only)」) が含まれています。

### <a name="to-classify-a-file-by-using-file-explorer"></a>エクスプローラーを使用してファイルを分類するには

1. エクスプローラーで、1 つのファイル、複数のファイル、またはフォルダーを選択します。 右クリックして **[分類して保護する]** を選択します。 次に例を示します。
    
    ![Azure Information Protection を使用する場合のファイル エクスプローラーの右クリック オプション [分類して保護する]](../media/right-click-classify-protect-folder.png)

2. **[分類と保護 - Azure Information Protection]** ダイアログ ボックスで、Office アプリケーションでの操作と同様にラベルを使用し、管理者によって定義されたとおりに分類を設定します。 
    
    選択できるラベルがない場合 (すべてのラベルが淡色表示されている場合): 選択したファイルは分類をサポートしていません。 例:
    
    ![[分類と保護 - Azure Information Protection]** ダイアログ ボックスで使用できるラベルがない](../media/info-protect-dialog-labels-dimmed.png)

3. 分類をサポートしていないファイルを選択した場合は、**[閉じる]** をクリックします。 このファイルは保護せずに分類することはできません。
    
    ラベルを選択した場合は、**[適用]** をクリックし、**"作業が終了しました"** というメッセージで結果が示されるまで待ちます。 次に、**[閉じる]** をクリックします。

選択したラベルを変更する場合は、この手順を繰り返して、別のラベルを選択します。

ファイルを電子メールで送信したり、別の場所に保存した場合にも、指定した分類はファイルに設定されたままです。 
## <a name="other-instructions"></a>その他の手順
他の操作手順については、Azure Information Protection ユーザー ガイドを参照してください。

- [目的に合ったトピックをクリックしてください](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>管理者向け追加情報    
「[Azure Information Protection ポリシーの構成](../configure-policy.md)」を参照してください。

