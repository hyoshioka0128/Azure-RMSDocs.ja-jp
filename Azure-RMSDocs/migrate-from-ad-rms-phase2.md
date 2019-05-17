---
title: AD RMS から Azure Information Protection への移行 - フェーズ 2
description: AD RMS から Azure Information Protection への移行のフェーズ 2 には、手順 4 から 6 が含まれます。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 05/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5a189695-40a6-4b36-afe6-0823c94993ef
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: dbbea622800561cb0a466f6dda90e9910f1c7db4
ms.sourcegitcommit: 3e948723644f19c935bc7111dec1cc54a1ff0231
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2019
ms.locfileid: "65781861"
---
# <a name="migration-phase-2---server-side-configuration-for-ad-rms"></a>移行フェーズ 2 - AD RMS のサーバー側の構成

>*適用対象: Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

AD RMS から Azure Information Protection への移行フェーズ 2 では、次の情報を使用してください。 これらの手順では、「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」の手順 4 から手順 6 を説明します。


## <a name="step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection"></a>手順 4. AD RMS から構成データをエクスポートし、それを Azure Information Protection にインポートする
この手順は、2 段階の処理です。

1. 信頼された発行ドメイン (TPD) を .xml ファイルにエクスポートすることによって、AD RMS から構成データをエクスポートします。 このプロセスは、すべての移行について同じです。

2. 構成データを Azure Information Protection にインポートします。 現在の AD RMS のデプロイ構成と、Azure RMS テナント キーに対する優先トポロジに応じて、この手順のプロセスは異なります。

### <a name="export-the-configuration-data-from-ad-rms"></a>構成データを AD RMS からエクスポートする

すべての AD RMS クラスター上の、組織のコンテンツを保護していたすべての信頼された発行ドメインに対して、次の手順を実行します。 ライセンス専用クラスターでこの手順を実行する必要はありません。

#### <a name="to-export-the-configuration-data-trusted-publishing-domain-information"></a>構成データ (信頼された発行ドメインの情報) をエクスポートするには

1. AD RMS の管理権限を持つユーザーとして AD RMS クラスターにログオンします。

2. AD RMS 管理コンソール (**Active Directory Rights Management サービス**) から、AD RMS クラスター名を展開し、 **[信頼ポリシー]** を展開し、 **[信頼された発行ドメイン]** をクリックします。

3. 結果ウィンドウで信頼された発行ドメインを選択し、操作ウィンドウから **[信頼された発行ドメインのエクスポート]** をクリックします。

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

- NCipher ハードウェア セキュリティ モジュール (HSM) を使用した HSM 保護。

- NCipher 以外のサプライヤーからハードウェア セキュリティ モジュール (HSM) を使用した HSM 保護。

- 外部暗号プロバイダーを使用して保護されたパスワード。

