---
title: "Azure Information Protection のドキュメント追跡"
description: "管理者が Azure Information Protection のドキュメント追跡を構成して使用する方法を説明します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 983ecdc9-5631-48b8-8777-f4cbbb4934e8
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 727ff705c4a90a9c029820332983b4cf7bec5e05
ms.sourcegitcommit: 31c79d948ec3089a4dc65639f1842c07c7aecba6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2018
---
# <a name="admin-guide-configuring-and-using-document-tracking-for-azure-information-protection"></a>管理者ガイド: Azure Information Protection のドキュメント追跡の構成と使用

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012, Windows Server 2008 R2*

[ドキュメント追跡をサポートするサブスクリプション](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)がある場合、組織内のすべてのユーザーに対してドキュメント追跡サイトが既定で有効になっています。 ユーザーと管理者は、保護されたドキュメントにいつアクセスがあったのかをドキュメント追跡によって知ることができ、必要に応じて追跡対象のドキュメントへのアクセス権を取り消すことができます。

## <a name="privacy-controls-for-your-document-tracking-site"></a>ドキュメント追跡サイトのプライバシー管理

組織のプライバシーに関する要件により、すべてのドキュメント追跡情報の表示が禁止されている場合は、[Disable-AadrmDocumentTrackingFeature](/powershell/module/aadrm/disable-aadrmdocumenttrackingfeature) コマンドレットを使用してドキュメント追跡を無効にすることができます。 

このコマンドレットは、組織内のすべてのユーザーが保護されたドキュメントへのアクセスを追跡したり取り消ししたりできないように、ドキュメント追跡サイトへのアクセスを無効にします。 ドキュメント追跡は、[Enable-AadrmDocumentTrackingFeature](/powershell/module/aadrm/enable-aadrmdocumenttrackingfeature) を使用して、いつでも有効にしなおすことができます。また、[Get-AadrmDocumentTrackingFeature](/powershell/module/aadrm/get-aadrmdocumenttrackingfeature) を使用して、ドキュメント追跡が現在有効になっているか無効になっているかを確認できます。 これらのコマンドレットを使用するには、バージョン **2.3.0.0** 以降の PowerShell 用 Azure Rights Management (AADRM) モジュールが必要です。 

ドキュメント追跡サイトを有効にすると、既定では、保護されたドキュメントにアクセスしようとしている人の電子メール アドレス、アクセスを試みた時刻、その人がいる位置情報などが示されます。 このレベルの情報は、共有ドキュメントの使用方法を決めたり、不審なアクティビティが確認された際にアクセス権を取り消すべきかどうかを判断したりするのに役立ちます。 ただし、このユーザー情報へのアクセス権は、プライバシー保護の観点から一部またはすべてのユーザーに対して無効にする必要がある場合もあります。 

他のユーザーがアクティビティを追跡すべきではないユーザーがいる場合は、Azure AD に格納されているグループにそのユーザーを追加し、[Set-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/Set-AadrmDoNotTrackUserGroup) コマンドレットでこのグループを指定します。 このコマンドレットを使用するときに指定できるグループは 1 つだけです。 ただし、グループは入れ子構造にすることができます。 

これらのグループ メンバーについては、ユーザーがグループ メンバーと共有したドキュメントに関連するアクティビティが発生した場合に、ドキュメント追跡サイトでユーザーがアクティビティを確認することはできません。 また、ドキュメントを共有したユーザーには電子メール通知が送信されません。

この構成を使用する場合、引き続きすべてのユーザーがドキュメント追跡サイトを使用でき、保護されたドキュメントへのアクセスを取り消すことができます。 ただし、Set-AadrmDoNotTrackUserGroup コマンドレットを使用して指定したユーザーのアクティビティを確認することはできません。

