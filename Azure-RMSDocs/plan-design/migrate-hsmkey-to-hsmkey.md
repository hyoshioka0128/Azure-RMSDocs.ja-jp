---
title: "手順 2.&colon; HSM で保護されているキーから HSM で保護されているキーへの移行 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5bbf37e-f1bf-4010-a60f-37177c9e9b39
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7a9c8b531ec342e7d5daf0cbcacd6597a79e6a55
ms.openlocfilehash: 7b531ebba1923653cb37c70a02fa888a40e96528


---

# 手順 2. HSM で保護されているキーから HSM で保護されているキーへの移行

*適用対象: Active Directory Rights Management サービス、Azure Rights Management*


これらの手順は [AD RMS から Azure Rights Management への移行パス](migrate-from-ad-rms-to-azure-rms.md)の一部であり、AD RMS キーが HSM で保護されているときに HSM で保護されているテナント キーを持つ Azure Rights Management に移行する場合にのみ適用されます。 

選択した構成シナリオでない場合、[手順 2 に戻ってください。AD RMS から構成データをエクスポートし、それを Azure RMS にインポートし](migrate-from-ad-rms-phase1.md#step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-rms)、別の構成を選択します。

> [!NOTE]
> これらの手順は、AD RMS キーがモジュールで保護されていることを前提としています。 これは一般的なケースです。 AD RMS キーが OCS で保護されている場合は、次の手順を実行する前に [AskIPTeam@microsoft.com](mailto: askipteam@microsoft.com?subject=AD%20RMS%20migration%20with%20OCS-protected%20key) にお問い合わせください。

これは、HSM キーと AD RMS 構成を Azure RMS にインポートする 2 段階の手順で、結果はお客様が管理 (BYOK) する Azure RMS テナント キーです。

最初に Azure RMS に転送できるように HSM キーをパッケージ化し、次に構成データと共にインポートする必要があります。

## パート 1:Azure RMS に転送できるように HSM キーをパッケージ化します。

1.  「[Azure Rights Management テナント キーを計画して実装する](plan-implement-tenant-key.md)」の「[BYOK (Bring Your Own Key) の実装](plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key)」セクションの手順に従います。その際、「**テナント キーを生成して転送する – インターネット経由**」の手順を使用します。例外を次に示します。

    -   「 **テナント キーを生成する**」の手順を実行しないでください。それと同等のものが、既に AD RMS のデプロイメントから取得されています。 Thales のインストールから AD RMS サーバーで使用されるキーを識別し、移行中にこのキーを使用する必要があります。 Thales で暗号化されたキー ファイルの名前は通常、サーバー上のローカルな **key_(keyAppName)_(keyIdentifier)** です。

    -   「**Transfer your tenant key to Azure RMS (テナント キーの Azure RMS への転送)**」の手順を実行しないでください。この手順では Add-AadrmKey コマンドが使用されます。  代わりに、エクスポートされた信頼できる発行ドメインをアップロードするとき、Import-AadrmTpd コマンドを使用し、準備した HSM キーを転送します。

2.  インターネットに接続されているワークステーションでは、Windows PowerShell セッションで、Azure RMS サービスに再接続します。

これで、Azure RMS の HSM キーが準備されたので、HSM キー ファイルと AD RMS 構成データをインポートできます。

## パート 2:HSM キーと構成データを Azure RMS にインポートする

1.  インターネットに接続されたままのワークステーションと Windows PowerShell セッションで、最初にエクスポートした信頼された発行ドメイン (.xml) ファイルをアップロードします。 信頼された発行ドメインが複数あるために複数の .xml ファイルがある場合は、移行後にコンテンツを保護するために Azure RMS で使用する HSM キーに対応するエクスポートされた信頼された発行ドメインが含まれるファイルを選択します。 次のコマンドを使用します。

    ```
    Import-AadrmTpd -TpdFile <PathToTpdPackageFile> -ProtectionPassword -HsmKeyFile <PathToBYOKPackage> -Active $True -Verbose
    ```
    例: **Import -TpdFile E:\no_key_tpd_contosokey1.xml  -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $true -Verbose**

    プロンプトが表示されたら、前に指定したパスワードを入力し、この操作を実行することを確認します。

2.  コマンドが完了したら、信頼された発行ドメインをエクスポートして作成した他の各 .xml ファイルに対して手順 1 を繰り返します。 ただし、これらのファイルの場合は、Import コマンドを実行するときに **-Active** を **false** に設定します。  例: **Import -TpdFile E:\contosokey2.xml -HsmKeyFile E:\KeyTransferPackage-contosokey.byok -ProtectionPassword -Active $false -Verbose**

3.  [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) コマンドレットを使用して Azure RMS サービスから切断します。

    ```
    Disconnect-AadrmService
    ```

以上で「[手順 3. RMS テナントをアクティブ化する](migrate-from-ad-rms-phase1.md#step-3-activate-your-rms-tenant)」に進む準備が完了しました。




<!--HONumber=Jul16_HO3-->


