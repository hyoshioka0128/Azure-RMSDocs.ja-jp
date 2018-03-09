---
title: "AD RMS から Azure Information Protection への移行 - フェーズ 5"
description: "AD RMS から Azure Information Protection への移行のフェーズ 5 には、手順 10 から 12 が含まれます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/16/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 0c15bcca607992a2782611286205509377f9fd4d
ms.sourcegitcommit: c2aecb470d0aab89baae237b892dcd82b3ad223e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/09/2018
---
# <a name="migration-phase-5---post-migration-tasks"></a>移行フェーズ 5 - 移行後のタスク

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Office 365*


AD RMS から Azure Information Protection への移行フェーズ 5 では、次の情報を使用してください。 これらの手順では、「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」の手順 10 から手順 12 を説明します。

## <a name="step-10-deprovision-ad-rms"></a>手順 10. AD RMS のプロビジョニング解除

サービス接続ポイント (SCP) を Active Directory から削除し、コンピューターがオンプレミス Rights Management インフラストラクチャを検出しないようにします。 既存のクライアントを移行した場合、レジストリに (たとえば、移行スクリプトを実行して) 構成したリダイレクトがあるため、この操作は省略可能です。 ただし、SCP を削除すると、移行の完了後に新しいクライアントと一部の RMS 関連サービスおよびツールは SCP を見つけられなくなります。 この時点で、すべてのコンピューター接続は Azure Rights Management サービスにアクセスすることになります。 

SCP を削除するには、ドメイン エンタープライズ管理者としてログインしていることを確認し、次の手順を使用します。

1. Active Directory Rights Management サービス コンソールで、AD RMS クラスターを右クリックし、**[プロパティ]** をクリックします。

2. **[SCP]** タブをクリックします。

3. **[SCPを変更する]** チェック ボックスをオンにします。

4. **[現在の SCP を削除する]** を選択して **[OK]** をクリックします。

次に AD RMS サーバーのアクティビティを監視します。 たとえば、[システム正常性レポートの要求の確認](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx)、[ServiceRequest テーブルの確認](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx)、[保護コンテンツに対するユーザー アクセスの監査](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx)などです。 

RMS クライアントがこれらのサーバーと通信していないこと、およびクライアントが Azure Information Protection を正常に使用していることを確認できたら、これらのサーバーから AD RMS サーバーの役割を削除できます。 専用のサーバーを使用している場合は、最初のサーバーのシャットダウン期間に警告手順を使用してもかまいません。 この方法では、サービス継続性のためにこれらのサーバーを再起動する必要がある問題の報告が発生していないことを確認でき、クライアントが Azure Information Protection を使用していない理由を調査する時間を確保できます。

また、AD RMS サーバーのプロビジョニングを解除した後に、Azure Portal でテンプレートを見直す機会が必要な場合があります。 たとえば、ユーザーが選択または再構成する対象が少なくなるように、ラベルに変換して統合する場合です。 これは、既定のテンプレートを発行する絶好のタイミングでもあります。 詳細については、「[Azure Information Protection のテンプレートを構成して管理する](../deploy-use/configure-policy-templates.md)」を参照してください。

>[!IMPORTANT]
> この移行が終わると、Azure Information Protection および Hold Your Own Key (HYOK) オプションで AD RMS クラスターを使うことができなくなります。 Azure Information Protection のラベルに HYOK を使う場合は、現在行われているリダイレクションのため、使用する AD RMS クラスターに、移行したクラスターとは異なるライセンス URL が必要です。

## <a name="step-11-complete-client-migration-tasks"></a>手順 11. クライアントの移行タスクを完了する

