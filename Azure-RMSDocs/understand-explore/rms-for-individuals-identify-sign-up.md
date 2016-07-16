---
title: "ユーザーが個人用 RMS にサインアップしているかどうかを確認する方法 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: a36c3d99-a794-4f7a-aafb-64a950f1fcf9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 0f355da35dff62ecee111737eb1793ae286dc93e
ms.openlocfilehash: e577366be26f7296079751e72fb6531b9e28c504


---


# ユーザーが個人用 RMS にサインアップしているかどうかを確認する方法

*適用対象: Azure Rights Management*

ユーザーが個人用 RMS にサインアップしたかどうかを、管理者はどのようにして知ることができるでしょうか。 次に示す方法のいずれかを使用する場合もあれば、組み合わせて使用する場合もあります。

-   機密性の高いファイルをどのように保護しているかを (組織外の人物と共同作業している場合は特に) ユーザーにたずねます。

-   組織用の Azure サブスクリプションを所有している場合は、[Get-MsolAccountSku](https://msdn.microsoft.com/library/azure/dn194118.aspx) コマンドレットを使用して、サブスクリプションの 1 つとして **RIGHTSMANAGEMENT_ADHOC** が返されるかどうかを確認します。 返される場合、それは組織に付与された個人向けサブスクリプションの RMS であり、ユーザーがセルフ サービスのサインアップ プロセスで使用できるアクティブなユニットが多数存在します。

-   System Center Configuration Manager などのシステム管理ソリューションを使用して、インストール済みのソフトウェアと使用中のソフトウェアのインベントリを作成します。 Rights Management 共有アプリケーションの実行には、 **ipviewer.exe** プログラムが使用されています。また、 [アプリケーションを無料でダウンロードしてインストール](http://go.microsoft.com/fwlink/?LinkId=303970) し、このアプリケーションに関するその他の特性を確認して、ソフトウェア インベントリで利用することができます。

-   Rights Management 共有アプリケーションによって作成されるファイル名拡張子を監視します。 .pfile と .ppdf ファイル名拡張子は最もわかりやすい例ですが、他のファイルでは、Rights Management がネイティブで保護しているときに元のファイル名拡張子が変更される場合があります。 詳細については、「[Rights Management 共有アプリケーション管理者ガイド](http://technet.microsoft.com/library/dn339003.aspx)」の「[サポートされているファイルの種類とファイル名拡張子](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions)」セクションを参照してください。




<!--HONumber=Jun16_HO4-->


