---
title: Azure Information Protection クライアントで PowerShell を使用する
description: 管理者が PowerShell を使って Azure Information Protection クライアントを管理するための手順と情報について説明します。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/26/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4f9d2db7-ef27-47e6-b2a8-d6c039662d3c
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 7853cfc577329e04a1f378a419f0e1ef3eca0f2a
ms.sourcegitcommit: 6cbd03b28873b192dc730556c6dd5a7da6e705df
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/02/2018
ms.locfileid: "39411072"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-client"></a>管理者ガイド: Azure Information Protection クライアントでの PowerShell の使用

>*適用対象: Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012, Windows Server 2008 R2*

Azure Information Protection クライアントをインストールすると、PowerShell コマンドが自動的にインストールされます。 自動化のためのスクリプトに追加できるコマンドを実行することでクライアントを管理できます。

コマンドレットは PowerShell モジュール **AzureInformationProtection** と共にインストールされます。 このモジュールには、(サポートされなくなった) RMS 保護ツールの Rights Management コマンドレットがすべて含まれます。 ラベル付けに Azure Information Protection を利用するコマンドレットもあります。 次に例を示します。

|ラベル付けコマンドレット|使用例|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|共有フォルダーで、すべてのファイルを特定のラベルで識別します。|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|共有フォルダーで、ファイルの内容を検査したあと、指定した条件に基づいて、ラベル付けされていないファイルに自動的にラベルを付与します。|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|共有フォルダーで、ラベルが付いていないすべてのファイルに指定したラベルを適用します。|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|スケジュールに基づいて実行されるスクリプトを利用するなど、非対話式にファイルにラベルを付けます。|

> [!TIP]
> 260 文字よりも長いパスとともにコマンドレットを使用するには、Windows 10 Anniversary Update で利用できる次の[グループ ポリシー設定](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)を使用します。<br /> **ローカル コンピューター ポリシー** > **コンピューターの構成** > **管理用テンプレート** > **すべての設定** > **NTFS** > **Win32 の長いパスを有効にする** 
> 
> Windows Server 2016 の場合、Windows 10 用の最新の管理用テンプレート (.admx) をインストールすれば、同じグループ ポリシー設定を使用できます。

[Azure Information Protection スキャナー](../deploy-use/deploy-aip-scanner.md)では AzureInformationProtection モジュールのコマンドレットを使用して、Windows Server にサービスをインストールし、構成します。 このスキャナーでは、データ ストアのファイルを検出、分類、保護できます。

すべてのコマンドレットと対応するヘルプの一覧については、「[AzureInformationProtection Module](/powershell/module/azureinformationprotection)」 (AzureInformationProtection モジュール) を参照してください。 PowerShell セッション内で、「`Get-Help <cmdlet name> -online`」と入力すると、最新のヘルプが表示されます。  

このモジュールは、**\ProgramFiles (x86)\Microsoft Azure Information Protection** にインストールされ、このフォルダーを **PSModulePath** システム変数に追加します。 このモジュールの .dll の名前は **AIP.dll** です。

現時点では、モジュールをインストールするときに使うユーザーと、同じコンピューターでコマンドレットを実行するときに使うユーザーが異なる場合は、最初に `Import-Module AzureInformationProtection` コマンドを実行する必要があります。 このシナリオでは、コマンドレットを初めて実行するときに、モジュールは自動的に読み込まれません。

AzureInformationProtection モジュールの現在のリリースには、以下の制限があります。

- Outlook 個人フォルダー (.pst ファイル) の保護を解除することはできますが、現在は、この PowerShell モジュールを使ってこれらのファイルまたは他のコンテナー ファイルをネイティブに保護することはできません。

- Outlook の保護された電子メール メッセージ (.rpmsg ファイル) が Outlook 個人フォルダー (.pst) 内にある場合は、メッセージの保護を解除できますが、個人フォルダー外にある場合は .rpmsg ファイルの保護を解除できません。

これらのコマンドレットを使い始める前に、デプロイに対応する追加の前提条件と手順を参照してください。

