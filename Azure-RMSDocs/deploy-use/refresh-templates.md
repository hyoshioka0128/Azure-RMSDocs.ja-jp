---
# required metadata

title: テンプレートの更新 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8c2064f0-dd71-4ca5-9040-1740ab8876fb

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# ユーザー用のテンプレートの更新
Azure RMS を使用する場合、テンプレートは自動的にクライアント コンピューターにダウンロードされるので、ユーザーはアプリケーションからテンプレートを選択できます。 しかし、テンプレートを変更する場合は、追加の手順が必要になることがあります。

|アプリケーションまたはサービス|変更後のテンプレートの更新方法|
|--------------------------|---------------------------------------------|
|Exchange Online|テンプレートを更新するには、手動構成が必要です。<br /><br />構成手順については、以下の「[Exchange Online のみ: 変更されたカスタム テンプレートをダウンロードするように Exchange を構成する方法](#exchange-online-only-how-to-configure-exchange-to-download-changed-custom-templates)」セクションを参照してください。|
|Office 365|自動更新 - 追加の手順は必要ありません。|
|Office 2016 と Office 2013:<br /><br />Windows 用 RMS 共有アプリケーション|自動更新 - スケジュールどおりに更新されます。<br /><br />以降のバージョンの Office の場合: 既定の更新間隔は 7 日ごとです。<br /><br />Windows 用 RMS 共有アプリケーション: バージョン 1.0.1784.0 以降では、既定の更新間隔は 1 日ごとです。 それ以前のバージョンでは、既定の更新間隔は 7 日ごとです。<br /><br />このスケジュールより前に強制的に更新するには、以下の「[Office 2016、Office 2013、Windows 用 RMS 共有アプリケーション: 変更されたカスタム テンプレートを強制的に更新する方法](#office-2016-office-2013-and-rms-sharing-application-for-windows-how-to-force-a-refresh-for-a-changed-custom-template)」セクションを参照してください。|
|Office 2010|ユーザーがログオンしたときに更新されます。<br /><br />強制的に更新するには、ログオフしてもう一度ログオンするようにユーザーに依頼します。 または、以下の「[Office 2010 のみ: 変更されたカスタム テンプレートを強制的に更新する方法](#office-2010-only-how-to-force-a-refresh-for-a-changed-custom-template)」セクションを参照してください。|
RMS 共有アプリケーションを使用している モバイル デバイスの場合、テンプレートは自動的にダウンロードされるので (必要な場合はさらに更新されます)、追加の構成は必要ありません。

## Exchange Online のみ: 変更されたカスタム テンプレートをダウンロードするように Exchange を構成する方法
Exchange Online 用の Information Rights Management (IRM) を既に構成している場合は、Exchange Online で Windows PowerShell を使用して、次の変更を加えるまでカスタム テンプレートはユーザーにダウンロードされません。

> [!NOTE]
> Exchange Online で Windows PowerShell を使用する方法の詳細については、「[Exchange Online による PowerShell の使用](https://technet.microsoft.com/library/jj200677%28v=exchg.160%29.aspx)」を参照してください。

テンプレートを変更するたびにこの手順を実行する必要があります。

### Exchange Online 用のテンプレートを更新するには

1.  Exchange Online で Windows PowerShell を使用し、サービスに接続します。

    1.  Office 365 のユーザー名とパスワードを入力します。

        ```
        $Cred = Get-Credential
        ```

    2.  Exchange Online サービスに接続するには、次の 2 つのコマンドを実行します。

        ```
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
        ```

        ```
        Import-PSSession $Session
        ```

2.  [Import-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200724%28v=exchg.160%29.aspx) コマンドレットを使用して、信頼された発行ドメイン (TPD) を Azure RMS から再インポートします。

    ```
    Import-RMSTrustedPublishingDomain -Name "<TPD name>" -RefreshTemplates -RMSOnline
    ```
    たとえば、TPD 名が **RMS Online - 1** (多くの組織で一般的に使用される名前) の場合、「**Import-RMSTrustedPublishingDomain -Name "RMS Online - 1" -RefreshTemplates -RMSOnline**」と入力します。

    > [!NOTE]
    > TPD 名を確認するには、[Get-RMSTrustedPublishingDomain](http://technet.microsoft.com/library/jj200707%28v=exchg.160%29.aspx) コマンドレットを使用できます。

3.  テンプレートが正常にインポートされたことを確認するには、数分待ってから、[Get-RMSTemplate](http://technet.microsoft.com/library/dd297960%28v=exchg.160%29.aspx) コマンドレットを実行します。このとき、Type には All を設定します。 例:

    ```
    Get-RMSTemplate -TrustedPublishingDomain "RMS Online - 1" -Type All
    ```
    > [!TIP]
    > 出力のコピーを残しておくと、後でテンプレートを保存する場合にテンプレート名または GUID を簡単にコピーできて便利です。

4.  インポートしたテンプレートのうち、Outlook Web App で使用できるようにするテンプレートごとに、[Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) コマンドレットを使用し、Type を Distributed に設定する必要があります。

    ```
    Set-RMSTemplate -Identity "<name  or GUID of the template>" -Type Distributed
    ```
    Outlook Web Access は UI を 24 時間キャッシュするため、ユーザーには最長 1 日間新しいテンプレートが表示されない可能性があります。

さらに、テンプレート (カスタムまたは既定) がアーカイブされ、Exchange Online と Office 365 が使用されている場合、ユーザーが Outlook Web App または Exchange ActiveSync プロトコルを使用するモバイル デバイスを使用する場合、ユーザーはアーカイブされたテンプレートを引き続き表示できます。

これらのテンプレートがユーザーに表示されないようにするには、Exchange Online の Windows PowerShell を使用してサービスに接続し、次のコマンドを実行して [Set-RMSTemplate](http://technet.microsoft.com/library/hh529923%28v=exchg.160%29.aspx) コマンドレットを使用します。

```
Set-RMSTemplate -Identity "<name or GUID of the template>" -Type Archived
```

## Office 2016、Office 2013、Windows 用 RMS 共有アプリケーション: 変更されたカスタム テンプレートを強制的に更新する方法
Office 2016、Office 2013 または Windows 用 Rights Management (RMS) 共有アプリケーションを実行しているコンピューター上でレジストリを編集すると、変更されたテンプレートがコンピューター上で、既定値よりも短い周期で更新されるように自動スケジュールを変更できます。 レジストリ値の既存のデータを削除して直ちに更新することもできます。

> [!WARNING]
> レジストリ エディターを誤って使用すると、深刻な問題が発生し、オペレーティング システムの再インストールが必要になることがあります。 マイクロソフトは、レジストリ エディターを誤って使用したために発生した問題を解決できることを保証できません。 レジストリ エディターは、各自の責任で使用してください。

### 自動スケジュールを変更するには

1.  レジストリ エディターを使用して、次のレジストリ値のいずれかを作成し設定します。

    - 更新頻度を日単位で設定するには (最短 1 日): **TemplateUpdateFrequency** という名前の新しいレジストリ値を作成し、データの整数値を定義します。これにより、ダウンロードされたテンプレートの変更をダウンロードする周期 (日数) が指定されます。 この新しいレジストリ値を作成する際にレジストリ パスを検索するには、次の表を使用します。

        **レジストリ パス:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **種類:** REG_DWORD

        **値:** TemplateUpdateFrequency


    - To set an update frequency in seconds (minimum of 1 second):  Create a new registry value named **TemplateUpdateFrequencyInSeconds** and define an integer value for the data, which specifies the frequency in seconds to download any changes to a downloaded template. Use the following table to locate the registry path to create this new registry value.

        **Registry path:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **Type:** REG_DWORD

        **Value:** TemplateUpdateFrequencyInSeconds

    Make sure that you create and set one of these registry values, not both. If both are present, **TemplateUpdateFrequency** is ignored.

2.  テンプレートを直ちに更新する場合は、次の手順に進みます。 それ以外の場合は、Office アプリケーションとエクスプローラーのインスタンスを再起動します。

### 直ちに更新するには

1.  レジストリ エディターを使用して、 **LastUpdatedTime** 値のデータを削除します。 たとえば、"**2015-04-20T15:52**" と表示されている場合は、この 2015-04-20T15:52 を削除して、何も表示されていない状態にします。 次の情報を使用して、このレジストリ値データを削除するレジストリ パスを見つけてください。

    **レジストリ パス:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\<*MicrosoftRMS_FQDN*>\Template

    **種類:** REG_SZ

    **値:** LastUpdatedTime

    > [!TIP]
        > レジストリ パスの <*MicrosoftRMS_FQDN*> は、Microsoft RMS サービスの FQDN を指します。 この値を確認するには:

    > 1.  Azure RMS 用の [Get-AadrmConfiguration](https://msdn.microsoft.com/library/windowsazure/dn629410.aspx) コマンドレットを実行します。 Azure RMS 用の Windows PowerShell モジュールをまだインストールしていない場合は、「[Azure Rights Management 用 Windows PowerShell をインストールする](install-powershell.md)」を参照してください。
    > 2.  出力から、 **LicensingIntranetDistributionPointUrl** の値を確認します。
    > 
    >     例: **LicensingIntranetDistributionPointUrl: https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
    > 3.  この値から、**https://** 文字列と **/_wmcs/licensing** 文字列を削除します。 残りの値が、Microsoft RMS サービスの FQDN です。 この例では、Microsoft RMS サービスの FQDN は次の値になります。
    > 
    >     **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2.  **%localappdata%\Microsoft\MSIPC\Templates** フォルダーとその中に含まれているすべてのファイルを削除します。

3.  Office アプリケーションとエクスプローラーのインスタンスを再起動します。

## Office 2010 のみ: 変更されたカスタム テンプレートを強制的に更新する方法
Office 2010 を実行するコンピューター上でレジストリを編集することで、ユーザーがログオフしてもう一度ログオンするまで待たなくても、変更されたテンプレートがコンピューター上で更新されるように値を設定できます。 レジストリ値の既存のデータを削除して直ちに更新することもできます。

> [!WARNING]
> レジストリ エディターを誤って使用すると、深刻な問題が発生し、オペレーティング システムの再インストールが必要になることがあります。 マイクロソフトは、レジストリ エディターを誤って使用したために発生した問題を解決できることを保証できません。 レジストリ エディターは、各自の責任で使用してください。

### 更新頻度を変更するには

1.  レジストリ エディターを使用して、 **UpdateFrequency** という名前の新しいレジストリ値を作成し、データの整数値を定義します。これにより、ダウンロードされたテンプレートの変更をダウンロードする周期 (日数) が指定されます。 この新しいレジストリ値を作成する際にレジストリ パスを検索するには、次の表を使用します。

    **レジストリ パス:** HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement

    **種類:** REG_DWORD

    **値:** UpdateFrequency

2.  テンプレートを直ちに更新する場合は、次の手順に進みます。 それ以外の場合は、Office アプリケーションを再起動します。

### 直ちに更新するには

1.  レジストリ エディターを使用して、 **LastUpdatedTime** 値のデータを削除します。 たとえば、"**2015-04-20T15:52**" と表示されている場合は、この 2015-04-20T15:52 を削除して、何も表示されていない状態にします。 このレジストリ値データを削除する際にレジストリ パスを検索するには、次の表を使用します。

    **レジストリ パス:** HKEY_CURRENT_USER\Software\Microsoft\MSDRM\TemplateManagement

    **種類:** REG_SZ

    **値:** lastUpdatedTime


2.  **%localappdata%\Microsoft\MSIPC\Templates** フォルダーとその中に含まれているすべてのファイルを削除します。

3.  Office アプリケーションを再起動します。

## 参照
[Azure Rights Management のカスタム テンプレートを構成する](configure-custom-templates.md)

<!--HONumber=Apr16_HO3-->


