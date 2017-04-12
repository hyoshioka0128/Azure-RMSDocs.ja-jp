---
title: "Rights Management をアクティブにする - AIP"
description: "この情報保護ソリューションをサポートするアプリケーションとサービスを使用して、組織の重要な文書や電子メールの保護を開始するには、Azure Rights Management をアクティブにする必要があります。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/30/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 0e7feff31adb118439dfce082a831bdc51bc4a87
ms.sourcegitcommit: 58d1f87763f8756621a6cba6dfe51e26ec38cd48
translationtype: HT
---
# <a name="activating-azure-rights-management"></a>Rights Management をアクティブにする

>*適用対象: Azure Information Protection、Office 365*

Azure Information Protection の Azure Rights Management サービスをアクティブにすると、この情報保護ソリューションをサポートするアプリケーションとサービスを使用して、組織の重要なデータを保護し始めることができます。 管理者は、組織が所有する保護されたファイルや電子メールを管理および監視することもできます。 Office、SharePoint、Exchange で Information Rights Management (IRM) 機能を使用して機密ファイルを保護するには、あらかじめこのサービスを有効にする必要があります。

サービスをアクティブ化する前に Azure Rights Management の詳細 (解決するビジネス上の問題、一般的な用途、そのしくみなど) を把握したい場合は、「[Azure Rights Management とは](../understand-explore/what-is-azure-rms.md)」を参照してください。

> [!IMPORTANT]
> [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] をアクティブ化する前に、組織に Azure Rights Management データ保護を含むサービス プランがあることを確認します。 ない場合は、Azure Rights Management をアクティブにすることはできません。
>
> [Azure Information Protection Premium プラン](https://www.microsoft.com/en-us/cloud-platform/azure-information-protection-pricing)を取得するか、[Rights Management を含む Office 365 プラン](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)を取得する必要があります。

Azure Rights Management をアクティブにした後は、組織内のすべてのユーザーがファイルに情報保護を適用したり、Azure Rights Management で保護されているファイルを開く (使用する) ことができます。 ただし、そちらを希望する場合は、段階的デプロイのオンボーディング コントロールを使用して、情報保護を適用できるユーザーを制限できます。 詳細については、この記事の「[段階的デプロイのオンボーディング コントロールの構成](#configuring-onboarding-controls-for-a-phased-deployment)」セクションを参照してください。

管理ポータルから Rights Management サービスをアクティブ化する手順については、Office 365 管理センター (プレビューまたはクラシック) と Azure クラシック管理ポータルのどちらを使用するかを選択してください。


- [Office 365 管理センター - プレビュー](activate-office365-preview.md)
- [Office 365 管理センター - クラシック](activate-office365-classic.md)
- [Azure クラシック ポータル](activate-azure-classic.md)

または、PowerShell を使用して [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] をアクティブ化することもできます。

1. Azure Rights Management Administration Tool をインストールすると、Azure Rights Management 管理モジュールがインストールされます。 手順については、「[Azure Rights Management 用 Windows PowerShell をインストールする](../deploy-use/install-powershell.md)」を参照してください。

2. PowerShell セッションから [Connect-AadrmService](https://msdn.microsoft.com/library/windowsazure/dn629415.aspx) を実行し、メッセージが表示されたら、Azure Information Protection テナントのグローバル管理者アカウントの詳細を指定します。

3. [Enable-Aadrm](http://msdn.microsoft.com/library/windowsazure/dn629412.aspx) を実行して、Azure Rights Management サービスをアクティブ化します。

## <a name="configuring-onboarding-controls-for-a-phased-deployment"></a>段階的デプロイのオンボーディング コントロールの構成
すべてのユーザーが Azure Rights Management を使用してすぐにファイルを保護できるようにしたくない場合は、[Set-AadrmOnboardingControlPolicy](http://msdn.microsoft.com/library/azure/dn857521.aspx) PowerShell コマンドを使用してユーザー オンボーディング コントロールを構成できます。 このコマンドを実行するのは、Azure Rights Management サービスをアクティブ化する前と後のどちらでもかまいません。

> [!IMPORTANT]
> このコマンドを使用するには、バージョン **2.1.0.0** 以降の [Azure Rights Management PowerShell モジュール](http://go.microsoft.com/fwlink/?LinkId=257721)が必要です。
>
> インストールされているバージョンを確認するには、**(Get-Module aadrm –ListAvailable).Version** を実行します。

たとえば、テストのために最初は “IT department” グループ (オブジェクト ID が fbb99ded-32a0-45f1-b038-38b519009503) の管理者だけがコンテンツを保護できるようにする場合は、次のコマンドを使用します。

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False -SecurityGroupObjectId "fbb99ded-32a0-45f1-b038-38b519009503"
```

この構成オプションでは、グループを指定する必要があります。個々 のユーザーを指定することはできません。 グループのオブジェクト ID を取得するには、Azure AD PowerShell を使用します。たとえば、バージョン 1.0 のモジュールについては、[Get-MsolGroup](/powershell/msonline/v1/get-msolgroup) コマンドを使用します。 または、Azure Portal から、グループの**オブジェクト ID** 値をコピーしてもかまいません。

あるいは、Azure Information Protection を使用するライセンスがあるユーザーのみがコンテンツを保護できるようにする場合は、次のコマンドを使用します。

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $True
```

オンボーディング コントロールを使用する必要がなくなった場合は、使用していたのがグループ オプションかライセンス オプションかに関係なく、次のコマンドレットを実行します。

```
Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False
```


このコマンドレットとその他の例の詳細については、[Set-AadrmOnboardingControlPolicy](/powershell/aadrm/vlatest/set-aadrmonboardingcontrolpolicy) ヘルプを参照してください。

これらのオンボーディング コントロールを使用するときは、保護されたコンテンツを組織内のすべてのユーザーがいつでも使用できますが、コンテンツを保護できるのは組織内の一部のユーザーのみとなり、それ以外のユーザーは情報保護を自分でクライアント アプリケーションから適用することはできません。 たとえば、そのようなユーザーの Office クライアントには、Azure Rights Management がアクティブになると自動的に公開される既定のテンプレートや管理者が構成したカスタム テンプレートは表示されません。  Exchange などのサーバー側のアプリケーションには、Rights Management と統合された場合に同じ結果を達成するための、独自のユーザー単位コントロールを実装する機能があります。


## <a name="next-steps"></a>次のステップ
これで組織で [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] がアクティブになったので、「[Azure Information Protection デプロイ ロードマップ](../plan-design/deployment-roadmap.md)」を参照して、Azure Information Protection をユーザーおよび管理者にロールアウトする前にその他に構成が必要であるかを判断することができます。 

たとえば、[カスタム テンプレート](configure-custom-templates.md)を使用してユーザーが簡単に情報保護をファイルに適用できるようにする、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] を使用するために [Rights Management コネクタ](deploy-rms-connector.md)をインストールしてオンプレミス サーバーに接続する、すべてのデバイスですべてのファイルの種類の保護をサポートする [Azure Information Protection クライアント](../rms-client/aip-client.md)をデプロイする、などが考えられます。 

Exchange Online や SharePoint Online などの Office サービスの Information Rights Management (IRM) 機能を使用するには、あらかじめ追加の構成手順が必要です。 お使いのアプリケーションで Rights Management サービスを使用する方法については、「[アプリケーションによる Azure Rights Management サービスのサポート](../understand-explore/applications-support.md)」を参照してください。


[!INCLUDE[Commenting house rules](../includes/houserules.md)]