- [Azure Information Protection と Azure Rights Management サービス](#azure-information-protection-service-and-azure-rights-management-service)

    - 分類のみ、または Rights Management 保護で分類を使っている場合に適用: Azure Information Protection を含むサブスクリプションがある場合 (例: Enterprise Mobility + Security)。
    - Azure Rights Management サービスで保護のみを使っている場合に適用: Azure Rights Management サービスを含むサブスクリプションがある場合 (例: Office 365 E3、Office 365 E5)。

- [Active Directory Rights Management サービス](#active-directory-rights-management-services)

    - オンプレミス バージョンの Azure Rights Management で保護のみを使っている場合に適用: Active Directory Rights Management サービス (AD RMS)。


## <a name="azure-information-protection-and-azure-rights-management-service"></a>Azure Information Protection と Azure Rights Management サービス

組織が分類と保護に Azure Information Protection を使用しているとき、あるいはデータ保護に Azure Rights Management サービスを使用しているとき、PowerShell コマンドを使い始める前にこのセクションをお読みください。


### <a name="prerequisites"></a>必要条件

AzureInformationProtection モジュールのインストールに関する前提条件に加えて、Azure Information Protection ラベル付けと Azure Rights Management データ保護サービスに関する追加の前提条件があります。

1. Azure Rights Management サービスをアクティブ化する必要があります。

2. 自分のアカウントを使って他のユーザーのファイルから保護を削除するには: 
    
    - 組織のスーパー ユーザー機能を有効にし、自分のアカウントを Azure Rights Management のスーパー ユーザーとして構成する必要があります。

3. ユーザー操作なしにファイルを直接保護または保護解除するには: 
    
    - サービス プリンシパル アカウントを作成し、Set-RMSServerAuthentication を実行して、このサービス プリンシパルを Azure Rights Management のスーパー ユーザーにします。

4. 北米以外のリージョンの場合： 
    
    - サービス検出のレジストリを編集します。

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>前提条件 1: Azure Rights Management サービスをアクティブ化する必要がある

この前提条件は、ラベルを使ってデータ保護を適用する場合、または Azure Rights Management サービスに直接接続してデータ保護を適用する場合に適用されます。

Azure Information Protection テナントがアクティブ化されていない場合は、「[Rights Management をアクティブにする](../deploy-use/activate-service.md)」の手順をご覧ください。

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>前提条件 2: 自分のアカウントを使って他のユーザーのファイルから保護を削除するには

他のユーザーのファイルから保護を削除する一般的なシナリオには、データの探索またはデータの回復が含まれます。 ラベルを使って保護を適用している場合は、保護を適用しない新しいラベルを設定することによって、またはラベルを削除することによって保護を削除できます。 ただし、Azure Rights Management サービスに直接接続して保護を削除することもできます。

ファイルから保護を削除するには、Rights Management の使用権限を持っているか、スーパー ユーザーである必要があります。 データの探索またはデータの回復には、スーパー ユーザー機能が通常使われます。 この機能を有効にし、アカウントをスーパー ユーザーとして構成するには、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../deploy-use/configure-super-users.md)」をご覧ください。

#### <a name="prerequisite-3-to-protect-or-unprotect-files-without-user-interaction"></a>前提条件 3: ユーザー操作なしにファイルを保護または保護解除するには

非対話形式で Azure Rights Management サービスに直接接続し、ファイルを保護または保護解除できます。

サービス プリンシパル アカウントを使って、非対話形式で Azure Rights Management サービスに接続する必要があります。それには、`Set-RMSServerAuthentication` コマンドレットを使います。 Azure Rights Management サービスに直接接続するコマンドレットを実行する Windows PowerShell セッションごとに、これを行う必要があります。 このコマンドレットを実行する前に、次の 3 つの識別子があることを確認します。

- BposTenantId

- AppPrincipalId

- 対称キー

次の PowerShell コマンドとコメント付き手順を利用し、識別子の値を自動的に取得し、Set-RMSServerAuthentication コマンドレットを実行できます。 あるいは、値を手動で取得し、指定できます。

値を自動で取得し、Set-RMSServerAuthentication を実行するには:

````
# Make sure that you have the AADRM and MSOnline modules installed

$ServicePrincipalName="<new service principal name>"
Connect-AadrmService
$bposTenantID=(Get-AadrmConfiguration).BPOSId
Disconnect-AadrmService
Connect-MsolService
New-MsolServicePrincipal -DisplayName $ServicePrincipalName

# Copy the value of the generated symmetric key

$symmetricKey="<value from the display of the New-MsolServicePrincipal command>"
$appPrincipalID=(Get-MsolServicePrincipal | Where { $_.DisplayName -eq $ServicePrincipalName }).AppPrincipalId
Set-RMSServerAuthentication -Key $symmetricKey -AppPrincipalId $appPrincipalID -BposTenantId $bposTenantID

````

次のセクションでは、値を手動で取得し、指定する方法について説明します。それぞれの値について詳しく説明します。

##### <a name="to-get-the-bpostenantid"></a>BposTenantId を取得するには

Azure RMS Windows PowerShell モジュールから Get-AadrmConfiguration コマンドレットを実行します。

1. このモジュールがコンピューターにまだインストールされていない場合は、「[AADRM PowerShell モジュールのインストール](../deploy-use/install-powershell.md)」を参照してください。

2. **[管理者として実行]** オプションを使って、Windows PowerShell を起動します。

3. `Connect-AadrmService` コマンドレットを使って、Azure Rights Management サービスに接続します。
    
        Connect-AadrmService
    
    プロンプトが表示されたら、Azure Information Protection テナント管理者資格情報を入力します。 通常、Azure Active Directory または Office 365 のグローバル管理者であるアカウントを使用します。
    
4. `Get-AadrmConfiguration` を実行して、BPOSId の値をコピーします。
    
    Get-AadrmConfiguration の出力例
    
            BPOSId                                   : 23976bc6-dcd4-4173-9d96-dad1f48efd42
        
            RightsManagement ServiceId               : 1a302373-f233-440600909-4cdf305e2e76
        
            LicensingIntranetDistributionPointUrl    : https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/licensing
        
            LicensingExtranetDistributionPointUrl    : https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/licensing
        
            CertificationIntranetDistributionPointUrl: https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/certification
        
            CertificationExtranetDistributionPointUrl: https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/certification

5. サービスから切断します。
    
        Disconnect-AadrmService

##### <a name="to-get-the-appprincipalid-and-symmetric-key"></a>AppPrincipalId と対称キーを取得するには

Azure Active Directory の MSOnline PowerShell モジュールから `New-MsolServicePrincipal` コマンドレットを実行し、次の手順に従うことで、新しいサービス プリンシパルを作成します。 

> [!IMPORTANT]
> 新しい Azure AD PowerShell コマンドレット、New-AzureADServicePrincipal を使用してこのサービス プリンシパルを作成しないでください。 Azure Rights Management サービスでは、New-AzureADServicePrincipal をサポートしていません。 

1. MSOnline モジュールがまだコンピューターにインストールされていない場合は、`Install-Module MSOnline` を実行します。

2. **[管理者として実行]** オプションを使って、Windows PowerShell を起動します。

3. **Connect-MsolService** コマンドレットを使って、Azure AD に接続します。
    
        Connect-MsolService
    
    プロンプトが表示されたら、Azure AD のテナント管理者の資格情報を入力します (通常は、Azure Active Directory または Office 365 のグローバル管理者であるアカウントを使います)。

4. New-MsolServicePrincipal コマンドレットを実行して、新しいサービス プリンシパルを作成します。
    
        New-MsolServicePrincipal
    
    プロンプトが表示されたら、Azure Rights Management サービスに接続してファイルの保護と保護解除を行うアカウントであることが後に分かるように、サービス プリンシパルの表示名を入力します。
    
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

    今、この対称キーをコピーしておくことが重要です。 このキーは後で取得できません。Azure Rights Management サービスで認証するときにキーがわからなければ、新しいサービス プリンシパルを作成する必要があります。

以上の手順と例から、Set-RMSServerAuthentication の実行に必要な 3 つの識別子が得られます。

- テナント Id: **23976bc6-dcd4-4173-9d96-dad1f48efd42**

- 対称キー: **zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=**

- AppPrincipalId: **b5e3f76a-b5c2-4c96-a594-a0807f65bba4**

ここで使うコマンドの例は、次のようになります。

    Set-RMSServerAuthentication -Key zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=-AppPrincipalId b5e3f76a-b5c2-4c96-a594-a0807f65bba4-BposTenantId 23976bc6-dcd4-4173-9d96-dad1f48efd42

前のコマンドのように、単一のコマンドで値を指定できます。これは、非対話的に実行するスクリプトの場合と同じです。 ただし、テストが目的の場合は、単に Set-RMSServerAuthentication と入力し、プロンプトに 1 つずつ値を入力してもかまいません。 コマンドが完了すると、クライアントは "サーバー モード" で動作するようになります。これは、スクリプトや Windows Server ファイル分類インフラストラクチャなどの非対話型の使用に適しています。

このサービス プリンシパル アカウントをスーパー ユーザーにすることを検討します。このサービス プリンシパル アカウントでいつでも他のユーザーのファイルの保護を解除できるように、スーパー ユーザーとして構成できます。 標準のユーザー アカウントをスーパー ユーザーとして構成するときと同じように、Azure RMS コマンドレットの [Add-AadrmSuperUser](/powershell/aadrm/vlatest/Add-AadrmSuperUser.md) を使いますが、**ServicePrincipalId** パラメーターには AppPrincipalId の値を指定します。

スーパー ユーザーについて詳しくは、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../deploy-use/configure-super-users.md)」をご覧ください。