> [!NOTE]
> AD RMS でのハードウェア セキュリティ モジュールの使用に関する詳細については、「 [AD RMS でのハードウェア セキュリティ モジュールの使用](https://technet.microsoft.com/library/jj651024.aspx)」を参照してください。

Azure Information Protection テナント キー トポロジには、テナント キーを Microsoft が管理するか (**マイクロソフト管理**) または Azure Key Vault でユーザーが自分で管理するか (**顧客管理**) の 2 つのオプションがあります。 独自の Azure Information Protection テナント キーを管理する場合は、“Bring Your Own Key” (BYOK) と呼ばれることもあります。 詳細については、「[Azure Information Protection テナント キーを計画して実装する](plan-implement-tenant-key.md)」を参照してください。

次の表を参考にして、移行に使用する手順を識別してください。 

|現在の AD RMS のデプロイ|選択した Azure Information Protection テナント キーのトポロジ|移行手順|
|-----------------------------|----------------------------------------|--------------------------|
|AD RMS データベースでのパスワード保護|マイクロソフト管理|後で説明される「**ソフトウェアで保護されたキーからソフトウェアで保護されたキーへの移行**」の手順を参照してください。<br /><br />これは最も簡単な移行パスであり、Azure Information Protection に構成データを転送するだけで済みます。|
|NCipher nShield ハードウェア セキュリティ モジュール (HSM) を使用した HSM 保護 |お客様が管理 (BYOK)|後で説明される「**HSM で保護されたキーから HSM で保護されたキーへの移行**」の手順を参照してください。<br /><br />Azure Key Vault の BYOK ツールセットが必要であり、3 つの一連の手順を実行する必要があります。最初にオンプレミスの HSM から Azure Key Vault の HSM にキーを転送し、次に Azure Information Protection からの Azure Rights Management サービスがテナント キーを使用するのを承認し、最後に構成データを Azure Information Protection に転送します。|
|AD RMS データベースでのパスワード保護|お客様が管理 (BYOK)|後で説明される「**ソフトウェアで保護されたキーから HSM で保護されたキー**への移行」の手順を参照してください。<br /><br />Azure Key Vault の BYOK ツールセットが必要であり、一連の 4 つの手順を実行する必要があります。最初にソフトウェア キーを抽出してオンプレミスの HSM にインポートし、次にオンプレミスの HSM から Azure Information Protection HSM にキーを転送し、さらに Key Vault データを Azure Information Protection に転送して、最後に構成データを Azure Information Protection に転送します。|
|NCipher 以外のサプライヤーからハードウェア セキュリティ モジュール (HSM) を使用した HSM 保護 |お客様が管理 (BYOK)|NCipher nShield ハードウェア セキュリティ モジュール (HSM) に、この HSM からキーを転送する方法を手順については、hsm 業者に連絡します。 後で説明される「**HSM で保護されたキーから HSM で保護されたキー**への移行」の手順に従います。|
|外部暗号プロバイダーを使用して保護されたパスワード|お客様が管理 (BYOK)|NCipher nShield ハードウェア セキュリティ モジュール (HSM) に、キーを転送する方法を手順については、暗号化サービス プロバイダーの業者に連絡します。 後で説明される「**HSM で保護されたキーから HSM で保護されたキー**への移行」の手順に従います。|

エクスポートできない HSM で保護されたキーがある場合でも、読み取り専用モード用に AD RMS クラスターを構成することで、Azure Information Protection に移行できます。 このモードでは、以前に保護されたコンテンツを引き続き開くことはできますが、新たに保護されたコンテンツでは、ユーザー (BYOK) または Microsoft によって管理されている新しいテナント キーが使用されます。 詳細については、「[AD RMS から Azure RMS への移行がサポートされている Office の更新プログラムが利用可能になりました](https://support.microsoft.com/help/4023955/an-update-is-available-for-office-to-support-migrations-from-ad-rms-to)」を参照してください。

これらのキーの移行手順を開始する前に、信頼された発行ドメインをエクスポートしたときに作成した .xml ファイルにアクセスできることを確認します。 たとえば、これらは AD RMS サーバーからインターネットに接続されたワークステーションに移動する USB ドライブに保存されている可能性があります。

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
    
        Enable-Aadrm

**Azure Information Protection テナントが既にアクティブになっている場合はどうすればよいですか。** Azure Rights Management サービスが組織で既にアクティブ化されていて、移行後に使用するカスタム テンプレートを作成済みである場合は、そのテンプレートをエクスポートしてからインポートする必要があります。 これについては次の手順で説明します。 

## <a name="step-6-configure-imported-templates"></a>手順 6. インポートされたテンプレートを構成する

インポートしたテンプレートは **アーカイブ済み**という既定の状態なので、ユーザーが Azure Rights Management サービスでこれらのテンプレートを使用できるようにする場合は、この状態を **公開済み** に変更する必要があります。

AD RMS からインポートしたテンプレートの外観と動作は、Azure Portal で作成するカスタム テンプレートと同じです。 インポートしたテンプレートを公開に変更し、ユーザーがアプリケーションからそれらを表示して選択できるようにする方法は、「[Azure Information Protection のテンプレートを構成して管理する](./configure-policy-templates.md)」を参照してください。

新しくインポートしたテンプレートを公開するだけでなく、移行を続ける前に行う必要があるテンプレートの重要な変更が 2 つあります。 移行プロセス中のユーザーに対するエクスペリエンスを一貫したものにするため、インポートしたテンプレートに変更を加えないでください。また、Azure Information Protection に付属する 2 つの既定のテンプレートを公開したり、この時点で新しいテンプレートを作成したりしないでください。 代わりに、移行プロセスが完了するまで待ち、AD RMS サーバーをプロビジョニング解除します。

この手順で必要な場合があるテンプレートの変更:

- 移行前に Azure Information Protection カスタム テンプレートを作成した場合は、手動でエクスポートしてインポートする必要があります。

- AD RMS のテンプレートで **ANYONE** グループが使用されていた場合、ユーザーまたはグループを手動で追加することが必要になる場合があります。 
    
    AD RMS では、ANYONE グループはオンプレミスの Active Directory によって認証されたすべてのユーザーに権限を付与します。また、このグループは Azure Information Protection ではサポートされていません。 最も近いのは、Azure AD テナント内のすべてのユーザーに対して自動的に作成されるグループです。 AD RMS テンプレートに対して ANYONE グループを使用していた場合、ユーザーおよびそのユーザーに付与したい権限を追加することが必要になる場合があります。

### <a name="procedure-if-you-created-custom-templates-before-the-migration"></a>移行前にカスタム テンプレートを作成した場合の手順

Azure Rights Management サービスをアクティブ化する前でも後でも、移行前にカスタム テンプレートを作成した場合は、**公開済み**に設定してあっても、移行後にユーザーはテンプレートを使用できません。 ユーザーが使用できるようにするには、最初に次のようにする必要があります。 

1. [Get-AadrmTemplate](/powershell/aadrm/vlatest/get-aadrmtemplate) を実行して、そのようなテンプレートを識別し、テンプレート ID を記録しておきます。 

2. Azure RMS PowerShell コマンドレット [Export-AadrmTemplate](/powershell/aadrm/vlatest/export-aadrmtemplate) を使用して、テンプレートをエクスポートします。

3. Azure RMS PowerShell コマンドレット [Import-AadrmTemplate](/powershell/module/aadrm/import-aadrmtemplate) を使用して、テンプレートをインポートします。

その後は、移行後に作成した他のテンプレートと同様に、これらのテンプレートを発行したりアーカイブしたりできます。

### <a name="procedure-if-your-templates-in-ad-rms-used-the-anyone-group"></a>AD RMS のテンプレートが **ANYONE** グループを使用していた場合の手順

AD RMS のテンプレートで **ANYONE** グループが使用されていた場合、Azure Information Protection 内の最も近いグループは **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@\<tenant_name>.onmicrosoft.com** という名前です。 たとえば、Contoso の場合、このグループは <strong>AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@contoso.onmicrosoft.com</strong> のようになります。 このグループは、Azure AD テナントからのすべてのユーザーを含んでいます。

Azure Portal でテンプレートとラベルを管理する場合、このグループは、Azure AD でのテナントのドメイン名として表示されます。 たとえば、Contoso の場合、このグループは **contoso.onmicrosoft.com** のようになります。 このグループを追加するために、オプションの表示は [**追加\<組織名> - すべてのメンバー**] となります。

AD RMS テンプレートに ANYONE グループが含まれるかどうかわからない場合は、次のサンプルの Windows PowerShell スクリプトを使用してこれらのテンプレートを識別できます。 AD RMS での Windows PowerShell の使用に関する詳細については、「[Using Windows PowerShell to Administer AD RMS ](https://technet.microsoft.com/library/ee221079%28v=ws.10%29.aspx)」 (Windows PowerShell を使用した AD RMS の管理) を参照してください。

Azure Portal でテンプレートをラベルに変換すると、外部ユーザーをそれらのテンプレートに容易に追加できます。 次に、**[アクセス許可の追加]** ブレードで、**[詳細を入力]** を選択して、対象のユーザーのメール アドレスを手動で指定します。 

この構成の詳細については、「[Rights Management による保護を適用するようにラベルを構成する方法](./configure-policy-protection.md)」を参照してください。

#### <a name="sample-windows-powershell-script-to-identify-ad-rms-templates-that-include-the-anyone-group"></a>ANYONE グループを含む AD RMS テンプレートを識別するためのサンプル Windows PowerShell スクリプト
このセクションに含まれるサンプル スクリプトを使用すると、前のセクションで説明したように、ANYONE グループが定義されている AD RMS テンプレートを識別できます。

**免責事項:** このサンプル スクリプトは、Microsoft の標準サポート プログラムまたはサービスでサポートされていません。 このサンプル スクリプトは、どのような種類の保証も伴わずそのままの状態で提供されます。

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


## <a name="next-steps"></a>次の手順
「[フェーズ 3 - クライアント側の構成](migrate-from-ad-rms-phase3.md)」に進みます。
