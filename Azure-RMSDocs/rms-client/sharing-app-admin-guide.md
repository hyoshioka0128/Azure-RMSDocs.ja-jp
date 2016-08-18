---
title: "Rights Management 共有アプリケーション管理者ガイド | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/05/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d9992e30-f3d1-48d5-aedc-4e721f7d7c25
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f7cf74355aa39928fd66a4be13a9b65428da7480
ms.openlocfilehash: 08226cd930f90bc7c9cda4c65315ee6472fbcf52


---


# Rights Management 共有アプリケーション管理者ガイド

*適用対象: Active Directory Rights Management サービス、Azure Rights Management、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*


企業ネットワークで Microsoft Rights Management 共有アプリケーションを担当している場合や、「[Rights Management sharing application user guide (Rights Management 共有アプリケーション ガイド](sharing-app-user-guide.md))」または「[FAQ for Microsoft Rights Management Sharing Application for Windows (Windows 用 Microsoft Rights Management 共有アプリケーションの FAQ)](http://go.microsoft.com/fwlink/?LinkId=303971)」よりも詳細な技術情報が必要な場合は、以下の情報を使用してください。

RMS 共有アプリケーションは Azure RMS での作業に最適です。このデプロイメント構成では、別の組織のユーザーへの保護された添付ファイルの送信、および電子メール通知やドキュメントの追跡と取り消しなどのオプションがサポートされているためです。  ただし、いくつかの制限はあるものの、オンプレミス バージョンの AD RMS でも使用できます。 Azure RMS と AD RMS でサポートされている機能の包括的な比較については、「[Azure Rights Management と AD RMS の比較](../understand-explore/compare-azure-rms-ad-rms.md)」をご覧ください。 AD RMS を所有していて、Azure RMS に移行する場合は、「[AD RMS から Azure Rights Management に移行する](../plan-design/migrate-from-ad-rms-to-azure-rms.md)」をご覧ください。

Rights Management 共有アプリケーションの技術的概要、ネイティブ保護とジェネリック保護についての情報、サポートされているファイルの種類とファイル名拡張子、既定の保護レベルの変更方法については、「[Microsoft Rights Management 共有アプリケーションの技術的概要と保護の詳細](sharing-app-admin-guide-technical.md)」を参照してください。 

## Microsoft Rights Management 共有アプリケーションの自動デプロイ
Windows 版の RMS 共有アプリケーションはスクリプト化されたインストールをサポートするため、企業のデプロイメントに適しています。

インストールの前提条件は、コンピューターで Windows 7 Service Pack 1 以降のバージョンを実行していることと、Microsoft Framework Version 4.0 以降がインストールされていることだけです。 Microsoft .NET Framework 4.0 をインストールする必要がある場合は、 [Microsoft ダウンロード センターからダウンロードしてインストール](http://www.microsoft.com/download/details.aspx?id=17718)できます。

### RMS 共有アプリケーションを自動デプロイメント用にダウンロードするには

1.  Microsoft ダウンロード センターの「 [Windows 用 Microsoft Rights Management 共有アプリケーション](http://www.microsoft.com/download/details.aspx?id=40857) 」ページに移動して、[ **ダウンロード**] をクリックします。

2.  必要なファイルを選択してダウンロードします。 次の 2 つのクライアント インストール パッケージがあります。1 つは Windows 64 ビット (Microsoft Rights Management 共有アプリケーション x64.zip)、もう 1 つは Windows 32 ビット (Microsoft Rights Management 共有アプリケーション x86.zip) です。

3.  圧縮されたインストール パッケージから、ダブルクリックなどによりファイルを抽出します。 次に、抽出したファイルを、クライアント コンピューターがアクセスできるネットワークの場所にコピーします。

RMS 共有アプリケーションのセットアップ パッケージは、さまざまなデプロイメント シナリオをサポートしており、次のものが含まれます。

|説明|展開シナリオ|
|---------------|-----------------------|
|Microsoft Online サインイン アシスタント|Office 2010 および Azure RMS<br /><br />Office 2013 および Azure RMS ([2015 年 6 月 9 日付 Office 2013 用更新プログラム](https://support.microsoft.com/kb/3054853) (KB3054853) をインストールしていない場合)|
|Office 用の修正プログラム (KB 2596501)|Office 2010 および Azure RMS<br /><br />Office 2010 および Active Directory RMS|
|AD RMS クライアント 1.0 が Azure RMS と連携できるようにするための修正プログラム (KB 2843630)|Office 2010 および Azure RMS<br /><br />Office 2010 および Active Directory RMS|
|AD RMS クライアントおよび RMS 共有アプリケーション|Office 2016 または Office 2013 および Azure RMS または Active Directory RMS<br /><br />Office 2010 および Azure RMS<br /><br />Office 2010 および Active Directory RMS<br /><br />RMS 共有アプリケーションおよび Office アドインのみ|
|リボン用 Office アドイン|Office 2016 または Office 2013 および Azure RMS または Active Directory RMS<br /><br />Office 2010 および Azure RMS<br /><br />Office 2010 および Active Directory RMS<br /><br />RMS 共有アプリケーションおよび Office アドインのみ|
|Azure Active Directory Rights Management 準備ツール|Office 2010 および Azure RMS|
次の手順を使用して、これらのデプロイメント シナリオ用に RMS 共有アプリケーションのデプロイに必要なコマンドを識別します。

-   **Office 2016 または Office 2013 および Azure RMS または Active Directory RMS**

    ユーザーが Office 2016 または Office 2013 を実行しており、組織では Azure RMS または Active Directory RMS を使用していて、ユーザーが Azure RMS または Active Directory RMS を使用している他の組織と共同作業を行っている。

-   **Office 2010 および Azure RMS**

    ユーザーが Office 2010 を実行しており、組織では Azure RMS を使用していて、ユーザーが Azure RMS または Active Directory RMS を使用している他の組織と共同作業を行っている。

-   **Office 2010 および Active Directory RMS**

    ユーザーが Office 2010 を実行しており、組織では AD RMS を使用していて、ユーザーが Azure RMS を使用している他の組織と共同作業を行っている。

-   **RMS 共有アプリケーションおよび Office アドインのみ**

    ユーザーが Office 2016、Office 2013 または Office 2010 を実行しており、組織では AD RMS を使用していて、ユーザーが Azure RMS を使用している他の組織と共同作業を行う必要がない。 このインストールでは、共有アプリケーションと Office アドインのみをインストールできます。

> [!NOTE]
> これらのシナリオにおいて、組織で AD RMS を実行している場合、ユーザーは Azure RMS を使用している他の組織から保護されたコンテンツを受信できますが、Azure RMS を使用している組織のユーザーに保護されたコンテンツを送信することはできません。 ただし、組織が Azure RMS を実行している場合、ユーザーは保護されたコンテンツを他の組織との間で送受信することができます。

各手順のインストールを完了するには、コンピューターを再起動する必要があります。 **shutdown /i** のようなコマンドを使用して、自動再起動を開始できます。

### Office 2016 または Office 2013 用 RMS 共有アプリケーションおよび Azure RMS または Active Directory RMS をデプロイするには

-   RMS 共有アプリケーションと関連コンポーネントをインストールする各コンピューターで、昇格した特権で次のコマンドを実行します。

    ```
    setup.exe /s
    ```

成功したかどうかを確認するには、このトピックの[インストールの成功の確認](#verifying-installation-success)セクションをご覧ください。

### Office 2010 用 RMS 共有アプリケーションおよび Azure RMS をデプロイするには

1.  Azure Active Directory Rights Management 準備ツールを実行して組織の証明サービスの URL を取得できるように、Office 365 または Azure Active Directory テナントのグローバル管理者である必要があります。 このツールは、1 台のコンピューターで 1 回のみ実行する必要があります。 RMS 共有アプリケーションを各コンピューターにインストールする場合は、証明サービスの URL を使用します。

    1.  ローカル管理者アカウントを使用して、コンピューターにログインします。

    2.  そのコンピューターで、 [Microsoft Online サインイン アシスタントをダウンロードしてインストールします](http://www.microsoft.com/download/details.aspx?id=28177)。

    3.  次のコマンドを実行し、証明サービスの URL を画面に表示します。次に、これをコピーして、この後の手順のために保存します。

        -   Windows 8.1 および Windows 8、64 ビットの場合:

            ```
            x64\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   Windows 8.1 および Windows 8、32 ビットの場合:

            ```
            X86\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        -   Windows 7、64 ビットの場合:

            ```
            x64\win7\aadrmprep.exe /findCertificationUrl /logfile "<log file path and name>"
            ```

        > [!NOTE]
        > このコマンドでは、Azure の資格情報の入力が求められる場合があります。 コンピューターがドメインに参加していない場合は、入力が求められます。 コンピューターがドメインに参加している場合は、キャッシュされた資格情報をツールで使用できる場合があります。

2.  RMS 共有アプリケーションをインストールする各コンピューターで、昇格した特権を使用して次のコマンドを 1 回実行します。

    ```
    setup.exe /s /configureO2010Admin /certificationUrl <certification_url>
    ```

3.  RMS 共有アプリケーションのインストール先となる各コンピューターで、そのコンピューターの各ユーザーが次のコマンドを実行する必要があります (昇格した特権は必要ありません)。 これを行うにはさまざまな方法があります。たとえば、コマンド (電子メール メッセージ内のリンクやヘルプ デスク ポータル上のリンクなど) の実行をユーザーに依頼したり、ログオン スクリプトに追加したりします。

    ```
    bin\RMSSetup.exe /configureO2010Only
    ```

成功したかどうかを確認するには、このトピックの[インストールの成功の確認](#verifying-installation-success)セクションをご覧ください。

### Office 2010 用 RMS 共有アプリケーションおよび Active Directory RMS をデプロイするには

1.  RMS 共有アプリケーションをインストールする各コンピューターで、昇格した特権で次のコマンドを実行します。

    ```
    setup.exe /s /configureO2010Admin
    ```

2.  RMS 共有アプリケーションをインストールする各コンピューターで、ユーザーは次のコマンドを実行する必要があります (昇格した特権は必要ありません)。 これを行うにはさまざまな方法があります。たとえば、コマンド (電子メール メッセージ内のリンクやヘルプ デスク ポータル上のリンクなど) の実行をユーザーに依頼したり、ログオン スクリプトに追加したりします。

    -   Windows 10、Windows 8.1 および Windows 8、64 ビットの場合:

        ```
        x64\aadrmprep.exe /configureO2010
        ```

    -   Windows 10、Windows 8.1 および Windows 8、32 ビットの場合:

        ```
        X86\aadrmprep.exe /configureO2010
        ```

    -   Windows 7、64 ビットの場合:

        ```
        x64\win7\aadrmpep.exe /configureO2010
        ```

成功したかどうかを確認するには、このトピックの[インストールの成功の確認](#verifying-installation-success)セクションをご覧ください。

### RMS 共有アプリケーションおよび Office アドインのみをインストールするには

1.  次のコマンドを使用して、AD RMS クライアントと RMS 共有アプリケーションをインストールします。

    -   64 ビット Windows の場合:

        ```
        x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    -   32 ビット Windows の場合:

        ```
        X86\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "<log file path and name>"
        ```

    例: `\\server5\apps\rms\x64\setup_ipviewer.exe /norestart /quiet /msicl "MSIRESTARTMANAGERCONTROL=Disable" /log "C:\Log files\ipviewerinstall.log"`

2.  次のコマンドを使用して、Office アドインをインストールします。

    -   64 ビット版の Office の場合:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "<log file path and name>"
        ```

    -   32 ビット版の Office の場合:

        ```
        msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x86\Setup.msi" /L*v "<log file path and name>"
        ```

    例: `\\server5\apps\rms\msiexec.exe /norestart /quiet MSIRESTARTMANAGERCONTROL=Disable /i "x64\Setup64.msi" /L*v "C:\Log files\rmsofficeinstall.log"`

成功したかどうかを確認するには、このトピックの[インストールの成功の確認](#verifying-installation-success)セクションをご覧ください。

## インストールの成功の確認
インストール ログ ファイルを使用して、インストールの成功を確認することができます。

### Office 2016 または Office 2013 用 RMS 共有アプリケーションおよび Azure RMS または Active Directory RMS のインストールの成功を確認するには

-   Setup.exe コマンドの成功を確認するには、各コンピューターで、インストール ログ ファイル **RMInstaller.log** を *%temp%\RMS_installer_&lt;guid&gt;* フォルダーで探し、終了コードを確認します。

    インストールが成功した場合、終了コードは 0 となり、それ以外の場合はインストールが失敗したことを示します。

    ログ ファイル名の例: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0\RMInstaller.log**

### Office 2010 用 RMS 共有アプリケーションおよび Azure RMS のインストールの成功を確認するには

1.  Setup.exe コマンドの成功を確認するには、各コンピューターで、インストール ログ ファイル **RMInstaller.log** を *%temp%\RMS_installer_&lt;guid&gt;* フォルダーで探し、終了コードを確認します。

    インストールが成功した場合、終了コードは 0 となり、それ以外の場合はインストールが失敗したことを示します。

    ログ ファイル名の例: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  RMSSetup.exe コマンドの成功を確認するには、ユーザーが *%localappdata%\microsoft\drm* フォルダーに次のファイルを作成しておく必要があります。

    -   CERT-Machine-2048.drm

    -   CERT-Machine.drm

    -   CLC-&#42;.drm

    -   GIC-&#42;.drm

    CLC-&#42; drm ファイルの例:

    **CLC-alice@isvtenant999.onmicrosoft.com-{1b9cfccf;k5b11;k4a10;kac15;k29b2b6980f4c}.drm**

### Office 2010 用 RMS 共有アプリケーションおよび Active Directory RMS のインストールの成功を確認するには

1.  Setup.exe コマンドの成功を確認するには、各コンピューターで、インストール ログ ファイルを *%temp%\RMS_installer_&lt;guid&gt;* フォルダーで探し、終了コードを確認します。

    インストールが成功した場合、終了コードは 0 となり、それ以外の場合はインストールが失敗したことを示します。

    ログ ファイル名の例: **C:\temp\RMS_Installer_9352fc91-1982-43bf-958a-2ef1fe9c2ed0**

2.  aadrmprep.exe コマンドの成功を確認するには、各コンピューターのインストール ログ ファイルで、 **aadrmprep.exe exited with status SUCCESS**というテキストを探します。

    > [!NOTE]
    > 場合によっては、このインストールは 2 回実行され、1 回目に失敗し、2 回目に成功することがあります。

    このツールによって変更されたレジストリを手動で確認する場合、変更は次のとおりです。

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSDRM\Federation]

        "FederationホームRealm"="urn:HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\Federation]

        "FederationホームRealm"="urn:HostedRmsOnlineService:Certification"

    -   [HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\MSDRM\ServiceLocation\Activation]

        @="&lt;certification url&gt;"

    -   [HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\14.0\Common\DRM]

        DefaultUser="&lt;default_user&gt;"

### RMS 共有アプリケーションおよび Office アドインのみのインストールの成功を確認するには

1.  Setup_ipviewer.exe コマンドの成功を確認するには、インストール ログ ファイルでテキスト「**インストールの成功またはエラーの状態 0**」を探します。

    インストールの成功を示す行の例:

    **MSI (s) (F0:B8) [14:19:57:854]:Product:Active Directory Rights Management Services Client 2.1 -- Installation completed successfully.**

    **MSI (s) (F0:B8) [14:19:57:854]:Windows Installer installed the product. Product Name:Active Directory Rights Management Services Client 2.1. Product Version:1.0.1179.1. Product Language:1033. 製造元:Microsoft Corporation. Installation success or error status:0.**

2.  Office アドインの成功を確認するには、各コンピューターのインストール ログ ファイルでテキスト「**インストールの成功またはエラーの状態 0**」を探します。

    インストールの成功を示す行の例:

    **MSI (s) (9C:88) [18:49:04:007]:Product:Microsoft RMS Office Addins -- Installation completed successfully.**

    **MSI (s) (9C:88) [18:49:04:007]:Windows Installer installed the product. Product Name:Microsoft RMS Office Addins. Product Version:1.0.7. Product Language:1033. 製造元:Microsoft. Installation success or error status:0.**

## アンインストール コマンド
これらのデプロイメントに必要なすべてのインストール コマンドで、アンインストール コマンドがサポートされているわけではありません。 AD RMS クライアントと、共有アプリケーションをアンインストールし、Office アドインをアンインストールすることができます。 これらの要素をアンインストールするには、次のコマンドを使用します。

### AD RMS クライアントおよび RMS 共有アプリケーションをアンインストールするには

-   次のコマンドを使用します。

    -   64 ビット Windows の場合:

        ```
        x64\setup_ipviewer.exe /uninstall /quiet
        ```

    -   32 ビット Windows の場合:

        ```
        x86\setup_ipviewer.exe /uninstall /quiet
        ```

### Office アドインをアンインストールするには

-   次のコマンドを使用します。

    -   64 ビット版の Office の場合:

        ```
        msiexec /x \x64\Setup[64].msi /quiet
        ```

    -   32 ビット版の Office の場合:

        ```
        msiexec /x \x86\Setup.msi /quiet
        ```

## 自動更新の抑制
既定では、新しいバージョンの RMS 共有アプリケーションがある場合、ユーザーに通知され、ダウンロードを求めるメッセージが表示されます。 次のレジストリを編集すると、この通知が表示されないようにすることができます。

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** に移動し、まだ存在していない場合は、**RmsSharingApp** という名前の新しいキーを作成します。

2.  **RmsSharingApp**を選択し、新しい DWORD 値の **AllowUpdatePrompt**を作成して、その値を **0**に設定します。

RMS 共有アプリケーションは、WSUS ではサポートされていないため、次の手法を使用して、すべてのユーザーにデプロイする前に RMS 共有アプリケーションの新しいバージョンをテストできます。

1.  すべてのユーザーのコンピューターで、自動更新を抑制するスクリプトを実行します。 管理者が新しいバージョンのテストに使用するコンピューターでは、このスクリプトを実行しないでください。

2.  新しいバージョンが使用可能になったら、管理者はそれをダウンロードしてテストします。

3.  テストが完了し、問題を解決したら、このガイドの自動デプロイメントの手順を使用して、すべてのユーザーに最新バージョンをデプロイします。

## Azure RMS のみ:ドキュメント追跡の構成
[ドキュメント追跡をサポートするサブスクリプション](https://technet.microsoft.com/dn858608)がある場合、組織内のすべてのユーザーに対してドキュメント追跡サイトが既定で有効になっています。  ドキュメント追跡では、ユーザーが共有している保護されたドキュメントにアクセスしようとしている人々の電子メール アドレス、これらの人々がアクセスを試みた時刻、およびその場所などの情報が示されます。 プライバシーに関する要件により、組織でこの情報の表示が禁止されている場合、[Disable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623032) コマンドレットを使用して、ドキュメント追跡サイトへのアクセスを無効にすることができます。 サイトへのアクセスは [Enable-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037) を使用して、いつでも再度有効にすることができます。また、[Get-AadrmDocumentTrackingFeature](http://go.microsoft.com/fwlink/?LinkId=623037) を使用して、アクセスが現在有効になっているか無効になっているかを確認できます。

これらのコマンドを使用するには、バージョン **2.3.0.0** 以降の Windows PowerShell 用 Azure RMS モジュールが必要です。  インストール手順については、「[Azure Rights Management 用 Windows PowerShell をインストールする](../deploy-use/install-powershell.md)」を参照してください。

> [!TIP]
> 事前にモジュールをダウンロードしてインストールしてある場合は、次のコマンドレットを実行してバージョン番号を確認します。 `(Get-Module aadrm –ListAvailable).Version`

次の URL はドキュメント追跡で使用されるため、許可する必要があります (たとえば、セキュリティ強化を有効にして Internet Explorer を使用する場合は、信頼済みサイトに追加します):

-   https://&#42;.azurerms.com

-   https://ecn.dev.virtualearth.net

    > [!NOTE]
    > この URL は Bing マップ用です。

-   https://&#42;.microsoftonline.com

-   https://&#42;.microsoftonline-p.com

### ユーザーのドキュメントの追跡と取り消し

ユーザーは、ドキュメント追跡サイトにサインインすると、RMS 共有アプリケーションを使用して共有したドキュメントを追跡し、取り消すことができます。 Azure RMS の管理者 (グローバル管理者) としてサインインすると、ページの右上にある [管理者] アイコンをクリックして管理者モードに切り替え、組織内のユーザーが共有しているドキュメントを表示することができます。

管理者モードで実行したアクションは監査され、使用状況ログ ファイルに記録されます。これを確認してから次に進む必要があります。 このログ記録の詳細については、次のセクションを参照してください。

管理者モードの場合、ユーザーまたはドキュメントを指定して検索できます。 ユーザーを指定して検索すると、指定したユーザーが共有したすべてのドキュメントが表示されます。 ドキュメントを指定して検索すると、そのドキュメントを共有した組織内のユーザーが全員表示されます。 検索結果を調べて、ユーザーが共有したドキュメントを追跡し、必要に応じてそのドキュメントを取り消すことができます。 

管理者モードを終了するには、**[管理者モードを終了する]** の横にある **[X]** をクリックします。

ドキュメント追跡サイトを使用する手順については、ユーザー ガイドの「[RMS 共有アプリケーションを使用してドキュメントを追跡および取り消す](sharing-app-track-revoke.md)」を参照してください。



### ドキュメント追跡サイトの使用状況のログ記録

使用状況ログ ファイルの 2 つのフィールド **AdminAction** と **ActingAsUser** は、ドキュメント追跡に適用できます。

**AdminAction** - このフィールドは、管理者が管理者モードでドキュメント追跡サイトを使用した場合 (たとえば、ユーザーの代理でドキュメントを取り消した場合や、ドキュメントが共有された時間を確認した場合) に true になります。 ユーザーがドキュメント追跡サイトにサインインすると、このフィールドは空になります。

**ActingAsUser** - AdminAction フィールドが true の場合、このフィールドには、検索したユーザーまたはドキュメント所有者の代理で管理者が操作しているユーザー名が含まれます。 ユーザーがドキュメント追跡サイトにサインインすると、このフィールドは空になります。 

また、ユーザーと管理者がドキュメント追跡サイトを使用する方法をログに記録する要求の種類もあります。 たとえば、**RevokeAccess** は、ユーザーまたはユーザーの代理の管理者が、ドキュメント追跡サイトでドキュメントを取り消した場合の要求の種類です。 この要求の種類と AdminAction フィールドを組み合わせて、ユーザーが自分のドキュメントを取り消したか (AdminAction フィールドが空)、管理者がユーザーの代理でドキュメントを取り消したか (AdminAction が true) を判断できます。


使用状況ログの詳細については、「[Azure Rights Management の利用状況をログに記録して分析する](../deploy-use/log-analyze-usage.md)」を参照してください。

## AD RMS のみ: 組織内での複数の電子メール ドメインのサポート
AD RMS を使用し、(たとえば、合併や買収の結果) 組織のユーザーが複数の電子メール ドメインを保有している場合は、次のレジストリ編集を行います。

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC** に移動し、まだ存在していない場合は、**RmsSharingApp** という名前の新しいキーを作成します。

2.  **RmsSharingApp** を選択し、**FederatedDomains** という名前の新しい複数文字列値を作成して、組織で使用されるドメインとすべてのサブドメインを追加します。 ワイルドカードはサポートされません。

    例:Coho Vineyard &amp; Winery という会社には、標準の電子メール ドメインとして **cohovineyardandwinery.com** がありますが、合併の結果、**cohowinery.com**、**eastcoast.cohowinery.com**、および **cohovineyard** という電子メール ドメインも使用されています。 **FederatedDomains** 値のデータとして、管理者は「**cohowinery.com; eastcoast.cohowinery.com; cohovineyard**」と入力します。

このレジストリ変更を行わないと、ユーザーは、組織の他のユーザーによって保護されたコンテンツを使用できなくなる可能性があります。 Azure RMS を使用する場合、このレジストリ編集は必要ありません。


## 次のステップ
保護レベルの違い (ネイティブとジェネリック)、サポートされているファイルの種類とファイル名拡張子、既定の保護レベルの変更方法などを説明する追加の技術情報については、「[Technical overview for the Rights Management sharing application (Rights Management 共有アプリケーションの技術概要)](sharing-app-admin-guide-technical.md)」をご覧ください。




<!--HONumber=Aug16_HO1-->


