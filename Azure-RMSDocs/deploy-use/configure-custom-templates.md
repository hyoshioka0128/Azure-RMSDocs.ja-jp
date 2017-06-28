---
title: "Azure RMS のカスタム テンプレートを構成する - AIP"
description: "使用権限のテンプレートを構成および管理するための管理者用の情報および手順です。 テンプレートを使用すると、ユーザーおよび他の管理者は、承認されたユーザーにアクセスが制限されている機密ファイルにポリシーを簡単に適用できます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 1775d8d0-9a59-42c8-914f-ce285b71ac1c
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 27ffbc6eb9e88840f1b33c59b76bdaa5d028cc36
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
ms.translationtype: HT
ms.contentlocale: ja-JP
---
# <a name="configuring-custom-templates-for-the-azure-rights-management-service"></a>Azure Rights Management サービスのカスタム テンプレートを構成する

>*適用対象: Azure Information Protection、Office 365*

Azure Rights Management サービスを[アクティブ化](activate-service.md)すると、ユーザーは&2; つの既定のテンプレートを自動的に使用できるようになります。これにより、組織内の承認されたユーザーにアクセスが制限されている機密ファイルに権限管理ポリシーを簡単に適用できるようになります。 これらの&2; つのテンプレートには、次の権限ポリシーの制限があります。

-   保護されたコンテンツの読み取り専用の表示

    -   表示名: **&lt;組織名&gt; - 社外秘、表示のみ**

    -   特定の権限:コンテンツの表示

-   保護されたコンテンツの読み取りまたは変更の権限

    -   表示名: **&lt;組織名&gt; - 社外秘**

    -   特定の権限:コンテンツの表示、ファイルの保存、コンテンツの編集、割り当てられた権限の表示、Macro の許可、転送、返信、全員に返信

また、ユーザーは [Azure Information Protection クライアント](../rms-client/aip-client.md)を使用して独自のアクセス許可を定義できます。 また、Outlook クライアントおよび Outlook Web Access の場合、ユーザーは [[転送不可]](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails) オプションを選択できます。

多くの組織では、既定のテンプレートで十分です。 ただし、独自のカスタム権限ポリシー テンプレートを作成する必要がある場合は、作成できます。 カスタム テンプレートを作成する理由として、次のようなケースが考えられます。

-   テンプレートですべてのユーザーではなく組織のユーザーのサブセットに権限を付与する必要がある。

-   組織のすべてのユーザーがアプリケーションのテンプレート (部門別テンプレート) を表示し、選択できるのではなく、一部のユーザーだけがそれを表示し、選択できるようにする必要がある。

-   表示と編集 (コピーと印刷を除く) などのテンプレートのカスタム権限を定義する必要がある。

-   有効期限や、インターネット接続なしでのコンテンツへのアクセスの可否などの追加のオプションをテンプレート内で構成する必要がある。

このような設定を含むカスタム テンプレートをユーザーが選択できるようにするには、最初にカスタム テンプレートを作成して構成してから発行する必要があります。 使用するテンプレートはおそらく数個で足りるでしょうが、最大 500 個のカスタム テンプレートを Azure に保存することができます。 

カスタム テンプレートの構成と使用については、次の情報を参照してください。

-   [カスタム テンプレートを作成、構成、および発行する方法](create-template.md)

-   [テンプレートのコピー方法](copy-template.md)

-   [テンプレートを削除 (アーカイブ) する方法](remove-template.md)

-   [ユーザー用のテンプレートを更新する方法](refresh-templates.md)

-   [PowerShell を使用してテンプレートを管理する方法](configure-templates-with-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

