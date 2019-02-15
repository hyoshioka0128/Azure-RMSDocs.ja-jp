---
title: Azure Information Protection の保護のみのモード
description: 保護のみモードで Azure Information Protection クライアントを実行しているユーザーの情報。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 01/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 16042717-0d7a-41f5-87e3-12826fda35df
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 57bcea5841823cf5ae15681d247966346b14c1d2
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2019
ms.locfileid: "56253763"
---
# <a name="user-guide-protection-only-mode-for-the-azure-information-protection-client"></a>ユーザー ガイド: Azure Information Protection クライアントの保護のみモード

>*適用対象: Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*


Azure Information Protection クライアントにドキュメントや電子メールを分類するラベルが割り当てられていない場合、このクライアントは**保護のみ**モードで実行されます。 たとえば、このモードでは、Windows ファイル エクスプローラーの使用時に右クリックして **[分類して保護する]** を選択すると、以下が表示される場合があります。

![保護のみモード](../media/protection-only-mode.png)

保護のみモードは、次のようなシナリオで実行されます。

- 組織が分類機能とラベル付け機能を含む Azure Information Protection のサブスクリプションを保有せず、Azure Rights Management サービスを使用したデータ保護を含む Office 365 のサブスクリプションを保有している場合。 
    
    - Azure Information Protection クライアントを使用してファイルを保護し、保護されたファイルを表示できます。 ドキュメントや電子メールを分類したり、ラベル付けしたりすることはできません。

- 組織が一部のユーザーのみを対象とする Azure Information Protection のサブスクリプションを保有している場合。
    
    - このサブスクリプションの組み合わせの場合、管理者は、分類機能とラベル付け機能を一部のユーザーのみが使用できるようにする必要があります。 残りのユーザーは Azure Information Protection クライアントを保護のみモードで実行します。 

- 組織が Azure Information Protection のサブスクリプションを保有しているが、自分用に構成されたラベルを保有していない場合。
    
    - この状況は、グローバル ポリシーのラベルがすべて無効になっていて、アカウントがスコープ付きポリシーに追加されていないときに発生します。 IT 部門が Azure Information Protection のロール アウトを始めたばかりで、ドキュメントとメールを分類するラベルがまだユーザーに提供されていないために発生している可能性があります。 ラベルが提供されるまでは、Azure Information Protection クライアントを使ってファイルを保護し、保護されたファイルを表示できます。

- 組織が Azure Information Protection のサブスクリプションを持っているのに、Azure Information Protection ポリシーをダウンロードできない場合。 
    
    - この状況は、構成の誤りやサインインの失敗によって発生します。 ヘルプ デスクまたは管理者に問い合わせてください。ただし、その間に、Azure Information Protection クライアントを使用してファイルを保護し、保護されたファイルを表示できるようになる可能性があります。

- 組織で Active Directory Rights Management Services (AD RMS) のみを使用しています。 


## <a name="limitations-for-protection-only-mode"></a>保護のみモードの制限

- Office アプリに Azure Information Protection バーは表示されません。 **[保護]** > **[バーの表示]** をクリックしても、このメニュー オプションを使用できません。

- エクスプローラーで **[分類と保護 - Azure Information Protection]** ダイアログ ボックスを使用しても、分類のラベルが表示されません。 その代わり、前の図のように、Rights Management (RMS) テンプレートを選択するオプションが表示されます。 

## <a name="supported-tasks-for-protection-only-mode"></a>保護のみモードでサポートされるタスク

- Office アプリ内からドキュメントと電子メールを保護する (または保護を解除する) には、Office Information Rights Management (IRM) 機能を使用します。次に例を示します。**[ファイル]** > **[情報]** > **[文書の保護]** > **[アクセスの制限]** をクリックします。 詳細については、「[Office 365、Office 2019、Office 2016、または Office 2013 での情報保護の使用](../help-users.md#using-information-protection-with-Office-365-Office 2019-Office-2016-or-Office-2013)」を参照してください。

- ファイルを保護する (または保護を解除する) には、エクスプローラーを使用します。単一ファイル、複数ファイル、またはフォルダーを右クリックし、**[分類して保護する]** を選択します。 管理者が構成した保護を適用するには、**[分類と保護 - Azure Information Protection]** ダイアログ ボックスの **[テンプレートの選択]** をクリックし、使用できるテンプレートのいずれかを選択します。

- 保護されたファイルを表示するには、Azure Information Protection ビューアーを使用します。

- Office アプリからドキュメント追跡サイトにアクセスします。 ただし、このサイトからドキュメントを追跡して取り消すには、有効なサブスクリプションを持っている必要があります。
  
