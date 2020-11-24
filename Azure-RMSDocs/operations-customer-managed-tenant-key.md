---
title: 'お客様が管理: AIP テナント キーのライフサイクル操作'
description: Azure Information Protection のテナント キーを自分で管理する場合 (Bring Your Own Key (BYOK) のシナリオ) に関連するライフサイクル操作についての情報です。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 12/06/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: c5b19c59-812d-420c-9c54-d9776309636c
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b1e06581cb7291674d3a94c99338a9749b46f9a0
ms.sourcegitcommit: b763a7204421a4c5f946abb7c5cbc06e2883199c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2020
ms.locfileid: "95569758"
---
# <a name="customer-managed-tenant-key-life-cycle-operations"></a>お客様が管理: テナント キーのライフサイクル操作

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection のテナント キーを自分で管理する場合 (Bring Your Own Key (BYOK) のシナリオ) は、次のセクションでこのトポロジに関連するライフサイクル操作に関する詳細を参照してください。

## <a name="revoke-your-tenant-key"></a>テナント キーを取り消します

キーを更新する代わりに、キーを失効させることが必要になるシナリオはごくわずかです。 キーを取り消すと、そのキーを使用してテナントによって保護されているすべてのコンテンツは、復元可能なキーのバックアップがない限り、すべてのユーザー (Microsoft、グローバル管理者、およびスーパーユーザー) がアクセスできなくなります。 キーを取り消した後は、Azure Information Protection 用に新しいテナントキーを作成して構成するまで、新しいコンテンツを保護することはできません。 

お客様が管理するテナントキーを失効させるには、Azure Key Vault で、Azure Information Protection テナントキーを含む key Vault のアクセス許可を変更して、Azure Rights Management サービスがキーにアクセスできなくなるようにします。 この操作により、Azure Information Protection のテナントキーが実質的に取り消されます。

Azure Information Protection のサブスクリプションをキャンセルすると、Azure Information Protection ではお客様のテナント キーの使用を停止します。操作を行う必要はありません。

## <a name="rekey-your-tenant-key"></a>テナント キーの再入力
再入力は「キーをロールする」とも呼ばれます。 この操作を実行すると、Azure Information Protection は、ドキュメントおよびメールの保護に既存のテナント キーを使用することを停止し、別のキーを使い始めます。 ポリシーとテンプレートはすぐに再署名されますが、Azure Information Protection を使用しているクライアントおよびサービスの場合、この移行は段階的に行われます。 そのため、しばらくの間、一部の新しいコンテンツは引き続き以前のテナント キーで保護されます。

キーの再入力を行うには、テナント キー オブジェクトを構成し、代わりに使用するキーを指定する必要があります。 これで、前に使用していたキーは自動的に Azure Information Protection のアーカイブされたキーとしてマークされます。 この構成により、このキーを使用して保護されていたコンテンツはアクセス可能なままとなります。

Azure Information Protection に対してキーの再入力が必要になる場合の例を次に示します。

- あなたの会社が 2 つ以上の会社に分かれました。 テナント キーを再入力すると、新しい会社はあなたの社員が公開する新しいコンテンツにアクセスできません。 以前のテナント キーのコピーがあれば、以前のコンテンツにアクセスできます。

- 別のキー管理トポロジに移行したい。 

- テナント キーのマスター コピー (あなたが所有するコピー) の盗難が疑われています。

管理している別のキーにキーを再入力するには、Azure Key Vault で新しいキーを作成することも、Azure Key Vault に既にある別のキーを使用することもできます。 Azure Information Protection に BYOK を実装したときと同じ手順を実行します。 

1. 新しいキーが Azure Information Protection に既に使用しているキーコンテナーとは別のキーコンテナーにある場合にのみ: [AzKeyVaultAccessPolicy](/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy) コマンドレットを使用して、キーコンテナーを使用する Azure Information Protection を承認します。

2. Azure Information Protection 使用するキーがまだわからない場合は、 [AipServiceKeyVaultKey](/powershell/module/aipservice/use-aipservicekeyvaultkey) コマンドレットを実行します。

3. Run [Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties) コマンドレットを使用して、テナントキーオブジェクトを構成します。

これらの段階の詳細については、次を参照してください。

