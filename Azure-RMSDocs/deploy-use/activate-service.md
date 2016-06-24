---
# required metadata

title: Azure Rights Management をアクティブにする | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/16/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Rights Management をアクティブにする

*適用対象: Azure Rights Management、Office 365*

[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (Azure RMS) をアクティブにすると、この情報保護ソリューションをサポートするアプリケーションとサービスを使用して、組織の重要なデータの保護を開始できます。 管理者は、組織が所有する保護されたファイルや電子メールを管理および監視することもできます。 Office、SharePoint、Exchange の中で Information Rights Management (IRM) 機能を使用して機密ファイルを保護するには、あらかじめ [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] を有効にする必要があります。

サービスをアクティブ化する前に Azure Rights Management の詳細 (解決するビジネス上の問題、一般的な用途、そのしくみなど) を把握しておく必要がある場合は、「[Azure Rights Management とは](../understand-explore/what-is-azure-rms.md)」を参照してください。

> [!IMPORTANT]
> [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] をアクティブ化する前に、組織に [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] サービスを含むサービス プランがあることを確認します。 ない場合は、Azure RMS をアクティブにすることはできません。
>
> 詳細については、[Azure RMS をサポートするクラウド サブスクリプション](../get-started/requirements-subscriptions.md)に関するページを参照してください。

Azure RMS をアクティブ化した後は、組織内のすべてのユーザーはファイルに情報保護を適用でき、すべてのユーザーは Azure RMS で保護されているファイルを開く (使用する) ことができます。 ただし、そちらを希望する場合は、段階的デプロイのオンボーディング コントロールを使用して、情報保護を適用できるユーザーを制限できます。 詳細については、この記事の「[段階的デプロイのオンボーディング コントロールの構成](#configuring-onboarding-controls-for-a-phased-deployment)」セクションを参照してください。

管理ポータルから Rights Management をアクティブ化する手順については、Office 365 管理センター (プレビューまたはクラシック) と Azure クラシック管理ポータルのどちらを使用するかを選択してください。


- [Office 365 管理センター - プレビュー](activate-office365-preview.md)
- [Office 365 管理センター - クラシック](activate-office365-classic.md)
- [Azure クラシック ポータル](activate-azure-classic.md)

または、Window PowerShell を使用して [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] をアクティブ化することもできます。

1. Azure Rights Management Administration Tool をインストールすると、Azure Rights Management 管理モジュールがインストールされます。 手順については、「[Azure Rights Management 用 Windows PowerShell をインストールする](../deploy-use/install-powershell.md)」を参照してください。

2. Windows PowerShell セッションから [Connect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx) を実行し、メッセージが表示されたら、Azure RMS テナントのグローバル管理者アカウントの詳細を指定します。

3. [Enable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629412.aspx) を実行して、Azure RMS サービスをアクティブ化します。

## 段階的デプロイのオンボーディング コントロールの構成
すべてのユーザーが Azure RMS を使用してすぐにファイルを保護できるようにしたくない場合は、 [Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx) Windows PowerShell コマンドを使用してユーザー オンボーディング コントロールを構成できます このコマンドを実行するのは、Azure RMS をアクティブ化する前と後のどちらでもかまいません。

> [!IMPORTANT] このコマンドを使用するには、バージョン **2.1.0.0** 以降の [Azure RMS Windows PowerShell モジュール](http://go.microsoft.com/fwlink/?LinkId=257721)が必要です。
>
> インストールされているバージョンを確認するには、**(Get-Module aadrm –ListAvailable).Version** を実行します。

たとえば、テストのために最初は “IT department” グループ (オブジェクト ID が fbb99ded-32a0-45f1-b038-38b519009503) の管理者だけがコンテンツを保護できるようにする場合は、次のコマンドを使用します。

```
Set-AadrmOnboardingControlPolicy – SecurityGroupObjectId fbb99ded-32a0-45f1-b038-38b519009503
```
この構成オプションでは、グループを指定する必要があります。個々 のユーザーを指定することはできません。

または、Azure RMS の使用を適切にライセンスされているユーザーのみがコンテンツを保護できるようにする場合は、次のコマンドを使用します。

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $true
```
これらのオンボーディング コントロールを使用するときは、保護されたコンテンツを組織内のすべてのユーザーがいつでも使用できますが、コンテンツを保護できるのは組織内の一部のユーザーのみとなり、それ以外のユーザーは情報保護を自分でクライアント アプリケーションから適用することはできません。 たとえば、そのようなユーザーの Office クライアントには、Azure RMS がアクティブになると自動的に公開される既定のテンプレートや管理者が構成したカスタム テンプレートは表示されません。  Exchange などのサーバー側のアプリケーションには、RMS と統合された場合に同じ結果を達成するための、独自のユーザー単位コントロールを実装する機能があります。


## 次のステップ
これで組織で [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] がアクティブになったので、[Azure Rights Management のデプロイ ロードマップ](../plan-design/deployment-roadmap.md)を使用して、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] をユーザーおよび管理者にロールアウトする前にその他の構成手順が必要かどうかを判断します。 

たとえば、[カスタム テンプレート](configure-custom-templates.md)を使用してユーザーが簡単に情報保護をファイルに適用できるようにする、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] を使用するために [RMS コネクタ](deploy-rms-connector.md)をインストールしてオンプレミス サーバーに接続する、すべてのデバイスですべてのファイルの種類の保護をサポートする [Rights Management](../rms-client/sharing-app-windows.md) 共有アプリケーションをデプロイする、などが考えられます。 

Exchange Online や SharePoint Online などの Office サービスの Information Rights Management (IRM) 機能を使用するには、あらかじめ追加の構成手順が必要です。 お使いのアプリケーションで [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] を使用する方法については、「[アプリケーションで Azure Rights Management をサポートする方法](../understand-explore/applications-support.md)」を参照してください。



<!--HONumber=May16_HO3-->


