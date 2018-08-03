---
title: 'お客様が管理: AIP テナント キーのライフサイクル操作'
description: Azure Information Protection のテナント キーを自分で管理する場合 (Bring Your Own Key (BYOK) のシナリオ) に関連するライフサイクル操作についての情報です。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/07/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c5b19c59-812d-420c-9c54-d9776309636c
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d1c2f96dfd915134385fd4e790e9477c77fa17ad
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39375176"
---
# <a name="customer-managed-tenant-key-life-cycle-operations"></a>お客様が管理: テナント キーのライフサイクル操作

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection のテナント キーを自分で管理する場合 (Bring Your Own Key (BYOK) のシナリオ) は、次のセクションでこのトポロジに関連するライフサイクル操作に関する詳細を参照してください。

## <a name="revoke-your-tenant-key"></a>テナント キーの取り消し
Azure Key Vault では、Azure Information Protection テナント キーが格納されたキー コンテナーに対するアクセス許可を変更して、Azure Rights Management サービスがキーにアクセスできないようにすることができます。 ただし、これを行うと、以前に Azure Rights Management サービスで保護したドキュメントや電子メールを誰も開けなくなります。

Azure Information Protection のサブスクリプションをキャンセルすると、Azure Information Protection ではお客様のテナント キーの使用を停止します。操作を行う必要はありません。

## <a name="rekey-your-tenant-key"></a>テナント キーの再入力
再入力は「キーをロールする」とも呼ばれます。 この操作を実行すると、Azure Information Protection は、ドキュメントおよびメールの保護に既存のテナント キーを使用することを停止し、別のキーを使い始めます。 ポリシーとテンプレートはすぐに再署名されますが、Azure Information Protection を使用しているクライアントおよびサービスの場合、この移行は段階的に行われます。 そのため、しばらくの間、一部の新しいコンテンツは引き続き以前のテナント キーで保護されます。

キーの再入力を行うには、テナント キー オブジェクトを構成し、代わりに使用するキーを指定する必要があります。 これで、前に使用していたキーは自動的に Azure Information Protection のアーカイブされたキーとしてマークされます。 この構成により、このキーを使用して保護されていたコンテンツはアクセス可能なままとなります。

Azure Information Protection に対してキーの再入力が必要になる場合の例を次に示します。

- あなたの会社が 2 つ以上の会社に分かれました。 テナント キーを再入力すると、新しい会社はあなたの社員が公開する新しいコンテンツにアクセスできません。 以前のテナント キーのコピーがあれば、以前のコンテンツにアクセスできます。

- 別のキー管理トポロジに移行したい。 

- テナント キーのマスター コピー (あなたが所有するコピー) の盗難が疑われています。

管理している別のキーにキーを再入力するには、Azure Key Vault で新しいキーを作成することも、Azure Key Vault に既にある別のキーを使用することもできます。 Azure Information Protection に BYOK を実装したときと同じ手順を実行します。

1. 新しいキーが Azure Information Protection で既に使用しているキーとは異なるキー コンテナーにある場合にのみ: [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) コマンドレットを使用して、Azure Information Protection が目的のキー コンテナーを使用することを承認します。

2. 使用する予定のキーを Azure Information Protection がまだ認識していない場合、[Use-AadrmKeyVaultKey](/powershell/module/aadrm/use-aadrmkeyvaultkey) コマンドレットを実行します。

3. [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) コマンドレットによって、テナント キー オブジェクトを構成します。

これらの段階の詳細については、次を参照してください。

- 管理する別のキーにキーを再入力するには、「[Azure Information Protection テナント キーの BYOK を実装する](../plan-design/plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key)」を参照してください。

- キーを再入力し、マイクロソフトが代わりに管理するキーに変更するには、マイクロソフト管理操作の「[テナント キーの再入力](operations-microsoft-managed-tenant-key.md#rekey-your-tenant-key)」セクションをご覧ください。

## <a name="backup-and-recover-your-tenant-key"></a>テナント キーのバックアップ/復旧
あなたはテナント キーを管理しているので、Azure Information Protection で使用されるキーをバックアップする責任があります。 

オンプレミスの Thales HSM で、テナント キーを生成した場合: キーをバックアップするにはトークン化されたキー ファイル、World ファイル、および管理者カードをバックアップします。 Azure Key Vault にキーを転送すると、サービス ノードの障害から守るために、トークン化されたキー ファイルがサービスによって保存されます。 このファイルは、特定の Azure リージョンまたはインスタンスを対象としたセキュリティ ワールドにバインドされます。 ただし、このトークン化されたキー ファイルを完全なバックアップとは考えないでください。 これは回復不可能なコピーであるため、たとえば Thales HSM の外部で使用するためにキーのプレーンテキスト コピーが必要になった場合でも、Azure Key Vault はこれを取得することができません。

Azure Key Vault には、[バックアップ コマンドレット](/powershell/module/azurerm.keyvault/Backup-AzureKeyVaultKey)が用意されています。これを使用すれば、キーをダウンロードしてファイルに保存することで、キーのバックアップを作成できます。 ダウンロードされたコンテンツは暗号化されているため、Azure Key Vault の外部で使用することはできません。 

## <a name="export-your-tenant-key"></a>テナント キーのエクスポート
BYOK を使用する場合、テナント キーを Azure Key Vault または Azure Information Protection からエクスポートできません。 Azure Key Vault 内のコピーは回復不可能です。 

## <a name="respond-to-a-breach"></a>侵害への対応
違反対応プロセスがなければ、どれほど強固でも、セキュリティ システムは完全になりません。 あなたのテナント キーが盗まれた可能性があります。 たとえ十分に保護されていても、現在の生成キー技術、または現在のキーの長さおよびアルゴリズムに脆弱性が見つかる可能性があります。

製品とサービスのセキュリティ インシデントに対応するためにマイクロソフトは専用のチームを置いています。 インシデントが認められる報告があった場合、至急、このチームは範囲、根本原因、軽減の調査にあたります。 このインシデントがあなたの資産に影響を与える場合、Microsoft は Azure Information Protection テナント管理者に電子メールで通知します。その場合、サブスクリプションで指定されたアドレスが使われます。

侵害がある場合、あなたまたはマイクロソフトがとれる最善策は侵害の範囲によって異なります。マイクロソフトはあなたと連携し、このプロセスを進めます。 次の表は一般的な状況と、考えられる対応をいくつかまとめたものです。ただし、実際の対応は調査中に明らかになった情報によって変わります。

|インシデントの説明|考えられる対応|
|------------------------|-------------------|
|テナント キーが漏れています。|テナント キーを再入力します。 「[テナント キーの再入力](#rekey-your-tenant-key)」をご覧ください。|
|無許可の個人またはマルウェアがテナント キーを使用する権利を手に入れましたが、キー自体は漏えいしていません。|テナント キーを再入力してもここでは役に立ちません。根本原因の分析が必要です。 無許可の個人がアクセスを得た原因がプロセスまたはソフトウェアのバグにある場合、その状況は解決する必要があります。|
|現行世代の HSM テクノロジに脆弱性が発見された|Microsoft は HSM を更新する必要があります。 脆弱性によってキーが公開されたと信じるに足る理由が存在する場合、Microsoft はすべてのユーザーにテナント キーを再入力するように指示します。|
|RSA アルゴリズム、キーの長さ、ブルート フォース攻撃に見られる脆弱性がコンピューターで実現可能になります。|Microsoft は回復力のある新しいアルゴリズムまたは長いキーをサポートするように Azure Key Vault または Azure Information Protection を更新し、すべてのお客様にテナント キーの再入力を指示する必要があります。|