この設定はエンド ユーザーのみに影響します。 Azure Information Protection の管理者は、Set-AadrmDoNotTrackUserGroup を使用して指定されているユーザーも含めた、すべてのユーザーのアクティビティを常に追跡できます。 管理者がユーザーのドキュメントを追跡する方法については、「[ユーザーのドキュメントの追跡と取り消し](#tracking-and-revoking-documents-for-users)」のセクションをご覧ください。

このオプションが不要になった場合は、[Clear-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/Clear-AadrmDoNotTrackUserGroup) を使用できます。 または、ユーザーを選択的に削除するには、グループからユーザーを削除します。その際、[グループ キャッシュ](../plan-design/prepare.md#group-membership-caching-by-azure-information-protection)にご注意ください。 このオプションが現在使用中であるかどうかは、[Get-AadrmDoNotTrackUserGroup](/powershell/module/aadrm/get-AadrmDoNotTrackUserGroup) を使用して確認できます。 このグループ構成のコマンドレットを使用するには、バージョン **2.10.0.0** 以降の PowerShell 用 Azure Rights Management (AADRM) モジュールが必要です。

これらのコマンドレットの詳細については、各リンク先ページをご覧ください。 PowerShell モジュールのインストール手順については、「[AADRM PowerShell モジュールのインストール](../deploy-use/install-powershell.md)」を参照してください。 事前にモジュールをダウンロードしてインストールしてある場合は、`(Get-Module aadrm –ListAvailable).Version` を実行してバージョン番号を確認します。


## <a name="destination-urls-used-by-the-document-tracking-site"></a>ドキュメント追跡サイトで使用される追跡先 URL

次の URL はドキュメント追跡で使用されます。Azure Information Protection を実行するクライアントとインターネットとの間にあるすべてのデバイスとサービスで、この URL を許可する必要があります。 たとえば、これらの URL をファイアウォールに追加します。あるいは、Internet Explorer でセキュリティ強化を使用している場合は信頼済みサイトに追加します。

-  `https://*.azurerms.com`

- `https://*.microsoftonline.com`

- `https://*.microsoftonline-p.com`

- `https://ecn.dev.virtualearth.net`

これらの URL は、Bing マップでユーザーの位置情報を表示するために使用される virtualearth.net の URL を除き、Azure Rights Management サービスでは標準です。

## <a name="tracking-and-revoking-documents-for-users"></a>ユーザーのドキュメントの追跡と取り消し

ユーザーは、ドキュメント追跡サイトにサインインすると、Azure Information Protection クライアントを使って保護しているドキュメント、または Rights Management 共有アプリケーションを使って共有しているドキュメントを、追跡したり取り消したりすることができます。 Azure Information Protection の管理者 (全体管理者) としてサインインすると、[管理者] アイコンをクリックし、管理者モードに切り替えることができます。 管理者モードでは、組織内のユーザーが Azure Information Protection クライアントを使用して追跡することを選択したドキュメントや、Rights Management 共有アプリケーションを使用して共有したドキュメントを表示できます。

![ドキュメント追跡サイトの [管理者] アイコン](../media/tracking-site-admin-icon.png)

> [!NOTE] 
> グローバル管理者でもこのアイコンが表示されない場合、ドキュメントを共有していません。 その場合、次の URL からドキュメント追跡サイトにアクセスします: https://portal.azurerms.com/#/admin

管理者モードで実行したアクションは監査され、使用状況ログ ファイルに記録されます。これを確認してから次に進む必要があります。 このログ記録の詳細については、次のセクションを参照してください。

管理者モードの場合、ユーザーまたはドキュメントを指定して検索できます。 ユーザーを指定して検索すると、指定したユーザーが Azure Information Protection クライアントを使用して追跡することを選択したドキュメントや、Rights Management 共有アプリケーションを使用して共有したドキュメントを表示できます。 

ドキュメントを指定して検索すると、Azure Information Protection クライアントを使用してそのドキュメントを追跡した組織内のすべてのユーザーや、Rights Management 共有アプリケーションを使用して共有したドキュメントを表示できます。 検索結果を調べて、ユーザーが保護したドキュメントを追跡し、必要に応じてそのドキュメントを取り消すことができます。 

管理者モードを終了するには、**[管理者モードを終了する]** の横にある **[X]** をクリックします。

![ドキュメント追跡サイトで管理者モードを終了する](../media/tracking-site-exit-admin-icon.png)

ドキュメント追跡サイトを使用する手順については、ユーザー ガイドの「[RMS 共有アプリケーションを使用してドキュメントを追跡および取り消す](client-track-revoke.md)」を参照してください。

## <a name="usage-logging-for-the-document-tracking-site"></a>ドキュメント追跡サイトの使用状況のログ記録

使用状況ログ ファイルの 2 つのフィールド **AdminAction** と **ActingAsUser** は、ドキュメント追跡に適用できます。

**AdminAction** - このフィールドは、管理者が管理者モードでドキュメント追跡サイトを使用した場合 (たとえば、ユーザーの代理でドキュメントを取り消した場合や、ドキュメントが共有された時間を確認した場合) に true になります。 ユーザーがドキュメント追跡サイトにサインインすると、このフィールドは空になります。

**ActingAsUser** - AdminAction フィールドが true の場合、このフィールドには、検索したユーザーまたはドキュメント所有者の代理で管理者が操作しているユーザー名が含まれます。 ユーザーがドキュメント追跡サイトにサインインすると、このフィールドは空になります。 

また、ユーザーと管理者がドキュメント追跡サイトを使用する方法をログに記録する要求の種類もあります。 たとえば、**RevokeAccess** は、ユーザーまたはユーザーの代理の管理者が、ドキュメント追跡サイトでドキュメントを取り消した場合の要求の種類です。 この要求の種類と AdminAction フィールドを組み合わせて、ユーザーが自分のドキュメントを取り消したか (AdminAction フィールドが空)、管理者がユーザーの代理でドキュメントを取り消したか (AdminAction が true) を判断できます。


使用状況ログの詳細については、「[Azure Rights Management サービスの使用状況をログに記録して分析する](../deploy-use/log-analyze-usage.md)」を参照してください。



## <a name="next-steps"></a>次の手順
Azure Information Protection クライアント用にドキュメント追跡サイトを構成した後は、このクライアントのサポートに必要な追加情報を以下の記事でご覧ください。

- [カスタマイズ](client-admin-guide-customizations.md)

- [クライアント ファイルおよび使用状況ログの記録](client-admin-guide-files-and-logging.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
