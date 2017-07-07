---
title: "AD RMS から Azure Information Protection への移行 - フェーズ 2"
description: "AD RMS から Azure Information Protection への移行のフェーズ 2 には、手順 4 から 6 が含まれます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/18/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5a189695-40a6-4b36-afe6-0823c94993ef
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 7fb7beccf2f9fdf788f13e76796702ff64bffbbc
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2017
---
# <a name="migration-phase-2---server-side-configuration-for-ad-rms"></a>移行フェーズ 2 - AD RMS のサーバー側の構成

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Office 365*

AD RMS から Azure Information Protection への移行フェーズ 2 では、次の情報を使用してください。 これらの手順では、「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」の手順 4 から手順 6 を説明します。


## <a name="step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection"></a>手順 4. AD RMS から構成データをエクスポートし、それを Azure Information Protection にインポートする
この手順は、2 段階の処理です。

1. 信頼された発行ドメイン (TPD) を .xml ファイルにエクスポートすることによって、AD RMS から構成データをエクスポートします。 このプロセスは、すべての移行について同じです。

2. 構成データを Azure Information Protection にインポートします。 現在の AD RMS のデプロイ構成と、Azure RMS テナント キーに対する優先トポロジに応じて、この手順のプロセスは異なります。

### <a name="export-the-configuration-data-from-ad-rms"></a>構成データを AD RMS からエクスポートする

すべての AD RMS クラスター上の、組織のコンテンツを保護していたすべての信頼された発行ドメインに対して、次の手順を実行します。 ライセンス専用クラスターでこれを実行する必要はありません。

#### <a name="to-export-the-configuration-data-trusted-publishing-domain-information"></a>構成データ (信頼された発行ドメインの情報) をエクスポートするには

1. AD RMS の管理権限を持つユーザーとして AD RMS クラスターにログオンします。

2. AD RMS 管理コンソール (**Active Directory Rights Management サービス**) から、AD RMS クラスター名を展開し、 **[信頼ポリシー]**を展開し、 **[信頼された発行ドメイン]**をクリックします。

3. 結果ウィンドウで信頼された発行ドメインを選択し、操作ウィンドウから [ **信頼された発行ドメインのエクスポート**] をクリックします。

4. **[信頼された発行ドメインのエクスポート]** ダイアログ ボックスで:

    - **[名前を付けて保存]** をクリックし、パスとファイル名を指定して保存します。 ファイル名の拡張子としては必ず **.xml** を指定します (自動的には付加されません)。

    - 強いパスワードを指定して確認します。 このパスワードを覚えておいてください。後で、構成データを Azure Information Protection にインポートするときに必要になります。

    - 信頼されたドメイン ファイルを RMS バージョン 1.0 で保存するチェック ボックスをオンにしないでください。

信頼された発行ドメインをすべてエクスポートしたら、このデータを Azure Information Protection にインポートする手順を開始できます。

信頼された発行ドメインには、保護済みのファイルの暗号化を解除するサーバー ライセンス証明書 (SLC) キーが含まれているため、現在アクティブな信頼された発行ドメインだけではなく、すべての信頼された発行ドメインをエクスポートすること (そして後で Azure にインポートすること) が重要です。

たとえば、暗号化モード 1 から暗号化モード 2 に AD RMS サーバーをアップグレードする場合、信頼された発行ドメインが複数になります。 移行の最後に、暗号化モード 1 を使用してアーカイブされたキーを含む信頼された発行ドメインをエクスポートおよびインポートしない場合、ユーザーは暗号化モード 1 キーで保護されていたコンテンツを開けなくなります。


### <a name="import-the-configuration-data-to-azure-information-protection"></a>構成データを Azure Information Protection にインポートする
正確な手順は、現在の AD RMS のデプロイ構成と、Azure Information Protection テナント キーの優先トポロジによって異なります。

現在の AD RMS のデプロイでは、次のいずれかの構成をサーバー ライセンス証明書 (SLC) キーに使用します。

- AD RMS データベースでのパスワード保護。 これが既定の構成です。

- Thales ハードウェア セキュリティ モジュール (HSM) を使用する HSM 保護。

- Thales 以外のサプライヤーのハードウェア セキュリティ モジュール (HSM) を使用した HSM 保護。

- 外部暗号プロバイダーを使用して保護されたパスワード。

