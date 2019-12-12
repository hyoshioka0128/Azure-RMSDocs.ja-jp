---
title: Azure Information Protection からの保護サービスのアクティブ化
description: この情報保護ソリューションをサポートするアプリケーションとサービスを使用して、組織がドキュメントと電子メールの保護を開始する前に、保護サービス (Azure Rights Management) をアクティブにする必要があります。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 181320c5046137d96816723c9b9ae55979998453
ms.sourcegitcommit: c20c7f114ae58ed6966785d8772d0bf1c1d39cce
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2019
ms.locfileid: "74934859"
---
# <a name="activating-the-protection-service-from-azure-information-protection"></a>Azure Information Protection からの保護サービスのアクティブ化

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!NOTE]
> この構成情報は、組織内のすべてのユーザーに適用されるサービスを担当する管理者のためのものです。 特定のアプリケーション用の Rights Management 機能の使用、または権利保護されたファイルや電子メールを開く方法に関するユーザー向けヘルプや情報をお探しの場合は、アプリケーションに付属しているヘルプとガイダンスを使用してください。
>
> たとえば、Office アプリケーションの場合、[ヘルプ] アイコンをクリックし、「 **Rights Management** 」や「 **IRM**」などの検索語句を入力します。 Windows 用 Azure Information Protection クライアントについては、「[Azure Information Protection ユーザー ガイド](./rms-client/client-user-guide.md)」を参照してください。
>
> このサービスのテクニカル サポートとその他の質問については、「[サポート オプションとコミュニティ リソース](information-support.md#support-options-and-community-resources)」の情報を参照してください。

Azure Information Protection の保護サービスが組織に対してアクティブ化されると、管理者とユーザーは、この情報保護ソリューションをサポートするアプリケーションとサービスを使用して、重要なデータの保護を開始できます。 管理者は、組織が所有する保護されたドキュメントや電子メールを管理および監視することもできます。 


## <a name="do-you-need-to-activate-the-protection-service-azure-rights-management"></a>保護サービスの Azure Rights Management をアクティブ化する必要がありますか。

Azure Rights Management を含むサービス プランを持っている場合は、サービスをアクティブにする必要がない可能性があります。

- **Azure Rights Management または Azure Information Protection を含むサブスクリプションを 2018 年 2 月末日以降を対象として取得した場合**、サービスが自動的にアクティブになります。 お客様または組織の他のグローバル管理者が Azure Rights Management を非アクティブ化しない限り、サービスをアクティブ化する必要はありません。

- **Azure Rights Management または Azure Information Protection を含むサブスクリプションを 2018 年 2 月以前に取得した場合**については、Microsoft は、テナントで Exchange Online を使用している場合にこれらのサブスクリプションの Azure Rights Management サービスのアクティブ化を開始しています。 これらのサブスクリプションの場合、サービスがアクティブ化される 2018 年 8 月 1 日から自動アクティブ化のロール アウトが開始されます。ただし、[Get-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration?view=exchange-ps) を実行するときに **AutomaticServiceUpdateEnabled** が **false** に設定されていない場合に限ります。 

後続のシナリオがどちらも当てはまらない場合は、保護サービスを手動でアクティブ化する必要があります。 

サービスをアクティブにした後は、組織内のすべてのユーザーが各自のドキュメントや電子メールに情報保護を適用したり、Azure Rights Management で保護されているドキュメントや電子メールを開く (使用する) ことができます。 ただし、そちらを希望する場合は、段階的デプロイのオンボーディング コントロールを使用して、情報保護を適用できるユーザーを制限できます。 詳細については、この記事の「[段階的デプロイのオンボーディング コントロールの構成](#configuring-onboarding-controls-for-a-phased-deployment)」セクションを参照してください。

## <a name="how-to-activate-or-confirm-the-status-of-the-protection-service"></a>保護サービスの状態をアクティブ化または確認する方法 

> [!IMPORTANT]
> Active Directory Rights Management サービス (AD RMS) が組織に展開されている場合は、保護サービスをアクティブ化しないでください。 [詳細情報](prepare-environment-adrms.md)

このデータ保護ソリューションを使用するには、組織が、Azure Information Protection からの Azure Rights Management サービスを含むサービス プランを持っている必要があります。 これを行わないと、保護サービスをアクティブにできません。 次のいずれかを用意する必要があります。

- [Azure Information Protection プラン](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) 

- [Rights Management が含まれている Office 365 プラン](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

保護サービスをアクティブ化すると、組織内のすべてのユーザーがドキュメントと電子メールに情報保護を適用でき、すべてのユーザーがこのサービスによって保護されているドキュメントと電子メールを開く (使用) ことができます。 ただし、そちらを希望する場合は、段階的デプロイのオンボーディング コントロールを使用して、情報保護を適用できるユーザーを制限できます。 詳細については、この記事の「[段階的デプロイのオンボーディング コントロールの構成](#configuring-onboarding-controls-for-a-phased-deployment)」セクションを参照してください。

## <a name="choosing-your-activation-method"></a>アクティブ化メソッドを選択する

管理ポータルから保護サービスをアクティブ化する手順については、Microsoft 365 管理センターと Azure portal のどちらを使用するかを選択してください。

- [Microsoft 365 管理センター](activate-office365.md) - グローバル管理者アカウントが必要

- [Azure Portal](activate-azure.md) - グローバル管理者アカウントは不要

代わりに、次の PowerShell コマンドを使用することができます。

1. AIPService モジュールをインストールして、保護サービスを構成および管理します。 手順については、「 [AIPService PowerShell モジュールのインストール](install-powershell.md)」を参照してください。

2. PowerShell セッションから、 [Connect-AipService](/powershell/module/aipservice/connect-aipservice)を実行し、メッセージが表示されたら、Azure Information Protection テナントのグローバル管理者アカウントの詳細を入力します。

3. [Get AipService](/powershell/module/aipservice/get-aipservice)を実行して、保護サービスがアクティブ化されているかどうかを確認します。 **Enabled** の状態でアクティブであることを確認し、**Disabled** はサービスが非アクティブであることを示します。

4. サービスをアクティブ化するには、 [Enable-AipService](/powershell/module/aipservice/enable-aipservice)を実行します。

## <a name="configuring-onboarding-controls-for-a-phased-deployment"></a>段階的デプロイのオンボーディング コントロールの構成
すべてのユーザーが Azure Information Protection を使用してドキュメントや電子メールを直ちに保護できないようにする場合は、 [Set-Aipserviceonworkplace Ingcontrolpolicy](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy) PowerShell コマンドを使用して、ユーザーのオンボードコントロールを構成できます。 このコマンドを実行するのは、Azure Rights Management サービスをアクティブ化する前と後のどちらでもかまいません。

たとえば、テストのために最初は “IT department” グループ (オブジェクト ID が fbb99ded-32a0-45f1-b038-38b519009503) の管理者だけがコンテンツを保護できるようにする場合は、次のコマンドを使用します。

```
Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $False -SecurityGroupObjectId "fbb99ded-32a0-45f1-b038-38b519009503"
```

この構成オプションでは、グループを指定する必要があります。個々 のユーザーを指定することはできません。 グループのオブジェクト ID を取得するには、Azure AD PowerShell を使用します。たとえば、バージョン 1.0 のモジュールについては、[Get-MsolGroup](/powershell/msonline/v1/get-msolgroup) コマンドを使用します。 または、Azure Portal から、グループの**オブジェクト ID** 値をコピーしてもかまいません。

あるいは、Azure Information Protection を使用するライセンスがあるユーザーのみがコンテンツを保護できるようにする場合は、次のコマンドを使用します。

```
Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $True
```

オンボーディング コントロールを使用する必要がなくなった場合は、使用していたのがグループ オプションかライセンス オプションかに関係なく、次のコマンドレットを実行します。

```
Set-AipServiceOnboardingControlPolicy -UseRmsUserLicense $False
```

このコマンドレットとその他の例の詳細については、「 [Set-Aipserviceonworkplace Ingcontrolpolicy](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy) help」を参照してください。

これらのオンボーディング コントロールを使用するときは、保護されたコンテンツを組織内のすべてのユーザーがいつでも使用できますが、コンテンツを保護できるのは組織内の一部のユーザーのみとなり、それ以外のユーザーは情報保護を自分でクライアント アプリケーションから適用することはできません。 たとえば、保護サービスがアクティブになったときに自動的に公開される既定の保護テンプレートや、構成されているカスタムテンプレートは、Office アプリに表示されません。 Exchange などのサーバー側アプリケーションは、ユーザーごとのコントロールを実装して、同じ結果を得ることができます。 たとえば、ユーザーが Outlook on the web 内の電子メールを保護できないようにするには、[Set-OwaMailboxPolicy](/powershell/module/exchange/client-access/set-owamailboxpolicy?view=exchange-ps) を使用して *IRMEnabled* パラメーターを *$false* に設定します。


## <a name="next-steps"></a>次のステップ
保護サービスが組織に対してアクティブ化されている場合は、 [Azure Information Protection 展開ロードマップ](deployment-roadmap.md)を使用して、Azure Information Protection をユーザーと管理者にロールアウトする前に他の構成手順が必要かどうかを確認します。 

たとえば、[テンプレート](configure-policy-templates.md)を使用して、ユーザーがファイルに保護を適用し、[Rights Management コネクタ](deploy-rms-connector.md)をインストールして、オンプレミスのサーバーを接続して保護サービスを使用するようにし、Azure をデプロイすることができます。すべてのデバイスですべてのファイルの種類の保護をサポートする [Azure Information Protection クライアント](./rms-client/aip-client.md)。 

Exchange Online や SharePoint Online などの Office サービスの Information Rights Management (IRM) 機能を使用するには、あらかじめ追加の構成手順が必要です。 アプリケーションが保護サービス、Azure Rights Management でどのように機能するかについては、「[アプリケーションが azure Rights Management サービスをサポートする方法](applications-support.md)」を参照してください。

