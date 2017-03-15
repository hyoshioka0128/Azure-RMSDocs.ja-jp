---
title: "Azure Information Protection クライアントで PowerShell を使用する"
description: "管理者が PowerShell を使って Azure Information Protection クライアントを管理するための手順と情報について説明します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/09/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4f9d2db7-ef27-47e6-b2a8-d6c039662d3c
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 13bed15fa5fff020d77a4362e38903c5ca55d2ce
ms.sourcegitcommit: cbdbabd626fa5b91c418d84cd6228c9ca94a2525
translationtype: HT
---
# <a name="using-powershell-with-the-azure-information-protection-client"></a>Azure Information Protection クライアントでの PowerShell の使用

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*

Azure Information Protection クライアントをインストールすると、PowerShell コマンドが自動的にインストールされ、自動化するスクリプトを作成できるコマンドを実行してクライアントを管理できます。

コマンドレットは PowerShell モジュール **AzureInformationProtection** でインストールされます。このモジュールは、RMS 保護ツールでインストールされていた RMSProtection モジュールに代わるものです。 RMSProtection ツールがインストールされているシステムに Azure Information Protection クライアントをインストールすると、RMSProtection モジュールは自動的にアンインストールされます。

AzureInformationProtection モジュールには、RMS 保護ツールのすべての Rights Management コマンドレットに加えて、ラベル付け用に Azure Information Protection (AIP) サービスを使う&2; つの新しいコマンドレットが含まれます。

|ラベル付けコマンドレット|使用例|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/azureinformationprotection/vlatest/get-aipfilestatus)|共有フォルダーで、すべてのファイルを特定のラベルで識別します。|
|[Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel)|共有フォルダーで、ラベルが付いていないすべてのファイルに指定したラベルを適用します。|

すべてのコマンドレットと対応するヘルプの一覧については、「[AzureInformationProtection Module](/powershell/azureinformationprotection/vlatest/aip)」 (AzureInformationProtection モジュール) を参照してください。

このモジュールは、**\ProgramFiles (x86)\Microsoft Azure Information Protection** にインストールされ、このフォルダーを **PSModulePath** システム変数に追加します。 このモジュールの .dll の名前は **AIP.dll** です。

RMSProtection モジュールと同様に、AzureInformationProtection モジュールの現在のリリースには以下の制限があります。

- Outlook 個人フォルダー (.pst ファイル) の保護を解除することはできますが、現在は、この PowerShell モジュールを使ってこれらのファイルまたは他のコンテナー ファイルをネイティブに保護することはできません。

- Outlook 個人フォルダー (.pst) 内にある Outlook で保護されたメール メッセージ (.rpmsg ファイル) の保護を解除することはできますが、個人フォルダーの外にある .rpmsg ファイルの保護を解除することはできません。

これらのコマンドレットを使い始める前に、デプロイに対応する追加の前提条件と手順を参照してください。

