---
title: "お客様が管理: AIP テナント キーのライフサイクル操作"
description: "Azure Information Protection のテナント キーを自分で管理する場合 (Bring Your Own Key (BYOK) のシナリオ) に関連するライフサイクル操作についての情報です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c5b19c59-812d-420c-9c54-d9776309636c
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3220b1cbe93b110c838a4e85cc143b44de0d2d14
ms.sourcegitcommit: 0fa5dd38c9d66ee2ecb47dfdc9f2add12731485e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2017
---
# <a name="customer-managed-tenant-key-life-cycle-operations"></a>お客様が管理: テナント キーのライフサイクル操作

>*適用対象: Azure Information Protection、Office 365*

Azure Information Protection のテナント キーを自分で管理する場合 (Bring Your Own Key (BYOK) のシナリオ) は、次のセクションでこのトポロジに関連するライフサイクル操作に関する詳細を参照してください。

## <a name="revoke-your-tenant-key"></a>テナント キーの取り消し
Azure Key Vault では、Azure Information Protection テナント キーが格納されたキー コンテナーに対するアクセス許可を変更して、Azure Rights Management サービスがキーにアクセスできないようにすることができます。 ただし、これを行うと、以前に Azure Rights Management サービスで保護したドキュメントや電子メールを誰も開けなくなります。

Azure Information Protection のサブスクリプションをキャンセルすると、Azure Information Protection ではお客様のテナント キーの使用を停止します。操作を行う必要はありません。

## <a name="rekey-your-tenant-key"></a>テナント キーの再入力
再入力は「キーをロールする」とも呼ばれます。 この操作を実行すると、Azure Information Protection は、ドキュメントおよびメールの保護に既存のテナント キーを使用することを停止し、別のキーを使い始めます。 ポリシーとテンプレートはすぐに再署名されますが、Azure Information Protection を使用しているクライアントおよびサービスの場合、この移行は段階的に行われます。 そのため、しばらくの間、一部の新しいコンテンツは引き続き以前のテナント キーで保護されます。

キーの再入力を行うには、テナント キー オブジェクトを構成し、代わりに使用するキーを指定する必要があります。 これで、前に使用していたキーは自動的に Azure Information Protection のアーカイブされたキーとしてマークされます。 この構成により、このキーを使用して保護されていたコンテンツはアクセス可能なままとなります。

Azure Information Protection に対してキーの再入力が必要になる場合の例を次に示します。

- あなたの会社が 2 つ以上の会社に分かれました。 テナント キーを再入力すると、新しい会社はあなたの社員が公開する新しいコンテンツにアクセスできません。 以前のテナント キーのコピーがあれば、以前のコンテンツにアクセスできます。

- テナント キーのマスター コピー (あなたが所有するコピー) の盗難が疑われています。

キーを再入力するには、Azure Key Vault で新しいキーを作成することも、Azure Key Vault に既にある別のキーを使用することもできます。 Azure Information Protection に BYOK を実装したときと同じ手順を実行します。

1. 新しいキーが Azure Information Protection で既に使用しているキーとは異なるキー コンテナーにある場合にのみ: [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) コマンドレットを使用して、Azure Information Protection が目的のキー コンテナーを使用することを承認します。

2. [Use-AadrmKeyVaultKey](/powershell/module/aadrm/use-aadrmkeyvaultkey) コマンドレットによって、新しいキーを使用するように Azure Information Protection を構成します。

3. [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) コマンドレットによって、テナント キー オブジェクトを構成します。

これらの各ステップの詳細については、「[Azure Information Protection テナント キーを実装する](../plan-design/plan-implement-tenant-key.md#implementing-your-azure-information-protection-tenant-key)」を参照してください。

## <a name="backup-and-recover-your-tenant-key"></a>テナント キーのバックアップ/復旧
テナント キーのバックアップは自分で行う必要があります。 Thales HSM でテナント キーを生成した場合、キーをバックアップするにはトークン化されたキー ファイル、World ファイル、および管理者カードをバックアップするだけです。

[BYOK (Bring Your Own Key) の実装](../plan-design/plan-implement-tenant-key.md#implementing-your-azure-information-protection-tenant-key)に関するセクションの手順に従ってキーを転送してあるので、Key Vault はトークン化されたキー ファイルを保持して任意のサービス ノードの障害から保護します。 このファイルは、特定の Azure リージョンまたはインスタンスを対象としたセキュリティ ワールドにバインドされます。 ただし、これを完全なバックアップとは考えないでください。 これは回復不可能なコピーであるため、たとえば Thales HSM の外部で使用するためにキーのプレーンテキスト コピーが必要になった場合でも、Azure Key Vault はこれを取得することができません。

## <a name="export-your-tenant-key"></a>テナント キーのエクスポート
BYOK を使用する場合、テナント キーを Azure Key Vault または Azure Information Protection からエクスポートできません。 Azure Key Vault 内のコピーは回復不可能です。 

## <a name="respond-to-a-breach"></a>侵害への対応
違反対応プロセスがなければ、どれほど強固でも、セキュリティ システムは完全になりません。 あなたのテナント キーが盗まれた可能性があります。 たとえ十分に保護されていても、現在の生成キー技術、または現在のキーの長さおよびアルゴリズムに脆弱性が見つかる可能性があります。

製品とサービスのセキュリティ インシデントに対応するためにマイクロソフトは専用のチームを置いています。 インシデントが認められる報告があった場合、至急、このチームは範囲、根本原因、軽減の調査にあたります。 このインシデントがあなたの資産に影響を与える場合、Microsoft は Azure Information Protection テナント管理者に電子メールで通知します。その場合、サブスクリプションで指定されたアドレスが使われます。

侵害がある場合、あなたまたはマイクロソフトがとれる最善策は侵害の範囲によって異なります。マイクロソフトはあなたと連携し、このプロセスを進めます。 次の表は一般的な状況と、考えられる対応をいくつかまとめたものです。ただし、実際の対応は調査中に明らかになった情報によって変わります。

|インシデントの説明|考えられる対応|
|------------------------|-------------------|
|テナント キーが漏れています。|テナント キーを再入力します。 「[テナント キーの再入力](#rkey-your-tenant-key)」をご覧ください。|
|無許可の個人またはマルウェアがテナント キーを使用する権利を手に入れましたが、キー自体は漏えいしていません。|テナント キーを再入力してもここでは役に立ちません。根本原因の分析が必要です。 無許可の個人がアクセスを得た原因がプロセスまたはソフトウェアのバグにある場合、その状況は解決する必要があります。|
|現行世代の HSM テクノロジに脆弱性が発見された|Microsoft は HSM を更新する必要があります。 脆弱性によってキーが公開されたと信じるに足る理由が存在する場合、Microsoft はすべてのユーザーにテナント キーを更新するように指示します。|
|RSA アルゴリズム、キーの長さ、ブルート フォース攻撃に見られる脆弱性がコンピューターで実現可能になります。|Microsoft は回復力のある新しいアルゴリズムまたは長いキーをサポートするように Azure Key Vault または Azure Information Protection を更新し、すべてのお客様にテナント キーの更新を指示する必要があります。|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

