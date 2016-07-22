---
title: "Azure Rights Management のデプロイ ロードマップ | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 05/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 086600c2-c5d8-47ec-a4c0-c782e1797486
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7f8a4d53665dd79a6d0e02d340b0e7a09d995e00
ms.openlocfilehash: 96ee0aa3151ede8b8a263f3ce6c3d2e5b8ec9c81


---

# Azure Rights Management のデプロイ ロードマップ

*適用対象: Azure Rights Management、Office 365*

組織の Azure Rights Management (Azure RMS) を準備、実装、管理するには、次の手順に沿います。

ただし、運用環境にロールアウトせずに、簡単に Azure RMS を試す場合は、「[Azure Rights Management のクイック スタート チュートリアル](../get-started/quick-start-tutorial.md)」を参照してください。

特定のシナリオ、関連する構成手順、エンド ユーザー文書の一覧が必要な場合、「[Azure Rights Management の迅速なデプロイ ガイド](../get-started/rapid-deployment-guide.md)」を参照してください。

> [!IMPORTANT]
> 次の手順を実行する前に、「[Azure Rights Management の要件](../get-started/requirements-azure-rms.md)」を確認してください。

## 手順 1:Azure Rights Management を含むサブスクリプションがあることを確認します。
[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] を含むサブスクリプションのタイプは複数あります。 「[Cloud subscriptions that support Azure RMS (Azure RMS をサポートするクラウド サブスクリプション)](../get-started/requirements-subscriptions.md)」を参照してください。さらに、「[Comparison of Rights Management Services (RMS) Offerings (Rights Management サービス (RMS) の提供内容の比較)](https://technet.microsoft.com/dn858608)」の表を参照して、組織で使用する機能がサブスクリプションに含まれていることを確認します。 Azure RMS を使用してファイルや電子メールを保護する組織内の各ユーザーに対して、このサブスクリプションからライセンスを割り当てる必要があります。

## 手順 2:Rights Management を使用するためにテナント アカウントを準備する
[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] を使用する前に、次の準備を行います。

1.  Azure または Office 365 テナントに、組織のユーザーを認証するのに Azure RMS で使用されるユーザー アカウントとグループが含まれていることを確認します。 必要に応じて、これらのアカウントとグループを作成するか、またはオンプレミスのディレクトリからそれらを同期します。 詳細については、「[Azure Rights Management の準備を行う](prepare.md)」を参照してください。

2.  マイクロソフトでテナント キーを管理するか (既定値)、テナント キーを自分で生成して管理するか (Bring Your Own Key または BYOK と呼ばれます) を決定します。 現時点では、Exchange Online を使用する場合、BYOK は使用できない点に注意してください。 詳細については、「[Azure Rights Management テナント キーを計画して実装する](plan-implement-tenant-key.md)」を参照してください。

3.  インターネットにアクセスできる 1 つ以上のコンピューターで [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 向けの Windows PowerShell モジュールをインストールします。 この手順は、今実行しても後で実行しても構いません。 詳細については、「[Azure Rights Management 用 Windows PowerShell をインストールする](../deploy-use/install-powershell.md)」を参照してください。

4.  現在、オンプレミスの Rights Management サービスを使用している場合: キー、テンプレート、URL をクラウドに移行する統合を実行します。 詳細については、「[Migrating from AD RMS to Azure Rights Management (AD RMS から Azure Rights Management への移行)](migrate-from-ad-rms-to-azure-rms.md)」を参照してください。

5.  サービスの使用を開始できるように Rights Management をアクティブ化します。 段階的に展開する必要がある場合、特定のユーザーの使用量を制限するオンボーディング コントロールを構成します。 詳細については、「[Rights Management をアクティブにする](../deploy-use/activate-service.md)」を参照してください。

必要に応じて、次の構成を考慮してください。

-   既定の権限ポリシー テンプレートが組織にとって十分でない場合はカスタム テンプレート。 この手順は、今実行しても後で実行しても構いません。 詳細については、「[Azure Rights Management のカスタム テンプレートを構成する](../deploy-use/configure-custom-templates.md)」を参照してください。

-   組織での Rights Management の使用方法を監視できるようにするための使用ログ。 この手順は、今実行しても後で実行しても構いません。 詳細については、「[Azure Rights Management の利用状況をログに記録して分析する](../deploy-use/log-analyze-usage.md)」を参照してください。

## 手順 3:Rights Management 用にアプリケーションとサービスを構成する
アプリケーションとサービスの構成には、Rights Management 共有アプリケーションのインストール、SharePoint Online または Exchange Online での Information Rights Management (IRM) 機能のサポートの有効化が含まれることがあります。 詳細については、「[Azure Rights Management 用にアプリケーションを構成する](../deploy-use/configure-applications.md)」を参照してください。

Azure RMS によって保護されるファイルを確認する必要がある既存の IT サービスがある場合 (情報漏えい防止 (DLP) ソリューション、コンテンツ暗号化ゲートウェイ (CEG)、マルウェア対策製品など)、サービス アカウントを Azure RMS のスーパー ユーザーとして構成します。 詳細については、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../deploy-use/configure-super-users.md)」を参照してください。

すべての種類のファイルを一括で保護したり保護解除したりする場合、RMS Protection PowerShell モジュールを使用する RMS 保護ツールをインストールします。 詳細については、「[RMS Protection Cmdlets](https://msdn.microsoft.com/library/mt433195.aspx)」 (RMS 保護コマンドレット) を参照してください。

Azure Rights Management で使用するオンプレミスのサービスがある場合は、Rights Management コネクタをインストールして構成します。 詳細については、「[Azure Rights Management コネクタをデプロイする](../deploy-use/deploy-rms-connector.md)」を参照してください。

## 手順 4. 権限保護されたコンテンツを発行および使用する
これで、保護されたコンテンツを発行して利用し、組織で Rights Management を使用する方法を記録する準備が整いました。 詳細については、「[ユーザーに Azure Rights Management でファイルを保護するためのヘルプを提供する](../deploy-use/help-users.md)」および「[Azure Rights Management の利用状況をログに記録して分析する](../deploy-use/log-analyze-usage.md)」を参照してください。

Windows ベースのファイル サーバーで、ファイル分類インフラストラクチャを使用してファイルを自動的に保護することに関する情報は、「[Windows Server ファイル分類インフラストラクチャ (FCI) での RMS 保護](../rms-client/configure-fci.md)」を参照してください。

## 手順 5:必要に応じてテナント アカウントの Rights Management を管理する
[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] の使用を開始すると、Windows PowerShell の[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] モジュールがスクリプトまたは管理変更の自動化に役立つことがあります。 詳細については、「[Windows PowerShell を使用した Azure Rights Management の管理](../deploy-use/administer-powershell.md)」を参照してください。





<!--HONumber=Jun16_HO4-->