> [!NOTE]
> 自分のアカウントを使って Azure Rights Management サービスへの認証を行う場合は、ファイルを保護または保護解除する前、またはテンプレートを取得する前に、Set-RMSServerAuthentication を実行する必要はありません。

#### <a name="prerequisite-4-for-regions-outside-north-america"></a>前提条件 4: 北米以外のリージョンの場合

サービス プリンシパル アカウントを使用して、Azure 北米リージョン以外でファイルを保護し、テンプレートをダウンロードする場合は、レジストリを次のように編集する必要があります。 

1. Get-AadrmConfiguration コマンドレットを再び実行し、**CertificationExtranetDistributionPointUrl** と **LicensingExtranetDistributionPointUrl** の値を書き留めておきます。

2. AzureInformationProtection コマンドレットを実行する各コンピューターで、レジストリ エディターを開きます。

3. `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation` のパスに移動します。 
    
    **MSIPC** キーまたは **ServiceLocation** キーがない場合は、それらを作成します。

4. **ServiceLocation** キーに対し、**EnterpriseCertification** および **EnterprisePublishing** という名前の 2 つのキーを作成します (存在しない場合)。 
    
    キーに自動作成される文字列値については、"(Default)" の名前を変更せず、文字列を編集して値データを設定してください。

    - **EnterpriseCertification** には、CertificationExtranetDistributionPointUrl の値を貼り付けます。
    
    - **EnterprisePublishing** には、LicensingExtranetDistributionPointUrl の値を貼り付けます。
    
    たとえば、EnterpriseCertification のレジストリ エントリは次のようになります。
    
    ![北米以外の地域に関して、Azure Information Protection PowerShell モジュールのレジストリを編集する](../media/registry-example-rmsprotection.png)

