---
title: "お客様が管理 - テナント キーのライフサイクル操作 | Azure Information Protection"
description: "Azure Information Protection のテナント キーを自分で管理する場合 (Bring Your Own Key (BYOK) のシナリオ) に関連するライフサイクル操作についての情報です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/04/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c5b19c59-812d-420c-9c54-d9776309636c
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 92918ceae563d0e32d39543938862497c6437372


---


# <a name="customer-managed-tenant-key-lifecycle-operations"></a>お客様が管理: テナント キーのライフサイクル操作

>*適用対象: Azure Information Protection、Office 365*

Azure Information Protection のテナント キーを自分で管理する場合 (Bring Your Own Key (BYOK) のシナリオ) は、次のセクションでこのトポロジに関連するライフサイクル操作に関する詳細を参照してください。

## <a name="revoke-your-tenant-key"></a>テナント キーを取り消します
Azure Key Vault では、Azure Information Protection テナント キーが格納されたキー コンテナーに対するアクセス許可を変更して、Azure Rights Management サービスがキーにアクセスできないようにすることができます。 ただし、これを行うと、以前に Azure Rights Management サービスで保護したドキュメントや電子メールを誰も開けなくなります。

Azure Information Protection のサブスクリプションをキャンセルすると、Azure Information Protection ではお客様のテナント キーの使用を停止します。操作を行う必要はありません。


## <a name="re-key-your-tenant-key"></a>テナント キーを再入力します
再入力は「キーをロールする」とも呼ばれます。 本当に必要でない限り、テナント キーは再入力しないでください。 Office 2010 など、以前のクライアントはキー変更を滑らかに処理するようには設計されていません。 このシナリオでは、グループ ポリシーまたは同等のメカニズムを使用し、コンピューターの Rights Management 状態を消去する必要があります。 ただし、場合によってはテナント キーの再入力を強制する正規のイベントがいくつかあります。 たとえば、

-   あなたの会社が&2; つ以上の会社に分かれました。 テナント キーを再入力すると、新しい会社はあなたの社員が公開する新しいコンテンツにアクセスできません。 以前のテナント キーのコピーがあれば、以前のコンテンツにアクセスできます。

-   テナント キーのマスター コピー (あなたが所有するコピー) の盗難が疑われています。

テナント キーを再入力すると、新しいコンテンツは新しいテナント キーの利用により保護されます。 これは段階的に行われます。そのため、一定期間、一部の新しいコンテンツは引き続き以前のテナント キーで保護されます。 以前に保護されたコンテンツは以前のテナント キーで引き続き保護されます。 このシナリオをサポートするために、Azure Information Protection は以前のテナント キーを保有します。そのため、古いコンテンツのライセンスを発行できます。

テナント キーを再入力するには、最初に Key Vault で Azure Information Protection テナント キーを再入力します。 次に、Add-AadrmKeyVaultKey コマンドレットをもう一度実行して、新しいキー URL を指定します。

## <a name="backup-and-recover-your-tenant-key"></a>テナント キーをバックアップ/復旧します
テナント キーのバックアップは自分で行う必要があります。 Thales HSM でテナント キーを生成した場合、キーをバックアップするにはトークン化されたキー ファイル、World ファイル、および管理者カードをバックアップするだけです。

「[Azure Rights Management テナント キーを計画して実装する](../plan-design/plan-implement-tenant-key.md)」の「[Implementing bring your own key (BYOK) (BYOK (Bring Your Own Key) の実装)](../plan-design/plan-implement-tenant-key.md#implementing-your-azure-information-protection-tenant-key)」セクションの手順に従ってキーを転送してあるので、Key Vault はトークン化されたキー ファイルを保持して任意のサービス ノードの障害から保護します。 このファイルは、特定の Azure リージョンまたはインスタンスを対象としたセキュリティ ワールドにバインドされます。 ただし、これを完全なバックアップとは考えないでください。 これは回復不可能なコピーであるため、たとえば Thales HSM の外部で使用するためにキーのプレーンテキスト コピーが必要になった場合でも、Azure Key Vault はこれを取得することができません。

## <a name="export-your-tenant-key"></a>テナント キーをエクスポートします
BYOK を使用する場合、テナント キーを Azure Key Vault または Azure Information Protection からエクスポートできません。 Azure Key Vault 内のコピーは回復不可能です。 

## <a name="respond-to-a-breach"></a>侵害に反応します
違反対応プロセスがなければ、どれほど強固でも、セキュリティ システムは完全になりません。 あなたのテナント キーが盗まれた可能性があります。 たとえ十分に保護されていても、現在の HSM 技術、現在のキー長、アルゴリズムに脆弱性が見つかる可能性があります。

製品とサービスのセキュリティ インシデントに対応するためにマイクロソフトは専用のチームを置いています。 インシデントが認められる報告があった場合、至急、このチームは範囲、根本原因、軽減の調査にあたります。 このインシデントがあなたの資産に影響を与える場合、Microsoft は Azure Information Protection テナント管理者に電子メールで通知します。その場合、サブスクリプションで指定されたアドレスが使われます。

侵害がある場合、あなたまたはマイクロソフトがとれる最善策は侵害の範囲によって異なります。マイクロソフトはあなたと連携し、このプロセスを進めます。 次の表は一般的な状況と考えられる対応をいくつかまとめたものです。ただし、厳密な対応は調査中に明らかになった情報によって変わります。

|インシデントの説明|考えられる対応|
|------------------------|-------------------|
|テナント キーが漏れています。|テナント キーを再入力します。 「[テナント キーを再入力します](#re-key-your-tenant-key)」を参照してください。|
|無許可の個人またはマルウェアがテナント キーを使用する権利を手に入れましたが、キー自体は漏えいしていません。|テナント キーを再入力してもここでは役に立ちません。根本原因の分析が必要です。 無許可の個人がアクセスを得た原因がプロセスまたはソフトウェアのバグにある場合、その状況は解決する必要があります。|
|現行世代の HSM テクノロジに脆弱性が発見された|Microsoft は HSM を更新する必要があります。 脆弱性によってキーが公開されたと信じるに足る理由が存在する場合、Microsoft はすべてのユーザーにテナント キーを更新するように指示します。|
|RSA アルゴリズム、キーの長さ、ブルート フォース攻撃に見られる脆弱性がコンピューターで実現可能になります。|Microsoft は回復力のある新しいアルゴリズムまたは長いキーをサポートするように Azure Key Vault または Azure Information Protection を更新し、すべてのお客様にテナント キーの更新を指示する必要があります。|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]




<!--HONumber=Jan17_HO4-->


