---
title: Microsoft が管理 - AIP テナント キーのライフサイクル操作
description: Microsoft が Azure Information Protection のテナント キーを管理する場合 (既定) に関連するライフサイクル操作に関する詳細です。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 08/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 3c48cda6-e004-4bbd-adcf-589815c56c55
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 00e99f55130f25fa9368a7fdcd1f8c2795250c89
ms.sourcegitcommit: dc655736e531260c7718a8808f4f1016391d2d7d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70020489"
---
# <a name="microsoft-managed-tenant-key-life-cycle-operations"></a>Microsoft が管理:テナント キーのライフサイクル操作

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Microsoft が Azure Information Protection のテナント キーを管理する場合 (既定)、次のセクションを使用してこのトポロジに関連するライフサイクル操作に関する詳細を参照してください。

## <a name="revoke-your-tenant-key"></a>テナント キーを取り消します
Azure Information Protection のサブスクリプションをキャンセルすると、Azure Information Protection ではお客様のテナント キーの使用を停止します。操作を行う必要はありません。

## <a name="rekey-your-tenant-key"></a>テナント キーの再入力
再入力は「キーをロールする」とも呼ばれます。 この操作を実行すると、Azure Information Protection は、ドキュメントおよびメールの保護に既存のテナント キーを使用することを停止し、別のキーを使い始めます。 ポリシーとテンプレートはすぐに再署名されますが、Azure Information Protection を使用しているクライアントおよびサービスの場合、この移行は段階的に行われます。 そのため、しばらくの間、一部の新しいコンテンツは引き続き以前のテナント キーで保護されます。

キーの再入力を行うには、テナント キー オブジェクトを構成し、代わりに使用するキーを指定する必要があります。 これで、前に使用していたキーは自動的に Azure Information Protection のアーカイブされたキーとしてマークされます。 この構成により、このキーを使用して保護されていたコンテンツはアクセス可能なままとなります。

Azure Information Protection に対してキーの再入力が必要になる場合の例を次に示します。

- 暗号化モード 1 のキーを使用する Active Directory Rights Management サービス (AD RMS) から移行しました。 移行が完了したら、暗号化モード 2 を使用するキーを使うように変更します。

- あなたの会社が 2 つ以上の会社に分かれました。 テナント キーを再入力すると、新しい会社はあなたの社員が公開する新しいコンテンツにアクセスできません。 以前のテナント キーのコピーがあれば、以前のコンテンツにアクセスできます。

- 別のキー管理トポロジに移行したい。

- テナント キーのマスター コピーの盗難が疑われています。

キーを再入力する場合、Microsoft が管理している別のキーを選択してテナント キーとすることはできますが、Microsoft が管理するキーを自分で新たに作成することはできません。 新しいキーを作成するには、キー トポロジを変更して、"お客様が管理 (BYOK)" とする必要があります。

Active Directory Rights Management サービス (AD RMS) から移行済みである場合に、Azure Information Protection 用に Microsoft が管理するキー トポロジを選択すると、Microsoft が管理するキーを複数持つことができます。 このシナリオでは、テナントに対して Microsoft が管理するキーは少なくとも 2 つあります。 1 つ (または複数の) キーが、AD RMS からインポートしたキーとなります。 Azure Information Protection テナント用に自動的作成された既定のキーもあります。

Azure Information Protection のアクティブなテナントキーとして別のキーを選択するには、AIPService モジュールの[Set-AipServiceKeyProperties](/powershell/module/aipservice/set-aipservicekeyproperties)コマンドレットを使用します。 使用するキーを識別できるように、 [Get AipServiceKeys](/powershell/module/aipservice/get-aipservicekeys)コマンドレットを使用します。 Azure Information Protection テナント用に自動的に作成された既定のキーを特定するには、次のコマンドを実行します。

    (Get-AipServiceKeys) | Sort-Object CreationTime | Select-Object -First 1

キー トポロジを、お客様による管理 (BYOK) に変更するには、「[Azure Information Protection テナント キーの BYOK を実装する](plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key)」を参照してください。

## <a name="backup-and-recover-your-tenant-key"></a>テナント キーをバックアップ/復旧します
テナント キーのバックアップは Microsoft が行うため、ユーザーの操作は必要ありません。

## <a name="export-your-tenant-key"></a>テナント キーをエクスポートします
Azure Information Protection の構成およびテナント キーをエクスポートするには、次の 3 つの手順に従います。

### <a name="step-1-initiate-export"></a>手順 1:エクスポートの開始

