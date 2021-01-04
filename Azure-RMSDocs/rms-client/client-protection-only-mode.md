---
title: Azure Information Protection の保護のみのモード
description: 保護のみモードで Azure Information Protection クライアントを実行しているユーザーの情報。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 1/13/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 16042717-0d7a-41f5-87e3-12826fda35df
ROBOTS: NOINDEX
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: af64fc43cd137bfe9f9f05c4237d4a617fd0898d
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/29/2020
ms.locfileid: "97807231"
---
# <a name="user-guide-protection-only-mode-for-the-azure-information-protection-client"></a>ユーザー ガイド: Azure Information Protection クライアントの保護のみモード

>***適用対象**: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8 *
>
>***関連する内容**:[Windows 用 Azure Information Protection クラシック クライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure Portal の **Azure Information Protection のクラシック クライアント** と **ラベル管理** は、**2021 年 3 月 31 日** をもって **非推奨** になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Azure Information Protection クライアントにドキュメントや電子メールを分類するラベルが割り当てられていない場合、このクライアントは **保護のみ** モードで実行されます。 たとえば、このモードでは、Windows ファイル エクスプローラーの使用時に右クリックして **[分類して保護する]** を選択すると、以下が表示される場合があります。

![保護のみモード](../media/protection-only-mode.png)

保護のみモードは、次のようなシナリオで実行されます。

- 組織には、分類機能とラベル付け機能を含む Azure Information Protection のサブスクリプションがありませんが、Azure Rights Management サービスを使用したデータ保護を含む Microsoft 365 のサブスクリプションがあります。 
    
    - Azure Information Protection クライアントを使用してファイルを保護し、保護されたファイルを表示できます。 ドキュメントや電子メールを分類したり、ラベル付けしたりすることはできません。

- 組織が一部のユーザーのみを対象とする Azure Information Protection のサブスクリプションを保有している場合。
    
    - このサブスクリプションの組み合わせの場合、管理者は、分類機能とラベル付け機能を一部のユーザーのみが使用できるようにする必要があります。 残りのユーザーは Azure Information Protection クライアントを保護のみモードで実行します。 

- 組織が Azure Information Protection のサブスクリプションを保有しているが、自分用に構成されたラベルを保有していない場合。
    
    - この状況は、グローバル ポリシーのラベルがすべて無効になっていて、アカウントがスコープ付きポリシーに追加されていないときに発生します。 IT 部門が Azure Information Protection のロール アウトを始めたばかりで、ドキュメントとメールを分類するラベルがまだユーザーに提供されていないために発生している可能性があります。 ラベルが提供されるまでは、Azure Information Protection クライアントを使ってファイルを保護し、保護されたファイルを表示できます。

- 組織が Azure Information Protection のサブスクリプションを持っているのに、Azure Information Protection ポリシーをダウンロードできない場合。 
    
    - この状況は、構成の誤りやサインインの失敗によって発生します。 ヘルプ デスクまたは管理者に問い合わせてください。ただし、その間に、Azure Information Protection クライアントを使用してファイルを保護し、保護されたファイルを表示できるようになる可能性があります。

- 組織で Active Directory Rights Management Services (AD RMS) のみを使用しています。 


## <a name="limitations-for-protection-only-mode"></a>保護のみモードの制限

- Office アプリに Azure Information Protection バーは表示されません。 [**保護** する] をクリックすると  >  、このメニューオプションは使用できません。

- エクスプローラーで **[分類と保護 - Azure Information Protection]** ダイアログ ボックスを使用しても、分類のラベルが表示されません。 その代わり、前の図のように、Rights Management (RMS) テンプレートを選択するオプションが表示されます。 

## <a name="supported-tasks-for-protection-only-mode"></a>保護のみモードでサポートされるタスク

- Office アプリ内からドキュメントや電子メールを保護 (および保護解除) するには、office Information Rights Management (IRM) 機能を使用します。たとえば、[**ファイル**  >  **情報**] [ドキュメントの保護] [アクセスの  >    >  **制限**] の順にクリックします。 詳細については、「[Office 365、Office 2019、Office 2016、または Office 2013 での情報保護の使用](../help-users.md#using-information-protection-with-office365-office-2019-office-2016-or-office2013)」を参照してください。

- ファイルを保護する (または保護を解除する) には、エクスプローラーを使用します。たとえば、1 つまたは複数のファイルまたはフォルダーを右クリックし、**[分類して保護する]** をクリックします。 管理者が構成した保護を適用するには、**[分類と保護 - Azure Information Protection]** ダイアログ ボックスの **[テンプレートの選択]** をクリックし、使用できるテンプレートのいずれかを選択します。

- 保護されたファイルを表示するには、Azure Information Protection ビューアーを使用します。

- Office アプリからドキュメント追跡サイトにアクセスします。 ただし、このサイトからドキュメントを追跡して取り消すには、有効なサブスクリプションを持っている必要があります。
  
