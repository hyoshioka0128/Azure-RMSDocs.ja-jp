---
title: "Microsoft が管理 - テナント キーのライフサイクル操作 | Azure Information Protection"
description: "Microsoft が Azure Information Protection のテナント キーを管理する場合 (既定) に関連するライフサイクル操作に関する詳細です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3c48cda6-e004-4bbd-adcf-589815c56c55
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 0aad5eeb88dd471ece1bf6425a4efe8050bbdf2c


---


# <a name="microsoft-managed-tenant-key-lifecycle-operations"></a>Microsoft が管理: テナント キーのライフサイクル操作

>*適用対象: Azure Information Protection、Office 365*

Microsoft が Azure Information Protection のテナント キーを管理する場合 (既定)、次のセクションを使用してこのトポロジに関連するライフサイクル操作に関する詳細を参照してください。

## <a name="revoke-your-tenant-key"></a>テナント キーを取り消します
Azure Information Protection のサブスクリプションをキャンセルすると、Azure Information Protection ではお客様のテナント キーの使用を停止します。操作を行う必要はありません。

## <a name="re-key-your-tenant-key"></a>テナント キーを再入力します
再入力は「キーをロールする」とも呼ばれます。 本当に必要でない限り、テナント キーは再入力しないでください。 Office 2010 など、以前のクライアントはキー変更を滑らかに処理するようには設計されていません。 このシナリオでは、グループ ポリシーまたは同等のメカニズムを使用し、コンピューターの Rights Management 状態を消去する必要があります。 ただし、場合によってはテナント キーの再入力を強制する正規のイベントがいくつかあります。 たとえば、

-   あなたの会社が&2; つ以上の会社に分かれました。 テナント キーを再入力すると、新しい会社はあなたの社員が公開する新しいコンテンツにアクセスできません。 以前のテナント キーのコピーがあれば、以前のコンテンツにアクセスできます。

-   テナント キーのマスター コピー (あなたが所有するコピー) の盗難が疑われています。