- 管理する別のキーにキーを再入力する方法については、「 [Azure Information Protection テナントキーの計画と実装](plan-implement-tenant-key.md)」を参照してください。

    
    オンプレミスで作成し Key Vault に転送する、HSM で保護されているキーを再入力する場合は、現在のキーで使用したものと同じセキュリティ ワールドとアクセス カードを使用できます。

- キーを再入力し、マイクロソフトが代わりに管理するキーに変更するには、マイクロソフト管理操作の「[テナント キーの再入力](operations-microsoft-managed-tenant-key.md#rekey-your-tenant-key)」セクションをご覧ください。

## <a name="backup-and-recover-your-tenant-key"></a>テナント キーをバックアップ/復旧します
あなたはテナント キーを管理しているので、Azure Information Protection で使用されるキーをバックアップする責任があります。 

オンプレミスでテナントキーを生成した場合は、nCipher HSM: キーをバックアップするには、トークン化されたキーファイル、world ファイル、および管理者カードをバックアップします。 Azure Key Vault にキーを転送すると、サービス ノードの障害から守るために、トークン化されたキー ファイルがサービスによって保存されます。 このファイルは、特定の Azure リージョンまたはインスタンスを対象としたセキュリティ ワールドにバインドされます。 ただし、このトークン化されたキー ファイルを完全なバックアップとは考えないでください。 たとえば、nCipher HSM の外部で使用するためにキーのプレーンテキストコピーが必要な場合、Azure Key Vault は回復不可能なコピーしかないため、このキーを取得することはできません。

Azure Key Vault には、[バックアップ コマンドレット](/powershell/module/az.keyvault/backup-azkeyvaultkey)が用意されています。これを使用すれば、キーをダウンロードしてファイルに保存することで、キーのバックアップを作成できます。 ダウンロードされたコンテンツは暗号化されているため、Azure Key Vault の外部で使用することはできません。 

## <a name="export-your-tenant-key"></a>テナント キーをエクスポートします
BYOK を使用する場合、テナント キーを Azure Key Vault または Azure Information Protection からエクスポートできません。 Azure Key Vault 内のコピーは回復不可能です。 

## <a name="respond-to-a-breach"></a>侵害に反応します
違反対応プロセスがなければ、どれほど強固でも、セキュリティ システムは完全になりません。 あなたのテナント キーが盗まれた可能性があります。 たとえ十分に保護されていても、現在の生成キー技術、または現在のキーの長さおよびアルゴリズムに脆弱性が見つかる可能性があります。

製品とサービスのセキュリティ インシデントに対応するためにマイクロソフトは専用のチームを置いています。 インシデントが認められる報告があった場合、至急、このチームは範囲、根本原因、軽減の調査にあたります。 このインシデントが資産に影響する場合、Microsoft はテナントのグローバル管理者に電子メールで通知します。

侵害がある場合、あなたまたはマイクロソフトがとれる最善策は侵害の範囲によって異なります。マイクロソフトはあなたと連携し、このプロセスを進めます。 次の表は一般的な状況と、考えられる対応をいくつかまとめたものです。ただし、実際の対応は調査中に明らかになった情報によって変わります。

|インシデントの説明|考えられる対応|
|------------------------|-------------------|
|テナント キーが漏れています。|テナント キーを再入力します。 「 [テナントキーのキー更新](#rekey-your-tenant-key)」を参照してください。|
|無許可の個人またはマルウェアがテナント キーを使用する権利を手に入れましたが、キー自体は漏えいしていません。|テナント キーを再入力してもここでは役に立ちません。根本原因の分析が必要です。 無許可の個人がアクセスを得た原因がプロセスまたはソフトウェアのバグにある場合、その状況は解決する必要があります。|
|現行世代の HSM テクノロジに脆弱性が発見された|Microsoft は HSM を更新する必要があります。 脆弱性によってキーが公開されたと信じるに足る理由が存在する場合、Microsoft はすべてのユーザーにテナント キーを再入力するように指示します。|
|RSA アルゴリズム、キーの長さ、ブルート フォース攻撃に見られる脆弱性がコンピューターで実現可能になります。|Microsoft は回復力のある新しいアルゴリズムまたは長いキーをサポートするように Azure Key Vault または Azure Information Protection を更新し、すべてのお客様にテナント キーの再入力を指示する必要があります。|