5. レジストリ エディターを閉じます。 コンピューターを再起動する必要はありません。 ただし、自分のユーザー アカウントではなくサービス プリンシパル アカウントを使っている場合は、このレジストリの編集を行った後で、Set-RMSServerAuthentication コマンドを実行する必要があります。

### <a name="example-scenarios-for-using-the-cmdlets-for-azure-information-protection-and-the-azure-rights-management-service"></a>Azure Information Protection および Azure Rights Management サービスのコマンドレットを使うシナリオの例

ラベルを使ってファイルを分類および保護する方が効率的です。必要なコマンドレットが [Get-AIPFileStatus](/powershell/azureinformationprotection/get-aipfilestatus) と [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel) の 2 つだけであり、単独で、または一緒に実行できるためです。 詳細と例については、これら両方のコマンドレットのヘルプを使ってください。

ただし、Azure Rights Management サービスに直接接続してファイルを保護または保護解除するには、通常、次に説明するように一連のコマンドレットを実行する必要があります。

最初に、自分のアカウントではなくサービス プリンシパル アカウントを使って Azure Rights Management サービスの認証を行う場合は、PowerShell セッションで次のように入力します。

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

Set-RMSServerAuthentication コマンドを実行しなかった場合は、自分のユーザー アカウントを使用して Azure Rights Management サービスの認証を行うことに注意してください。 ドメインに参加しているコンピューターの場合は、現在の資格情報が常に自動的に使用されます。 ワークグループ コンピューターの場合は、Azure へのサインインを求められ、これらの資格情報は後続のコマンドのためにキャッシュされます。 このシナリオでは、後で別のユーザーとしてサインインする必要がある場合は、`Clear-RMSAuthentication` コマンドレットを使います。

テンプレート ID がわかったので、`Protect-RMSFile` コマンドレットでそれを使って、フォルダー内の 1 つのファイルまたはすべてのファイルを保護できます。 たとえば、1 つのファイルだけを保護し、元のファイルを上書きする場合は、"Contoso, Ltd - Confidential" テンプレートを使います。

    Protect-RMSFile -File C:\Test.docx -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

出力は次のようになります。

    InputFile             EncryptedFile
    ---------             -------------
    C:\Test.docx          C:\Test.docx

フォルダー内のすべてのファイルを保護するには、**-Folder** パラメーターにドライブ文字とパスまたは UNC パスを指定して実行します。 次に例を示します。

    Protect-RMSFile -Folder \Server1\Documents -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

出力は次のようになります。

    InputFile                          EncryptedFile
    ---------                          -------------
    \Server1\Documents\Test1.docx     \Server1\Documents\Test1.docx
    \Server1\Documents\Test2.docx     \Server1\Documents\Test2.docx
    \Server1\Documents\Test3.docx     \Server1\Documents\Test3.docx
    \Server1\Documents\Test4.docx     \Server1\Documents\Test4.docx

保護を適用した後でファイル名拡張子が変わっていない場合は、いつでも `Get-RMSFileStatus` コマンドレットを使って、ファイルが保護されているかどうかを確認できます。 次に例を示します。

    Get-RMSFileStatus -File \Server1\Documents\Test1.docx

出力は次のようになります。

    FileName                              Status
    --------                              ------
    \Server1\Documents\Test1.docx         Protected

ファイルの保護を解除するには、ファイルを保護したときから所有者または抽出の権限を持っている必要があります。 あるいは、スーパー ユーザーとしてコマンドレットを実行する必要があります。 その後、Unprotect コマンドレットを使います。 次に例を示します。

    Unprotect-RMSFile C:\test.docx -InPlace

