---
title: アプリのデプロイ方法 - AIP
description: この記事では、開発時にもともと使用されていたものとは異なるテナントにサービス アプリケーションをデプロイするプロセスについて説明します。
keywords: ''
author: kkanakas
ms.author: kartikka
manager: barbkess
ms.date: 02/27/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 34dc6d6f-cfe4-4848-9b11-8d90c4b38ef7
audience: developer
ms.reviewer: kartikka
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 5150c9f3339f442f7898f273d2275cd267e8d6b8
ms.sourcegitcommit: 9968a003865ff2456c570cf552f801a816b1db07
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2019
ms.locfileid: "68791154"
---
# <a name="deploying-a-service-application-into-a-different-tenant"></a>別のテナントへのサービス アプリケーションのデプロイ

この記事では、サービス アプリケーションのデプロイ プロセスについて説明します。 このシナリオでは、初期開発 AD テナントに登録しているアプリケーションを別の会社の運用 AD テナントに登録するようにします。

> [!Note]
> このシナリオは、サービス アプリケーションで対称キー認証を使用する場合にのみ関連します。

## <a name="scenario"></a>シナリオ
*CoolApp* という会社は、ユーザーが Dynamics、SAP、Salesforce などのビジネス アプリケーションからドキュメントをエクスポートする際にドキュメントを暗号化し、ラベルを付けて保護する Azure Information Protection (AIP) を使用してサービス アプリケーションを開発しました。 このシナリオでは、*ABC* という大企業は *CoolApp の*新しいアプリケーションを購入したため、*CoolApp* チームはソリューションを *ABC の*環境にデプロイする必要があります。 

![別のテナントで対照キーを作成する場合のサンプル フロー](../media/develop/service-app-provision.jpg)

## <a name="flow-1-coolapp-provides-a-ui-dialog-to-abc-to-implement-the-deployment"></a>フロー 1:*CoolApp* による *ABC* へのデプロイを実装するための UI ダイアログの提供

*ABC* が *CoolApp の*ソリューションを購入した場合、*ABC* の IT 管理者は *CoolApp* のサービス プリンシパルを作成し、*ABC の* Azure AD テナントにアプリケーションを登録する必要があります。 

この手順の概要については、「[アプリケーションの開発](developing-your-application.md)」の「**サービス プリンシパルの作成**」セクションを参照してください。

![IT 管理者がアプリケーションについて入力する UI の例](../media/develop/how-to-deploy-app-UI.png)

> [!Note]
> テナントでサービス プリンシパルを作成するには、テナントの管理者権限が必要です。

その後、*ABC の* IT 管理者は使用環境でサービスとして *CoolApp の*アプリケーションを起動し、アプリケーション ID、テナント ID、対称キーなど、使用する *CoolApp* アプリケーションの詳細を埋め込みます。

希望するエクスペリエンスで *ABC* の IT 管理者にサービス プリンシパル情報の UI ダイアログが提供されない場合は、**フロー 2** の方法に従います。

## <a name="flow-2-abc-it-administrator-provides-the-key-to-the-coolapp-team"></a>フロー 2:*ABC* の IT 管理者による *CoolApp* チームへのキーの提供

*ABC の* IT 管理者がサービス プリンシパルを作成した場合、**図 1** のように、*ABC* は *CoolApp* チームに情報を提供します。 その後、*CoolApp* チームは、*ABC の*テナントで使用するために *CoolApp* アプリケーションの情報の埋め込みに進みます。
