---
title: Rights Management をアクティブにする - AIP
description: この情報保護ソリューションをサポートするアプリケーションとサービスを使用して、組織の重要な文書や電子メールの保護を開始するには、Azure Rights Management をアクティブにする必要があります。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 7c257b16737a916d597be858fcfeaf6c475bb423
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="activating-azure-rights-management"></a>Rights Management をアクティブにする

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!NOTE]
> この構成情報は、組織内のすべてのユーザーに適用されるサービスを担当する管理者のためのものです。 特定のアプリケーション用の Rights Management 機能の使用、または権利保護されたファイルや電子メールを開く方法に関するユーザー向けヘルプや情報をお探しの場合は、アプリケーションに付属しているヘルプとガイダンスを使用してください。
>
> たとえば、Office アプリケーションの場合、[ヘルプ] アイコンをクリックし、「 **Rights Management** 」や「 **IRM**」などの検索語句を入力します。 Windows 用 Azure Information Protection クライアントについては、「[Azure Information Protection ユーザー ガイド](../rms-client/client-user-guide.md)」を参照してください。
>
> このサービスのテクニカル サポートとその他の質問については、「[サポート オプションとコミュニティ リソース](../get-started/information-support.md#support-options-and-community-resources)」の情報を参照してください。

Azure Information Protection の Azure Rights Management サービスを組織用にアクティブにすると、この情報保護ソリューションをサポートするアプリケーションとサービスを使用して、管理者とユーザーが重要なデータを保護し始めることができます。 管理者は、組織が所有する保護されたドキュメントや電子メールを管理および監視することもできます。 


## <a name="do-you-need-to-activate-azure-rights-management"></a>Azure Rights Management をアクティブにする必要がある場合

Azure Rights Management を含むサービス プランを持っている場合は、サービスをアクティブにする必要がない可能性があります。

- Azure Rights Management または Azure Information Protection を含むサブスクリプションを **2018 年 2 月**末日以降を対象として取得した場合は、サービスが自動的にアクティブになります。 お客様または組織の他のグローバル管理者が Azure Rights Management を非アクティブ化しない限り、サービスをアクティブ化する必要はありません。

- 今月より前にサブスクリプションを取得した場合は、自分でサービスをアクティブにする必要があります。 

Azure Rights Management をアクティブにした後は、組織内のすべてのユーザーがファイルに情報保護を適用したり、Azure Rights Management で保護されているファイルを開く (使用する) ことができます。 ただし、そちらを希望する場合は、段階的デプロイのオンボーディング コントロールを使用して、情報保護を適用できるユーザーを制限できます。 詳細については、この記事の「[段階的デプロイのオンボーディング コントロールの構成](#configuring-onboarding-controls-for-a-phased-deployment)」セクションを参照してください。

## <a name="how-to-activate-or-confirm-the-status-of-the-azure-rights-management-service"></a>Azure Rights Management サービスの状態をアクティブ化または確認する方法 

> [!IMPORTANT]
> 組織に Active Directory Rights Management Services (AD RMS) をデプロイしている場合、Azure Rights Management サービスをアクティブ化しないでください。 [詳細情報](prepare-environment-adrms.md)

このデータ保護ソリューションを使用するには、組織が、Azure Information Protection からの Azure Rights Management サービスを含むサービス プランを持っている必要があります。 このサービス プランがない場合は、Azure Rights Management サービスをアクティブ化することはできません。 次のいずれかを用意する必要があります。

- [Azure Information Protection プラン](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) 

- [Rights Management が含まれている Office 365 プラン](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

Azure Rights Management をアクティブにした後は、組織内のすべてのユーザーがファイルに情報保護を適用したり、Azure Rights Management で保護されているファイルを開く (使用する) ことができます。 ただし、そちらを希望する場合は、段階的デプロイのオンボーディング コントロールを使用して、情報保護を適用できるユーザーを制限できます。 詳細については、この記事の「[段階的デプロイのオンボーディング コントロールの構成](#configuring-onboarding-controls-for-a-phased-deployment)」セクションを参照してください。

## <a name="choosing-your-activation-method"></a>アクティブ化メソッドを選択する

管理ポータルから Rights Management サービスをアクティブ化する手順については、Office 365 管理センターと Azure Portal のどちらを使うかを選択してください。

- [Office 365 管理センター](activate-office365.md) - グローバル管理者アカウントが必要

- [Azure Portal](activate-azure.md) - グローバル管理者アカウントは不要

代わりに、次の PowerShell コマンドを使用することができます。

1. 保護サービスを構成および管理するには、AADRM モジュールをインストールします。 手順については、「[AADRM PowerShell モジュールのインストール](../deploy-use/install-powershell.md)」を参照してください。

2. PowerShell セッションから [Connect-AadrmService](/powershell/module/aadrm/connect-aadrmservice) を実行し、メッセージが表示されたら、Azure Information Protection テナントのグローバル管理者アカウントの詳細を指定します。

3. Azure Rights Management サービスがアクティブかどうかを確認するには、[Get-Aadrm](/powershell/aadrm/vlatest/get-aadrm) を実行します。 **Enabled** の状態でアクティブであることを確認し、**Disabled** はサービスが非アクティブであることを示します。

4. サービスをアクティブ化するには、[Enable-Aadrm](/powershell/aadrm/vlatest/enable-aadrm) を実行します。

## <a name="configuring-onboarding-controls-for-a-phased-deployment"></a>段階的デプロイのオンボーディング コントロールの構成
すべてのユーザーが Azure Rights Management を使用してすぐにファイルを保護できるようにしたくない場合は、[Set-AadrmOnboardingControlPolicy](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy) PowerShell コマンドを使用してユーザー オンボーディング コントロールを構成できます。 このコマンドを実行するのは、Azure Rights Management サービスをアクティブ化する前と後のどちらでもかまいません。

> [!IMPORTANT]
> このコマンドを使用するには、バージョン **2.1.0.0** 以降の [Azure Rights Management PowerShell モジュール](https://go.microsoft.com/fwlink/?LinkId=257721)が必要です。
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


## <a name="next-steps"></a>次の手順
組織に対して Azure Rights Management サービスがアクティブになっている場合、「[Azure Information Protection デプロイ ロードマップ](../plan-design/deployment-roadmap.md)」を使用して、Azure Information Protection をユーザーおよび管理者にロールアウトする前に、必要な構成の手順がほかにもあるかどうかを確認します。 

たとえば、[テンプレート](configure-policy-templates.md)を使用してユーザーが簡単に情報保護をファイルに適用できるようにする、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] を使用するために [Rights Management コネクタ](deploy-rms-connector.md)をインストールしてオンプレミス サーバーに接続する、すべてのデバイスですべてのファイルの種類の保護をサポートする [Azure Information Protection クライアント](../rms-client/aip-client.md)をデプロイする、などが考えられます。 

Exchange Online や SharePoint Online などの Office サービスの Information Rights Management (IRM) 機能を使用するには、あらかじめ追加の構成手順が必要です。 お使いのアプリケーションで Rights Management サービスを使用する方法については、「[アプリケーションによる Azure Rights Management サービスのサポート](../understand-explore/applications-support.md)」を参照してください。


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