出力は次のようになります。

    InputFile                             DecryptedFile
    ---------                             -------------
    C:\Test.docx                          C:\Test.docx

Rights Management テンプレートが変更された場合は、もう一度 `Get-RMSTemplate -force` でダウンロードしてください。 

## <a name="active-directory-rights-management-services"></a>Active Directory Rights Management サービス

Active Directory Rights Management サービスだけを使っている場合は、PowerShell コマンドを使ってファイルを保護または保護解除する前に、このセクションをお読みください。


### <a name="prerequisites"></a>必要条件

AzureInformationProtection モジュールをインストールするための前提条件に加えて、ファイルの保護と保護解除に使用するアカウントには、ServerCertification.asmx にアクセスする読み取り許可と実行許可を与える必要があります。

1. AD RMS サーバーにログオンします。

2. **[スタート]** ボタンをクリックし、**[コンピューター]** をクリックします。

3. エクスプローラーで、%systemdrive%\Initpub\wwwroot\_wmsc\Certification に移動します。

4. **ServerCertification.asmx** を右クリックし、**[プロパティ]** をクリックします。

5. **[ServerCertification.asmx のプロパティ]** ダイアログ ボックスで、**[セキュリティ]** タブをクリックします。 

6. **[続行]** または **[編集]** ボタンをクリックします。 

7. **[ServerCertification.asmx のアクセス許可]** ダイアログ ボックスで、**[追加]** をクリックします。 

8. アカウント名を追加します。 他の AD RMS 管理者やサービス アカウントもこれらのコマンドレットを使ってファイルを保護し、保護解除する場合、そのアカウントも追加します。 
    
    非対話式でファイルを保護または保護解除する場合、関連するコンピューター アカウントやアカウントを追加します。 たとえば、ファイル分類インフラストラクチャに対して構成されてあり、PowerShell スクリプトでファイルを保護する Windows Server コンピューターのコンピューター アカウントを追加します。

9. **[許可]** 列で、**[読み取りと実行]** および **[読み取り]** チェック ボックスがオンになっていることを確認します。

10. **[OK]** を 2 回クリックします。

### <a name="example-scenarios-for-using-the-cmdlets-for-active-directory-rights-management-services"></a>Active Directory Rights Management サービスにコマンドレットを使うシナリオの例

権利ポリシー テンプレートを使ってフォルダー内のすべてのファイルを保護するか、1 つのファイルの保護を解除するのが、これらのコマンドレットの一般的なシナリオです。 

最初に、AD RMS のデプロイが複数ある場合は、AD RMS サーバーの名前が必要になります。Get-RMSServer コマンドレットを使用することで、使用可能なサーバーの一覧が表示されます。

    Get-RMSServer

出力は次のようになります。

    Number of RMS Servers that can provide templates: 2 
    ConnectionInfo             DisplayName          AllowFromScratch
    --------------             -------------        ----------------
    Microsoft.InformationAnd…  RmsContoso                       True
    Microsoft.InformationAnd…  RmsFabrikam                      True

ファイルを保護するには、先に、RMS テンプレートを取得して使うものを確認し、それに対応する ID 番号の一覧を確認する必要があります。 AD RMS のデプロイが複数ある場合のみ、RMS サーバーも指定する必要があります。 

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

テンプレート ID がわかったので、Protect-RMSFile コマンドレットでそれを使って、フォルダー内の 1 つのファイルまたはすべてのファイルを保護できます。 たとえば、1 つのファイルだけを保護し、元のファイルを置き換える場合は、"Contoso, Ltd - Confidential" テンプレートを使います。

    Protect-RMSFile -File C:\Test.docx -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

出力は次のようになります。

    InputFile             EncryptedFile
    ---------             -------------
    C:\Test.docx          C:\Test.docx   

フォルダー内のすべてのファイルを保護するには、-Folder パラメーターにドライブ文字とパスまたは UNC パスを指定して実行します。 次に例を示します。

    Protect-RMSFile -Folder \\Server1\Documents -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

出力は次のようになります。

    InputFile                          EncryptedFile
    ---------                          -------------
    \\Server1\Documents\Test1.docx     \\Server1\Documents\Test1.docx   
    \\Server1\Documents\Test2.docx     \\Server1\Documents\Test2.docx   
    \\Server1\Documents\Test3.docx     \\Server1\Documents\Test3.docx   
    \\Server1\Documents\Test4.docx     \\Server1\Documents\Test4.docx   

保護を適用した後でファイル名拡張子が変わっていない場合は、いつでも Get-RMSFileStatus コマンドレットを使って、ファイルが保護されているかどうかを確認できます。 次に例を示します。 

    Get-RMSFileStatus -File \\Server1\Documents\Test1.docx

出力は次のようになります。

    FileName                              Status
    --------                              ------
    \\Server1\Documents\Test1.docx        Protected

