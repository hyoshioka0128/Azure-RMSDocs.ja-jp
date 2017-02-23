---
title: "AD RMS から Azure Information Protection への移行 - フェーズ 4 | Azure Information Protection"
description: "AD RMS から Azure Information Protection への移行のフェーズ 4 には、手順 8 ～ 9 が含まれます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e45bbfe0fc2b064d987016cac8af8c4f57d465c9
ms.openlocfilehash: e10b271872935b7903a3e1bcfe2e8287e693c613


---

# <a name="migration-phase-4---post-migration-tasks"></a>移行フェーズ 4 - 移行後のタスク

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Office 365*


AD RMS から Azure Information Protection への移行フェーズ 4 では、次の情報を使用してください。 これらの手順では、「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」の手順 8 から手順 9 を説明します。


## <a name="step-8-decommission-ad-rms"></a>手順 8. AD RMS の使用を停止する

サービス接続ポイント (SCP) を Active Directory から削除し、コンピューターがオンプレミス Rights Management インフラストラクチャを検出しないようにします。 既存のクライアントを移行した場合、レジストリに (たとえば、移行スクリプトを実行して) 構成したリダイレクトがあるため、この操作は省略可能です。 ただし、SCP を削除すると、移行の完了後に新しいクライアントと一部の RMS 関連サービスおよびツールは SCP を見つけられなくなり、Azure Rights Management サービスにアクセスすることになります。 

SCP を削除するには、ドメイン エンタープライズ管理者としてログインしていることを確認し、次の手順を使用します。

1. Active Directory Rights Management サービス コンソールで、AD RMS クラスターを右クリックし、**[プロパティ]** をクリックします。

2. [ **SCP** ] タブをクリックします。

3. [ **SCPを変更する** ] チェック ボックスをオンにします。

4. **[現在の SCP を削除する]** を選択して **[OK]** をクリックします。

たとえば、[システム正常性レポートの要求](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx)、[ServiceRequest テーブル](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx)、[保護されたコンテンツへのユーザー アクセスの監査](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx)などを調べることによって、AD RMS サーバーのアクティビティを監視します。 RMS クライアントがこれらのサーバーと通信していないこと、およびクライアントが Azure Information Protection を正常に使用していることを確認できたら、これらのサーバーから AD RMS サーバーの役割を削除できます。 専用のサーバーを使用している場合は、クライアントが Azure Information Protection を使用しない理由を調査するときにサービスの継続性を確保するように、サーバーの再起動が必要となる報告された問題がないことを確認するあめに、最初にサーバーのシャットダウン期間に警告手順を使用してもかまいません。

AD RMS サーバーの使用を停止した後、Azure クラシック ポータルでテンプレートをレビューして統合しユーザーの選択肢を減らしたり、再構成したり、新しいテンプレートを追加したりできます。 これは、既定のテンプレートを発行する絶好のタイミングでもあります。 詳細については、「[Azure Rights Management サービスのカスタム テンプレートを構成する](../deploy-use/configure-custom-templates.md)」を参照してください。

## <a name="step-9-re-key-your-azure-information-protection-tenant-key"></a>手順 9. Azure Information Protection テナント キーを更新する
この手順は、選択したテナント キー トポロジが顧客管理 (Azure Key Vault での BYOK) ではなくマイクロソフト管理である場合にのみ適用されます。

この手順は省略できます。ただし、Azure Information Protection テナント キーが Microsoft によって管理されていて、AD RMS から移行済みである場合は、実行することをお勧めします。 このシナリオでのキーの更新は、AD RMS キーに対する潜在的なセキュリティ侵害から Azure Information Protection テナント キーを保護するのに役立ちます。

Azure Information Protection テナント キーを更新すると ("キーのローリング" とも呼ばれます)、新しいキーが作成され、元のキーがアーカイブされます。 ただし、キーの移動には数週間かかりすぐには完了しないので、元のキーの侵害が疑われるまで待たず、移行が完了したらすぐに Azure Information Protection テナント キーを更新してください。

マイクロソフト管理の Azure Information Protection テナント キーを更新するには、[Microsoft サポート](../get-started/information-support.md#to-contact-microsoft-support)に連絡し、**AD RMS からの移行後の Azure Information Protection テナント キーの更新要求に関する Azure Information Protection サポート ケース**を開きます。 自分が Azure Information Protection テナントの管理者であることを証明する必要があります。また、このプロセスの確認には数日かかることを承知する必要があります。 Standard サポートの料金が適用されます。テナント キーの更新は無料のサポート サービスではありません。


## <a name="next-steps"></a>次のステップ

Azure Information Protection テナント キーの管理の詳細については、「[Azure Rights Management テナント キーに対する操作](../deploy-use/operations-tenant-key.md)」を参照してください。

移行が完了した後は、[デプロイ ロードマップ](deployment-roadmap.md)を参照して、必要になる可能性があるその他のデプロイ タスクを確認します。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Feb17_HO2-->


