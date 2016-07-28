---
title: "Azure Information Protection クイック スタート チュートリアル | Azure Rights Management"
description: "4 つの手順を実行するだけで 15 分もかからずに組織の Microsoft Azure Information Protection を簡単に試すことができるチュートリアルの概要を説明します。"
author: cabailey
manager: mbaldwin
ms.date: 07/16/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1260b9e5-dba1-41de-84fd-609076587842
translationtype: Human Translation
ms.sourcegitcommit: cac95dec84f99d2e6caa3458dc8284defe2324bc
ms.openlocfilehash: 7dc988365c1fa86827d1a7edc33c0a2eb6180f0e


---

# Azure Information Protection のクイック スタート チュートリアル 

*適用対象: Azure Information Protection プレビュー*

このチュートリアルを使用すると、4 つの手順を実行するだけで 15 分もかからずに組織の Azure Information Protection プレビューを簡単に試すことができます。 必要に応じて、Azure Rights Management サービスをアクティブ化し、既定の Azure Information Protection ポリシーを確認および変更し、Azure Information Protection クライアントをインストールし、Word 文書を使用して分類、ラベル付け、および保護の例を参照できます。

このチュートリアルは、IT 管理者やコンサルタントが組織向けのエンタープライズ情報保護ソリューションとして Azure Information Protection を評価する際の支援を目的としたものです。 運用環境では、サービスのアクティブ化、Information Protection ポリシーの構成、ユーザー用のクライアントのインストールに関する手順は、管理者が行います。 ドキュメントにラベルを付ける手順は、エンド ユーザーが行います。 このチュートリアルでは両方の手順について説明し、組織のデータの分類、ラベル付け、保護に関するシナリオを最初から最後まで示します。 

このチュートリアルの実行や Azure Information Protection のレビュー リリースの使用に関して問題がある場合、または他のユーザーの意見を知りたい場合は、[Azure Information Protection の Yammerサイト](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)を参照してください。

## 必要条件 
このチュートリアルでは、以下のものが必要です。

- Azure Rights Management を含む任意のサブスクリプション。Azure Information Protection のプレビュー リリースにアクセスできるようになります。 Azure Information Protection は、Azure Rights Management をサポートするすべてのリージョンで使用できます。 使用できるサブスクリプション オプションの詳細と無料試用版へのリンクについては、「[Azure RMS の要件: Azure RMS をサポートするクラウド サブスクリプション](../get-started/requirements-subscriptions.md)」を参照してください。

- Azure のサブスクリプション。Azure ポータルにアクセスして Azure Information Protection ポリシーを構成するために必要です。 組織の Azure サブスクリプションがまだない場合は、無料試用版にサインアップして取得できます。「[Microsoft Azure はじめに](https://account.windowsazure.com/organization)」ページにアクセスし、指示に従ってください。

  > [!TIP] 
  > サブスクリプションの取得プロセスの完了までに時間がかかる可能性があるため、取得が必要な場合は、事前に済ませてください。

- Rights Management サービスをアクティブ化する必要がある場合は、Office 365 管理センターまたは Azure クラシック ポータルにサインインするためのグローバル管理者アカウント。 このアカウントには、電子メール アドレスと、動作している電子メール サービス (たとえば、Exchange Online または Exchange Server) も必要です。

- Windows (Windows 7 Service Pack 1 以降) を実行し、Office 2016、Office 2013 Service Pack 1 または Office 2010 がインストールされているコンピューター。 

- Active Directory Rights Management サービス (AD RMS) が組織にデプロイされている場合: コンピューターは AD RMS を以前に使用していないワークグループ コンピューターである必要があります。 これは、ドキュメントを保護し、テンプレートが Azure Rights Management からのみダウンロードされるようにする場合に必要です。 AD RMS と Azure RMS への同時接続はサポートされていません。 移行については、「[AD RMS から Azure Rights Management への移行](../plan-design/migrate-from-ad-rms-to-azure-rms.md)」を参照してください。   

では、始めましょう。

>[!div class="step-by-step"]
[&#187; 手順 1](infoprotect-tutorial-step1.md)





<!--HONumber=Jul16_HO3-->