ファイルの保護を解除するには、ファイルを保護したときから所有者または抽出の使用権限を持っているか、AD RMS のスーパー ユーザーである必要があります。 その後、Unprotect コマンドレットを使います。 次に例を示します。

    Unprotect-RMSFile C:\test.docx -InPlace

出力は次のようになります。

    InputFile                             DecryptedFile
    ---------                             -------------
    C:\Test.docx                          C:\Test.docx

## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>非対話形式でファイルに Azure Information Protection のラベル付けをする方法

**Set-AIPAuthentication** コマンドレットを利用し、ラベル付けコマンドレットを非対話式に実行できます。 Azure Information Protection スキャナーには、非対話型操作も必要です。

既定では、ラベル付けのコマンドレットを実行するとき、対話型 PowerShell セッション内のユーザー コンテキストでコマンドは動作します。 自動実行するには、そのための新しい Azure AD ユーザー アカウントを作成します。 次に、ユーザーのコンテキストで Set-AIPAuthentication コマンドレットを実行し、Azure AD のアクセス トークンを使用して資格情報を設定し、格納します。 次に、このユーザー アカウントは、Azure Rights Management サービスに認証され、ブートストラップされます。 このアカウントは、Azure Information Protection ポリシーと、ラベルが使用する Rights Management テンプレートをダウンロードします。

> [!NOTE]
> [スコープ付きポリシー](../deploy-use/configure-policy-scope.md)を使用する場合は、このアカウントをスコープ付きポリシーに追加しなければならない場合があります。

このコマンドレットを初めて実行する際は、Azure Information Protection へのサインインを求められます。 自動実行ユーザー用に作成したユーザー アカウント名とパスワードを指定します。 これ以降、このアカウントでは、認証トークンの有効期限が切れるまで、ラベル付けのコマンドレットを非対話形式で実行できます。 

この初回でユーザー アカウントが対話式サインインできるようにするには、アカウントに**ローカル ログオン**権限を与える必要があります。 この権限はユーザー アカウントの標準ですが、会社のポリシーによっては、サービス アカウントに対してこの構成を禁止することがあります。 禁止される場合、*Token* パラメーターを指定して Set-AIPAuthentication を実行できます。サインイン プロンプトなしで認証が完了します。 スケジュールされたタスクとしてこのコマンドを実行し、**バッチ ジョブとしてログオン**という低い権限をアカウントに与えることができます。 詳細については、後続のセクションを参照してください。 

トークンが期限切れになったら、コマンドレットを再度実行して新しいトークンを取得します。

パラメーターを指定せずにこのコマンドレットを実行すると、アカウントは 90 日間またはパスワードの有効期限が切れるまで有効なアクセス トークンを取得します。  

アクセス トークンの有効期限を制御するには、パラメーターを指定してこのコマンドレットを実行します。 これにより、1 年間有効、2 年間有効、または期限なしのアクセス トークンを構成できます。 この構成には、2 つのアプリケーション、すなわち **Web アプリ/API** アプリケーションと**ネイティブ アプリケーション**を Azure Active Directory に登録する必要があります。 このコマンドレットのパラメーターには、これらのアプリケーションからの値を使用します。

このコマンドレットを実行した後は、作成したユーザー アカウントのコンテキストでラベル付けコマンドレットを実行できます。

### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication"></a>Set-AIPAuthentication 用の Azure AD アプリケーションを作成し、構成するには