- [Azure Information Protection サービスと Azure Rights Management サービス](#azure-information-protection-service-and-azure-rights-management-service)

    - 分類のみ、または Rights Management 保護で分類を使っている場合に適用: Azure Information Protection を含むサブスクリプションがある場合 (例: Enterprise Mobility + Security)。
    - Azure Rights Management サービスで保護のみを使っている場合に適用: Azure Rights Management サービスを含むサブスクリプションがある場合 (例: Office 365 E3、Office 365 E5)。

- [Active Directory Rights Management サービス](#active-directory-rights-management-services)

    - オンプレミス バージョンの Azure Rights Management で保護のみを使っている場合に適用: Active Directory Rights Management サービス (AD RMS)。


## <a name="azure-information-protection-service-and-azure-rights-management-service"></a>Azure Information Protection サービスと Azure Rights Management サービス

組織が Azure Information Protection と Azure Rights Management のデータ保護サービスを使っている場合、または Azure Rights Management サービスだけを使っている場合は、PowerShell を使い始める前にこのセクションをお読みください。


### <a name="prerequisites-for-aip-and-azure-rms"></a>AIP と Azure RMS の前提条件

AzureInformationProtection モジュールのインストールに関する前提条件に加えて、Azure Information Protection サービスおよび Azure Rights Management データ保護サービスに関する追加の前提条件があります。

1. Azure Rights Management サービスをアクティブ化する必要があります。

2. 自分のアカウントを使って他のユーザーのファイルから保護を削除するには: 組織のスーパー ユーザー機能を有効にし、自分のアカウントを Azure Rights Management のスーパー ユーザーとして構成する必要があります。

3. ユーザーの操作なしに直接ファイルを保護または保護解除するには: サービス プリンシパル アカウントを作成し、Set-RMSServerAuthentication を実行して、このサービス プリンシパルを Azure Rights Management のスーパー ユーザーにします。

4. 北米以外のリージョンの場合: サービスに対する認証のレジストリを編集します。

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>前提条件 1: Azure Rights Management サービスをアクティブ化する必要がある

この前提条件は、データ保護をラベルを使って適用する場合、または Azure Rights Management サービスに直接接続することによって適用する場合に適用されます。 データ保護を適用するために構成されます。

Azure Information Protection テナントがアクティブ化されていない場合は、「[Rights Management をアクティブにする](../deploy-use/activate-service.md)」の手順をご覧ください。

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>前提条件 2: 自分のアカウントを使って他のユーザーのファイルから保護を削除するには

他のユーザーのファイルから保護を削除する一般的なシナリオには、データの探索またはデータの回復が含まれます。 ラベルを使って保護を適用している場合は、保護を適用しない新しいラベルを設定することによって、またはラベルを削除することによって保護を削除できます。 ただし、Azure Rights Management サービスに直接接続して保護を削除することもできます。

ファイルから保護を削除するには、Rights Management のアクセス許可を持っているか、スーパー ユーザーである必要があります。 データの探索またはデータの回復には、スーパー ユーザー機能が通常使われます。 この機能を有効にし、アカウントをスーパー ユーザーとして構成するには、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../deploy-use/configure-super-users.md)」をご覧ください。

#### <a name="prerequisite-3-to-protect-or-unprotect-files-without-user-interaction"></a>前提条件 3: ユーザー操作なしにファイルを保護または保護解除するには

現在はラベルを非対話形式で適用することはできませんが、非対話形式で Azure Rights Management サービスに直接接続して、ファイルを保護または保護解除することができます。

サービス プリンシパルを使って、非対話形式で Azure Rights Management サービスに接続する必要があります。それには、`Set-RMSServerAuthentication` コマンドレットを使います。 Azure Rights Management サービスに直接接続するコマンドレットを実行する Windows PowerShell セッションごとに、これを行う必要があります。 このコマンドレットを実行する前に、次の&3; つの識別子があることを確認します。

- BposTenantId

- AppPrincipalId

- 対称キー

次のセクションでは、これらの識別子を取得する方法について説明します。

##### <a name="to-get-the-bpostenantid"></a>BposTenantId を取得するには

Azure RMS Windows PowerShell モジュールから Get-AadrmConfiguration コマンドレットを実行します。

1. このモジュールがコンピューターにまだインストールされていない場合は、「[Azure Rights Management 用 Windows PowerShell をインストールする](../deploy-use/install-powershell.md)」をご覧ください。

2. **[管理者として実行]** オプションを使って、Windows PowerShell を起動します。

3. `Connect-AadrmService` コマンドレットを使って、Azure Rights Management サービスに接続します。
    
        Connect-AadrmService
    
    プロンプトが表示されたら、Azure Information Protection のテナント管理者の資格情報を入力します (通常は、Azure Active Directory または Office 365 のグローバル管理者であるアカウントを使います)。
    
4. `Get-AadrmConfiguration` を実行して、BPOSId の値をコピーします。
    
    Get-AadrmConfiguration の出力の例を次に示します。
    
            BPOSId                                   : 23976bc6-dcd4-4173-9d96-dad1f48efd42
        
            RightsManagement ServiceId               : 1a302373-f233-440600909-4cdf305e2e76
        
            LicensingIntranetDistributionPointUrl    : https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/licensing
        
            LicensingExtranetDistributionPointUrl    : https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/licensing
        
            CertificationIntranetDistributionPointUrl: https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/certification
        
            CertificationExtranetDistributionPointUrl: https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/certification

5. サービスから切断します。
    
        Disconnect-AadrmService

##### <a name="to-get-the-appprincipalid-and-symmetric-key"></a>AppPrincipalId と対称キーを取得するには

Azure Active Directory の MSOnline PowerShell モジュールから `New-MsolServicePrincipal` コマンドレットを実行することによって、またはさらに新しい Azure Active Directory バージョン 2 PowerShell モジュールの `New-AzureADServicePrincipal` を実行することによって、新しいサービス プリンシパルを作成します。 

以下の手順は、Azure Active Directory の MSOnline PowerShell モジュールから New-MsolServicePrincipal を実行する場合のものです。

1. このモジュールがコンピューターにまだインストールされていない場合は、「[Install the Azure AD Module](/powershell/azuread/#install-the-azure-ad-module)」(Azure AD モジュールをインストールする) をご覧ください。

2. **[管理者として実行]** オプションを使って、Windows PowerShell を起動します。

3. **Connect-MsolService** コマンドレットを使って、Azure AD に接続します。
    
        Connect-MsolService
    
    プロンプトが表示されたら、Azure AD のテナント管理者の資格情報を入力します (通常は、Azure Active Directory または Office 365 のグローバル管理者であるアカウントを使います)。

4. New-MsolServicePrincipal コマンドレットを実行して、新しいサービス プリンシパルを作成します。
    
        New-MsolServicePrincipal
    
    プロンプトが表示されたら、ファイルを保護および保護解除できるように Azure Rights Management サービスに接続するためのアカウントとしての目的が後でわかりやすいように、このサービス プリンシパルの表示名を入力します。
    
    New-MsolServicePrincipal の出力例を次に示します。
    
        Supply values for the following parameters:
        
        DisplayName: AzureRMSProtectionServicePrincipal
        The following symmetric key was created as one was not supplied
        zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=
        
        Display Name: AzureRMSProtectionServicePrincipal
        ServicePrincipalNames: (b5e3f7g1-b5c2-4c96-a594-a0807f65bba4)
        ObjectId: 23720996-593c-4122-bfc7-1abb5a0b5109
        AppPrincialId: b5e3f76a-b5c2-4c96-a594-a0807f65bba4
        TrustedForDelegation: False
        AccountEnabled: True
        Addresses: ()
        KeyType: Symmetric
        KeyId: 8ef61651-ca11-48ea-a350-25834a1ba17c
        StartDate: 3/7/2014 4:43:59 AM
        EndDate: 3/7/2014 4:43:59 AM
        Usage: Verify

5. この出力から、対称キーと AppPrincialId を書き写しておきます。

    対称キーをコピーしておくことが特に重要です。後で完全な対称キーを取得することはできないので、わからないと、次に Azure Rights Management サービスに対する認証を行うときに新しいサービス プリンシパルを作成する必要があります。

以上の手順と例から、Set-RMSServerAuthentication の実行に必要な&3; つの識別子が得られます。

- テナント Id: **23976bc6-dcd4-4173-9d96-dad1f48efd42**

- 対称キー: **zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=**

- AppPrincipalId: **b5e3f76a-b5c2-4c96-a594-a0807f65bba4**

ここで使うコマンドの例は、次のようになります。

    Set-RMSServerAuthentication -Key zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=-AppPrincipalId b5e3f76a-b5c2-4c96-a594-a0807f65bba4-BposTenantId 23976bc6-dcd4-4173-9d96-dad1f48efd42

前のコマンドで示すように&1; つのコマンドで値を指定することも、Set-RMSServerAuthentication だけを入力してプロンプトで&1; つずつ値を指定することもできます。 コマンドが完了すると、"**The RmsServerAuthentication is set to ON**" と表示されます。これは、サービス プリンシパルを使ってファイルの保護と保護解除を実行できることを意味します。

このサービス プリンシパルをスーパー ユーザーにすることを検討します。このサービス プリンシパルでいつでも他のユーザーのファイルの保護を解除できるように、スーパー ユーザーとして構成できます。 標準のユーザー アカウントをスーパー ユーザーとして構成するときと同じように、Azure RMS コマンドレットの [Add-AadrmSuperUser](/powershell/aadrm/vlatest/Add-AadrmSuperUser.md) を使いますが、**-ServicePrincipalId** パラメーターには AppPrincipalId の値を指定します。

スーパー ユーザーについて詳しくは、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../deploy-use/configure-super-users.md)」をご覧ください。

> [!NOTE]
> 自分のアカウントを使って Azure Rights Management サービスへの認証を行う場合は、ファイルを保護または保護解除する前、またはテンプレートを取得する前に、Set-RMSServerAuthentication を実行する必要はありません。

#### <a name="prerequisite-4-for-regions-outside-north-america"></a>前提条件 4: 北米以外のリージョンの場合

Azure 北米リージョン以外での認証の場合は、レジストリを次のように編集する必要があります。 Azure Information Protection テナントが北米にある場合は、この手順を行う必要はありません。

1. Get-AadrmConfiguration コマンドレットを再び実行し、**CertificationExtranetDistributionPointUrl** と **LicensingExtranetDistributionPointUrl** の値を書き留めておきます。

2. AzureInformationProtection コマンドレットを実行する各コンピューターで、レジストリ エディターを開き、`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC` に移動します。

3. **ServiceLocation** キーが表示されない場合は、レジストリのパスが **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation** となるように作成します。

4. **ServiceLocation** キーに対し、**EnterpriseCertification** および **EnterprisePublishing** という名前の&2; つのキーを作成します (存在しない場合)。 
    
    これらの REG_SZ キーを作成するときは、"(既定)" の名前は変更せず、値データを次のように設定します。

    - **EnterpriseCertification** には、CertificationExtranetDistributionPointUrl の値を貼り付けます。
    
    - **EnterprisePublishing** には、LicensingExtranetDistributionPointUrl の値を貼り付けます。

5. レジストリ エディターを閉じます。 コンピューターを再起動する必要はありません。 ただし、自分のユーザー アカウントではなくサービス プリンシパル アカウントを使っている場合は、このレジストリの編集を行った後で、Set-RMSServerAuthentication コマンドを実行する必要があります。

### <a name="example-scenarios-for-using-the-cmdlets-for-azure-information-protection-and-the-azure-rights-management-service"></a>Azure Information Protection および Azure Rights Management サービスのコマンドレットを使うシナリオの例

ラベルを使ってファイルを分類および保護する方が効率的です。必要なコマンドレットが [Get-AIPFileStatus](/powershell/azureinformationprotection/vlatest/get-aipfilestatus) と [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel) の&2; つだけであり、単独で、または一緒に実行できるためです。 詳細と例については、これら両方のコマンドレットのヘルプを使ってください。

ただし、Azure Rights Management サービスに直接接続してファイルを保護または保護解除するには、通常、次に説明するように一連のコマンドレットを実行する必要があります。

最初に、自分のアカウントではなくサービス プリンシパルを使って Azure Rights Management サービスの認証を行う場合は、Powershell セッションで次のように入力します。

    Set-RMSServerAuthentication

メッセージが表示されたら、「[前提条件 3: ユーザーの介入なしにファイルを保護または保護解除するには](client-admin-guide-powershell.md#prerequisite-3-to-protect-or-unprotect-files-without-user-interaction)」で説明されているように、3 つの識別子を入力します。

ファイルを保護するには、Rights Management テンプレートをお使いのコンピューターにダウンロードして、使用するものとそれに対応する ID 番号を確認する必要があります。 出力から、テンプレート ID をコピーできます。

    Get-RMSTemplate
    
出力は次のようになります。

    TemplateId        : {82bf3474-6efe-4fa1-8827-d1bd93339119}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content cannot be modified.
    Name              : Contoso, Ltd - Confidential View Only
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    
    TemplateId        : {e6ee2481-26b9-45e5-b34a-f744eacd53b0}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content can be modified but cannot be copied and printed.
    Name              : Contoso, Ltd - Confidential
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    FromTemplate      : True

Set-RMSServerAuthentication コマンドを実行しなかった場合は、自分のユーザー アカウントを使って Azure Rights Management サービスへの認証を行うことに注意してください。 ドメインに参加しているコンピューターでは、現在の資格情報が常に自動的に使われます。 ワークグループ コンピューターの場合は、Azure へのサインインを求められ、これらの資格情報は後続のコマンドのためにキャッシュされます。 このシナリオでは、後で別のユーザーとしてサインインする必要がある場合は、`Clear-RMSAuthentication` コマンドレットを使います。

テンプレート ID がわかったので、`Protect-RMSFile` コマンドレットでそれを使って、フォルダー内の&1; つのファイルまたはすべてのファイルを保護できます。 たとえば、1 つのファイルだけを保護し、元のファイルを上書きする場合は、"Contoso, Ltd - Confidential" テンプレートを使います。

    Protect-RMSFile -File C:\Test.docx -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

出力は次のようになります。

    InputFile             EncryptedFile
    ---------             -------------
    C:\Test.docx          C:\Test.docx

フォルダー内のすべてのファイルを保護するには、**-Folder** パラメーターにドライブ文字とパスまたは UNC パスを指定して実行します。 たとえば、

    Protect-RMSFile -Folder \Server1\Documents -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

出力は次のようになります。

    InputFile                          EncryptedFile
    ---------                          -------------
    \Server1\Documents\Test1.docx     \Server1\Documents\Test1.docx
    \Server1\Documents\Test2.docx     \Server1\Documents\Test2.docx
    \Server1\Documents\Test3.docx     \Server1\Documents\Test3.docx
    \Server1\Documents\Test4.docx     \Server1\Documents\Test4.docx

保護を適用した後でファイル名拡張子が変わっていない場合は、いつでも `Get-RMSFileStatus` コマンドレットを使って、ファイルが保護されているかどうかを確認できます。 たとえば、

    Get-RMSFileStatus -File \Server1\Documents\Test1.docx

出力は次のようになります。

    FileName                              Status
    --------                              ------
    \Server1\Documents\Test1.docx         Protected

ファイルの保護を解除するには、ファイルを保護したときから所有者または抽出の権限を持っているか、スーパー ユーザーとしてコマンドレットを実行する必要があります。 その後、Unprotect コマンドレットを使います。 たとえば、

    Unprotect-RMSFile C:\test.docx -InPlace

出力は次のようになります。

    InputFile                             DecryptedFile
    ---------                             -------------
    C:\Test.docx                          C:\Test.docx

Rights Management テンプレートが変更された場合は、もう一度 `Get-RMSTemplate -force` でダウンロードしてください。 

## <a name="active-directory-rights-management-services"></a>Active Directory Rights Management サービス

Active Directory Rights Management サービスだけを使っている場合は、PowerShell コマンドを使ってファイルを保護または保護解除する前に、このセクションをお読みください。


### <a name="prerequisites-for-ad-rms"></a>AD RMS の前提条件

AzureInformationProtection モジュールをインストールするための前提条件に加えて、ServerCertification.asmx にアクセスするにはアカウントに読み取りと実行のアクセス許可が必要です。

1. AD RMS サーバーにログオンします。

2. **[スタート]** ボタンをクリックし、**[コンピューター]** をクリックします。

3. エクスプローラーで、%systemdrive%\Initpub\wwwroot\_wmsc\Certification に移動します。

4. **ServerCertification.asmx** を右クリックし、**[プロパティ]** をクリックします。

5. **[ServerCertification.asmx のプロパティ]** ダイアログ ボックスで、**[セキュリティ]** タブをクリックします。 

6. **[続行]** または **[編集]** ボタンをクリックします。 

7. **[ServerCertification.asmx のアクセス許可]** ダイアログ ボックスで、**[追加]** をクリックします。 

8. アカウント名を追加します。 他の AD RMS 管理者もこれらのコマンドレットを使ってファイルを保護および保護解除する場合は、その名前も追加します。

9. **[許可]** 列で、**[読み取りと実行]** および **[読み取り]** チェック ボックスがオンになっていることを確認します。

10. **[OK]** を&2; 回クリックします。

### <a name="example-scenarios-for-using-the-cmdlets-for-active-directory-rights-management-services"></a>Active Directory Rights Management サービスにコマンドレットを使うシナリオの例

権利ポリシー テンプレートを使ってフォルダー内のすべてのファイルを保護するか、1 つのファイルの保護を解除するのが、これらのコマンドレットの一般的なシナリオです。 

最初に、AD RMS の複数のデプロイがある場合は、AD RMS サーバーの名前が必要になります。Get-RMSServer コマンドレットを使って、使用可能なサーバーの一覧を表示します。

    Get-RMSServer

出力は次のようになります。

    Number of RMS Servers that can provide templates: 2 
    ConnectionInfo             DisplayName          AllowFromScratch
    --------------             -------------        ----------------
    Microsoft.InformationAnd…  RmsContoso                       True
    Microsoft.InformationAnd…  RmsFabrikam                      True

ファイルを保護するには、先に、RMS テンプレートを取得して使うものを確認し、それに対応する ID 番号の一覧を確認する必要があります。 AD RMS のデプロイが複数ある場合にのみ、RMS サーバーも指定する必要があります。 

出力から、テンプレート ID をコピーできます。

    Get-RMSTemplate -RMSServer RmsContoso

出力は次のようになります。

    TemplateId        : {82bf3474-6efe-4fa1-8827-d1bd93339119}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content cannot be modified.
    Name              : Contoso, Ltd - Confidential View Only
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    
    
    TemplateId        : {e6ee2481-26b9-45e5-b34a-f744eacd53b0}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content can be modified but cannot be copied and printed.
    Name              : Contoso, Ltd - Confidential
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    FromTemplate      : True

テンプレート ID がわかったので、Protect-RMSFile コマンドレットでそれを使って、フォルダー内の&1; つのファイルまたはすべてのファイルを保護できます。 たとえば、1 つのファイルだけを保護し、元のファイルを置き換える場合は、"Contoso, Ltd - Confidential" テンプレートを使います。

    Protect-RMSFile -File C:\Test.docx -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

出力は次のようになります。

    InputFile             EncryptedFile
    ---------             -------------
    C:\Test.docx          C:\Test.docx   

フォルダー内のすべてのファイルを保護するには、-Folder パラメーターにドライブ文字とパスまたは UNC パスを指定して実行します。 たとえば、

    Protect-RMSFile -Folder \\Server1\Documents -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

出力は次のようになります。

    InputFile                          EncryptedFile
    ---------                          -------------
    \\Server1\Documents\Test1.docx     \\Server1\Documents\Test1.docx   
    \\Server1\Documents\Test2.docx     \\Server1\Documents\Test2.docx   
    \\Server1\Documents\Test3.docx     \\Server1\Documents\Test3.docx   
    \\Server1\Documents\Test4.docx     \\Server1\Documents\Test4.docx   

RMS の保護を適用した後でファイル名拡張子が変わっていない場合は、いつでも Get-RMSFileStatus コマンドレットを使って、ファイルが保護されているかどうかを確認できます。 たとえば、 

    Get-RMSFileStatus -File \\Server1\Documents\Test1.docx

出力は次のようになります。

    FileName                              Status
    --------                              ------
    \\Server1\Documents\Test1.docx        Protected

ファイルの保護を解除するには、ファイルを保護したときから所有者または抽出の権限を持っているか、AD RMS のスーパー ユーザーである必要があります。 その後、Unprotect コマンドレットを使います。 たとえば、

    Unprotect-RMSFile C:\test.docx -InPlace

出力は次のようになります。

    InputFile                             DecryptedFile
    ---------                             -------------
    C:\Test.docx                          C:\Test.docx


## <a name="next-steps"></a>次のステップ
PowerShell セッション内でコマンドレットのヘルプを見るには、Get-Help <cmdlet name> コマンドレットを使います。<cmdlet name> は、調べるコマンドレットの名前です。 たとえば、 

    Get-Help Get-RMSTemplate

Azure Information Protection クライアントのサポートに必要な詳細については、以下をご覧ください。

- [クライアント ファイルおよび使用状況ログの記録](client-admin-guide-files-and-logging.md)

- [ドキュメント追跡](client-admin-guide-document-tracking.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]
