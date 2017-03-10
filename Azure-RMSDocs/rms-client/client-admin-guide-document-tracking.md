---
title: "Azure Information Protection のドキュメント追跡"
description: "管理者が Azure Information Protection のドキュメント追跡を構成して使用する方法を説明します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 983ecdc9-5631-48b8-8777-f4cbbb4934e8
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: f47b177ece91f775d53c72d379d6ffa3a2f3c98b
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="configuring-and-using-document-tracking-for-azure-information-protection"></a>Azure Information Protection のドキュメント追跡の構成と使用

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*

[ドキュメント追跡をサポートするサブスクリプション](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-features)がある場合、組織内のすべてのユーザーに対してドキュメント追跡サイトが既定で有効になっています。 ドキュメント追跡では、ユーザーが共有している保護されたドキュメントにアクセスしようとしている人々の電子メール アドレス、これらの人々がアクセスを試みた時刻、およびその場所などの情報が示されます。 プライバシーに関する要件により、組織でこの情報の表示が禁止されている場合、[Disable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623032) コマンドレットを使用して、ドキュメント追跡サイトへのアクセスを無効にすることができます。 サイトへのアクセスは [Enable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037) を使用して、いつでも再度有効にすることができます。また、[Get-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037) を使用して、アクセスが現在有効になっているか無効になっているかを確認できます。

これらのコマンドを使用するには、バージョン **2.3.0.0** 以降の Windows PowerShell 用 Azure Information Protection モジュールが必要です。 インストール手順については、「[Azure Rights Management 用 Windows PowerShell をインストールする](../deploy-use/install-powershell.md)」を参照してください。

> [!TIP]
> 事前にモジュールをダウンロードしてインストールしてある場合は、`(Get-Module aadrm –ListAvailable).Version` を実行してバージョン番号を確認します。

次の URL はドキュメント追跡で使用されるため、許可する必要があります (たとえば、セキュリティ強化を有効にして Internet Explorer を使用する場合は、信頼済みサイトに追加します):

-   https://&#42;.azurerms.com

-   https://ecn.dev.virtualearth.net

    > [!NOTE]
    > この URL は Bing マップ用です。

-   https://&#42;.microsoftonline.com

-   https://&#42;.microsoftonline-p.com

## <a name="tracking-and-revoking-documents-for-users"></a>ユーザーのドキュメントの追跡と取り消し

ユーザーは、ドキュメント追跡サイトにサインインすると、Azure Information Protection クライアントを使って保護しているドキュメント、または Rights Management 共有アプリケーションを使って共有しているドキュメントを、追跡したり取り消したりすることができます。 Azure Information Protection の管理者 (グローバル管理者) としてサインインすると、[管理者] アイコンをクリックして管理者モードに切り替え、組織内のユーザーが共有しているドキュメントを表示することができます。

![ドキュメント追跡サイトの [管理者] アイコン](../media/tracking-site-admin-icon.png)

管理者モードで実行したアクションは監査され、使用状況ログ ファイルに記録されます。これを確認してから次に進む必要があります。 このログ記録の詳細については、次のセクションを参照してください。

管理者モードの場合、ユーザーまたはドキュメントを指定して検索できます。 ユーザーを指定して検索すると、指定したユーザーが共有したすべてのドキュメントが表示されます。 ドキュメントを指定して検索すると、そのドキュメントを共有した組織内のユーザーが全員表示されます。 検索結果を調べて、ユーザーが共有したドキュメントを追跡し、必要に応じてそのドキュメントを取り消すことができます。 

管理者モードを終了するには、**[管理者モードを終了する]** の横にある **[X]** をクリックします。

![ドキュメント追跡サイトで管理者モードを終了する](../media/tracking-site-exit-admin-icon.png)

ドキュメント追跡サイトを使用する手順については、ユーザー ガイドの「[RMS 共有アプリケーションを使用してドキュメントを追跡および取り消す](client-track-revoke.md)」を参照してください。

## <a name="usage-logging-for-the-document-tracking-site"></a>ドキュメント追跡サイトの使用状況のログ記録

使用状況ログ ファイルの&2; つのフィールド **AdminAction** と **ActingAsUser** は、ドキュメント追跡に適用できます。

**AdminAction** - このフィールドは、管理者が管理者モードでドキュメント追跡サイトを使用した場合 (たとえば、ユーザーの代理でドキュメントを取り消した場合や、ドキュメントが共有された時間を確認した場合) に true になります。 ユーザーがドキュメント追跡サイトにサインインすると、このフィールドは空になります。

**ActingAsUser** - AdminAction フィールドが true の場合、このフィールドには、検索したユーザーまたはドキュメント所有者の代理で管理者が操作しているユーザー名が含まれます。 ユーザーがドキュメント追跡サイトにサインインすると、このフィールドは空になります。 

また、ユーザーと管理者がドキュメント追跡サイトを使用する方法をログに記録する要求の種類もあります。 たとえば、**RevokeAccess** は、ユーザーまたはユーザーの代理の管理者が、ドキュメント追跡サイトでドキュメントを取り消した場合の要求の種類です。 この要求の種類と AdminAction フィールドを組み合わせて、ユーザーが自分のドキュメントを取り消したか (AdminAction フィールドが空)、管理者がユーザーの代理でドキュメントを取り消したか (AdminAction が true) を判断できます。


使用状況ログの詳細については、「[Azure Rights Management サービスの使用状況をログに記録して分析する](../deploy-use/log-analyze-usage.md)」を参照してください。



## <a name="next-steps"></a>次のステップ
Azure Information Protection クライアント用にドキュメント追跡サイトを構成した後は、このクライアントのサポートに必要な追加情報を以下の記事でご覧ください。

- [クライアント ファイルおよび使用状況ログの記録](client-admin-guide-files-and-logging.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
