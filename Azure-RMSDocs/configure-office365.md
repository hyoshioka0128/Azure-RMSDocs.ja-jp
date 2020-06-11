---
title: Azure RMS を使用する Office 365 サービスの構成-AIP
description: Azure Information Protection から Azure Rights Management サービスと連携するように Office 365 サービスを構成するための管理者向けの情報と手順です。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0a6ce612-1b6b-4e21-b7fd-bcf79e492c3b
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 4f66b49a6f4ad5ee50efb26849b06492cad89715
ms.sourcegitcommit: f32928f7dcc03111fc72d958cda9933d15065a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/10/2020
ms.locfileid: "84666015"
---
# <a name="office365-configuration-for-online-services-to-use-the-azure-rights-management-service"></a>Office 365: Azure Rights Management サービスを使用するためのオンラインサービスの構成

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

次のセクションでは、Azure Information Protection から Azure Rights Management サービスを使用するように Exchange Online、Microsoft SharePoint、および Microsoft OneDrive を構成する方法について説明します。

## <a name="exchangeonline-irm-configuration"></a>Exchange Online: IRM 構成
Exchange Online が Azure Rights Management サービスと連携する方法の詳細については、「 [Office アプリケーションおよびサービスが azure Rights Management をサポートする方法](office-apps-services-support.md)」の「 [Exchange Online と exchange Server](office-apps-services-support.md#exchange-online-and-exchange-server) 」セクションを参照してください。

Exchange Online で既に Azure Rights Management サービスの使用が有効になっている可能性があります。 これを確認するには、次のコマンドを実行します。

1. コンピューターで Exchange Online 用 Windows PowerShell を初めて使用する場合は、署名済みスクリプトを実行するように Windows PowerShell を構成する必要があります。 [**管理者として実行**] オプションを使用して Windows PowerShell セッションを開始し、次のように入力します。
    
        Set-ExecutionPolicy RemoteSigned
    
    **Y** を押して確認します。

2. Windows PowerShell セッションで、リモート シェル アクセスが有効になっているアカウントを使用して Exchange Online にサインインします。 既定では、Exchange Online で作成されたすべてのアカウントではリモートシェルアクセスが有効になっていますが、[ユーザー &lt; useridentity &gt; -remotepowershellenabled](https://technet.microsoft.com/library/jj984292%28v=exchg.160%29.aspx)コマンドを使用して無効 (および有効) にすることができます。
    
    サインインするには、最初に次のように入力します。
    
        $Cred = Get-Credential
   
    次に **[Windows PowerShell 資格情報要求]** ダイアログ ボックスで、Office 365 のユーザー名とパスワードを入力します。

3. 最初に次のように変数を設定して、Exchange Online サービスに接続します。
    
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
    
    次に、次のコマンドを実行します。
    
        Import-PSSession $Session

4. [Get-IRMConfiguration](https://technet.microsoft.com/library/dd776120(v=exchg.160).aspx) コマンドを実行して、保護サービスでお使いの Exchange Online 構成を表示します。
    
        Get-IRMConfiguration
    
    出力で、**AzureRMSLicensingEnabled** の値を探します。
    
    - AzureRMSLicensingEnabled が **True** に設定されている場合は、Azure Rights Management サービスに対して Exchange Online が既に有効になっています。 
    
    - AzureRMSLicensingEnabled が **False** に設定されている場合は、Azure Rights Management サービスに対して Exchange Online を有効にするコマンド `Set-IRMConfiguration -AzureRMSLicensingEnabled $true` を実行します

5. Exchange Online が正しく構成されているかどうかをテストするには、次のコマンドを実行します。
    ```
    Test-IRMConfiguration -Sender <user email address>
    ```
    例: <strong>Test-IRMConfiguration -Sender  adams@contoso.com</strong>
    
    このコマンドは、サービスへの接続の確認、構成の取得、URI、ライセンス、および任意のテンプレートの取得を含む一連のチェックを実行します。 Windows PowerShell セッションでは、これらのチェックのそれぞれの結果、およびすべてのチェックをパスした場合は最後にも、その結果が表示されます。 **全体的な結果:パス**

Azure Rights Management サービスを使用するように Exchange Online を有効にすると、情報保護を自動的に適用する機能を構成できます。[メール フロー ルール](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8)、[データ損失防止 (DLP) ポリシー](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx)、[保護されたボイス メール](https://technet.microsoft.com/library/dn198211%28v=exchg.150%29.aspx) (ユニファイド メッセージング) などです。

## <a name="sharepoint-in-microsoft-365-and-onedrive-irm-configuration"></a>Microsoft 365 の SharePoint と OneDrive: IRM の構成

SharePoint IRM が Azure Rights Management サービスと連携する方法の詳細については、このドキュメントの「 **Rights Management 保護**」セクションの「 [Microsoft 365 および Sharepoint Server の sharepoint](office-apps-services-support.md#sharepoint-in-microsoft-365-and-sharepoint-server) 」を参照してください。

Azure Rights Management サービスをサポートするように Microsoft 365 と OneDrive で SharePoint を構成するには、sharepoint 管理センターを使用して、sharepoint の information Rights Management (IRM) サービスを最初に有効にする必要があります。 その後、サイト所有者は SharePoint リストとドキュメントライブラリを IRM で保護することができ、ユーザーは OneDrive ライブラリを IRM で保護することができます。これにより、そこに保存され、他のユーザーと共有されたドキュメントは、Azure Rights Management サービスによって自動的に保護されます。

> [!NOTE]
> IRM で保護された SharePoint 用ライブラリ (Microsoft 365 および OneDrive) では、新しい OneDrive 同期クライアント (OneDrive.exe) の最新バージョンと、 [Microsoft ダウンロードセンターの RMS クライアント](https://www.microsoft.com/download/details.aspx?id=38396)のバージョンが必要です。 Azure Information Protection クライアントをインストールした場合でも、このバージョンの RMS クライアントをインストールします。 このデプロイ シナリオについて詳しくは、「[エンタープライズ環境に新しい OneDrive 同期クライアントを展開する](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668)」をご覧ください。

SharePoint の information rights management (IRM) サービスを有効にするには、Office ドキュメントの次の手順を参照してください。

- [SharePoint 管理センターで情報 Rights Management (IRM) を設定する](https://docs.microsoft.com/microsoft-365/compliance/set-up-irm-in-sp-admin-center)

この構成は、Office 365 管理者が行います。

### <a name="configuring-irm-for-libraries-and-lists"></a>ライブラリおよびリスト用の IRM の構成
SharePoint で IRM サービスを有効にすると、サイト所有者は、SharePoint ドキュメント ライブラリとリストを IRM で保護できるようになります。 手順については、次の Office の Web サイトを参照してください。

- [Information Rights Management をリストまたはライブラリに適用する](https://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)

この構成は、SharePoint のサイト管理者が行います。

### <a name="configuring-irm-for-onedrive"></a>OneDrive 用の IRM の構成
SharePoint 用の IRM サービスを有効にした後、ユーザーの OneDrive ドキュメントライブラリまたは個々のフォルダーを Rights Management 保護用に構成できます。 ユーザーは、OneDrive の Web サイトから自分でこれを構成できます。 管理者は SharePoint 管理センターを使用してユーザーにこの保護を構成することはできませんが、Windows PowerShell を使用してこれを行うことができます。

> [!NOTE]
> OneDrive の構成の詳細については、Office のドキュメント「 [office 365 での onedrive のセットアップ](https://support.office.com/article/Set-up-OneDrive-for-Business-in-Office-365-3e21f8f0-e0a1-43be-aa3e-8c0236bf11bb)」を参照してください。

#### <a name="configuration-for-users"></a>ユーザー用の構成
ユーザーが各自のビジネスファイルを保護するように OneDrive を構成できるように、次の手順に従ってください。

1. 職場または学校のアカウントで Office 365 にサインインし、[OneDrive の Web サイト](https://admin.microsoft.com/onedrive)に移動します。

2. ナビゲーション ウィンドウの下部の、**[従来の OneDrive に戻す]** を選択します。

3. **[設定]** アイコンを選択します。 **[設定]** ウィンドウの**リボン**が **[オフ]** に設定されている場合、この設定を選択し、リボンをオンにします。

4. 保護するすべての OneDrive ファイルを構成するには、リボンから [**ライブラリ**] タブを選択し、[**ライブラリの設定**] を選択します。

5. **[ドキュメント > 設定]** ページの **[権限と管理]** セクションの **[Information Rights Management]** を選択します。

6. **[Information Rights Management 設定]** ページで **[ダウンロード時にこのライブラリへの権限を制限する]** チェック ボックスをオンにします。 このアクセス許可に名前を付け、説明を指定し、オプションで **[オプションの表示]** をクリックしてオプションを構成し、**[OK]** をクリックします。

    構成オプションの詳細については、Office のドキュメント、「[Information Rights Management をリストまたはライブラリに適用する](https://support.office.com/article/Apply-Information-Rights-Management-to-a-list-or-library-3bdb5c4e-94fc-4741-b02f-4e7cc3c54aa1)」で手順を参照してください。

この構成では、管理者ではなくユーザーが OneDrive ファイルを IRM で保護するので、ファイルを保護する利点とその方法についてユーザーを教育します。 たとえば、OneDrive からドキュメントを共有する場合、ファイルの名前を変更して別の場所にコピーしたとしても、承認されたユーザーのみが、構成した制限付きでアクセスできます。

#### <a name="configuration-for-administrators"></a>管理者用の構成
SharePoint 管理センターを使用してユーザーの OneDrive 用に IRM を構成することはできませんが、Windows PowerShell を使用してこれを行うことができます。 これらのライブラリで IRM を有効にするには、次の手順を実行します。

1. [SharePoint クライアントコンポーネント SDK](https://www.microsoft.com/download/details.aspx?id=42038)をダウンロードしてインストールします。

2. [SharePoint 管理シェル](https://www.microsoft.com/download/details.aspx?id=35588)をダウンロードしてインストールします。

3. 次のスクリプトの内容をコピーし、ファイルをコンピューター上で Set-irmononedriveforbusiness.ps1 と命名します。

   *&#42;&#42;免責事項&#42;&#42;*: このサンプル スクリプトは、Microsoft のいかなる標準サポート プログラムまたはサービスでもサポートされていません。 サンプル スクリプトは現状有姿で提供され、いかなる保証も行いません。

   ```
   # Requires Windows PowerShell version 3

   <#
     Description:

       Configures IRM policy settings for OneDrive and can also be used for SharePoint libraries and lists

    Script Installation Requirements:

      SharePoint Client Components SDK
      https://www.microsoft.com/download/details.aspx?id=42038

      SharePoint Management Shell
      https://www.microsoft.com/download/details.aspx?id=35588

   ======
   #>

   # URL will be in the format https://<tenant-name>-admin.sharepoint.com
   $sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

   $tenantAdmin = "admin@contoso.com"

   $webUrls = @("https://contoso-my.sharepoint.com/personal/user1_contoso_com",
                "https://contoso-my.sharepoint.com/personal/user2_contoso_com",
                "https://contoso-my.sharepoint.com/personal/user3_contoso_com")

   <# As an alternative to specifying the URLs as an array, you can import them from a CSV file (no header, single value per row).
      Then, use: $webUrls = Get-Content -Path "File_path_and_name.csv"

   #>

   $listTitle = "Documents"

   function Load-SharePointOnlineClientComponentAssemblies
   {
       [cmdletbinding()]
       param()

       process
       {
           # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
           try
           {
               Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               return $true
           }
           catch
           {
               if($_.Exception.Message -match "Could not load file or assembly")
               {
                   Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=42038"
               }
               else
               {
                   Write-Error -Exception $_.Exception
               }
               return $false
           }
       }
   }

   function Load-SharePointOnlineModule
   {
       [cmdletbinding()]
       param()

       process
       {
           do
           {
               # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
               $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

               if(-not $spoModule)
               {
                   try
                   {
                       Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                       return $true
                   }
                   catch
                   {
                       if($_.Exception.Message -match "Could not load file or assembly")
                       {
                           Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=35588"
                       }
                       else
                       {
                           Write-Error -Exception $_.Exception
                       }
                       return $false
                   }
               }
               else
               {
                   return $true
               }
           }
           while(-not $spoModule)
       }
   }

   function Set-IrmConfiguration
   {
       [cmdletbinding()]
       param(
           [parameter(Mandatory=$true)][Microsoft.SharePoint.Client.List]$List,
           [parameter(Mandatory=$true)][string]$PolicyTitle,
           [parameter(Mandatory=$true)][string]$PolicyDescription,
           [parameter(Mandatory=$false)][switch]$IrmReject,
           [parameter(Mandatory=$false)][DateTime]$ProtectionExpirationDate,
           [parameter(Mandatory=$false)][switch]$DisableDocumentBrowserView,
           [parameter(Mandatory=$false)][switch]$AllowPrint,
           [parameter(Mandatory=$false)][switch]$AllowScript,
           [parameter(Mandatory=$false)][switch]$AllowWriteCopy,
           [parameter(Mandatory=$false)][int]$DocumentAccessExpireDays,
           [parameter(Mandatory=$false)][int]$LicenseCacheExpireDays,
           [parameter(Mandatory=$false)][string]$GroupName
       )

       process
       {
           Write-Verbose "Applying IRM Configuration on '$($List.Title)'"

           # reset the value to the default settings
           $list.InformationRightsManagementSettings.Reset()

           $list.IrmEnabled = $true

           # IRM Policy title and description

               $list.InformationRightsManagementSettings.PolicyTitle       = $PolicyTitle
               $list.InformationRightsManagementSettings.PolicyDescription = $PolicyDescription

           # Set additional IRM library settings

               # Do not allow users to upload documents that do not support IRM
               $list.IrmReject = $IrmReject.IsPresent

               $parsedDate = Get-Date
               if([DateTime]::TryParse($ProtectionExpirationDate, [ref]$parsedDate))
               {
                   # Stop restricting access to the library at <date>
                   $list.IrmExpire = $true
                   $list.InformationRightsManagementSettings.DocumentLibraryProtectionExpireDate = $ProtectionExpirationDate
               }

               # Prevent opening documents in the browser for this Document Library
               $list.InformationRightsManagementSettings.DisableDocumentBrowserView = $DisableDocumentBrowserView.IsPresent

           # Configure document access rights

               # Allow viewers to print
               $list.InformationRightsManagementSettings.AllowPrint = $AllowPrint.IsPresent

               # Allow viewers to run script and screen reader to function on downloaded documents
               $list.InformationRightsManagementSettings.AllowScript = $AllowScript.IsPresent

               # Allow viewers to write on a copy of the downloaded document
               $list.InformationRightsManagementSettings.AllowWriteCopy = $AllowWriteCopy.IsPresent

               if($DocumentAccessExpireDays)
               {
                   # After download, document access rights will expire after these number of days (1-365)
                   $list.InformationRightsManagementSettings.EnableDocumentAccessExpire = $true
                   $list.InformationRightsManagementSettings.DocumentAccessExpireDays   = $DocumentAccessExpireDays
               }

           # Set group protection and credentials interval

               if($LicenseCacheExpireDays)
               {
                   # Users must verify their credentials using this interval (days)
                   $list.InformationRightsManagementSettings.EnableLicenseCacheExpire = $true
                   $list.InformationRightsManagementSettings.LicenseCacheExpireDays   = $LicenseCacheExpireDays
               }

               if($GroupName)
               {
                   # Allow group protection. Default group:
                   $list.InformationRightsManagementSettings.EnableGroupProtection = $true
                   $list.InformationRightsManagementSettings.GroupName             = $GroupName
               }
       }
       end
       {
           if($list)
           {
               Write-Verbose "Committing IRM configuration settings on '$($list.Title)'"
               $list.InformationRightsManagementSettings.Update()
               $list.Update()
               $script:clientContext.Load($list)
               $script:clientContext.ExecuteQuery()
           }
       }
   }

   function Get-CredentialFromCredentialCache
   {
       [cmdletbinding()]
       param([string]$CredentialName)

       #if( Test-Path variable:\global:CredentialCache )
       if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
       {
           if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
           {
               Write-Verbose "Credential Cache Hit: $CredentialName"
               return $global:O365TenantAdminCredentialCache[$CredentialName]
           }
       }
       Write-Verbose "Credential Cache Miss: $CredentialName"
       return $null
   }

   function Add-CredentialToCredentialCache
   {
       [cmdletbinding()]
       param([System.Management.Automation.PSCredential]$Credential)

       if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
       {
           Write-Verbose "Initializing the Credential Cache"
           $global:O365TenantAdminCredentialCache = @{}
       }

       Write-Verbose "Adding Credential to the Credential Cache"
       $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
   }

   # load the required assemblies and Windows PowerShell modules

       if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

   # Add the credentials to the client context and SharePoint service connection

       # check for cached credentials to use
       $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

       if(-not $o365TenantAdminCredential)
       {
           # when credentials are not cached, prompt for the tenant admin credentials
           $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

           if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
           {
               Write-Error -Message "Could not validate the supplied tenant admin credentials"
               return
           }

           # add the credentials to the cache
           Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
       }

   # connect to Office365 first, required for SharePoint cmdlets to run

       Connect-SPOService -Url $sharepointAdminCenterUrl -Credential $o365TenantAdminCredential

   # enumerate each of the specified site URLs

       foreach($webUrl in $webUrls)
       {
           $grantedSiteCollectionAdmin = $false

           try
           {
               # establish the client context and set the credentials to connect to the site
               $script:clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl)
               $script:clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

               # initialize the site and web context
               $script:clientContext.Load($script:clientContext.Site)
               $script:clientContext.Load($script:clientContext.Web)
               $script:clientContext.ExecuteQuery()

               # load and ensure the tenant admin user account if present on the target SharePoint site
               $tenantAdminUser = $script:clientContext.Web.EnsureUser($o365TenantAdminCredential.UserName)
               $script:clientContext.Load($tenantAdminUser)
               $script:clientContext.ExecuteQuery()

               # check if the tenant admin is a site admin
               if( -not $tenantAdminUser.IsSiteAdmin )
               {
                   try
                   {
                       # grant the tenant admin temporary admin rights to the site collection
                       Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $true | Out-Null
                       $grantedSiteCollectionAdmin = $true
                   }
                   catch
                   {
                       Write-Error $_.Exception
                       return
                   }
               }

               try
               {
                   # load the list orlibrary using CSOM

                   $list = $null
                   $list = $script:clientContext.Web.Lists.GetByTitle($listTitle)
                   $script:clientContext.Load($list)
                   $script:clientContext.ExecuteQuery()

                   # **************  ADMIN INSTRUCTIONS  **************
                   # If necessary, modify the following Set-IrmConfiguration parameters to match your required values
                   # The supplied options and values are for example only
                   # Example that shows the Set-IrmConfiguration command with all parameters: Set-IrmConfiguration -List $list -PolicyTitle "Protected Files" -PolicyDescription "This policy restricts access to authorized users" -IrmReject -ProtectionExpirationDate $(Get-Date).AddDays(180) -DisableDocumentBrowserView -AllowPrint -AllowScript -AllowWriteCopy -LicenseCacheExpireDays 25 -DocumentAccessExpireDays 90

                   Set-IrmConfiguration -List $list -PolicyTitle "Protected Files" -PolicyDescription "This policy restricts access to authorized users"  
               }
               catch
               {
                   Write-Error -Message "Error setting IRM configuration on site: $webUrl.`nError Details: $($_.Exception.ToString())"
               }
          }
          finally
          {
               if($grantedSiteCollectionAdmin)
               {
                   # remove the temporary admin rights to the site collection
                   Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $false | Out-Null
               }
          }
       }

   Disconnect-SPOService -ErrorAction SilentlyContinue
   ```

4. スクリプトを確認し、次の変更を行います。

   1. `$sharepointAdminCenterUrl` を検索し、値の例を自身の SharePoint 管理センター URL に置き換えます。

      この値は、SharePoint 管理センターにアクセスしたときのベース URL として表示され、https://<em> &lt; tenant_name &gt; </em>-admin.sharepoint.com という形式になっています。

      たとえば、テナント名が "contoso" の場合は、次のように指定します。**https://contoso-admin.sharepoint.com**

   2. `$tenantAdmin` を検索し、値の例を自身の Office 365 の完全修飾グローバル管理者アカウントに置き換えます。

      この値は、グローバル管理者として Microsoft 365 管理センターにサインインするために使用するものと同じであり、user_name@ の* &lt; テナントドメイン名 &gt; *.com という形式になります。

      たとえば、"contoso.com" テナントドメインの Office 365 グローバル管理者のユーザー名が "admin" である場合は、次のように指定します。<strong>admin@contoso.com</strong>

   3. を検索 `$webUrls` し、例の値をユーザーの OneDrive Web url に置き換え、必要な数だけエントリを追加または削除します。

      または、構成する必要のあるすべての URL を含む .CSV ファイルをインポートする、スクリプト内のこの配列を置き換える方法のコメントを確認します。  自動的に検索し、この .CSV ファイルに入力する URL を抽出する、サンプル スクリプトがもう 1 つ用意されています。 これを行う準備ができたら、追加のスクリプトを使用して[OneDrive のすべての url をに出力します。](#additional-script-to-output-all-onedrive-urls-to-a-csv-file)これらの手順の直後にある CSV ファイルセクション。

      ユーザーの OneDrive の web URL の形式は次のとおりです: https://<em> &lt; tenant name &gt; </em>-my.sharepoint.com/personal/* &lt; user_name &gt; *_* &lt; テナント名 &gt; *_com

      たとえば、contoso テナントのユーザーのユーザー名が "rシム one" の場合、次のように指定します。**https://contoso-my.sharepoint.com/personal/rsimone_contoso_com**

   4. このスクリプトを使用して OneDrive を構成しているので、変数の**ドキュメント**の値は変更しないで `$listTitle` ください。

   5. `ADMIN INSTRUCTIONS` を検索します。 このセクションに変更を加えないと、ユーザーの OneDrive は、"保護されたファイル" というポリシーのタイトルと、"このポリシーは、承認されたユーザーへのアクセスを制限する" という説明で IRM 用に構成されます。  その他の IRM オプションは設定されません。これは、おそらく多くの環境に適しています。 ただし、提示されたポリシー タイトルと説明を変更したり、環境に適したその他の IRM オプションも追加できます。 Set-IrmConfiguration コマンド用に独自のパラメーターのセットを構築する助けとなる、スクリプト内のコメント例を参照してください。

5. スクリプトを保存し、署名します。 スクリプトに署名しない場合 (より安全性は高いです)、Windows PowerShell で署名されていないスクリプトを実行できるよう、コンピューターが構成されている必要があります。 これを行うには、Windows PowerShell セッションを **[管理者として実行]** オプションを使用して実行し、「**Set-executionpolicy Unrestricted**」と入力します。 ただし、この構成では、署名されていないすべてのスクリプトが実行されます (セキュリティは低いです)。

   Windows PowerShell スクリプトの署名の詳細については、PowerShell のドキュメント ライブラリの「[about_Signing](https://technet.microsoft.com/library/hh847874.aspx)」を参照してください。

6. スクリプトを実行し、求められたら Office 365 管理者アカウントのパスワードを指定します。 スクリプトを変更し、同じ Windows PowerShell セッションでそれを実行した場合は、資格情報は求められません。

> [!TIP]
> また、このスクリプトを使用して、SharePoint ライブラリ用に IRM を構成することもできます。 この構成では、追加オプション [**IRM をサポートしないドキュメントのアップロードをユーザーに許可しない**] を有効にして、保護されたドキュメントだけがライブラリに含まれるようにできます。    これを実行するには、スクリプトの Set-IrmConfiguration コマンドに `-IrmReject` パラメーターを追加します。
>
> また、 `$webUrls` 変数 (たとえば、 **https: \/ /contoso.sharepoint.com**) と `$listTitle` 変数 (たとえば、 **$Reports**) も変更する必要があります。

ユーザーの OneDrive ライブラリに対して IRM を無効にする必要がある場合は、「 [onedrive 用に irm を無効にするスクリプト](#script-to-disable-irm-for-onedrive)」セクションを参照してください。

##### <a name="additional-script-to-output-all-onedrive-urls-to-a-csv-file"></a>すべての OneDrive Url をに出力する追加のスクリプト。CSV ファイル
上記の手順4c では、次の Windows PowerShell スクリプトを使用して、すべてのユーザーの OneDrive ライブラリの Url を抽出できます。これを確認し、必要に応じて編集して、メインスクリプトにインポートできます。

このスクリプトでは、 [Sharepoint クライアントコンポーネント SDK](https://www.microsoft.com/download/details.aspx?id=42038)と[sharepoint 管理シェル](https://www.microsoft.com/download/details.aspx?id=35588)も必要です。 同じ手順を実行して、コピーと貼り付けを行い、ファイル (例: "Report-onedriveforbusinesssiteinfo.ps1") をローカルに保存し、前と同様に `$sharepointAdminCenterUrl` と `$tenantAdmin` の値を変更して、スクリプトを実行します。

*&#42;&#42;免責事項&#42;&#42;*: このサンプル スクリプトは、Microsoft のいかなる標準サポート プログラムまたはサービスでもサポートされていません。 サンプル スクリプトは現状有姿で提供され、いかなる保証も行いません。

```
# Requires Windows PowerShell version 3

<#
  Description:

    Queries the search service of an Office 365 tenant to retrieve all OneDrive sites.  
    Details of the discovered sites are written to a .CSV file (by default,"OneDriveForBusinessSiteInfo_<date>.csv").

 Script Installation Requirements:

   SharePoint Client Components SDK
   https://www.microsoft.com/download/details.aspx?id=42038

   SharePoint Management Shell
   https://www.microsoft.com/download/details.aspx?id=35588

======
#>

# URL will be in the format https://<tenant-name>-admin.sharepoint.com
$sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

$tenantAdmin = "admin@contoso.onmicrosoft.com"                           

$reportName = "OneDriveForBusinessSiteInfo_$((Get-Date).ToString("yyyy-MM-dd_hh.mm.ss")).csv"

$oneDriveForBusinessSiteUrls= @()
$resultsProcessed = 0

function Load-SharePointOnlineClientComponentAssemblies
{
    [cmdletbinding()]
    param()

    process
    {
        # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
        try
        {
            Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            return $true
        }
        catch
        {
            if($_.Exception.Message -match "Could not load file or assembly")
            {
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=42038"
            }
            else
            {
                Write-Error -Exception $_.Exception
            }
            return $false
        }
    }
}

function Load-SharePointOnlineModule
{
    [cmdletbinding()]
    param()

    process
    {
        do
        {
            # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
            $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

            if(-not $spoModule)
            {
                try
                {
                    Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                    return $true
                }
                catch
                {
                    if($_.Exception.Message -match "Could not load file or assembly")
                    {
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=35588"
                    }
                    else
                    {
                        Write-Error -Exception $_.Exception
                    }
                    return $false
                }
            }
            else
            {
                return $true
            }
        }
        while(-not $spoModule)
    }
}

function Get-CredentialFromCredentialCache
{
    [cmdletbinding()]
    param([string]$CredentialName)

    #if( Test-Path variable:\global:CredentialCache )
    if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
    {
        if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
        {
            Write-Verbose "Credential Cache Hit: $CredentialName"
            return $global:O365TenantAdminCredentialCache[$CredentialName]
        }
    }
    Write-Verbose "Credential Cache Miss: $CredentialName"
    return $null
}

function Add-CredentialToCredentialCache
{
    [cmdletbinding()]
    param([System.Management.Automation.PSCredential]$Credential)

    if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
    {
        Write-Verbose "Initializing the Credential Cache"
        $global:O365TenantAdminCredentialCache = @{}
    }

    Write-Verbose "Adding Credential to the Credential Cache"
    $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
}

# load the required assemblies and Windows PowerShell modules

    if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

# Add the credentials to the client context and SharePoint service connection

    # check for cached credentials to use
    $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

    if(-not $o365TenantAdminCredential)
    {
        # when credentials are not cached, prompt for the tenant admin credentials
        $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

        if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
        {
            Write-Error -Message "Could not validate the supplied tenant admin credentials"
            return
        }

        # add the credentials to the cache
        Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
    }

# establish the client context and set the credentials to connect to the site

    $clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($sharepointAdminCenterUrl)
    $clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

# run a query against the Office 365 tenant search service to retrieve all OneDrive URLs

    do
    {
        # build the query object
        $query = New-Object Microsoft.SharePoint.Client.Search.Query.KeywordQuery($clientContext)
        $query.TrimDuplicates        = $false
        $query.RowLimit              = 500
        $query.QueryText             = "SPSiteUrl:'/personal/' AND contentclass:STS_Site"
        $query.StartRow              = $resultsProcessed
        $query.TotalRowsExactMinimum = 500000

        # run the query
        $searchExecutor = New-Object Microsoft.SharePoint.Client.Search.Query.SearchExecutor($clientContext)
        $queryResults = $searchExecutor.ExecuteQuery($query)
        $clientContext.ExecuteQuery()

        # enumerate the search results and store the site URLs
        $queryResults.Value[0].ResultRows | % {
            $oneDriveForBusinessSiteUrls += $_.Path
            $resultsProcessed++
        }
    }
    while($resultsProcessed -lt $queryResults.Value.TotalRows)

$oneDriveForBusinessSiteUrls | Out-File -FilePath $reportName
```

##### <a name="script-to-disable-irm-for-onedrive"></a>OneDrive の IRM を無効にするスクリプト
ユーザーの OneDrive で IRM を無効にする必要がある場合は、次のサンプルスクリプトを使用します。

このスクリプトでは、 [Sharepoint クライアントコンポーネント SDK](https://www.microsoft.com/download/details.aspx?id=42038)と[sharepoint 管理シェル](https://www.microsoft.com/download/details.aspx?id=35588)も必要です。 内容をコピーして貼り付け、ファイル (例: "Disable-IRMOnOneDriveForBusiness.ps1") をローカルに保存し、`$sharepointAdminCenterUrl` と `$tenantAdmin` の値を変更します。 OneDrive の Url を手動で指定するか、前のセクションのスクリプトを使用してインポートし、スクリプトを実行できるようにします。

*&#42;&#42;免責事項&#42;&#42;*: このサンプル スクリプトは、Microsoft のいかなる標準サポート プログラムまたはサービスでもサポートされていません。 サンプル スクリプトは現状有姿で提供され、いかなる保証も行いません。

```
# Requires Windows PowerShell version 3

<#
  Description:

    Disables IRM for OneDrive and can also be used for SharePoint libraries and lists

 Script Installation Requirements:

   SharePoint Client Components SDK
   https://www.microsoft.com/download/details.aspx?id=42038

   SharePoint Management Shell
   https://www.microsoft.com/download/details.aspx?id=35588

======
#>

$sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

$tenantAdmin = "admin@contoso.com"

$webUrls = @("https://contoso-my.sharepoint.com/personal/user1_contoso_com",
             "https://contoso-my.sharepoint.com/personal/user2_contoso_com",
             "https://contoso-my.sharepoint.com/personal/person3_contoso_com")

<# As an alternative to specifying the URLs as an array, you can import them from a CSV file (no header, single value per row).
   Then, use: $webUrls = Get-Content -Path "File_path_and_name.csv"

#>

$listTitle = "Documents"

function Load-SharePointOnlineClientComponentAssemblies
{
    [cmdletbinding()]
    param()

    process
    {
        # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
        try
        {
            Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            return $true
        }
        catch
        {
            if($_.Exception.Message -match "Could not load file or assembly")
            {
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=42038"
            }
            else
            {
                Write-Error -Exception $_.Exception
            }
            return $false
        }
    }
}

function Load-SharePointOnlineModule
{
    [cmdletbinding()]
    param()

    process
    {
        do
        {
            # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
            $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

            if(-not $spoModule)
            {
                try
                {
                    Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                    return $true
                }
                catch
                {
                    if($_.Exception.Message -match "Could not load file or assembly")
                    {
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=35588"
                    }
                    else
                    {
                        Write-Error -Exception $_.Exception
                    }
                    return $false
                }
            }
            else
            {
                return $true
            }
        }
        while(-not $spoModule)
    }
}

function Remove-IrmConfiguration
{
    [cmdletbinding()]
    param(
        [parameter(Mandatory=$true)][Microsoft.SharePoint.Client.List]$List
    )

    process
    {
        Write-Verbose "Disabling IRM Configuration on '$($List.Title)'"

        $List.IrmEnabled = $false
        $List.IrmExpire  = $false
        $List.IrmReject  = $false
        $List.InformationRightsManagementSettings.Reset()
    }
    end
    {
        if($List)
        {
            Write-Verbose "Committing IRM configuration settings on '$($list.Title)'"
            $list.InformationRightsManagementSettings.Update()
            $list.Update()
            $script:clientContext.Load($list)
            $script:clientContext.ExecuteQuery()
        }
    }
}

function Get-CredentialFromCredentialCache
{
    [cmdletbinding()]
    param([string]$CredentialName)

    #if( Test-Path variable:\global:CredentialCache )
    if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
    {
        if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
        {
            Write-Verbose "Credential Cache Hit: $CredentialName"
            return $global:O365TenantAdminCredentialCache[$CredentialName]
        }
    }
    Write-Verbose "Credential Cache Miss: $CredentialName"
    return $null
}

function Add-CredentialToCredentialCache
{
    [cmdletbinding()]
    param([System.Management.Automation.PSCredential]$Credential)

    if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
    {
        Write-Verbose "Initializing the Credential Cache"
        $global:O365TenantAdminCredentialCache = @{}
    }

    Write-Verbose "Adding Credential to the Credential Cache"
    $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
}

# load the required assemblies and Windows PowerShell modules

    if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

# Add the credentials to the client context and SharePoint service connection

    # check for cached credentials to use
    $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

    if(-not $o365TenantAdminCredential)
    {
        # when credentials are not cached, prompt for the tenant admin credentials
        $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

        if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
        {
            Write-Error -Message "Could not validate the supplied tenant admin credentials"
            return
        }

        # add the credentials to the cache
        Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
    }

# connect to Office365 first, required for SharePoint cmdlets to run

    Connect-SPOService -Url $sharepointAdminCenterUrl -Credential $o365TenantAdminCredential

# enumerate each of the specified site URLs

    foreach($webUrl in $webUrls)
    {
        $grantedSiteCollectionAdmin = $false

        try
        {
            # establish the client context and set the credentials to connect to the site
            $script:clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl)
            $script:clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

            # initialize the site and web context
            $script:clientContext.Load($script:clientContext.Site)
            $script:clientContext.Load($script:clientContext.Web)
            $script:clientContext.ExecuteQuery()

            # load and ensure the tenant admin user account if present on the target SharePoint site
            $tenantAdminUser = $script:clientContext.Web.EnsureUser($o365TenantAdminCredential.UserName)
            $script:clientContext.Load($tenantAdminUser)
            $script:clientContext.ExecuteQuery()

            # check if the tenant admin is a site admin
            if( -not $tenantAdminUser.IsSiteAdmin )
            {
                try
                {
                    # grant the tenant admin temporary admin rights to the site collection
                    Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $true | Out-Null
                    $grantedSiteCollectionAdmin = $true
                }
                catch
                {
                    Write-Error $_.Exception
                    return
                }
            }

            try
            {
                # load the list orlibrary using CSOM

                $list = $null
                $list = $script:clientContext.Web.Lists.GetByTitle($listTitle)
                $script:clientContext.Load($list)
                $script:clientContext.ExecuteQuery()

               Remove-IrmConfiguration -List $list                 
            }
            catch
            {
                Write-Error -Message "Error setting IRM configuration on site: $webUrl.`nError Details: $($_.Exception.ToString())"
            }
       }
       finally
       {
            if($grantedSiteCollectionAdmin)
            {
                # remove the temporary admin rights to the site collection
                Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $false | Out-Null
            }
       }
    }

Disconnect-SPOService -ErrorAction SilentlyContinue
```

