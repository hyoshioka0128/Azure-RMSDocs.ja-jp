---
title: "Office 365&colon; クライアントとオンライン サービスの構成 - AIP"
description: "Azure Information Protection から Azure Rights Management サービスで使用する Office 365 を構成するための、管理者向けの情報と手順です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 0a6ce612-1b6b-4e21-b7fd-bcf79e492c3b
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 5c1fad4b9e809a597f48d3bf394f3c097ca938e7
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="office-365-configuration-for-clients-and-online-services"></a>Office 365: クライアントとオンライン サービスの構成

>*適用対象: Azure Information Protection、Office 365*

Office 365 では、Azure Information Protection からの Azure Rights Management サービスをネイティブでサポートしているため、クライアント コンピューターを構成しなくても、Word、Excel、PowerPoint、Outlook、Outlook Web App などのアプリケーションで Information Rights Management (IRM) 機能がサポートされます。 すべてのユーザーは、各自の [!INCLUDE[o365_1](../includes/o365_1_md.md)] 資格情報を使用して Office アプリケーションにサインインするだけで、ファイルや電子メールを保護したり、他のユーザーが保護しているファイルや電子メールを使用することができます。

ただし、これらのアプリケーションを Azure Information Protection クライアントで補完して、ユーザーが Office アドインを利用し、追加のファイルの種類をサポートできるようにすることをお勧めします。 詳細については、「[Azure Information Protection client: Installation and configuration for clients](configure-client.md)」(Azure Information Protection クライアント: クライアントのインストールと構成) を参照してください。