> [!NOTE]
> AD RMS でのハードウェア セキュリティ モジュールの使用に関する詳細については、「 [AD RMS でのハードウェア セキュリティ モジュールの使用](http://technet.microsoft.com/library/jj651024.aspx)」を参照してください。

Azure Information Protection テナント キー トポロジには、テナント キーを Microsoft が管理するか (**マイクロソフト管理**) または Azure Key Vault でユーザーが自分で管理するか (**顧客管理**) の 2 つのオプションがあります。 顧客管理の Azure Information Protection テナント キーは、“Bring Your Own Key” (BYOK) と呼ばれることもあり、Thales のハードウェア セキュリティ モジュール (HSM) が必要です。 詳細については、「[Azure Information Protection テナント キーを計画して実装する](plan-implement-tenant-key.md)」を参照してください。

> [!IMPORTANT]
> 現在、Exchange Online は Azure Information Protection の BYOK と互換性がありません。 移行後に BYOK を使用し、Exchange Online を使用する場合は、この構成により Exchange Online の IRM 機能が制限されることを理解しておきます。 「[BYOK の料金と制限事項](byok-price-restrictions.md)」の情報は、移行に最適な Azure Information Protection テナント キー トポロジの選択に役立ちます。

次の表を参考にして、移行に使用する手順を識別してください。 記載されていない組み合わせはサポートされません。

|現在の AD RMS のデプロイ|選択した Azure Information Protection テナント キーのトポロジ|移行手順|
|-----------------------------|----------------------------------------|--------------------------|
|AD RMS データベースでのパスワード保護|マイクロソフト管理|後で説明される「**ソフトウェアで保護されたキーからソフトウェアで保護されたキーへの移行**」の手順を参照してください。<br /><br />これは最も簡単な移行パスであり、Azure Information Protection に構成データを転送するだけで済みます。|
|Thales nShield ハードウェア セキュリティ モジュール (HSM) を使用する HSM 保護|お客様が管理 (BYOK)|後で説明される「**HSM で保護されたキーから HSM で保護されたキーへの移行**」の手順を参照してください。<br /><br />Azure Key Vault の BYOK ツールセットが必要であり、3 つの一連の手順を実行する必要があります。最初にオンプレミスの HSM から Azure Key Vault の HSM にキーを転送し、次に Azure Information Protection からの Azure Rights Management サービスがテナント キーを使用するのを承認し、最後に構成データを Azure Information Protection に転送します。|
|AD RMS データベースでのパスワード保護|お客様が管理 (BYOK)|後で説明される「**ソフトウェアで保護されたキーから HSM で保護されたキー**への移行」の手順を参照してください。<br /><br />Azure Key Vault の BYOK ツールセットが必要であり、一連の 4 つの手順を実行する必要があります。最初にソフトウェア キーを抽出してオンプレミスの HSM にインポートし、次にオンプレミスの HSM から Azure Information Protection HSM にキーを転送し、さらに Key Vault データを Azure Information Protection に転送して、最後に構成データを Azure Information Protection に転送します。|
|Thales 以外のサプライヤーのハードウェア セキュリティ モジュール (HSM) を使用した HSM 保護|お客様が管理 (BYOK)|この HSM から Thales nShield ハードウェア セキュリティ モジュール (HSM) にキーを転送する方法については、HSM のサプライヤーに問い合わせてください。 後で説明される「**HSM で保護されたキーから HSM で保護されたキー**への移行」の手順に従います。|
|外部暗号プロバイダーを使用して保護されたパスワード|お客様が管理 (BYOK)|Thales nShield ハードウェア セキュリティ モジュール (HSM) にキーを転送する方法については、暗号プロバイダーのサプライヤーに問い合わせてください。 後で説明される「**HSM で保護されたキーから HSM で保護されたキー**への移行」の手順に従います。|
これらの手順を開始する前に、信頼された発行ドメインをエクスポートしたときに作成した .xml ファイルにアクセスできることを確認します。 たとえば、これらは AD RMS サーバーからインターネットに接続されたワークステーションに移動する USB ドライブに保存されている可能性があります。

> [!NOTE]
> ただし、このデータは秘密キーを含むので、これらのファイルを保存し、セキュリティのベスト プラクティスを使用して保護します。

手順 4 を完了するには、移行パスに応じた手順を選択します。 

- [ソフトウェアで保護されているキーからソフトウェアで保護されているキーへ](migrate-softwarekey-to-softwarekey.md)
- [HSM で保護されているキーから HSM で保護されているキーへ](migrate-hsmkey-to-hsmkey.md)
- [ソフトウェアで保護されているキーから HSM で保護されているキーへ](migrate-softwarekey-to-hsmkey.md)

## <a name="step-5-activate-the-azure-rights-management-service"></a>手順 5. Azure Rights Management サービスをアクティブにする

PowerShell セッションを開き、次のコマンドを実行します。

1. Azure Rights Management サービスに接続し、メッセージが表示されたら、グローバル管理者の資格情報を指定します。
    
        Connect-Aadrmservice

2. Azure Rights Management サービスをアクティブにします。
    
        Enable-Aadrmservice

**Azure Information Protection テナントが既にアクティブになっている場合はどうすればよいですか。** 組織の Azure Rights Management サービスが既にアクティブ化されている場合は、ユーザーが既に Azure Information Protection を使用してコンテンツを保護し、AD RMS の既存のキー (およびテンプレート) ではなく、自動的に生成されたテナント キー (および既定のテンプレート) を使用している可能性があります。 これは、イントラネット上で適切に管理されたコンピューターではほとんど起こりません。AD RMS インフラストラクチャ用に自動的に構成されるためです。 ただし、イントラネットへの接続の頻度が低いワークグループのコンピューターでは発生する可能性があります。 残念ながら、このようなコンピューターの識別は困難です。そのため、AD RMS から構成データをインポートする前に、サービスをアクティブ化しないようにお勧めします。

Azure Information Protection テナントが既にアクティブ化されていて、前述のようなコンピューターを識別できる場合は、[手順 7](migrate-from-ad-rms-phase3.md#step-7-reconfigure-clients-to-use-azure-information-protection) の説明に従って、それらのコンピューターで CleanUpRMS.cmd スクリプトを実行します。 このスクリプトを実行すると、それらのコンピューターで強制的にユーザーの環境が再初期化されるため、更新されたテナント キーとインポートされたテンプレートがダウンロードされます。

さらに、移行後に使用するカスタム テンプレートを作成した場合は、それをエクスポートしてインポートする必要があります。 これについては次の手順で説明します。 

## <a name="step-6-configure-imported-templates"></a>手順 6. インポートされたテンプレートを構成する

インポートしたテンプレートは **アーカイブ済み**という既定の状態なので、ユーザーが Azure Rights Management サービスでこれらのテンプレートを使用できるようにする場合は、この状態を **公開済み** に変更する必要があります。

AD RMS からインポートしたテンプレートの外観と動作は、Azure クラシック ポータルで作成するカスタム テンプレートと同じです。 インポートしたテンプレートを公開に変更し、ユーザーがアプリケーションからそれらを表示して選択できるようにする方法は、「[Azure Rights Management のカスタム テンプレートを構成する](../deploy-use/configure-custom-templates.md)」を参照してください。

新しくインポートしたテンプレートを公開するだけでなく、移行を続ける前に行う必要があるテンプレートの重要な変更が 2 つあります。 移行プロセス中のユーザーに対するエクスペリエンスを一貫したものにするため、インポートしたテンプレートに変更を加えないでください。また、Azure Information Protection に付属する 2 つの既定のテンプレートを公開したり、この時点で新しいテンプレートを作成したりしないでください。 代わりに、移行プロセスが完了するまで待ち、AD RMS サーバーをプロビジョニング解除します。

この手順で必要な場合があるテンプレートの変更:

- 移行前に Azure Information Protection カスタム テンプレートを作成した場合は、手動でエクスポートしてインポートする必要があります。

- AD RMS のテンプレートが **ANYONE** グループを使用していた場合は、同等のグループと権限を手動で追加する必要があります。

### <a name="procedure-if-you-created-custom-templates-before-the-migration"></a>移行前にカスタム テンプレートを作成した場合の手順

Azure Rights Management サービスをアクティブ化する前でも後でも、移行前にカスタム テンプレートを作成した場合は、**公開済み**に設定してあっても、移行後にユーザーはテンプレートを使用できません。 ユーザーが使用できるようにするには、最初に次のようにする必要があります。 

1. [Get-AadrmTemplate](/powershell/aadrm/vlatest/get-aadrmtemplate) を実行して、そのようなテンプレートを識別し、テンプレート ID を記録しておきます。 

2. Azure RMS PowerShell コマンドレット [Export-AadrmTemplate](/powershell/aadrm/vlatest/export-aadrmtemplate) を使用して、テンプレートをエクスポートします。

3. Azure RMS PowerShell コマンドレット [Import-AadrmTemplate](/powershell/aadrm/vlatest/Import-AadrmTpd) を使用して、テンプレートをインポートします。

その後は、移行後に作成した他のテンプレートと同様に、これらのテンプレートを発行したりアーカイブしたりできます。

### <a name="procedure-if-your-templates-in-ad-rms-used-the-anyone-group"></a>AD RMS のテンプレートが **ANYONE** グループを使用していた場合の手順

AD RMS のテンプレートが **ANYONE** グループを使用していた場合、テンプレートを Azure Information Protection にインポートすると、このグループは自動的に削除されます。同等のグループまたはユーザーおよび同じ権限を、インポートされたテンプレートに手動で追加する必要があります。 Azure Information Protection 用の同等グループの名前は **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@\<テナント名>.onmicrosoft.com** です。 たとえば、Contoso の場合、このグループは **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@contoso.onmicrosoft.com** のようになります。

AD RMS テンプレートに ANYONE グループが含まれるかどうかわからない場合は、次のサンプルの Windows PowerShell スクリプトを使用してこれらのテンプレートを識別できます。 AD RMS での Windows PowerShell の使用に関する詳細については、「[Using Windows PowerShell to Administer AD RMS (Windows PowerShell を使用した AD RMS の管理)](https://technet.microsoft.com/library/ee221079%28v=ws.10%29.aspx)」を参照してください。

Azure クラシック ポータルの既定の権限ポリシー テンプレートの 1 つをコピーした場合、組織の自動作成されたグループが表示され、その後 **[権限]** ページで **[ユーザー名]** を特定できます。 ただし、手動で作成またはインポートしたテンプレートに Azure クラシック ポータルを使用してこのグループを追加することはできないため、代わりに次の Azure RMS PowerShell オプションのいずれかを使用する必要があります。

- [New-AadrmRightsDefinition](/powershell/aadrm/vlatest/new-aadrmrightsdefinition) PowerShell コマンドレットを使用して、"AllStaff" グループおよび権限を権限定義オブジェクトとして定義し、ANYONE グループに加えて元のテンプレートで既に権限を付与されていた他の各グループまたはユーザーに対してこのコマンドを再度実行します。 その後、[Set-AadrmTemplateProperty](/powershell/aadrm/vlatest/set-aadrmtemplateproperty) コマンドレットを使用して、これらの権限定義オブジェクトをテンプレートに追加します。

- [Export-AadrmTemplate](/powershell/aadrm/vlatest/export-aadrmtemplate) コマンドレットを使用して、テンプレートを .XML ファイルにエクスポートします。このファイルを編集して、"AllStaff" グループおよび権限を既存のグループおよび権限に追加してから、[Import-AadrmTemplate](/powershell/aadrm/vlatest/import-aadrmtemplate) コマンドレットを使用してこの変更を Azure Information Protection にインポートします。

> [!NOTE]
> この同等グループ "AllStaff" は、AD RMS の ANYONE グループとまったく同じではありません。"AllStaff" グループには、Azure テナントのすべてのユーザーが含まれます。一方、ANYONE グループには、認証されたすべてのユーザーが含まれ、組織外のユーザーが含まれる場合があります。
> 
> こうしうた 2 つのグループの違いにより、"AllStaff" グループだけでなく外部ユーザーも追加しなければならない場合があります。 グループの外部の電子メール アドレスは、現在サポートされていません。


#### <a name="sample-windows-powershell-script-to-identify-ad-rms-templates-that-include-the-anyone-group"></a>ANYONE グループを含む AD RMS テンプレートを識別するためのサンプル Windows PowerShell スクリプト
このセクションに含まれるサンプル スクリプトを使用すると、前のセクションで説明したように、ANYONE グループが定義されている AD RMS テンプレートを識別できます。

**免責事項:** このサンプル スクリプトは、Microsoft の標準サポート プログラムまたはサービスではサポートされません。 このサンプル スクリプトは、どのような種類の保証も伴わずそのままの状態で提供されます。

```
import-module adrmsadmin 

New-PSDrive -Name MyRmsAdmin -PsProvider AdRmsAdmin -Root https://localhost -Force 

$ListofTemplates=dir MyRmsAdmin:\RightsPolicyTemplate

foreach($Template in $ListofTemplates) 
{ 
                $templateID=$Template.id

                $rights = dir MyRmsAdmin:\RightsPolicyTemplate\$Templateid\userright

     $templateName=$Template.DefaultDisplayName 

        if ($rights.usergroupname -eq "anyone")

                         {
                           $templateName = $Template.defaultdisplayname

                           write-host "Template " -NoNewline

                           write-host -NoNewline $templateName -ForegroundColor Red

                           write-host " contains rights for " -NoNewline

                           write-host ANYONE  -ForegroundColor Red
                         }
 } 
Remove-PSDrive MyRmsAdmin -force
```


## <a name="next-steps"></a>次のステップ
「[フェーズ 3 - クライアント側の構成](migrate-from-ad-rms-phase2.md)」に進みます。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]