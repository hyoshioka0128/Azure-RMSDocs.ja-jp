---
title: "Azure Information Protection クライアントの保護のみモード"
description: "保護のみモードで Azure Information Protection クライアントを実行しているユーザーの情報。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 16042717-0d7a-41f5-87e3-12826fda35df
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ffed64826982756072456be18cced0226b6bb6cc
ms.openlocfilehash: bc81b8587e999e6cbb036942e1c5d37e1e2b319b


---

# <a name="protection-only-mode-for-the-azure-information-protection-client"></a>Azure Information Protection クライアントの保護のみモード

Azure Information Protection ポリシーがない Azure Information Protection クライアントを実行すると、**保護のみ**モードで表示されます。 たとえば、エクスプローラーを使用し、右クリックして **[分類して保護する]** を右クリックします。

![保護のみモード](../media/protection-only-mode.png)

 このモードは、次のようなシナリオで実行します。

- 組織が Azure Information Protection のサブスクリプション (データの分類と保護用) を持っておらず、Azure Rights Management サービスのサブスクリプション (Office 365 でのデータ保護用) を持っている場合。 
    - これはサポートされるシナリオです。Azure Information Protection クライアントを使用してファイルを保護し、保護されたファイルを表示することができます。

- 組織が Azure Information Protection のサブスクリプションを持っているのに、Azure Information Protection ポリシーをダウンロードできない場合。 
    - この状況は、構成の誤りやサインインの失敗によって発生します。 ヘルプ デスクまたは管理者に問い合わせてください。ただし、その間に、Azure Information Protection クライアントを使用してファイルを保護し、保護されたファイルを表示できるようになる可能性があります。

## <a name="limitations-for-protection-only-mode"></a>保護のみモードの制限

- Office アプリに Azure Information Protection バーは表示されません。 **[保護]** > **[バーの表示]** をクリックしても、このメニュー オプションを使用できません。

- エクスプローラーで **[分類と保護 - Azure Information Protection]** ダイアログ ボックスを使用しても、分類のラベルが表示されません。 その代わり、前の図のように、Rights Management (RMS) テンプレートを選択するオプションが表示されます。 

## <a name="supported-tasks-for-protection-only-mode"></a>保護のみモードでサポートされるタスク

- Office アプリからドキュメントと電子メールを保護する (または保護を解除する) には、Office Information Rights Management (IRM) 機能を使用します。たとえば、**[ファイル]** > **[情報]** > **[文書の保護]** > **[アクセスの制限]** をクリックします。 詳細については、「[Office 365、Office 2016、または Office 2013 での情報保護の使用](../deploy-use/help-users.md)」を参照してください。

- ファイルを保護する (または保護を解除する) には、エクスプローラーを使用します。たとえば、1 つまたは複数のファイルまたはフォルダーを右クリックし、**[分類して保護する]** をクリックします。 管理者が構成した保護を適用するには、**[分類と保護 - Azure Information Protection]** ダイアログ ボックスの **[テンプレートの選択]** をクリックし、使用できるテンプレートのいずれかを選択します。

- 保護されたファイルを表示するには、Azure Information Protection ビューアーを使用します。

- Office アプリからドキュメント追跡サイトにアクセスします。 ただし、このサイトからドキュメントを追跡して取り消すには、有効なサブスクリプションを持っている必要があります。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]  



<!--HONumber=Feb17_HO2-->


