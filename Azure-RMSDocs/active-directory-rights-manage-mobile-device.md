---
title: AIP 用の rights management services モバイルデバイス拡張機能の Active Directory
description: AIP 向けのモバイルデバイス拡張機能の Active Directory について説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/28/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 874a73480e8d15380d9e69a532a1b8ff39d38eb7
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97384164"
---
# <a name="active-directory-rights-management-services-mobile-device-extension"></a>Active Directory Rights Management Services モバイル デバイス拡張機能

>***適用対象**: Windows Server 2019、2016、2012 R2、および 2012 *
>
>***関連**: [AIP のラベル付けクライアントと従来のクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Active Directory Rights Management サービス (AD RMS) モバイルデバイス拡張機能を [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=43738) からダウンロードし、この拡張機能を既存の AD RMS 展開の上にインストールすることができます。 これにより、デバイスが最新の API 対応アプリをサポートしているときに、ユーザーが機微なデータを保護および使用できるようになります。 たとえば、ユーザーは次の操作を実行できます。
- Azure Information Protection アプリを使用して、さまざまな形式 (.txt、.csv、.xml など) で保護されたテキストファイルを使用します。
- Azure Information Protection アプリを使用して、保護されたイメージファイル (.jpg、.gif、.tif など) を使用します。
- Azure Information Protection アプリを使用して、一般的に保護されているファイル (. pfile 形式) を開きます。
- Azure Information Protection アプリを使用して、PDF コピー (.pdf および ppdf 形式) である Office ファイル (Word、Excel、PowerPoint) を開きます。
- 保護された電子メールメッセージ (...) と保護された PDF ファイルを Microsoft SharePoint で開くには、Azure Information Protection アプリを使用します。
- クロスプラットフォームでの表示や、AIP 対応アプリケーションで保護された PDF ファイルを開くには、AIP-対応 PDF ビューアーを使用します。
- [MIP SDK](/information-protection/develop/)を使用して作成された、社内で開発された AIP-対応アプリを使用します。

> [!NOTE]
> Azure Information Protection アプリは、Microsoft web サイトの [microsoft Rights Management](https://go.microsoft.com/fwlink/?linkid=303970) のページからダウンロードできます。 モバイルデバイス拡張機能でサポートされているその他のアプリの詳細については、このドキュメントの「 [アプリケーション](./requirements-applications.md) 」ページにある表を参照してください。 RMS がサポートするさまざまなファイルの種類の詳細については、「Rights Management 共有アプリケーション管理者ガイド」の「 [サポートされているファイルの種類とファイル名拡張子](/rights-management/rms-client/sharing-app-admin-guide-technical#supported-file-types-and-file-name-extensions) 」セクションを参照してください。

> [!IMPORTANT]
> モバイルデバイス拡張機能をインストールする前に、必ず前提条件を読んで構成してください。

詳細については、 [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=40333)から「Microsoft Azure Information Protection」ホワイトペーパーと付随するスクリプトをダウンロードしてください。

## <a name="prerequisites-for-ad-rms-mobile-device-extension"></a>AD RMS モバイルデバイス拡張機能の前提条件

AD RMS モバイルデバイス拡張機能をインストールする前に、次の依存関係が配置されていることを確認してください。


|要件|詳細情報|
|---------------|------------------------|
|Windows Server 2019、2016、2012 R2、または2012における既存の AD RMS の展開には、次のものが含まれます。<br /><br /> -AD RMS クラスターには、インターネットからアクセスできる必要があります。 <br /><br /> -AD RMS は、同じサーバー上でのテストによく使用される Windows Internal Database ではなく、別のサーバー上の完全な Microsoft SQL Server ベースのデータベースを使用する必要があります。 <br /><br />-モバイルデバイス拡張機能のインストールに使用するアカウントには、AD RMS に使用している SQL Server インスタンスに対する sysadmin 権限が必要です。 <br /><br />-AD RMS サーバーは、モバイルデバイスクライアントによって信頼されている有効な x.509 証明書で SSL/TLS を使用するように構成されている必要があります。<br /><br /> -AD RMS サーバーがファイアウォールの内側にある場合、またはリバースプロキシを使用して公開されている場合は、 **/_wmcs** フォルダーをインターネットに発行するだけでなく、/マイフォルダーも発行する必要があります (例: **_https: \/ \/ RMSserver.contoso.com/my**)。|AD RMS の前提条件と展開情報の詳細については、この記事の「前提条件」セクションを参照してください。|
|AD FS Windows Server に展開されます。<br /><br /> -AD FS サーバーファームは、インターネット (フェデレーションサーバープロキシを展開済み) からアクセスできる必要があります。 <br /><br />-フォームベースの認証はサポートされていません。Windows 統合認証を使用する必要があります。 <br /><br /> **重要**: AD FS は、AD RMS を実行しているコンピューターとモバイルデバイスの拡張機能とは別のコンピューターを実行している必要があります。|AD FS に関するドキュメントについては、windows server ライブラリの [Windows server AD FS 展開ガイド](/office365/troubleshoot/active-directory/set-up-adfs-for-single-sign-on) を参照してください。<br /><br /> AD FS をモバイル デバイス拡張機能用に構成する必要があります。 手順については、このトピックの「 **AD RMS モバイルデバイス拡張機能の AD FS の構成** 」セクションを参照してください。|
|モバイルデバイスは、RMS サーバー (またはサーバー) の PKI 証明書を信頼する必要があります。|VeriSign や Comodo などのパブリック CA からサーバー証明書を購入する場合、モバイルデバイスでは、これらの証明書のルート CA が既に信頼されている可能性があります。これにより、これらのデバイスは、追加の構成なしにサーバー証明書を信頼できるようになります。<br /><br /> ただし、独自の内部 CA を使用して RMS 用のサーバー証明書を展開する場合は、追加の手順を実行して、ルート CA 証明書をモバイルデバイスにインストールする必要があります。 そうしないと、モバイルデバイスは RMS サーバーとの接続を正常に確立できなくなります。|
|DNS の SRV レコード|会社のドメインに 1 つ以上の SRV レコードを作成します。<br /><br />1: ユーザーが使用する電子メールドメインサフィックスごとにレコードを作成します。 <br /><br />2: RMS クラスターで使用されるすべての FQDN のレコードを作成し、クラスター名を含めずにコンテンツを保護します。 <br /><br />これらのレコードは、接続しているモバイルデバイスが使用するすべてのネットワークから解決できる必要があります。これには、モバイルデバイスがイントラネット経由で接続されている場合、イントラネットが含まれます。<br /><br /> ユーザーがモバイルデバイスから電子メールアドレスを入力すると、ドメインサフィックスを使用して、AD RMS インフラストラクチャと Azure AIP のどちらを使用する必要があるかを識別します。 SRV レコードが見つかると、クライアントはその URL に応答する AD RMS サーバーにリダイレクトされます。<br /><br /> ユーザーが保護されたコンテンツをモバイルデバイスで使用すると、クライアントアプリケーションは、コンテンツを保護したクラスターの URL (クラスター名なし) の FQDN に一致するレコードを DNS で検索します。 その後、デバイスは DNS レコードで指定された AD RMS クラスターに送られて、コンテンツを開くためのライセンスを取得します。 ほとんどの場合、RMS クラスターはコンテンツを保護したものと同じ RMS クラスターです。<br /><br /> SRV レコードを指定する方法の詳細については、このトピックの「 **AD RMS モバイルデバイス拡張機能の DNS SRV レコードの指定** 」セクションを参照してください。|
|このプラットフォーム用の MIP SDK を使用して開発されたアプリケーションを使用している、サポートされているクライアント。 |[Microsoft Azure Information Protection](https://www.microsoft.com/download/details.aspx?id=40333)のダウンロードページにあるリンクを使用して、使用するデバイスのサポートされているアプリをダウンロードします。|

### <a name="configuring-ad-fs-for-the-ad-rms-mobile-device-extension"></a>AD RMS モバイル デバイス拡張機能用の AD FS の構成

最初に AD FS を構成してから、使用するデバイスに対して AIP アプリを承認する必要があります。

#### <a name="step-1-to-configure-ad-fs"></a>手順 1: AD FS を構成するには

- Windows PowerShell スクリプトを実行して AD RMS モバイル デバイス拡張機能をサポートするための AD FS を自動的に構成するか、または構成オプションと値を手動で指定することができます。
    - AD RMS モバイルデバイス拡張機能の AD FS を自動的に構成するには、次のファイルをコピーして Windows PowerShell スクリプトファイルに貼り付けてから実行します。

```powershell
# This Script Configures the Microsoft Rights Management Mobile Device Extension and Claims used in the ADFS Server

# Check if Microsoft Rights Management Mobile Device Extension is configured on the Server
$CheckifConfigured = Get-AdfsRelyingPartyTrust -Identifier "api.rms.rest.com"
if ($CheckifConfigured)
{
Write-Host "api.rms.rest.com Identifer used for Microsoft Rights Management Mobile Device Extension is already configured on this Server"
Write-Host $CheckifConfigured
}
else
{
Write-Host "Configuring  Microsoft Rights Management Mobile Device Extension "

# TransformaRules used by Microsoft Rights Management Mobile Device Extension
# Claims: E-mail, UPN and ProxyAddresses
$TransformRules = @"
@RuleTemplate = "LdapClaims"
@RuleName = "Jwt Token"
c:[Type ==
"http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname",
Issuer == "AD AUTHORITY"]
 => issue(store = "Active Directory", types =
("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress",
"http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn",
"http://schemas.xmlsoap.org/claims/ProxyAddresses"), query =
";mail,userPrincipalName,proxyAddresses;{0}", param = c.Value);

@RuleTemplate = "PassThroughClaims"
@RuleName = "JWT pass through"
c:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"]
 => issue(claim = c);

@RuleTemplate = "PassThroughClaims"
@RuleName = "JWT pass through"
c:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"]
 => issue(claim = c);

@RuleTemplate = "PassThroughClaims"
@RuleName = "JWT pass through Proxy addresses"
c:[Type == "http://schemas.xmlsoap.org/claims/ProxyAddresses"]
 => issue(claim = c);
"@

# AuthorizationRules used by Microsoft Rights Management Mobile Device Extension
# Allow All users
$AuthorizationRules = @"
@RuleTemplate = "AllowAllAuthzRule"
 => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit",
Value = "true");
"@

# Add a Relying Part Truest with Name -"Microsoft Rights Management Mobile Device Extension" Identifier "api.rms.rest.com"
Add-ADFSRelyingPartyTrust -Name "Microsoft Rights Management Mobile Device Extension" -Identifier "api.rms.rest.com" -IssuanceTransformRules $TransformRules -IssuanceAuthorizationRules  $AuthorizationRules

Write-Host "Microsoft Rights Management Mobile Device Extension Configured"
}
```

- AD RMS モバイルデバイス拡張機能の AD FS を手動で構成するには、次の設定を使用します。

|**構成**|**Value**|
|-----|-----|
|**証明書利用者の信頼**|_api します。|
|**要求規則**|**属性ストア**: Active Directory <br /><br />**電子メールアドレス**: 電子メールアドレス<br /><br>**ユーザープリンシパル名**: UPN<br /><br /> **プロキシアドレス**: _https: \/ \/schemas.xmlsoap.org/claims/ProxyAddresses|

> [!TIP]
> AD FS を使用した AD RMS の展開例の詳細な手順については、「 [Active Directory フェデレーションサービス (AD FS) で Active Directory Rights Management サービスを展開](/office365/troubleshoot/active-directory/set-up-adfs-for-single-sign-on)する」を参照してください。

#### <a name="step-2-authorize-apps-for-your-devices"></a>手順 2: デバイスのアプリを承認する

- 変数を置き換えた後、次の Windows PowerShell コマンドを実行して、 **Azure Information Protection** アプリのサポートを追加します。 次に示す順序で両方のコマンドを実行してください。


```powershell
Add-AdfsClient -Name "R<your application name> " -ClientId "<YOUR CLIENT ID >" -RedirectUri @("<YOUR REDIRECT URI >")
```
```powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier '<YOUR CLIENT ID>' -ServerRoleIdentifier api.rms.rest.com -ScopeNames "openid"
```

**Powershell の例**
```powershell
Add-AdfsClient -Name "Fabrikam application for MIP" -ClientId "96731E97-2204-4D74-BEA5-75DCA53566C3" -RedirectUri @("com.fabrikam.MIPAPP://authorize")
```
```powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier '96731E97-2204-4D74-BEA5-75DCA53566C3' -ServerRoleIdentifier api.rms.rest.com -ScopeNames "openid"
```

- Azure Information Protection 統合された **ラベル付けクライアント** の場合は、次の Windows PowerShell コマンドを実行して、デバイスに Azure Information Protection クライアントのサポートを追加します。

```powershell
Add-AdfsClient -Name "Azure Information Protection Client" -ClientId "c00e9d32-3c8d-4a7d-832b-029040e7db99" -RedirectUri @("com.microsoft.azip://authorize")
Grant-AdfsApplicationPermission -ClientRoleIdentifier "c00e9d32-3c8d-4a7d-832b-029040e7db99" -ServerRoleIdentifier api.rms.rest.com -ScopeName "openid"
```
- **Windows 2016 および2019での ADFS** とサードパーティ製品用の **ADRMS MDE** をサポートするには、次の windows PowerShell コマンドを実行します。

```powershell
Add-AdfsClient -Name "YOUR APP" -ClientId 'YOUR CLIENT ID' -RedirectUri @("YOUR REDIRECT") 
Grant-AdfsApplicationPermission -ClientRoleIdentifier 'YOUR CLIENT ID' -ServerRoleIdentifier api.rms.rest.com -ScopeNames "openid"
```

Windows、Mac、モバイル、および windows **Server 2012 R2 以降の AD FS** で **保護されたコンテンツ** を使用する AD RMS ために、 **windows**、 **Mac**、mobile、および **Office mobile** で AIP クライアントを構成するには、次のようにします。 

- (RMS 共有アプリを使用して) Mac デバイスの場合は、次に示す順序で両方のコマンドを実行してください。

```powershell
Add-AdfsClient -Name "RMS Sharing App for macOS" -ClientId "96731E97-2204-4D74-BEA5-75DCA53566C3" -RedirectUri @("com.microsoft.rms-sharing-for-osx://authorize")
```
```powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier '96731E97-2204-4D74-BEA5-75DCA53566C3' -ServerRoleIdentifier api.rms.rest.com -ScopeNames "openid"
```

- (Azure Information Protection アプリを使用して) iOS デバイスの場合は、次に示す順序で両方のコマンドを実行してください。
```powershell
Add-AdfsClient -Name "Azure Information Protection app for iOS" -ClientId "9D7590FB-9536-4D87-B5AA-FAA863DCC3AB" -RedirectUri @("com.microsoft.rms-sharing-for-ios://authorize")
```

```powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier '9D7590FB-9536-4D87-B5AA-FAA863DCC3AB' -ServerRoleIdentifier api.rms.rest.com -ScopeNames "openid"
```

- (Azure Information Protection アプリを使用して) Android デバイスの場合は、次に示す順序で両方のコマンドを実行してください。
```powershell
Add-AdfsClient -Name "Azure Information Protection app for Android" -ClientId "ECAD3080-3AE9-4782-B763-2DF1B1373B3A" -RedirectUri @("com.microsoft.rms-sharing-for-android://authorize")
```
```powershell
Grant-AdfsApplicationPermission -ClientRoleIdentifier 'ECAD3080-3AE9-4782-B763-2DF1B1373B3A' -ServerRoleIdentifier api.rms.rest.com -ScopeNames "openid"
```

デバイスに Microsoft Office アプリのサポートを追加するには、次の PowerShell コマンドを実行します。
- Mac、iOS、Android デバイスの場合は、次の順序で両方のコマンドを実行してください。

```powershell
Add-AdfsClient –Name "Office for Mac and Office Mobile" –ClientId "d3590ed6-52b3-4102-aeff-aad2292ab01c" –RedirectUri @("urn:ietf:wg:oauth:2.0:oob")
```

```powershell
Set-AdfsClient -TargetClientId d3590ed6-52b3-4102-aeff-aad2292ab01c -RedirectUri "urn:ietf:wg:oauth:2.0:oob","launch-word://com.microsoft.Office.Word","launch-excel://com.microsoft.Office.Excel","launch-ppt://com.microsoft.Office.Powerpoint"
```

### <a name="specifying-the-dns-srv-records-for-the-ad-rms-mobile-device-extension"></a>AD RMS モバイルデバイス拡張機能の DNS SRV レコードの指定

ユーザーが使用する各電子メール ドメインに対して DNS SRV レコードを作成する必要があります。 すべてのユーザーが 1 つの親ドメインからの子ドメインを使用し、この連続する名前空間のすべてのユーザーが同じ RMS クラスターを使用する場合は、親ドメインの SRV レコードを 1 つだけ使用すれば済みます。RMS が、適切な DNS レコードを検索します。
SRV レコードの形式は次のとおりです: _rmsdisco _tcp。 \<emailsuffix>\<portnumber>\<RMSClusterFQDN>

> [!NOTE]
> に443を指定し \<portnumber> ます。 DNS で別のポート番号を指定することもできますが、モバイルデバイス拡張機能を使用するデバイスでは常に443が使用されます。

たとえば、組織に次の電子メール アドレスを使用するユーザーがいて、
  - _user@contoso.com
  - _user@sales.contoso.com
  - _user@fabrikam.com _Rmsserver の名前とは異なる RMS クラスターを使用する _contoso .com の子ドメインが他にない場合は、次の値を持つ2つの DNS SRV レコードを作成します。
- _rmsdisco _rmsdisco._http _rmsdisco._http._tcp. contoso .com 443 _rmsserver
- _rmsdisco _rmsdisco._http _rmsdisco._http._tcp. fabrikam. com 443 _rmsserver

Windows Server で DNS サーバーの役割を使用する場合は、DNS マネージャーコンソールで SRV レコードのプロパティを確認するために、次の表を参考にしてください。

|フィールド|値|
|------|------|
|Domain|_tcp. contoso .com
|サービス|_rmsdisco
|プロトコル|_http
|Priority|0
|Weight|0
|ポート番号|443
|このサービスを提供しているホスト|_rmsserver. contoso .com

|フィールド|値|
|------|------|
|Domain|_tcp. fabrikam .com
|サービス|_rmsdisco
|プロトコル|_http
|Priority|0
|Weight|0
|ポート番号|443
|このサービスを提供しているホスト|_rmsserver. contoso .com|
| | |

電子メールドメインの DNS SRV レコードに加えて、RMS クラスタードメインに別の DNS SRV レコードを作成する必要があります。 このレコードには、コンテンツを保護する RMS クラスターの Fqdn を指定する必要があります。 RMS で保護されているすべてのファイルには、そのファイルを保護したクラスターへの URL が含まれます。 モバイル デバイスは、DNS SRV レコードと、レコードで指定されている URL FQDN を使用して、モバイル デバイスをサポートできる対応する RMS クラスターを探します。

たとえば、RMS クラスターが **_rmsserver** の場合は、次の値を持つ DNS SRV レコードを作成します。 **_rmsdisco 443 _rmsserver** という値が指定されていることを確認します。

Windows Server で DNS サーバーの役割を使用する場合は、DNS マネージャーコンソールで SRV レコードのプロパティのガイドとして次の表を参照してください。

|フィールド|値|
|------|------|
|Domain|_tcp. contoso .com
|サービス|_rmsdisco
|プロトコル|_http
|Priority|0
|Weight|0
|ポート番号|443
|このサービスを提供しているホスト|_rmsserver. contoso .com|
| | |

## <a name="deploying-the-ad-rms-mobile-device-extension"></a>AD RMS モバイル デバイス拡張機能の展開

AD RMS モバイルデバイス拡張機能をインストールする前に、前のセクションの前提条件が満たされていることと、AD FS サーバーの URL がわかっていることを確認してください。 次に、次を実行します。

1. Microsoft ダウンロードセンターから AD RMS モバイルデバイス拡張機能 (ADRMS.MobileDeviceExtension.exe) をダウンロードします。
1. **ADRMS.MobileDeviceExtension.exe** を実行して、モバイルデバイス拡張機能のセットアップウィザード Active Directory Rights Management サービスを開始します。
メッセージが表示されたら、以前に構成した AD FS サーバーの URL を入力します。
1. ウィザードを完了します。

RMS クラスター内のすべてのノードで、このウィザードを実行します。

AD RMS クラスターと AD FS サーバーの間にプロキシサーバーがある場合、既定では、AD RMS クラスターはフェデレーションサービスに接続できません。 この場合、AD RMS はモバイルクライアントから受信したトークンを検証できず、要求を拒否します。 この通信をブロックするプロキシサーバーがある場合は、AD RMS が AD FS サーバーに接続する必要があるときにプロキシサーバーをバイパスできるように、AD RMS mobile device extension web サイトから web.config ファイルを更新する必要があります。

#### <a name="updating-proxy-settings-for-the-ad-rms-mobile-device-extension"></a>AD RMS モバイルデバイス拡張機能のプロキシ設定を更新しています

1. **Files\Active Directory Rights Management Services Mobile Device Extension\Web Service** にある web.config ファイルを開きます。

1. 次のノードをファイルに追加します。

    ```PowerShell
       <system.net>
        <defaultProxy>
            <proxy  proxyaddress="http://<proxy server>:<port>"
                    bypassonlocal="true"
            />
            <bypasslist>
                <add address="<AD FS URL>" />
            </bypasslist>
        </defaultProxy>
    <system.net>
    ```
1. 次の変更を行い、ファイルを保存します。
    - \<proxy-server>をプロキシサーバーの名前またはアドレスに置き換えます。
    - を、 \<port> プロキシサーバーが使用するように構成されているポート番号に置き換えます。
    - \<AD FS URL>をフェデレーションサービスの URL に置き換えます。 HTTP プレフィックスを含めないでください。

    > [!NOTE]
    > プロキシ設定の上書きの詳細については、 [プロキシ構成](/dotnet/framework/network-programming/proxy-configuration) のドキュメントを参照してください。

1. たとえば、コマンドプロンプトから管理者として **iisreset** を実行して、IIS をリセットします。

RMS クラスター内のすべてのノードで、この手順を繰り返します。


## <a name="see-also"></a>参照

Azure Information Protection の詳細を確認し、他の AIP のお客様と連絡をとって、AIP 製品マネージャーと [API yammer グループ](https://www.yammer.com/askipteam/)を使用します。 