モバイル デバイス クライアントおよび Mac コンピューターの場合: [AD RMS モバイル デバイス拡張機能](http://technet.microsoft.com/library/dn673574.aspx)をデプロイするときに作成した DNS SRV レコードを削除します。

このような DNS の変更が伝達されると、これらのクライアントは自動的に検出され、Azure Rights Management サービスの使用を開始します。 ただし、Office Mac を実行する Mac コンピューターは、AD RMS からの情報をキャッシュに入れます。 これらのコンピューターの場合、このプロセスには最大で 30 日かかることがあります。 

Mac コンピューターが検出プロセスを直ちに実行するようにするには、キーチェーンで "adal" を検索し、すべての ADAL エントリを削除します。 これらのコンピューターで次のコマンドを実行します。

````

rm -r ~/Library/Cache/MSRightsManagement

rm -r ~/Library/Caches/com.microsoft.RMS-XPCService

rm -r ~/Library/Caches/Microsoft\ Rights\ Management\ Services

rm -r ~/Library/Containers/com.microsoft.RMS-XPCService

rm -r ~/Library/Containers/com.microsoft.RMSTestApp

rm ~/Library/Group\ Containers/UBF8T346G9.Office/DRM.plist

killall cfprefsd

````

既存のすべての Windows コンピューターを Azure Information Protection に移行した後は、オンボーディング制御を使い続け、移行プロセス用に作成した **AIPMigrated** グループを残しておく理由はありません。 

最初にオンボーディング制御を解除すると、**AIPMigrated** グループと、移行スクリプトをデプロイするために作成した任意のソフトウェア デプロイ方法を削除できます。

オンボーディング制御を解除するには:

1. PowerShell セッションで Azure Rights Management サービスに接続し、メッセージが表示されたら、グローバル管理者の資格情報を指定します。

        Connect-Aadrmservice

2. 次のコマンドを実行し、「**Y**」と入力して確認します。

        Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False
    
    このコマンドを実行すると、Azure Rights Management 保護サービスのライセンスの強制が解除され、すべてのコンピューターでドキュメントおよび電子メールを保護できるようになります。

3. オンボーディング制御が設定されていないことを確認します。

        Get-AadrmOnboardingControlPolicy

    出力で、**License** が **False** と表示され、**SecurityGroupOjbectId** に対して GUID が表示されないことを確認します。

最後に、Office 2010 を使用していて、Windows タスク スケジューラ ライブラリで "**AD RMS Rights Policy Template Management (Automated) (AD RMS 権利ポリシー テンプレート管理 (自動))**" タスクを有効にしている場合、Azure Information Protection クライアントでは使用されていないため、このタスクを無効にします。 通常、このタスクはグループ ポリシーを使用して有効にされ、AD RMS デプロイをサポートします。 このタスクは次の場所で見つけることができます: **Microsoft**  >  **Windows**  >  **Active Directory Rights Management サービス クライアント**

## <a name="step-12-rekey-your-azure-information-protection-tenant-key"></a>手順 12. Azure Information Protection テナント キーを再入力する

AD RMS デプロイで RMS 暗号化モード 1 が使用されていた場合、移行が完了したら、この手順を実行することをお勧めします。 キーの再入力を行うと、RMS 暗号化モード 2 を使用した保護が行われます。 

AD RMS のデプロイで暗号化モード 2 が使用されている場合も、この手順を実行することをお勧めします。新しいキーは、AD RMS キーに対する潜在的なセキュリティ侵害からテナントを保護するのに役立つためです。

Azure Information Protection テナント キーの再入力を行うと ("キーをロールする" とも言われる)、現在アクティブなキーはアーカイブされ、Azure Information Protection は、指定した別のキーの使用を開始します。 この別のキーは、Azure Key Vault で自分で作成した新しいキーとすることも、テナント用に自動的に作成された既定のキーとすることもできます。

あるキーから別のキーへの移行は、即時には実行されず、数週間かかります。 即時には行われないために、元のキーの侵害が疑われるまで待たず、移行が完了したらすぐにこの手順を実行してください。

Azure Information Protection テナント キーを更新するには:

- **テナント キーが Microsoft によって管理されている場合**: PowerShell コマンドレット [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) を実行し、テナント用に自動的に作成されたキーの識別子を指定します。 指定する値を識別するには、[Get-AadrmKeys](/powershell/module/aadrm/get-aadrmkeys) コマンドレットを実行します。 テナント用に自動的に作成されたキーは作成日が最も古いので、次のコマンドを使用して識別することができます。
    
        (Get-AadrmKeys) | Sort-Object CreationTime | Select-Object -First 1

- **テナント キーを自分で管理している場合 (BYOK)**: Azure Key Vault で、Azure Information Protection テナントに対してキー作成プロセスを繰り返し、次に [Use-AadrmKeyVaultKey](/powershell/aadrm/vlatest/use-aadrmkeyvaultkey) コマンドレットを再度実行して、この新しいキーの URI を指定します。 

Azure Information Protection テナント キーの管理の詳細については、「[Azure Rights Management テナント キーに対する操作](../deploy-use/operations-tenant-key.md)」を参照してください。


## <a name="next-steps"></a>次の手順

移行が完了した後は、[デプロイ ロードマップ](deployment-roadmap.md)を参照して、必要になる可能性があるその他のデプロイ タスクを確認します。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
