---
title: "AIP から Azure RMS を使用するための Office 365 クライアントとオンライン サービスの構成"
description: "Azure Information Protection から Azure AD Rights Management サービスを使用するために管理者が Office 365 を設定するための情報および手順です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/18/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0a6ce612-1b6b-4e21-b7fd-bcf79e492c3b
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 367c41d91d4e4250370016bdff80bd9e2e366924
ms.sourcegitcommit: e21fb3385de6f0e251167e5dc973e90f0e7f2bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/01/2018
---
# <a name="office-365-configuration-for-clients-and-online-services-to-use-the-azure-rights-management-service"></a>Office 365: クライアントおよびオンライン サービスで Azure Rights Management サービスを使用するための構成

>*適用対象: Azure Information Protection、Office 365*

Office 365 は、Azure Information Protection の Azure AD Rights Management サービスをネイティブでサポートしているため、Word、Excel、PowerPoint、Outlook、および Outlook on the web などのアプリケーションで、Information Rights Management (IRM) 機能をサポートするために、クライアント コンピューターを構成する必要はありません。 ユーザーがしなければならないのは、自身の [!INCLUDE[o365_1](../includes/o365_1_md.md)] 資格情報を使用して Office アプリケーションにサインインすることだけです。 その後、ファイルおよびメールを保護し、他のユーザーが保護しているファイルやメールを使用することができます。

ただし、これらのアプリケーションに Azure Information Protection クライアントを補って、ユーザーが Office アドインと、その他のファイルの種類のサポートのメリットを受けることができるようにすることをお勧めします。 詳細については、「[Azure Information Protection クライアント: クライアントのインストールと構成](configure-client.md)」を参照してください。

