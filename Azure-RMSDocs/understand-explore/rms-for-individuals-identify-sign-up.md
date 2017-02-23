---
title: "ユーザーが個人用 RMS にサインアップしているかどうかを確認する方法 | Azure Information Protection"
description: "ユーザーが個人用 RMS にサインアップしたかどうかを、管理者はどのようにして知ることができるでしょうか。 この記事で説明している方法、または方法の組み合わせを使用できます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: a36c3d99-a794-4f7a-aafb-64a950f1fcf9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ffed64826982756072456be18cced0226b6bb6cc
ms.openlocfilehash: 5dae8412277be37cd3ff8cfe76c71a8109277146


---


# <a name="how-to-find-out-if-your-users-have-signed-up-for-rms-for-individuals"></a>ユーザーが個人用 RMS にサインアップしているかどうかを確認する方法

>*適用対象: Azure Information Protection*

ユーザーが個人用 RMS にサインアップしたかどうかを、管理者はどのようにして知ることができるでしょうか。 次に示す方法のいずれかを使用する場合もあれば、組み合わせて使用する場合もあります。

-   機密性の高いファイルをどのように保護しているかを (組織外の人物と共同作業している場合は特に) ユーザーにたずねます。

-   組織用の Azure サブスクリプションを所有している場合は、[Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) コマンドレットを使用して、ユーザーに **RIGHTSMANAGEMENT_ADHOC** ライセンスが割り当てられているかどうかを確認します。 このライセンスは、組織に付与された個人向けサブスクリプションの RMS からのものであり、ユーザーがセルフ サービスのサインアップ プロセスで使用できるアクティブなユニットが多数存在します。

-   System Center Configuration Manager などのシステム管理ソリューションを使用して、インストール済みのソフトウェアと使用中のソフトウェアのインベントリを作成します。 たとえば、**MSIP.App.exe** (Azure Information Protection クライアントで使用) と、**ipviewer.exe** (Rights Management 共有アプリケーション用) を探します。 このクライアントとアプリケーションは無料でダウンロードしてインストールできます。これにより、ソフトウェア インベントリで使用する他の特性を識別します。

-   Azure Information Protection クライアントまたは Rights Management 共有アプリケーションによって作成されるファイル名拡張子に注意してください。 .pfile と .ppdf ファイル名拡張子は最もわかりやすい例ですが、他のファイルでは、Rights Management サービスがネイティブで保護しているときに元のファイル名拡張子が変更される場合があります。 詳細については、Azure Information Protection クライアント管理者ガイドの[保護できるファイルの種類](../rms-client/client-admin-guide-file-types.md#file-types-supported-for-protection)に関する記述を参照してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Feb17_HO2-->


