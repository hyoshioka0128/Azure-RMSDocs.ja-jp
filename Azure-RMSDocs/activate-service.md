---
title: Azure Information Protection からの保護サービスをアクティブ化します。
description: 組織がこの情報保護ソリューションをサポートするアプリケーションとサービスを使用してドキュメントや電子メールを保護する前に、は、保護サービス、Azure Rights Management をアクティブにする必要があります。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f8707e01-b239-4d1a-a1ea-0d1cf9a8d214
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 16c3ded1ea8f5d7c2191b994ec63132bd5f9bf1e
ms.sourcegitcommit: a5f595f8a453f220756fdc11fd5d466c71d51963
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520316"
---
# <a name="activating-the-protection-service-from-azure-information-protection"></a>Azure Information Protection からの保護サービスをアクティブ化します。

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!NOTE]
> この構成情報は、組織内のすべてのユーザーに適用されるサービスを担当する管理者のためのものです。 特定のアプリケーション用の Rights Management 機能の使用、または権利保護されたファイルや電子メールを開く方法に関するユーザー向けヘルプや情報をお探しの場合は、アプリケーションに付属しているヘルプとガイダンスを使用してください。
>
> たとえば、Office アプリケーションの場合、[ヘルプ] アイコンをクリックし、「 **Rights Management** 」や「 **IRM**」などの検索語句を入力します。 Windows 用 Azure Information Protection クライアントについては、「[Azure Information Protection ユーザー ガイド](./rms-client/client-user-guide.md)」を参照してください。
>
> このサービスのテクニカル サポートとその他の質問については、「[サポート オプションとコミュニティ リソース](information-support.md#support-options-and-community-resources)」の情報を参照してください。

組織の Azure Information Protection の保護サービスがアクティブになるは、管理者とユーザーがこの情報保護ソリューションをサポートするアプリケーションとサービスを使用して重要なデータ保護を開始できます。 管理者は、組織が所有する保護されたドキュメントや電子メールを管理および監視することもできます。 


## <a name="do-you-need-to-activate-the-protection-service-azure-rights-management"></a>保護サービス、Azure Rights Management をアクティブ化する必要がありますか。

Azure Rights Management を含むサービス プランを持っている場合は、サービスをアクティブにする必要がない可能性があります。

- **Azure Rights Management または Azure Information Protection を含むサブスクリプションを 2018 年 2 月末日以降を対象として取得した場合:** サービスが自動的にアクティブになります。 お客様または組織の他のグローバル管理者が Azure Rights Management を非アクティブ化しない限り、サービスをアクティブ化する必要はありません。

- **Azure Rights Management または Azure Information Protection を含むサブスクリプションを 2018 年 2 月以前に取得した場合:** Microsoft は、ご利用のテナントで Exchange Online を使用している場合に、これらのサブスクリプションの Azure Rights Management サービスのアクティブ化を開始しています。 これらのサブスクリプションの場合、サービスがアクティブ化される 2018 年 8 月 1 日から自動アクティブ化のロール アウトが開始されます。ただし、[Get-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/get-irmconfiguration?view=exchange-ps) を実行するときに **AutomaticServiceUpdateEnabled** が **false** に設定されていない場合に限ります。 

後続のシナリオがどちらも当てはまらない場合は、保護サービスを手動でアクティブ化する必要があります。 

サービスをアクティブにした後は、組織内のすべてのユーザーが各自のドキュメントや電子メールに情報保護を適用したり、Azure Rights Management で保護されているドキュメントや電子メールを開く (使用する) ことができます。 ただし、そちらを希望する場合は、段階的デプロイのオンボーディング コントロールを使用して、情報保護を適用できるユーザーを制限できます。 詳細については、この記事の「[段階的デプロイのオンボーディング コントロールの構成](#configuring-onboarding-controls-for-a-phased-deployment)」セクションを参照してください。

## <a name="how-to-activate-or-confirm-the-status-of-the-protection-service"></a>アクティブ化または保護サービスの状態を確認する方法 

> [!IMPORTANT]
> Active Directory Rights Management サービス (AD RMS)、組織の展開がある場合は、保護サービスをアクティブにしないでください。 [詳細情報](prepare-environment-adrms.md)

このデータ保護ソリューションを使用するには、組織が、Azure Information Protection からの Azure Rights Management サービスを含むサービス プランを持っている必要があります。 これは、保護サービスをアクティブにできません。 次のいずれかを用意する必要があります。

- [Azure Information Protection プラン](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) 

- [Rights Management が含まれている Office 365 プラン](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)

保護サービスがアクティブになるし、組織内のすべてのユーザーは、ドキュメントや電子メールに情報保護を適用することができますし、すべてのユーザーが開くことができます (使用する) ドキュメントや電子メールをこのサービスによって保護されています。 ただし、そちらを希望する場合は、段階的デプロイのオンボーディング コントロールを使用して、情報保護を適用できるユーザーを制限できます。 詳細については、この記事の「[段階的デプロイのオンボーディング コントロールの構成](#configuring-onboarding-controls-for-a-phased-deployment)」セクションを参照してください。

## <a name="choosing-your-activation-method"></a>アクティブ化メソッドを選択する

手順については、管理ポータルからの保護サービスをアクティブ化、Microsoft 365 管理センターまたは Azure portal を使用するかどうかを選択する方法。

- [Microsoft 365 管理センター](activate-office365.md) - グローバル管理者アカウントが必要

- [Azure Portal](activate-azure.md) - グローバル管理者アカウントは不要

代わりに、次の PowerShell コマンドを使用することができます。

1. 構成して、保護サービスを管理する、AIPService モジュールをインストールします。 手順については、次を参照してください。 [AIPService PowerShell モジュールをインストールする](install-powershell.md)します。

2. PowerShell セッションから実行[Connect AipService](/powershell/module/aipservice/connect-aipservice)、し、メッセージが表示されたら、Azure Information Protection テナントのグローバル管理者アカウントの詳細を提供します。

3. 実行[Get AipService](/powershell/module/aipservice/get-aipservice)を保護サービスがアクティブになっているかどうかを確認します。 **Enabled** の状態でアクティブであることを確認し、**Disabled** はサービスが非アクティブであることを示します。

4. サービスを有効にするには実行[有効にする AipService](/powershell/module/aipservice/enable-aipservice)します。

## <a name="configuring-onboarding-controls-for-a-phased-deployment"></a>段階的デプロイのオンボーディング コントロールの構成
すべてのユーザーを Azure Information Protection を使用して、すぐにドキュメントや電子メールを保護できるにない場合は、使用してユーザー オンボーディング コントロールを構成することができます、[セット AipServiceOnboardingControlPolicy](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy) PowerShellコマンド。 このコマンドを実行するのは、Azure Rights Management サービスをアクティブ化する前と後のどちらでもかまいません。

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

このコマンドレットとその他の例の詳細については、次を参照してください。、[セット AipServiceOnboardingControlPolicy](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy)ヘルプ。

これらのオンボーディング コントロールを使用するときは、保護されたコンテンツを組織内のすべてのユーザーがいつでも使用できますが、コンテンツを保護できるのは組織内の一部のユーザーのみとなり、それ以外のユーザーは情報保護を自分でクライアント アプリケーションから適用することはできません。 たとえば、保護サービスをアクティブになると自動的に公開される既定の保護テンプレートまたはカスタム テンプレートを構成することに、Office アプリに表示されません。 Exchange などのサーバー側アプリケーションでは、同じ結果を実現するために、独自のユーザーごとのコントロールを実装できます。 たとえば、ユーザーが Outlook on the web 内の電子メールを保護できないようにするには、[Set-OwaMailboxPolicy](/powershell/module/exchange/client-access/set-owamailboxpolicy?view=exchange-ps) を使用して *IRMEnabled* パラメーターを *$false* に設定します。


## <a name="next-steps"></a>次の手順
使用して、組織の保護サービスがアクティブになる、 [Azure Information Protection デプロイ ロードマップ](deployment-roadmap.md)を Azure にロールアウトする前に実行する必要がある他の構成手順があるかどうかを確認するにはユーザーと管理者に情報保護します。 

使用するなど、[テンプレート](configure-policy-templates.md)ファイルに保護を適用するユーザーをより簡単にインストールすることで、保護サービスを使用して、オンプレミス サーバーを接続、 [Rights Management コネクタ](deploy-rms-connector.md)を展開し、 [Azure Information Protection クライアント](./rms-client/aip-client.md)すべてのデバイスであらゆる種類のファイルの保護をサポートします。 

Exchange Online や SharePoint Online などの Office サービスの Information Rights Management (IRM) 機能を使用するには、あらかじめ追加の構成手順が必要です。 保護サービスで、Azure Rights Management では、アプリケーションの動作については、次を参照してください。[アプリケーションによる Azure Rights Management サービスのサポート方法](applications-support.md)します。