## <a name="exchange-online-irm-configuration"></a>Exchange Online: IRM 構成
Exchange Online を構成して Azure Rights Management サービスをサポートするには、Exchange Online で Information Rights Management (IRM) サービスを構成する必要があります。 これを行うには、Windows PowerShell を使用して (個別のモジュールをインストールする必要はありません)、[Exchange Online 用 PowerShell コマンド](https://technet.microsoft.com/library/jj200677.aspx)を実行します。

> [!NOTE]
> 現時点では、マイクロソフト管理のテナント キーの既定の構成ではなく Azure Information Protection の顧客管理のテナント キー (BYOK) を使用する場合は、Azure Rights Management サービスをサポートするように Exchange Online を構成することはできません。 詳細については、「[BYOK の料金と制限事項](../plan-design/byok-price-restrictions.md)」を参照してください。
>
> Azure Rights Management サービスで BYOK を使用しているときに Exchange Online を構成しようとすると、キーをインポートするコマンド (次の手順 5) は、**[FailureCategory=Cmdlet-FailedToGetTrustedPublishingDomainFromRmsOnlineException]** というエラー メッセージで失敗します。

次の手順では、Exchange Online で Azure Rights Management サービスを使用可能にするために実行するコマンドの標準的なセットを提供します。

1.  コンピューターで Exchange Online 用 Windows PowerShell を初めて使用する場合は、署名済みスクリプトを実行するように Windows PowerShell を構成する必要があります。 [ **管理者として実行** ] オプションを使用して Windows PowerShell セッションを開始し、次のように入力します。

    ```
    Set-ExecutionPolicy RemoteSigned
    ```

2.  Windows PowerShell セッションで、リモート シェル アクセスが有効になっているアカウントを使用して Exchange Online にサインインします。 既定では、Exchange Online で作成されたすべてのアカウントではリモート シェル アクセスが有効になっていますが、[Set-User &lt;ユーザー ID&gt; -RemotePowerShellEnabled](https://technet.microsoft.com/library/jj984292%28v=exchg.160%29.aspx) コマンドを使用することで無効 (または有効) にすることができます。

    サインインするには、次のように入力します。

    ```
    $UserCredential = Get-Credential
    ```
    [ **Windows PowerShell 資格情報要求** ] ダイアログ ボックスで、Office 365 のユーザー名とパスワードを入力します。

3.  Exchange Online サービスに接続するには、次の&2; つのコマンドを実行します。

    ```
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection
    ```

    ```
    Import-PSSession $Session
    ```

4.  組織のテナントを作成した場所に応じて、Azure Information Protection テナント キーの場所を指定します。

    北アメリカ:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.na.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    ヨーロッパ:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.eu.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    アジア:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.ap.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    南アメリカ:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.sa.aadrm.com/TenantManagement/ServicePartner.svc"
    ```
    Office 365 Government (政府機関コミュニティ クラウド) の場合:

    ```
    Set-IRMConfiguration -RMSOnlineKeySharingLocation "https://sp-rms.govus.aadrm.com/TenantManagement/ServicePartner.svc"
    ```

5.  信頼された発行ドメイン (TPD) の形式で、Azure Rights Management サービスから構成データを Exchange Online にインポートします。 このデータには、Azure Information Protection テナント キーと Azure Rights Management テンプレートが含まれます。

    ```
    Import-RMSTrustedPublishingDomain -RMSOnline -name "RMS Online"
    ```
    このコマンドでは、Exchange Online での Azure Rights Management の TPD の基本名に **RMS Online** の名前が使用されています。 TPD がインポートされた後は、Exchange Online では **RMS Online - 1** という名前になります。

6.  Exchange Online で IRM 機能を利用できるように、Azure Rights Management の機能を有効にします。

    ```
    Set-IRMConfiguration -InternalLicensingEnabled $true
    ```
    このコマンドを実行した後は、Outlook クライアント、Outlook Web App、Exchange Active Sync 用の Rights Management が自動的に有効になります。

7.  必要に応じて、次のコマンドを使用して、この構成が正常に機能することをテストします。

    ```
    Test-IRMConfiguration -Sender <user email address>
    ```
    例: **Test-IRMConfiguration -Sender  adams@contoso.com**

    このコマンドは、サービスへの接続の確認、構成の取得、URI、ライセンス、および任意のテンプレートの取得を含む一連のチェックを実行します。 Windows PowerShell セッションでは、これらのチェックのそれぞれの結果、およびすべてのチェックをパスした場合は最後にも、その結果が表示されます。 **全体的な結果:パス**

8.  リモート PowerShell セッションの切断:

    ```
    Remove-PSSession $Session
    ```

ユーザーは、Active Rights Management サービスを使用して電子メール メッセージを保護できるようになります。 たとえば、Outlook Web App で、拡張メニュー ( **...** ) から [**権限の設定**] を選択し、[ **転送不可** ] を選択するか、または使用可能なテンプレートの&1; つを選択して、電子メール メッセージおよび添付ファイルに情報保護を適用します。 ただし、Outlook Web App では、1 日分の UI がキャッシュされるため、電子メール メッセージに情報保護を適用する前、およびこれらの構成コマンドを実行した後は、この期間を待機します。 UI に新しい構成が反映されるよう更新される前は、 [ **権限の設定** ] メニューにはオプションは表示されません。

> [!IMPORTANT]
> Azure Rights Management 用の新規 [カスタム テンプレート](configure-custom-templates.md) を作成する、またはテンプレートを更新する場合は常に、次の Exchange Online の PowerShell コマンドを実行して (必要に応じて手順 2 および 3 を最初に実行します)、これらの変更を Exchange Online に同期します。`Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates –RMSOnline`

Exchange 管理者は、 [トランスポート ルール](https://technet.microsoft.com/library/dd302432.aspx)、 [データ損失防止 (DLP) ポリシー](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx)、および [保護されたボイス メール](https://technet.microsoft.com/library/dn198211%28v=exchg.150%29.aspx) (ユニファイド メッセージング) などの情報保護を自動的に適用する機能を構成できます。

IRM 機能を有効にするために Exchange Online を構成する詳細な手順については、Exchange ライブラリのドキュメントを参照してください。 たとえば、

-   [リモート PowerShell を使用して Exchange Online に接続する](https://technet.microsoft.com/library/jj984289%28v=exchg.160%29.aspx)

-   [Azure Rights Management を使用するように IRM を構成する](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx)

### <a name="office-365-message-encryption"></a>Office 365 メッセージの暗号化
前のセクションで説明されているのと同じ手順を実行します。ただし、テンプレートを表示したくない場合は、手順 6 の前に次のコマンドを実行して、Outlook Web App および Outlook クライアントで IRM テンプレートが使用できないようにします。 `Set-IRMConfiguration -ClientAccessServerEnabled $false`

これで、 [トランスポート ルール](https://technet.microsoft.com/library/dd302432.aspx) を構成して、受信者が組織外部に居る場合にメッセージ セキュリティを自動的に更新し、[ **Office 365 のメッセージの暗号化を適用** ] オプションが選択できるようになります。

メッセージの暗号化の詳細については、Exchange ライブラリの「 [Office 365 での暗号化](https://technet.microsoft.com/library/dn569286.aspx) 」を参照してください。

## <a name="sharepoint-online-and-onedrive-for-business-irm-configuration"></a>SharePoint Online と OneDrive for Business:IRM 構成
SharePoint Online と OneDrive for Business を Azure Rights Management サービスをサポートするように構成するには、最初に SharePoint 管理センターを使用して、SharePoint Online の Information Rights Management (IRM) サービスを有効にする必要があります。 これで、サイトの所有者は SharePoint リストとドキュメント ライブラリを IRM で保護でき、ユーザーは OneDrive for Business ライブラリを IRM で保護することができます。それらの場所に保存されたドキュメント、および他のユーザーと共有しているドキュメントが、自動的に Azure Rights Management サービスで保護されるようになります。

> [!NOTE]
> SharePoint と OneDrive for Business 用の IRM で保護されたライブラリは、古い同期クライアントである OneDrive for Business 同期クライアント (Groove.exe) を使用していない限り、オンライン ダウンロードをサポートしています。 現在、新しい [OneDrive 同期クライアント (OneDrive.exe)](https://support.office.com/article/Enable-users-to-sync-SharePoint-files-with-the-new-OneDrive-sync-client-22e1f635-fb89-49e0-a176-edab26f69614) は、Rights Management 保護をサポートしていません。 

SharePoint Online 用の Information Rights Management (IRM) サービスを有効にするには、Office Web サイトの次の手順を参照してください。

-   [SharePoint 管理センターにおける Information Rights Management (IRM) の設定](http://office.microsoft.com/office365-sharepoint-online-enterprise-help/set-up-information-rights-management-irm-insharepoint-online-HA102895193.aspx)

この構成は、Office 365 管理者によって行われます。

### <a name="configuring-irm-for-libraries-and-lists"></a>ライブラリとリストの IRM を構成する
SharePoint の IRM サービスを有効にしたら、サイト所有者は SharePoint ドキュメント ライブラリとリストを IRM で保護することができます。 方法については、Office Web サイトの次の内容を参照してください。

-   [Information Rights Management をリストまたはライブラリに適用する](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)

この構成は、SharePoint サイト管理者によって行われます。

### <a name="configuring-irm-for-onedrive-for-business"></a>OneDrive for Business の IRM を構成する
SharePoint Online の IRM サービスを有効にした後、ユーザーの OneDrive for Business ドキュメント ライブラリを Rights Management 保護用に構成できます。  ユーザーは、OneDrive の [**設定**] アイコンを使用して自分でこれを構成できます。 管理者は SharePoint 管理センターを使用してユーザーの OneDrive for Business 用に Rights Management を構成することはできませんが、Windows PowerShell を使用してこれを行うことができます。

> [!NOTE]
> OneDrive for Business の構成について詳しくは、Office のドキュメント「[Office 365 での OneDrive for Business のセットアップ](https://support.office.com/article/Set-up-OneDrive-for-Business-in-Office-365-3e21f8f0-e0a1-43be-aa3e-8c0236bf11bb)」を参照してください。

#### <a name="configuration-for-users"></a>ユーザー用の構成
ユーザーが自分の OneDrive for Business および IRM で保護されたビジネス ファイルを構成できるように、ユーザーに次のことを指示します。

1.  OneDrive で、[ **設定** ] アイコンをクリックして [設定] メニューを開き、[ **サイト コンテンツ**] をクリックします。

2.  マウス ポインターを[ **ドキュメント** ] タイルに移動し、省略記号ボタン (**...**) を選択し、[ **設定**] をクリックします。

3.  [ **設定** ] ページの [ **権限と管理** ] セクションをクリックして、[ **Information Rights Management**] をクリックします。

4.  [ **Information Rights Management 設定** ] ページで、[ **ダウンロード時にこのライブラリへのアクセス許可を制限する** ] チェック ボックスをオンにし、権限の名前と説明を指定し、必要に応じて [ **オプションの表示** ] をクリックしてオプションの構成を設定し、[ **OK**] をクリックします。

    構成オプションの詳細については、Office ドキュメントの「 [Information Rights Management をリストまたはライブラリに適用する](https://support.office.com/article/Apply-Information-Rights-Management-to-a-list-or-library-3bdb5c4e-94fc-4741-b02f-4e7cc3c54aa1) 」の手順を参照してください。

この構成は管理者ではなくユーザーが自分で OneDrive for Business ライブラリを IRM で保護する必要があるため、ファイルを保護する利点とその方法について、ユーザーを教育します。 たとえば、OneDrive for Business でドキュメントを共有すると、ファイルの名前が変更され、別の場所にコピーされていても、権限があるユーザーに限り、構成した制限付きでアクセスできることを説明します。

#### <a name="configuration-for-administrators"></a>管理者用の構成
管理者は SharePoint 管理センターを使用してユーザーの OneDrive for Business 用に IRM を構成することはできませんが、Windows PowerShell を使用してこれを行うことができます。 これらのライブラリに対して IRM を有効にするには、次の手順を実行します。

1.  [SharePoint Online クライアント コンポーネント SDK](http://www.microsoft.com/en-us/download/details.aspx?id=42038) をダウンロードしてインストールします。

2.  [SharePoint Online 管理シェル](http://www.microsoft.com/en-us/download/details.aspx?id=35588)をダウンロードしてインストールします。

3.  次のスクリプトの内容をコピーし、Set-IRMOnOneDriveForBusiness.ps1 という名前のファイルでコンピューターに保存します。

    *&#42;&#42;免責事項&#42;&#42;* このサンプル スクリプトは、Microsoft の標準サポート プログラムまたはサービスではサポートされません。 このサンプル スクリプトは、どのような種類の保証も伴わずそのままの状態で提供されます。

    ```
    # Requires Windows PowerShell version 3

    <#
      Description:

        Configures IRM policy settings for OneDrive for Business and can also be used for SharePoint Online libraries and lists

     Script Installation Requirements:

       SharePoint Online Client Components SDK
       http://www.microsoft.com/en-us/download/details.aspx?id=42038

       SharePoint Online Management Shell
       http://www.microsoft.com/en-us/download/details.aspx?id=35588

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

4.  スクリプトを確認し、次のように変更します。

    1.  `$sharepointAdminCenterUrl` を探し、例の値を実際の SharePoint 管理センターの URL に置き換えます。

        SharePoint 管理センターでこの値をベース URL として探すことになります。形式は、https://*&lt;テナント名&gt;*-admin.sharepoint.com です。

        たとえば、テナント名が "contoso" の場合、**https://contoso-admin.sharepoint.com** と指定します。

    2.  `$tenantAdmin` を探し、例の値を Office 365 の実際の完全修飾グローバル管理者アカウントに置き換えます。

        この値は、グローバル管理者として Office 365 管理ポータルにサインインするために使用するものと同じで、形式は user_name@*&lt;テナント ドメイン名&gt;*.com です。

        たとえば、"contoso.com" テナント ドメインの Office 365 グローバル管理者ユーザーの名前が "admin" である場合、**admin@contoso.com** と指定します。

    3.  `$webUrls` を探し、例の値をユーザーの OneDrive for Business Web URL に置き換え、必要に応じてエントリを追加または削除します。

        または、スクリプトのコメントを参考にして、構成する必要のあるすべての URL を含む .CSV ファイルをインポートして、この配列を置き換えます。  自動的に URL を検索して抽出し、この .CSV ファイルを作成する、別のサンプル スクリプトが提供されています。 これを行う準備ができたら、これらの手順を実行した直後に「[すべての OneDrive for Business URL を .CSV ファイルに出力するための追加スクリプト](#additional-script-to-output-all-onedrive-for-business-urls-to-a-csv-file)」セクションの手順を実行します。

        ユーザーの OneDrive for Business の Web URL の形式は、https://*&lt;テナント名&gt;*-my.sharepoint.com/personal/*&lt;ユーザー名&gt;*_*&lt;テナント名&gt;*_com です。

        たとえば、contoso テナントのユーザーのユーザー名が "rsimone" である場合は、**https://contoso-my.sharepoint.com/personal/rsimone_contoso_com** と指定します。

    4.  スクリプトを使用して OneDrive for Business を構成しているので、`$listTitle` 変数の ** ドキュメント ** の値は変更しないでください。

    5.  `ADMIN INSTRUCTIONS` を探します。 このセクションを変更しないと、ユーザーの OneDrive for Business はポリシーのタイトル "Protected Files"、説明 "This policy restricts access to authorized users" で IRM 用に構成されます。  その他の IRM オプションは設定されません、おそらくほとんどの環境に最適です。 ただし、推奨されているポリシーのタイトルと説明を変更でき、環境に合わせて他の IRM オプションも追加できます。 Set-IrmConfiguration コマンドの独自のパラメーター セットの作成については、スクリプトのコメント付きの例を参照してください。

5.  スクリプトを保存し、署名します。 スクリプトに署名しない場合は (より安全)、署名されていないスクリプトを実行するようにコンピューターで Windows PowerShell を構成する必要があります。 そのためには、**[管理者として実行]** オプションを使用して Windows PowerShell セッションを実行し、「**Set-ExecutionPolicy Unrestricted**」と入力します。 ただし、この構成を使用すると署名されていないすべてのスクリプトを実行できます (セキュリティが低下)。

    Windows PowerShell スクリプトへの署名の詳細については、PowerShell のドキュメント ライブラリの「 [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) 」を参照してください。

6.  スクリプトを実行し、要求された場合は、Office 365 管理者アカウントのパスワードを入力します。 スクリプトを変更して同じ Windows PowerShell セッションで実行する場合は、資格情報を要求されません。

> [!TIP]
> このスクリプトを使用して、SharePoint Online ライブラリ用に IRM を構成することもできます。 この構成では、追加オプション [**IRM をサポートしないドキュメントのアップロードをユーザーに許可しない**] を有効にして、保護されたドキュメントだけがライブラリに含まれるようにできます。    そのためには、`-IrmReject` パラメーターをスクリプトの Set-IrmConfiguration コマンドに追加します。
>
> また、`$webUrls` 変数 (例: **https://contoso.sharepoint.com**) および `$listTitle` 変数 (例: **$Reports**) を変更する必要もあります。

ユーザーの OneDrive for Business ライブラリに対して IRM を無効にする必要がある場合、「[OneDrive for Business の IRM を無効にするスクリプト](#script-to-disable-irm-for-onedrive-for-business)」セクションを参照してください。

##### <a name="additional-script-to-output-all-onedrive-for-business-urls-to-a-csv-file"></a>すべての OneDrive for Business URL を .CSV ファイルに出力するための追加スクリプト
上の手順 4c では、次の Windows PowerShell スクリプトを使用してすべてのユーザーの OneDrive for Business ライブラリの URL を抽出できます。その後、それを確認し、必要であれば編集して、メイン スクリプトにインポートできます。

また、このスクリプトでは、[SharePoint Online クライアント コンポーネント SDK](http://www.microsoft.com/en-us/download/details.aspx?id=42038) および [SharePoint Online 管理シェル](http://www.microsoft.com/en-us/download/details.aspx?id=35588) も必要です。 同じ手順でコピーして貼り付け、ファイルをローカルに保存し (例: "Report-OneDriveForBusinessSiteInfo.ps1")、前と同じように `$sharepointAdminCenterUrl` および `$tenantAdmin` の値を変更して、スクリプトを実行します。

*&#42;&#42;免責事項&#42;&#42;* このサンプル スクリプトは、Microsoft の標準サポート プログラムまたはサービスではサポートされません。 このサンプル スクリプトは、どのような種類の保証も伴わずそのままの状態で提供されます。

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

##### <a name="script-to-disable-irm-for-onedrive-for-business"></a>OneDrive for Business の IRM を無効にするスクリプト
ユーザーの OneDrive for Business の IRM を無効にする必要がある場合は、次のサンプル スクリプトを使用します。

また、このスクリプトでは、[SharePoint Online クライアント コンポーネント SDK](http://www.microsoft.com/en-us/download/details.aspx?id=42038) および [SharePoint Online 管理シェル](http://www.microsoft.com/en-us/download/details.aspx?id=35588) も必要です。 内容をコピーして貼り付け、ファイルをローカルにコピーし (例: "Disable-IRMOnOneDriveForBusiness.ps1")、`$sharepointAdminCenterUrl` と `$tenantAdmin` の値を変更します。 OneDrive for Business の URL を手動で指定するか、または前のセクションのスクリプトを使用してインポートできるようにし、スクリプトを実行します。

*&#42;&#42;免責事項&#42;&#42;* このサンプル スクリプトは、Microsoft の標準サポート プログラムまたはサービスではサポートされません。 このサンプル スクリプトは、どのような種類の保証も伴わずそのままの状態で提供されます。

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
