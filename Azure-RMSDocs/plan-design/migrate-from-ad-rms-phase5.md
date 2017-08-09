---
title: "AD RMS から Azure Information Protection への移行 - フェーズ 5"
description: "AD RMS から Azure Information Protection への移行のフェーズ 5 には、手順 10 から 12 が含まれます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 2ab4d8c9d253098b4f9ecb7fb820a3df1891e124
ms.sourcegitcommit: 55a71f83947e7b178930aaa85a8716e993ffc063
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2017
---
# <a name="migration-phase-5---post-migration-tasks"></a>移行フェーズ 5 - 移行後のタスク

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Office 365*


AD RMS から Azure Information Protection への移行フェーズ 5 では、次の情報を使用してください。 これらの手順では、「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」の手順 10 から手順 12 を説明します。

## <a name="step-10-deprovison-ad-rms"></a>手順 10. AD RMS をプロビジョニング解除する

サービス接続ポイント (SCP) を Active Directory から削除し、コンピューターがオンプレミス Rights Management インフラストラクチャを検出しないようにします。 既存のクライアントを移行した場合、レジストリに (たとえば、移行スクリプトを実行して) 構成したリダイレクトがあるため、この操作は省略可能です。 ただし、SCP を削除すると、移行の完了後に新しいクライアントと一部の RMS 関連サービスおよびツールは SCP を見つけられなくなり、Azure Rights Management サービスにアクセスすることになります。 

SCP を削除するには、ドメイン エンタープライズ管理者としてログインしていることを確認し、次の手順を使用します。

1. Active Directory Rights Management サービス コンソールで、AD RMS クラスターを右クリックし、**[プロパティ]** をクリックします。

2. [ **SCP** ] タブをクリックします。

3. [ **SCPを変更する** ] チェック ボックスをオンにします。

4. **[現在の SCP を削除する]** を選択して **[OK]** をクリックします。

たとえば、[システム正常性レポートの要求](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx)、[ServiceRequest テーブル](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx)、[保護されたコンテンツへのユーザー アクセスの監査](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx)などを調べることによって、AD RMS サーバーのアクティビティを監視します。 

RMS クライアントがこれらのサーバーと通信していないこと、およびクライアントが Azure Information Protection を正常に使用していることを確認できたら、これらのサーバーから AD RMS サーバーの役割を削除できます。 専用のサーバーを使用している場合は、クライアントが Azure Information Protection を使用しない理由を調査するときにサービスの継続性を確保するように、サーバーの再起動が必要となる報告された問題がないことを確認するあめに、最初にサーバーのシャットダウン期間に警告手順を使用してもかまいません。

AD RMS サーバーをプロビジョニング解除した後、Azure Portal でテンプレートをレビューして統合しユーザーの選択肢を減らしたり、再構成したり、新しいテンプレートを追加したりできます。 これは、既定のテンプレートを発行する絶好のタイミングでもあります。 詳細については、「[Azure Information Protection のテンプレートを構成して管理する](../deploy-use/configure-policy-templates.md)」を参照してください。

>[!IMPORTANT]
> この移行が終わると、Azure Information Protection および Hold Your Own Key (HYOK) オプションで AD RMS クラスターを使うことができなくなります。 Azure Information Protection のラベルに HYOK を使う場合は、現在行われているリダイレクションのため、使用する AD RMS クラスターに、移行したクラスターとは異なるライセンス URL が必要です。

## <a name="step-11-remove-onboarding-controls"></a>手順 11. オンボーディング制御を解除する

既存のすべてのクライアントを Azure Information Protection に移行した後は、オンボーディング制御を使い続け、移行プロセス用に作成した **AIPMigrated** グループを残しておく理由はありません。 

最初にオンボーディング制御を削除した後、**AIPMigrated** グループおよびリダイレクト展開のために作成したソフトウェア展開タスクを解除できます。

オンボーディング制御を解除するには:

1. PowerShell セッションで Azure Rights Management サービスに接続し、メッセージが表示されたら、グローバル管理者の資格情報を指定します。

        Connect-Aadrmservice

2. 次のコマンドを実行し、「**Y**」と入力して確認します。

        Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False

3. オンボーディング制御が設定されていないことを確認します。

        Get-AadrmOnboardingControlPolicy

    出力で、**License** が **False** と表示され、**SecurityGroupOjbectId** に対して GUID が表示されないことを確認します。

## <a name="step-12-rekey-your-azure-information-protection-tenant-key"></a>手順 12. Azure Information Protection テナント キーを更新する
これは、AD RMS デプロイで RMS Cryptographic Mode 1 を使用していた場合、移行が完了したときに必要な手順です。キーの更新により RMS Cryptographic Mode 2 を使用する新しいテナント キーが作成されるためです。 Cryptographic Mode 1 での Azure RMS の使用は、移行プロセス中にのみサポートされます。

これは省略可能ですが、移行が完了したときに推奨される手順です。RMS 暗号化モード 2 を実行していた場合でも推奨されます。 このシナリオでのキーの更新は、AD RMS キーに対する潜在的なセキュリティ侵害から Azure Information Protection テナント キーを保護するのに役立ちます。

Azure Information Protection テナント キーを更新すると ("キーのローリング" とも呼ばれます)、新しいキーが作成され、元のキーがアーカイブされます。 ただし、キーの移動には数週間かかり、すぐには完了しないので、元のキーの侵害が疑われるまで待たず、移行が完了したらすぐに Azure Information Protection テナント キーを更新してください。

Azure Information Protection テナント キーを更新するには:

- テナント キーが Microsoft によって管理されている場合: [Microsoft サポート](../get-started/information-support.md#to-contact-microsoft-support)に連絡し、**AD RMS からの移行後の Azure Information Protection テナント キーの更新要求に関する Azure Information Protection サポート ケース**を開きます。 自分が Azure Information Protection テナントの管理者であることを証明する必要があります。また、このプロセスの確認には数日かかることを承知しておく必要があります。 Standard サポートの料金が適用されます。テナント キーの更新は無料のサポート サービスではありません。

- テナント キーを自分で管理している場合 (BYOK): Azure Key Vault で、Azure Information Protection テナントで使用しているキーを更新し、再度 [Use-AadrmKeyVaultKey](/powershell/aadrm/vlatest/use-aadrmkeyvaultkey) コマンドレットを実行して、新しいキー URL を指定します。 

Azure Information Protection テナント キーの管理の詳細については、「[Azure Rights Management テナント キーに対する操作](../deploy-use/operations-tenant-key.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

移行が完了した後は、[デプロイ ロードマップ](deployment-roadmap.md)を参照して、必要になる可能性があるその他のデプロイ タスクを確認します。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