テナント キーを更新するには、[Microsoft サポートに連絡](../get-started/information-support.md#to-contact-microsoft-support)し、**Azure Information Protection テナント キーを更新する要求で Azure Information Protection サポート ケース**を開きます。 自分が Azure Information Protection テナントの管理者であることを証明する必要があります。また、このプロセスの確認には数日かかることを承知する必要があります。 Standard サポートの料金が適用されます。テナント キーの更新は無料のサポート サービスではありません。

テナント キーを再入力すると、新しいコンテンツは新しいテナント キーの利用により保護されます。 これは段階的に行われます。そのため、一定期間、一部の新しいコンテンツは引き続き以前のテナント キーで保護されます。 以前に保護されたコンテンツは以前のテナント キーで引き続き保護されます。 このシナリオをサポートするために、Azure Information Protection は以前のテナント キーを保有します。そのため、古いコンテンツのライセンスを発行できます。

## <a name="backup-and-recover-your-tenant-key"></a>テナント キーをバックアップ/復旧します
テナント キーのバックアップは Microsoft が行うため、ユーザーの操作は必要ありません。

## <a name="export-your-tenant-key"></a>テナント キーをエクスポートします
Azure Information Protection の構成およびテナント キーをエクスポートするには、次の&3; つの手順に従います。

### <a name="step-1-initiate-export"></a>手順 1:エクスポートを開始する

-   これを行うには、[Microsoft サポートに連絡](../get-started/information-support.md#to-contact-microsoft-support)し、**Azure Information Protection キーのエクスポートの要求で Azure Information Protection サポート ケース**を開きます。 自分が Azure Information Protection テナントの管理者であることを証明する必要があります。また、このプロセスの確認には数日かかることを承知する必要があります。 標準サポートの料金が適用されます。テナント キーのエクスポートは無料のサポート サービスではありません。

### <a name="step-2-wait-for-verification"></a>手順 2:検証が完了するまで待機する

-   Microsoft は Azure Information Protection テナント キーのリリース要求が正当であることを確認します。 このプロセスには、最大 3 週間を要することがあります。

### <a name="step-3-receive-key-instructions-from-css"></a>手順 3:CSS からキーの手順を受領する

-   Microsoft カスタマー サポート サービス (CSS) は、Azure Information Protection の構成およびテナント キーを、パスワードで保護されたファイル (拡張子 .tpd) として暗号化して送付します。 これにあたって、CSS はまずエクスポートを開始したユーザーにツールを電子メールで送信します。 このツールをコマンド プロンプトから次のように実行します。

    ```
    AadrmTpd.exe -createkey
    ```
    この結果、RSA キー ペアが生成され、公開キーおよび秘密キーが現在のフォルダーにファイルとして保存されます。 たとえば、**PublicKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt** と **PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt** のようになります。

    CSS からの電子メールに返信します。返信には名前が **PublicKey** で始まるファイルを添付します。 次に CSS は、TPD ファイルを、RSA キーで暗号化された .xml ファイルとして送信します。 AadrmTpd ツールを最初に実行したフォルダーにこのファイルをコピーし、名前が **PrivateKey** で始まるファイルと CSS から受け取ったこのファイルを使用して、AadrmTpd ツールをもう一度実行します。 たとえば、

    ```
    AadrmTpd.exe -key PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt -target TPD-77172C7B-8E21-48B7-9854-7A4CEAC474D0.xml
    ```
    このコマンドの出力は&2; つのファイルです。一方のファイルにはパスワードで保護された TPD のプレーンテキスト パスワードが含まれ、他方のファイルにはパスワードで保護された TPD 自体が含まれています。 AadrmTpd.exe -createkey コマンドを実行した場合、相互参照のため、どちらのファイルの GUID も公開キーおよび秘密キー ファイルと同じになります。

    -   Password-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt

    -   ExportedTPD-FA29D0FE-5049-4C8E-931B-96C6152B0441.xml

    これらのファイルをバックアップし、安全な場所に保存します。これにより、このテナント キーで保護されたコンテンツを継続して暗号化解除できるようになります。 また、AD RMS に移行する場合は、この TPD ファイル (名前が **ExportedTDP** で始まるファイル) を AD RMS サーバーにインポートできます。

### <a name="step-4-ongoing-protect-your-tenant-key"></a>手順 4:継続:テナント キーを保護する

-   テナント キーを受領したら、厳重に保護してください。だれかがそれにアクセスできる場合、そのキーを使用して保護されているすべてのドキュメントを暗号化解除できるからです。

    テナント キーをエクスポートする理由が、Azure Information Protection を使用しなくなったためである場合、ベスト プラクティスとして、直ちに Azure Information Protection テナントから Azure Rights Management サービスを非アクティブ化してください。 これは、テナント キーの受領後すぐに実行してください。この予防策によって、アクセスすべきでないだれかがテナント キーにアクセスした場合の影響を最小限にできます。 手順については、「[Azure Rights Management の使用停止と非アクティブ化](decommission-deactivate.md)」を参照してください。

## <a name="respond-to-a-breach"></a>侵害に反応します
違反対応プロセスがなければ、どれほど強固でも、セキュリティ システムは完全になりません。 あなたのテナント キーが盗まれた可能性があります。 たとえ十分に保護されていても、現在の HSM 技術、現在のキー長、アルゴリズムに脆弱性が見つかる可能性があります。

製品とサービスのセキュリティ インシデントに対応するためにマイクロソフトは専用のチームを置いています。 インシデントが認められる報告があった場合、至急、このチームは範囲、根本原因、軽減の調査にあたります。 このインシデントがあなたの資産に影響を与える場合、Microsoft は Azure Information Protection テナント管理者に電子メールで通知します。その場合、サブスクリプションで指定されたアドレスが使われます。

侵害がある場合、あなたまたはマイクロソフトがとれる最善策は侵害の範囲によって異なります。マイクロソフトはあなたと連携し、このプロセスを進めます。 次の表は一般的な状況と考えられる対応をいくつかまとめたものです。ただし、厳密な対応は調査中に明らかになった情報によって変わります。

|インシデントの説明|考えられる対応|
|------------------------|-------------------|
|テナント キーが漏れています。|テナント キーを再入力します。 この記事の「[テナント キーを再入力します](operations-microsoft-managed-tenant-key.md#re-key-your-tenant-key)」セクションを参照してください。|
|無許可の個人またはマルウェアがテナント キーを使用する権利を手に入れましたが、キー自体は漏えいしていません。|テナント キーを再入力してもここでは役に立ちません。根本原因の分析が必要です。 無許可の個人がアクセスを得た原因がプロセスまたはソフトウェアのバグにある場合、その状況は解決する必要があります。|
|RSA アルゴリズム、キーの長さ、ブルート フォース攻撃に見られる脆弱性がコンピューターで実現可能になります。|Microsoft は回復力のある新しいアルゴリズムまたは長いキーをサポートするように Azure Information Protection を更新し、すべてのお客様にテナント キーの更新を指示する必要があります。|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]




<!--HONumber=Jan17_HO4-->


