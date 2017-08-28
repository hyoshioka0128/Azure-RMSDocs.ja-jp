---
title: "AD RMS から Azure Information Protection への移行 - フェーズ 3"
description: "AD RMS から Azure Information Protection への移行のフェーズ 3 には、手順 7 が含まれます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/22/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 35bd2d176cb71c54a489d4f4b8faca4d668a7867
ms.sourcegitcommit: c960f1d2140dea11e54cbeb37d53d1512621d90c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2017
---
# <a name="migration-phase-3---client-side-configuration"></a>移行フェーズ 3 - クライアント側の構成

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Office 365*

AD RMS から Azure Information Protection への移行フェーズ 3 では、次の情報を使用してください。 これらの手順では、「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」の手順 7 を説明します。

## <a name="step-7-reconfigure-clients-to-use-azure-information-protection"></a>手順 7. Azure Information Protection を使用するようにクライアントを再構成する

モバイル デバイス クライアントおよび Mac コンピューターの場合:

- [AD RMS モバイル デバイス拡張機能](http://technet.microsoft.com/library/dn673574.aspx)をデプロイするときに作成した DNS SRV レコードを削除します。

Windows クライアントの場合:

- 次の移行スクリプトを使って AD RMS クライアントを再構成します。 これらのスクリプトは、AD RMS ではなく Azure Rights Management サービスを使うように Windows コンピューター上の構成をリセットします。 
    
    **CleanUpRMS.cmd**
    
    - AD RMS クライアントが構成を格納するために使っていたすべてのフォルダーとレジストリ キーの内容を削除します。 この情報には、クライアントの AD RMS クラスターの場所が含まれます。
    
    **MigrateClient.cmd**
    
    - Azure Rights Management サービス用にユーザー環境 (ブートストラップ) を初期化するようクライアントを構成します。
    
    - Azure Rights Management サービスに接続して AD RMS クラスターによって保護されているコンテンツの使用ライセンスを取得するようクライアントを構成します。 

すべての Windows クライアントを一度に移行できない場合は、クライアントのバッチ処理のための次の手順を実行します。 バッチで移行する Windows コンピューターを使用しているユーザーごとに、前に作成した **AIPMigrated** グループにユーザーを追加します。

### <a name="windows-client-reconfiguration-by-using-registry-edits"></a>レジストリの編集を使用する Windows クライアントの再構成

1. 前に抽出した移行スクリプト **CleanUpRMS.cmd** および **MigrateClient.cmd** に戻ります。

2.  **MigrateClient.cmd** の指示に従ってスクリプトを修正し、テナントの Azure Rights Management サービスの URL と、AD RMS クラスターのエクストラネット ライセンス URL およびイントラネット ライセンス URL のサーバー名を追加します。

    > [!IMPORTANT]
    > 前と同様に、アドレスの前後に余分なスペースが挿入されないように注意してください。
    > 
    > さらに、AD RMS サーバーが SSL/TLS サーバー証明書を使用している場合は、ライセンス URL の文字列にポート番号 **443** が含まれることを確認します。 たとえば、https:// rms.treyresearch.net:443/_wmcs/licensing となっている必要があります。 この情報は、Active Directory Rights Management サービス コンソールでクラスター名をクリックして、**[クラスターの詳細]** で確認できます。 ポート番号 443 が URL に含まれる場合は、スクリプトを変更するときにこの値を含めます。 たとえば、https://rms.treyresearch.net:**443** などとします。 

    *&lt;YourTenantURL&gt;* の Azure Rights Management サービス URL を取得する必要がある場合は、前の「[Azure Rights Management サービス URL を識別するには](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url)」をご覧ください。

3.  **AIPMigrated** グループのメンバーによって使われている Windows クライアント コンピューターで、**CleanUpRMS.cmd** および **MigrateClient.cmd** を実行します。 たとえば、これらのスクリプトを実行するグループ ポリシー オブジェクトを作成し、このユーザー グループに割り当てます。

## <a name="next-steps"></a>次のステップ
移行を続行するには、「[移行フェーズ 4 - サービス構成のサポート](migrate-from-ad-rms-phase3.md)」に進んでください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]