---
title: Azure Information Protection のドキュメント追跡
description: 管理者が Azure Information Protection のドキュメント追跡を構成および使用するための手順と情報です。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 03/16/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 983ecdc9-5631-48b8-8777-f4cbbb4934e8
ROBOTS: NOINDEX
ms.subservice: doctrack
ms.reviewer: eymanor
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 5cc94944405b00139f472a2ab962706dd1f76dd8
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/29/2020
ms.locfileid: "97807435"
---
# <a name="admin-guide-configuring-and-using-document-tracking-for-azure-information-protection-using-the-classic-client"></a>管理者ガイド: 従来のクライアントを使用した Azure Information Protection のドキュメント追跡の構成と使用

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8、Windows Server 2019、Windows Server 2016、windows Server 2012 R2、windows server 2012 *
>
>***関連する内容**:[Windows 用 Azure Information Protection クラシック クライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

> [!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure Portal の **Azure Information Protection のクラシック クライアント** と **ラベル管理** は、**2021 年 3 月 31 日** をもって **非推奨** になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

ドキュメント追跡と AIP classic クライアントを [サポートするサブスクリプション](https://www.microsoft.com/cloud-platform/azure-information-protection-features) がある場合、組織内のすべてのユーザーに対してドキュメント追跡サイトが既定で有効になります。 ドキュメント追跡では、保護されたドキュメントがアクセスされた日時についてユーザーおよび管理者に情報を提供します。ドキュメント追跡は必要に応じて取り消すこともできます。

## <a name="using-powershell-to-manage-the-document-tracking-site"></a>PowerShell を使用したドキュメント追跡サイトの管理

次のセクションでは、PowerShell を使用してドキュメント追跡サイトを管理する方法について説明します。 PowerShell モジュールのインストール手順については、「 [AIPService powershell モジュールのインストール](../install-powershell.md)」を参照してください。

各コマンドレットの詳細については、各リンク先ページをご覧ください。

### <a name="privacy-controls-for-your-document-tracking-site"></a>ドキュメント追跡サイトのプライバシー管理

プライバシー要件により、組織ですべてのドキュメント追跡情報を表示できない場合は、 [disable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/disable-aipservicedocumenttrackingfeature) コマンドレットを使用してドキュメント追跡を無効にすることができます。 

このコマンドレットは、組織内のすべてのユーザーが保護されたドキュメントへのアクセスを追跡したり取り消ししたりできないように、ドキュメント追跡サイトへのアクセスを無効にします。 [Enable-AipServiceDocumentTrackingFeature](/powershell/module/aipservice/enable-aipservicedocumenttrackingfeature)を使用すると、いつでもドキュメント追跡を再度有効にできます。また、 [Get AipServiceDocumentTrackingFeature](/powershell/module/aipservice/get-aipservicedocumenttrackingfeature)を使用して、ドキュメント追跡が現在有効になっているか無効になっているかを確認できます。 

ドキュメント追跡サイトを有効にすると、既定では、保護されたドキュメントにアクセスしようとしている人の電子メール アドレス、アクセスを試みた日時、その人がいる位置などの情報が表示されます。 このレベルの情報は、共有ドキュメントの使用方法を決めたり、不審なアクティビティが確認された際にアクセス権を取り消すべきかどうかを判断したりするのに役立ちます。 ただし、このユーザー情報へのアクセス権は、プライバシー保護の観点から一部またはすべてのユーザーに対して無効にする必要がある場合もあります。 

このアクティビティが他のユーザーによって追跡されていないユーザーがいる場合は、Azure AD に格納されているグループにそのユーザーを追加し、 [AipServiceDoNotTrackUserGroup](/powershell/module/aipservice/Set-AipServiceDoNotTrackUserGroup) コマンドレットでこのグループを指定します。 このコマンドレットを実行するとき、指定できるグループは 1 つだけです。 ただし、グループは入れ子構造にすることができます。 

これらのグループ メンバーについて、ユーザーは、ドキュメント追跡サイトに対するアクティビティが共有ドキュメントに関連している場合、そのアクティビティを表示できません。 さらに、ドキュメントを共有するユーザーに電子メール通知は送信されません。

この構成を使用する場合、引き続きすべてのユーザーがドキュメント追跡サイトを使用でき、保護されたドキュメントへのアクセスを取り消すことができます。 ただし、Set-AipServiceDoNotTrackUserGroup コマンドレットを使用して指定したユーザーのアクティビティは表示されません。

この設定では、エンド ユーザーのみに影響します。 Azure Information Protection の管理者は、AipServiceDoNotTrackUserGroup を使用してユーザーを指定した場合でも、常にすべてのユーザーのアクティビティを追跡できます。 管理者がユーザーのドキュメントを追跡する方法の詳細については、「[ユーザーのドキュメントの追跡と取り消し](#tracking-and-revoking-documents-for-users)」のセクションをご覧ください。


### <a name="logging-information-from-the-document-tracking-site"></a>ドキュメント追跡サイトからのログ情報

ドキュメント追跡サイトからログ情報をダウンロードするには、次のコマンドレットを使用します。

- [Get AipServiceTrackingLog](/powershell/module/aipservice/Get-AipServiceTrackingLog)
    
    このコマンドレットは、ドキュメントを保護した特定のユーザー (Rights Management の発行者) または保護されたドキュメントにアクセスしたユーザーの保護されたドキュメントに関する追跡情報を返します。 このコマンドレットは、"指定したユーザーがどの保護されたドキュメントにアクセスまたは追跡したか?" という質問に回答するために役立ちます。

- [Get-AipServiceDocumentLog](/powershell/module/aipservice/Get-AipServiceDocumentLog)
    
    このコマンドレットは、特定のユーザー (Rights Management の発行者) がドキュメントを保護したかドキュメントの Rights Management 所有者であった場合、または保護されたドキュメントがそのユーザーに直接アクセス権を付与するように構成された場合に、そのユーザーの追跡されるドキュメントに関する保護情報を返します。 このコマンドレットは、"指定されたユーザーに対してドキュメントをどのように保護するか?" という質問に回答するために役立ちます。

## <a name="destination-urls-used-by-the-document-tracking-site"></a>ドキュメント追跡サイトで使用される追跡先 URL

次の Url はドキュメント追跡に使用され、Azure Information Protection クライアントとインターネットを実行するクライアント間のすべてのデバイスとサービスで許可される必要があります。 たとえば、これらの URL をファイアウォールに追加します。あるいは、Internet Explorer でセキュリティ強化を使用している場合は信頼済みサイトに追加します。

-  `https://*.azurerms.com`

- `https://*.microsoftonline.com`

- `https://*.microsoftonline-p.com`

- `https://ecn.dev.virtualearth.net`

これらの URL は、Bing マップでユーザーの位置情報を表示するために使用される virtualearth.net の URL を除き、Azure Rights Management サービスでは標準です。

## <a name="tracking-and-revoking-documents-for-users"></a>ユーザーのドキュメントの追跡と取り消し

ユーザーは、ドキュメント追跡サイトにサインインすると、Azure Information Protection クライアントを使って保護しているドキュメント追跡したり取り消したりすることができます。 テナントの Azure AD グローバル管理者としてサインインすると、[管理者] アイコンをクリックし、管理者モードに切り替えることができます。 その他の管理者ロールでは、このドキュメント追跡サイト用のモードはサポートされません。 

![ドキュメント追跡サイトの [管理者] アイコン](../media/tracking-site-admin-icon.png)

管理者モードでは、組織内のユーザーが Azure Information Protection クライアントを使用して追跡することを選択したドキュメントを表示できます。

> [!NOTE] 
> グローバル管理者でもこのアイコンが表示されない場合は、まだドキュメントを共有していません。 その場合、https://portal.azurerms.com/#/admin の URL からドキュメント追跡サイトにアクセスします。

管理者モードで実行したアクションは監査され、使用状況ログ ファイルに記録されます。これを確認してから次に進む必要があります。 このログ記録の詳細については、次のセクションを参照してください。

管理者モードの場合、ユーザーまたはドキュメントを指定して検索できます。 ユーザーを指定して検索すると、指定したユーザーが Azure Information Protection クライアントを使用して追跡することを選択したドキュメントを表示できます。 

ドキュメントを指定して検索すると、Azure Information Protection クライアントを使用してそのドキュメントを追跡した組織内のすべてのユーザーを表示できます。 検索結果を調べて、ユーザーが保護したドキュメントを追跡し、必要に応じてそれらのドキュメントを取り消すことができます。 

管理者モードを終了するには、**[管理者モードを終了する]** の横にある **[X]** をクリックします。

![ドキュメント追跡サイトでは、管理者モードを終了します。](../media/tracking-site-exit-admin-icon.png)

ドキュメント追跡サイトを使用する手順については、ユーザー ガイドの「[ドキュメントを追跡して取り消す](client-track-revoke.md)」を参照してください。

### <a name="using-powershell-to-register-labeled-documents-with-the-document-tracking-site"></a>PowerShell を使ってドキュメント追跡サイトにラベル付きのドキュメントを登録する

ドキュメントを追跡および取り消しできるようにするためには、まずこれをドキュメント追跡サイトに登録する必要があります。 ユーザーが Azure Information Protection クライアントを使っている場合、このアクションは、エクスプローラーまたは各 Office アプリの **[追跡と取り消し]** オプションを選択すると発生します。

[Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel) コマンドレットを使ってユーザーのファイルにラベルを付けて保護する場合、*EnableTracking* パラメーターを使ってドキュメント追跡サイトにファイルを登録できます。 例:

```ps
Set-AIPFileLabel -Path C:\Projects\ -LabelId ade72bf1-4714-4714-4714-a325f824c55a -EnableTracking
```

## <a name="usage-logging-for-the-document-tracking-site"></a>ドキュメント追跡サイトの使用状況のログ記録

使用状況ログ ファイルの 2 つのフィールド **AdminAction** と **ActingAsUser** は、ドキュメント追跡に適用できます。

**AdminAction** - このフィールドは、管理者が管理者モードでドキュメント追跡サイトを使用した場合 (たとえば、ユーザーの代理でドキュメントを取り消したりドキュメントが共有された日時を確認したりする目的で) に true になります。 ユーザーがドキュメント追跡サイトにサインインすると、このフィールドは空になります。

**ActingAsUser** - AdminAction フィールドが true の場合、このフィールドには、検索したユーザーまたはドキュメント所有者の代理で管理者が操作しているユーザー名が含まれます。 ユーザーがドキュメント追跡サイトにサインインすると、このフィールドは空になります。 

また、ユーザーと管理者がドキュメント追跡サイトを使用する方法をログに記録する要求の種類もあります。 たとえば、**RevokeAccess** は、ユーザーまたはユーザーの代理の管理者が、ドキュメント追跡サイトでドキュメントを取り消した場合の要求の種類です。 この要求の種類と AdminAction フィールドを組み合わせて、ユーザーが自分のドキュメントを取り消したか (AdminAction フィールドが空)、管理者がユーザーの代理でドキュメントを取り消したか (AdminAction が true) を判断できます。

使用状況ログの詳細については、「 [Azure Information Protection からの保護の使用状況のログと分析](../log-analyze-usage.md)」を参照してください。

## <a name="next-steps"></a>次のステップ
Azure Information Protection クライアント用にドキュメント追跡サイトを構成した後は、このクライアントのサポートに必要な追加情報を以下の記事でご覧ください。

- [カスタマイズ](client-admin-guide-customizations.md)

- [クライアントのファイルと使用状況ログ](client-admin-guide-files-and-logging.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)