1. 新しいブラウザー ウィンドウで、[Azure Portal](https://portal.azure.com/) にサインインします。

2. Azure Information Protection で使用する Azure AD テナントで、**[Azure Active Directory]** > **[アプリの登録]** と移動します。 

3. **[新しいアプリケーションの登録]** を選択し、Web アプリ/API アプリケーションを作成します。 **[作成]** ラベルで次の値を指定して、**[作成]** をクリックします。
    
    - 名前: **AIPOnBehalfOf**
    
    必要に応じて、別の名前を指定することもできます。 名前は、テナントごとに一意である必要があります。
    
    - アプリケーションの種類: **Web アプリ/API**
    
    - サインオン URL: **http://localhost**

4. 先ほど作成したアプリケーションを選択します (例: **AIPOnBehalfOf**)。 その後、**[設定]** ブレードで **[プロパティ]** を選択します。 **[プロパティ]** ブレードで **[アプリケーション ID]** の値をコピーし、このブレードを閉じます。 
    
    この値は、Set-AIPAuthentication コマンドレットを実行するときの `WebAppId` パラメーターに使用されます。 後で参照できるように、これを貼り付けて保存します。

5. **[設定]** ブレードを再度開き、**[必要なアクセス許可]** を選択します。 **[必要なアクセス許可]** ブレードで、**[アクセス許可の付与]** を選択し、確認のために **[はい]** をクリックして、このブレードを閉じます。

6. **[設定]** ブレードを再び開き、**[キー]** を選択します。 説明と期間 (1 年、2 年、または期限なし) を指定して、新しいキーを追加します。 次に **[保存]** を選択し、表示されている **[値]** の文字列をコピーします。 この文字列は再び表示されることがなく、取得することもできないため、保存しておくことが重要です。 使用するキーと同様に、保存した値を安全に格納すると同時に値へのアクセスを制限します。
    
    この値は、Set-AIPAuthentication コマンドレットを実行するときの `WebAppKey` パラメーターに使用されます。

7. **[アプリの登録]** ブレードに戻り、**[新しいアプリケーションの登録]** を選択してネイティブ アプリケーションを作成します。 **[作成]** ラベルで次の値を指定して、**[作成]** をクリックします。
    
    - [名前]: **AIPClient**
    
    必要に応じて、別の名前を指定することもできます。 名前は、テナントごとに一意である必要があります。
    
    - アプリケーションの種類: **ネイティブ**
    
    - サインオン URL: **http://localhost**

8. 先ほど作成したアプリケーションを選択します (例: **AIPClient**)。 その後、**[設定]** ブレードで **[プロパティ]** を選択します。 **[プロパティ]** ブレードで **[アプリケーション ID]** の値をコピーし、このブレードを閉じます。
    
    この値は、Set-AIPAuthentication コマンドレットを実行するときの `NativeAppId` パラメーターに使用されます。 後で参照できるように、これを貼り付けて保存します。

9. **[設定]** ブレードで **[必要なアクセス許可]** を選択します。 

10. **[必要なアクセス許可]** ブレードで **[追加]** をクリックし、**[API を選択します]** をクリックします。 検索ボックスに、「**AIPOnBehalfOf**」と入力します。 リスト ボックスでこの値を選択し、**[選択]** をクリックします。

11. **[アクセスの有効化]** ブレードで、**AIPOnBehalfOf** を選択して **[選択]** をクリックし、**[完了]** をクリックします。

12. **[必要なアクセス許可]** ブレードを再び開き、**[アクセス許可の付与]** を選択し、確認のために **[はい]** をクリックして、このブレードを閉じます。
    

2 つのアプリの構成を完了し、パラメーターとして *WebAppId*、*WebAppKey*、*NativeAppId* を指定して [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) を実行するために必要な値を取得しました。 次に例を示します。

`Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "sc9qxh4lmv31GbIBCy36TxEEuM1VmKex5sAdBzABH+M=" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f"`

アカウントで非対話式で文書にラベルを付け、保護するという状況でこのコマンドを実行します。 たとえば、PowerShell スクリプトのユーザー アカウントやサービス アカウントで Azure Information Protection スキャナーを実行します。  

このコマンドを初めて実行するとき、サインインが求められます。それにより、アカウントのアクセス トークンが作成され、%localappdata%\Microsoft\MSIP に安全に保管されます。 この初回サインイン後、コンピューターで非対話式でファイルにラベルを付け、保護できます。 ただし、サービス アカウントを利用してファイルにラベルを付け、保護するとき、そのサービス アカウントで対話式サインインができない場合、次のセクションの指示に従ってください。トークンを利用して認証できるようになります。

### <a name="specify-and-use-the-token-parameter-for-set-aipauthentication"></a>Set-AIPAuthentication の Token パラメーターを指定し、使用する

次の追加の手順と指示に従うと、ファイルにラベルを付け、保護するアカウントの初回対話式サインインを回避できます。 通常、この追加手順は、アカウントに**ローカルでログオンする**権限を与えられないが、**バッチ ジョブとしてログオン**権限が与えられている場合にのみ必要です。 たとえば、Azure Information Protection スキャナーを実行するサービス アカウントなどがこれに該当します。

大まかな手順:

1. ローカル コンピューターで PowerShell スクリプトを作成します。

2. Set-AIPAuthentication を実行してアクセス トークンを取得し、それをクリップボードにコピーします。

3. PowerShell スクリプトを修正し、トークンを追加します。

4. サービス アカウントでファイルにラベルを付け、保護するという状況で PowerShell スクリプトを実行するタスクを作成します。

5. サービス アカウントのトークンが保存されていることを確認し、PowerShell スクリプトを削除します。

#### <a name="step-1-create-a-powershell-script-on-your-local-computer"></a>手順 1: ローカル コンピューターで PowerShell スクリプトを作成します。

1. コンピューターで、Aipauthentication.ps1 という名前の新しい PowerShell スクリプトを作成します。

2. 次のコマンドをコピーし、このスクリプトに貼り付けます。
    
         Set-AIPAuthentication -WebAppId <ID of the "Web app / API" application> -WebAppKey <key value generated in the "Web app / API" application> -NativeAppId <ID of the "Native" application > -Token <token value>

3. 先のセクションの指示に従ってこのコマンドを修正します。**WebAppId**、**WebAppkey**、**NativeAppId** パラメーターに独自の値を指定してください。 今回は **Token** パラメーターの値を指定しません。これは後で指定します。 
    
    例: `Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "sc9qxh4lmv31GbIBCy36TxEEuM1VmKex5sAdBzABH+M=" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f -Token <token value>`
    
#### <a name="step-2-run-set-aipauthentication-to-get-an-access-token-and-copy-it-to-the-clipboard"></a>手順 2: Set-AIPAuthentication を実行してアクセス トークンを取得し、それをクリップボードにコピーします。

1. Windows PowerShell セッションを開始します。

2. スクリプトに指定したものと同じ値を利用し、次のコマンドを実行します。
    
        (Set-AIPAuthentication -WebAppId <ID of the "Web app / API" application>  -WebAppKey <key value generated in the "Web app / API" application> -NativeAppId <ID of the "Native" application >).token | clip
    
    例: `(Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "sc9qxh4lmv31GbIBCy36TxEEuM1VmKex5sAdBzABH+M=" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f").token | clip`

#### <a name="step-3-modify-the-powershell-script-to-supply-the-token"></a>手順 3: PowerShell スクリプトを修正し、トークンを指定します。

1. PowerShell スクリプトで、クリップボードから文字列を貼り付け、ファイルを保存してトークン値を指定します。

2. スクリプトに署名します。 スクリプトに署名 (セキュリティを強化) しない場合は、ラベル付けコマンドを実行するコンピューターで Windows PowerShell を構成する必要があります。 たとえば、**[管理者として実行]** オプションを使用して Windows PowerShell セッションを実行し、`Set-ExecutionPolicy RemoteSigned` と入力します。 ただし、この構成を使用すると、署名されていないすべてのスクリプトは、このコンピューターに保存されている場合に実行できます (セキュリティは低下)。
    
    Windows PowerShell スクリプトへの署名の詳細については、PowerShell のドキュメント ライブラリの「 [about_Signing](/powershell/module/microsoft.powershell.core/about/about_signing) 」を参照してください。

3. ファイルにラベルを付けて保護するコンピューターにこの PowerShell スクリプトをコピーし、自分のコンピューターのオリジナルを削除します。 たとえば、PowerShell スクリプトを Windows Server コンピューターの C:\Scripts\Aipauthentication.ps1 にコピーします。

#### <a name="step-4-create-a-task-that-runs-the-powershell-script"></a>手順 4: PowerShell スクリプトを実行するタスクを作成します。

1. ファイルにラベルを付けて保護するサービス アカウントに**バッチ ジョブとしてログオン**権限が与えられていることを確認します。

2. ファイルにラベルを付けて保護するコンピューターで、Task Scheduler を起動し、新しいタスクを作成します。 ファイルにラベルを付けて保護するサービス アカウントとして実行するようにこのタスクを構成し、**[アクション]** に次の値を構成します。
    
    - **アクション**: `Start a program`
    - **プログラム/スクリプト**: `Powershell.exe`
    - **引数の追加 (省略可能)**: `-NoProfile -WindowStyle Hidden -command "&{C:\Scripts\Aipauthentication.ps1}"` 
    
    引数の行については、例と異なるようであれば、独自のパスとファイル名を指定します。

3. このタスクを手動で実行します。

#### <a name="step-4-confirm-that-the-token-is-saved-and-delete-the-powershell-script"></a>手順 4: トークンが保存されていることを確認し、PowerShell スクリプトを削除します。

1. サービス アカウント プロファイルの %localappdata%\Microsoft\MSIP フォルダーにトークンが保存されていることを確認します。 この値はサービス アカウントによって保護されます。

2. トークン値が含まれている PowerShell スクリプトを削除します (たとえば、Aipauthentication.ps1)。
    
    必要に応じて、タスクを削除します。 トークンの有効期限が切れた場合、この過程を繰り返す必要があります。その場合、構成したタスクを残しておくと便利です。新しい PowerShell スクリプトを新しいトークン値で上書きコピーするとき、すぐに再実行できます。

## <a name="next-steps"></a>次の手順
PowerShell セッションでコマンドレットのヘルプを表示するには `Get-Help <cmdlet name> cmdlet` と入力します。また、最新情報を参照するには -online パラメーターを使用します。 次に例を示します。 

    Get-Help Get-RMSTemplate -online

Azure Information Protection クライアントのサポートに必要な詳細については、以下をご覧ください。

- [カスタマイズ](client-admin-guide-customizations.md)

- [クライアント ファイルおよび使用状況ログの記録](client-admin-guide-files-and-logging.md)

- [ドキュメント追跡](client-admin-guide-document-tracking.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)