- [Microsoft サポートに連絡](information-support.md#to-contact-microsoft-support)し、**Azure Information Protection キーのエクスポートの要求で Azure Information Protection サポート ケース**を開きます。 テナントのグローバル管理者であることを証明し、このプロセスの確認に数日かかることを理解しておく必要があります。 Standard サポートの料金が適用されます。テナント キーのエクスポートは無料のサポート サービスではありません。

### <a name="step-2-wait-for-verification"></a>手順 2:確認を待機する

- Microsoft は Azure Information Protection テナント キーのリリース要求が正当であることを確認します。 このプロセスには、最大 3 週間を要することがあります。

### <a name="step-3-receive-key-instructions-from-css"></a>手順 3:CSS からの主要な命令の受信

- Microsoft カスタマー サポート サービス (CSS) は、Azure Information Protection の構成およびテナント キーを、パスワードで保護されたファイルで暗号化した状態で送付します。 このファイルのファイル名拡張子は、 **.tpd** です。 これにあたって、CSS はまずエクスポートを開始したユーザーにツールを電子メールで送信します。 このツールをコマンド プロンプトから次のように実行します。

    ```
    AadrmTpd.exe -createkey
    ```
    この結果、RSA キー ペアが生成され、公開キーおよび秘密キーが現在のフォルダーにファイルとして保存されます。 例えば:**PublicKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt** や **PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt** のようになります。

    CSS からの電子メールに返信します。返信には名前が **PublicKey** で始まるファイルを添付します。 次に CSS は、TPD ファイルを、RSA キーで暗号化された .xml ファイルとして送信します。 AadrmTpd ツールを最初に実行したフォルダーにこのファイルをコピーし、名前が **PrivateKey** で始まるファイルと CSS から受け取ったこのファイルを使用して、AadrmTpd ツールをもう一度実行します。 例えば:

    ```
    AadrmTpd.exe -key PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt -target TPD-77172C7B-8E21-48B7-9854-7A4CEAC474D0.xml
    ```
    このコマンドの出力は、次の2つのファイルである必要があります。一方にはパスワードで保護された TPD のプレーンテキスト パスワードが含まれ、もう一方にはパスワードで保護された TPD 自体が含まれています。 ファイルには、以下のような新しい GUID が付けられます。
     
  - Password-5E4C2018-8C8C-4548-8705-E3218AA1544E.txt

  - ExportedTPD-5E4C2018-8C8C-4548-8705-E3218AA1544E.xml

    これらのファイルをバックアップし、安全な場所に保存します。これにより、このテナント キーで保護されたコンテンツを継続して暗号化解除できるようになります。 また、AD RMS に移行する場合は、この TPD ファイル (名前が **ExportedTDP** で始まるファイル) を AD RMS サーバーにインポートできます。

### <a name="step-4-ongoing-protect-your-tenant-key"></a>手順 4:メンテナンステナントキーを保護する

テナント キーを受領したら、厳重に保護してください。だれかがそれにアクセスできる場合、そのキーを使用して保護されているすべてのドキュメントを暗号化解除できるからです。

テナント キーをエクスポートする理由が、Azure Information Protection を使用しなくなったためである場合、ベスト プラクティスとして、直ちに Azure Information Protection テナントから Azure Rights Management サービスを非アクティブ化してください。 これは、テナント キーの受領後すぐに実行してください。この予防策によって、アクセスすべきでないだれかがテナント キーにアクセスした場合の影響を最小限にできます。 手順については、「[Azure Rights Management の使用停止と非アクティブ化](decommission-deactivate.md)」を参照してください。

## <a name="respond-to-a-breach"></a>侵害に反応します
違反対応プロセスがなければ、どれほど強固でも、セキュリティ システムは完全になりません。 あなたのテナント キーが盗まれた可能性があります。 たとえ十分に保護されていても、現在の生成キー技術、または現在のキーの長さおよびアルゴリズムに脆弱性が見つかる可能性があります。

製品とサービスのセキュリティ インシデントに対応するためにマイクロソフトは専用のチームを置いています。 インシデントが認められる報告があった場合、至急、このチームは範囲、根本原因、軽減の調査にあたります。 このインシデントが資産に影響する場合、Microsoft はテナントのグローバル管理者に電子メールで通知します。

侵害がある場合、あなたまたはマイクロソフトがとれる最善策は侵害の範囲によって異なります。マイクロソフトはあなたと連携し、このプロセスを進めます。 次の表は一般的な状況と、考えられる対応をいくつかまとめたものです。ただし、実際の対応は調査中に明らかになった情報によって変わります。

|インシデントの説明|考えられる対応|
|------------------------|-------------------|
|テナント キーが漏れています。|テナント キーを再入力します。 この記事の「[テナント キーの再入力](#rekey-your-tenant-key)」セクションをご覧ください。|
|無許可の個人またはマルウェアがテナント キーを使用する権利を手に入れましたが、キー自体は漏えいしていません。|テナント キーを再入力してもここでは役に立ちません。根本原因の分析が必要です。 無許可の個人がアクセスを得た原因がプロセスまたはソフトウェアのバグにある場合、その状況は解決する必要があります。|
|RSA アルゴリズム、キーの長さ、ブルート フォース攻撃に見られる脆弱性がコンピューターで実現可能になります。|Microsoft は回復力のある新しいアルゴリズムまたは長いキーをサポートするように Azure Information Protection を更新し、すべてのお客様にテナント キーの再入力を指示する必要があります。|