## <a name="exchange-online-irm-configuration"></a>Exchange Online: IRM の構成
Azure Rights Management サービスと Exchange Online IRM の動作のしくみについては、「**Understand & Explore**」 (概要と詳細) セクションの「[Exchange Online and Exchange Server](../understand-explore/office-apps-services-support.md#exchange-online-and-exchange-server)」 (Exchange Online と Exchange Server) を参照してください。

Azure Rights Management サービスを使用するように Exchange Online を構成する方法については、「[Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)」 (Azure Information Protection 上に Office 365 の新しいメッセージ暗号化機能を設定する) を参照してください。

Azure Rights Management サービスから信頼された発行ドメイン (TPD) をインポートして IRM 用に Exchange Online を既に構成している場合、Exchange Online で新機能を有効にするには同じ一連の手順を実行します。

Azure Rights Management サービスを使用するように Exchange Online を構成したら、自動的に情報を保護する、[トランスポート ルール](https://technet.microsoft.com/library/dd302432.aspx)、[データ損失防止 (DLP) ポリシー](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx)、および[保護されているボイス メール](https://technet.microsoft.com/library/dn198211%28v=exchg.150%29.aspx) (ユニファイド メッセージング) などの機能を構成できるようになります。

## <a name="sharepoint-online-and-onedrive-for-business-irm-configuration"></a>SharePoint Online と OneDrive for Business: IRM の構成

Azure Rights Management サービスと SharePoint Online IRM の動作のしくみについては、「**Understand & Explore**」 (概要と詳細) セクションの「[SharePoint Online and Exchange Server](../understand-explore/office-apps-services-support.md#sharepoint-online-and-sharepoint-server)」 (SharePoint Online と Exchange Server) を参照してください。

Azure Rights Management サービスをサポートするように、SharePoint Online および OneDrive for Business を構成するには、SharePoint 管理センターを使用して SharePoint Online 用に Information Rights Management (IRM) サービスを最初に有効にする必要があります。 次いで、ドキュメントがそこに保存され、他のユーザーと共有され、Azure Rights Management サービスによって自動的に保護されるよう、SharePoint リストとドキュメント ライブラリをサイト所有者が IRM で保護できます。

> [!NOTE]
> SharePoint および OneDrive for Business の IRM で保護されたライブラリには、新しい OneDrive 同期クライアント (OneDrive.exe) の最新バージョンが必要です。 詳細については、「[Enable users to sync IRM-protected files with the OneDrive sync client](https://support.office.com/en-us/article/6778d4de-b5f8-423c-af43-a1b2449e9b99)」 (OneDrive 同期クライアントで IRM で保護されたファイルをユーザーが同期できるようにする) を参照してください。

SharePoint Online で Information Rights Management (IRM) サービスを有効にするには、Office の次の Web サイトで手順を参照してください。

- [SharePoint 管理センターにおける Information Rights Management (IRM) の設定](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/set-up-information-rights-management-irm-insharepoint-online-HA102895193.aspx)

この構成は、Office 365 管理者が行います。

### <a name="configuring-irm-for-libraries-and-lists"></a>ライブラリおよびリスト用の IRM の構成
SharePoint で IRM サービスを有効にすると、サイト所有者は、SharePoint ドキュメント ライブラリとリストを IRM で保護できるようになります。 手順については、次の Office の Web サイトを参照してください。

- [Information Rights Management をリストまたはライブラリに適用する](https://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)

この構成は、SharePoint のサイト管理者が行います。

### <a name="configuring-irm-for-onedrive-for-business"></a>OneDrive for Business 用の IRM の構成
SharePoint Online で IRM サービスを有効にすると、ユーザーの OneDrive for Business のドキュメント ライブラリは Rights Management で保護する構成を行えるようになります。  ユーザーは、OneDrive の **[設定]** アイコンを使用してこれを構成できます。 ユーザーの OneDrive for Business の Rights Management は、管理者が SharePoint 管理センターを使用して構成することはできません。ユーザーが、Windows PowerShell を使用して構成できます。

> [!NOTE]
> OneDrive for Business の構成方法の詳細については、Office のドキュメント、「[OneDrive for Business - 管理者ヘルプ](https://support.office.com/article/Set-up-OneDrive-for-Business-in-Office-365-3e21f8f0-e0a1-43be-aa3e-8c0236bf11bb)」を参照してください。

#### <a name="configuration-for-users"></a>ユーザー用の構成
ユーザーに次の手順を教え、OneDrive for Business を構成し、ビジネス ファイルを IRM で保護できるようにします。

1.  OneDrive で **[設定]** アイコンをクリックして [設定] メニューを開き、**[サイト コンテンツ]** をクリックします。

2.  **[ドキュメント]** タイルにマウス ポインターを移動し、省略記号ボタン (**...**) を選択して、**[設定]** をクリックします。

3.  **[設定]** ページの **[権限と管理]** セクションで、**[Information Rights Management]** をクリックします。

4.  **[Information Rights Management 設定]** ページで、**[Restrict permissions on this library on download]\(ダウンロード時にこのライブラリの権限を制限する\)** チェック ボックスをオンにし、アクセス許可に選択した名前と説明を指定し、任意で **[オプションの表示]** をクリックして任意の構成を行い、**[OK]** をクリックします。

    構成オプションの詳細については、Office のドキュメント、「[Information Rights Management をリストまたはライブラリに適用する](https://support.office.com/article/Apply-Information-Rights-Management-to-a-list-or-library-3bdb5c4e-94fc-4741-b02f-4e7cc3c54aa1)」で手順を参照してください。

この構成は、OneDrive for Business ライブラリを管理者が IRM を使用して保護するのではなく、ユーザーが行うので、ユーザーにファイルの保護とその方法を教えます。 たとえば、ユーザーが OneDrive for Business のドキュメントを共有した場合、ファイルが名前変更され、他の場所にコピーされている場合でも、権限を付与したユーザーのみが構成された制限内でアクセスできることを説明します。

#### <a name="configuration-for-administrators"></a>管理者用の構成
ユーザーの OneDrive for Business の IRM は、SharePoint 管理センターを使用して構成することはできず、Windows PowerShell を使用して構成することができます。 これらのライブラリで IRM を有効にするには、次の手順を実行します。

1.  [SharePoint Online クライアント コンポーネント SDK](https://www.microsoft.com/en-us/download/details.aspx?id=42038) をダウンロードしてインストールします。

2.  [SharePoint Online Management Shell](https://www.microsoft.com/en-us/download/details.aspx?id=35588) をダウンロードしてインストールします。

3.  次のスクリプトの内容をコピーし、ファイルをコンピューター上で Set-irmononedriveforbusiness.ps1 と命名します。

    *&#42;&#42;免責事項&#42;&#42;*: このサンプル スクリプトは、Microsoft のいかなる標準サポート プログラムまたはサービスでもサポートされていません。 サンプル スクリプトは現状有姿で提供され、いかなる保証も行いません。

    ```
    # Requires Windows PowerShell version 3

    <#
      Description:

        Configures IRM policy settings for OneDrive for Business and can also be used for SharePoint Online libraries and lists

     Script Installation Requirements:

       SharePoint Online Client Components SDK
       https://www.microsoft.com/en-us/download/details.aspx?id=42038

       SharePoint Online Management Shell
       https://www.microsoft.com/en-us/download/details.aspx?id=35588

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
                    Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038"
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
                            Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588"
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

    # Add the credentials to the client context and SharePoint Online service connection

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

    # connect to Office365 first, required for SharePoint Online cmdlets to run

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

4.  スクリプトを確認し、次の変更を行います。

    1.  `$sharepointAdminCenterUrl` を検索し、値の例を自身の SharePoint 管理センター URL に置き換えます。

        この値は、SharePoint 管理センターに移動すると、https://*&lt;tenant_name&gt;*-admin.sharepoint.com という形式で、ベース URL としてあります。

        たとえば、テナント名が "contoso" の場合、**https://contoso-admin.sharepoint.com** と指定します。

    2.  `$tenantAdmin` を検索し、値の例を自身の Office 365 の完全修飾グローバル管理者アカウントに置き換えます。

        この値は、グローバル管理者として Office 365 管理ポータルにサインインするときに使用する値と同じです。形式は、user_name@*&lt;tenant domain name&gt;*.com です。

        たとえば、Office 365 のグローバル管理者の "contoso.com" テナント ドメインのユーザー名が "admin" の場合、**admin@contoso.com** と指定します。

    3.  `$webUrls` を検索し、値の例を、ユーザーの OneDrive for Business の Web URL に置き換えます。そのとき、必要数のエントリを追加または削除します。

        または、構成する必要のあるすべての URL を含む .CSV ファイルをインポートする、スクリプト内のこの配列を置き換える方法のコメントを確認します。  自動的に検索し、この .CSV ファイルに入力する URL を抽出する、サンプル スクリプトがもう 1 つ用意されています。 これを行う準備ができたら、これらの手順の直後に、「[.CSV ファイルに OneDrive for Business のすべての URL を出力する追加のスクリプト](#additional-script-to-output-all-onedrive-for-business-urls-to-a-csv-file)」セクションを実行します。

        ユーザーの OneDrive for Business の Web URL の形式は、https://*&lt;tenant name&gt;*-my.sharepoint.com/personal/*&lt;user_name&gt;*_*&lt;tenant name&gt;*_com です。

        たとえば、contoso テナントのユーザー名が "rsimone" の場合、**https://contoso-my.sharepoint.com/personal/rsimone_contoso_com** と指定します。

    4.  OneDrive for Business の構成にスクリプトを使用しているため、`$listTitle` 変数の **Documents** 値は変更しないでください。

    5.  `ADMIN INSTRUCTIONS` を検索します。 このセクションを変更しない場合、ユーザーの OneDrive for Business の IRM のポリシーのタイトルは、"Protected Files" となり、説明は "This policy restricts access to authorized users" となります。  その他の IRM オプションは設定されません。これは、おそらく多くの環境に適しています。 ただし、提示されたポリシー タイトルと説明を変更したり、環境に適したその他の IRM オプションも追加できます。 Set-IrmConfiguration コマンド用に独自のパラメーターのセットを構築する助けとなる、スクリプト内のコメント例を参照してください。

5.  スクリプトを保存し、署名します。 スクリプトに署名しない場合 (より安全性は高いです)、Windows PowerShell で署名されていないスクリプトを実行できるよう、コンピューターが構成されている必要があります。 これを行うには、Windows PowerShell セッションを **[管理者として実行]** オプションを使用して実行し、「**Set-executionpolicy Unrestricted**」と入力します。 ただし、この構成では、署名されていないすべてのスクリプトが実行されます (セキュリティは低いです)。

    Windows PowerShell スクリプトの署名の詳細については、PowerShell のドキュメント ライブラリの「[about_Signing](https://technet.microsoft.com/library/hh847874.aspx)」を参照してください。

6.  スクリプトを実行し、求められたら Office 365 管理者アカウントのパスワードを指定します。 スクリプトを変更し、同じ Windows PowerShell セッションでそれを実行した場合は、資格情報は求められません。

> [!TIP]
> このスクリプトを使用すると SharePoint Online ライブラリ用に IRM を構成することもできます。 この構成には、追加の **[IRM をサポートしないドキュメントのアップロードをユーザーに許可しない]** オプションも有効にして、ライブラリに保護されたドキュメントのみが含まれているようにできます。    これを実行するには、スクリプトの Set-IrmConfiguration コマンドに `-IrmReject` パラメーターを追加します。
>
> また、`$webUrls` 変数 (例: **https://contoso.sharepoint.com**) および `$listTitle` 変数 (例: **$Reports**) も変更する必要があります。

ユーザーの OneDrive for Business ライブラリで IRM を無効にする必要がある場合は、「[Onedrive for Business 用の IRM を無効にするスクリプト](#script-to-disable-irm-for-onedrive-for-business)」セクションを参照してください。

##### <a name="additional-script-to-output-all-onedrive-for-business-urls-to-a-csv-file"></a>.CSV ファイルに OneDrive for Business のすべての URL を出力する追加のスクリプト
上の手順 4c では、すべてのユーザーの OneDrive for Business ライブラリの URL を抽出するのに、次の Windows PowerShell スクリプトを使用することができます。その後、これを必要に応じて確認および編集して、メイン スクリプトにインポートします。

このスクリプトでは、[SharePoint Online クライアント コンポーネント SDK](http://www.microsoft.com/en-us/download/details.aspx?id=42038) と [SharePoint Online Management Shell](http://www.microsoft.com/en-us/download/details.aspx?id=35588) も必要です。 同じ手順を実行して、コピーと貼り付けを行い、ファイル (例: "Report-onedriveforbusinesssiteinfo.ps1") をローカルに保存し、前と同様に `$sharepointAdminCenterUrl` と `$tenantAdmin` の値を変更して、スクリプトを実行します。

*&#42;&#42;免責事項&#42;&#42;*: このサンプル スクリプトは、Microsoft のいかなる標準サポート プログラムまたはサービスでもサポートされていません。 サンプル スクリプトは現状有姿で提供され、いかなる保証も行いません。

```
# Requires Windows PowerShell version 3

<#
  Description:

    Queries the search service of an Office 365 tenant to retrieve all OneDrive for Business sites.  
    Details of the discovered sites are written to a .CSV file (by default,"OneDriveForBusinessSiteInfo_<date>.csv").

 Script Installation Requirements:

   SharePoint Online Client Components SDK
   http://www.microsoft.com/en-us/download/details.aspx?id=42038

   SharePoint Online Management Shell
   http://www.microsoft.com/en-us/download/details.aspx?id=35588

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
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038"
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
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588"
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

# Add the credentials to the client context and SharePoint Online service connection

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

# run a query against the Office 365 tenant search service to retrieve all OneDrive for Business URLs

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

##### <a name="script-to-disable-irm-for-onedrive-for-business"></a>Onedrive for Business 用の IRM を無効にするスクリプト
ユーザーの OneDrive for Business で IRM を無効にする必要がある場合は、次のサンプル スクリプトを使用します。

このスクリプトでは、[SharePoint Online クライアント コンポーネント SDK](http://www.microsoft.com/en-us/download/details.aspx?id=42038) と [SharePoint Online Management Shell](http://www.microsoft.com/en-us/download/details.aspx?id=35588) も必要です。 内容をコピーして貼り付け、ファイル (例: "Disable-IRMOnOneDriveForBusiness.ps1") をローカルに保存し、`$sharepointAdminCenterUrl` と `$tenantAdmin` の値を変更します。 OneDrive for Business の URL を手動で指定するか、前のセクションのスクリプトを使用して、これらをインポートしてスクリプトを実行します。

*&#42;&#42;免責事項&#42;&#42;*: このサンプル スクリプトは、Microsoft のいかなる標準サポート プログラムまたはサービスでもサポートされていません。 サンプル スクリプトは現状有姿で提供され、いかなる保証も行いません。

```
# Requires Windows PowerShell version 3

<#
  Description:

    Disables IRM for OneDrive for Business and can also be used for SharePoint Online libraries and lists

 Script Installation Requirements:

   SharePoint Online Client Components SDK
   http://www.microsoft.com/en-us/download/details.aspx?id=42038

   SharePoint Online Management Shell
   http://www.microsoft.com/en-us/download/details.aspx?id=35588

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
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=42038"
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
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: http://www.microsoft.com/en-us/download/details.aspx?id=35588"
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

# Add the credentials to the client context and SharePoint Online service connection

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

# connect to Office365 first, required for SharePoint Online cmdlets to run

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

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
