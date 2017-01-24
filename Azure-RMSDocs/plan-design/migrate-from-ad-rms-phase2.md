---
title: "AD RMS から Azure Information Protection への移行 - フェーズ 2 | Azure Information Protection"
description: "AD RMS から Azure Information Protection への移行のフェーズ 2 には、手順 5 が含まれます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/12/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 197ff53d64889487c457f574a235c76821fcf61a


---
# <a name="migration-phase-2---client-side-configuration"></a>移行フェーズ 2 - クライアント側の構成

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Office 365*

AD RMS から Azure Information Protection への移行フェーズ 2 では、次の情報を使用してください。 これらの手順では、「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」の手順 5 を説明します。


## <a name="step-5-reconfigure-clients-to-use-azure-information-protection"></a>手順 5. Azure Information Protection を使用するようにクライアントを再構成する
Windows クライアントの場合:

1.  [移行スクリプトをダウンロードする](https://go.microsoft.com/fwlink/?LinkId=524619):

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    これらのスクリプトは、AD RMS ではなく Azure Information Protection サービスを使用するように Windows コンピューター上の構成をリセットします。

2.  リダイレクト スクリプト (Redirect_OnPrem.cmd) の指示に従って、新しい Azure Information Protection テナントをポイントするようにスクリプトを変更します。

    > [!IMPORTANT]
    > この手順では、**adrms** および **adrms.contoso.com** のアドレス例を、実際の AD RMS サーバーのアドレスに置き換える必要があります。 これを行うときは、アドレスの前または後に余計なスペースが入らないように注意してください。余計なスペースがあると、移行スクリプトが中断し、問題の根本原因の特定が非常に困難になります。 編集ツールによっては、テキストを貼り付けた後でスペースが自動的に追加されることがあります。
    >
    > さらに、AD RMS サーバーが SSL/TLS サーバー証明書を使用している場合は、ライセンス URL の文字列にポート番号 **443** が含まれることを確認します。 たとえば、https:// rms.treyresearch.net:443/_wmcs/licensing となっている必要があります。 この情報は、Active Directory Rights Management サービス コンソールでクラスター名をクリックして、**[クラスターの詳細]** で確認できます。 ポート番号 443 が URL に含まれる場合は、スクリプトを変更するときにこの値を含めます。 たとえば、https://rms.treyresearch.net**:443** などとします。

3. Office 2016 を使用している場合: スクリプトは Office 2016 の構成を含むようにまだ更新されていないため、このバージョンの Office を使用している場合は、スクリプトを手動で更新する必要があります。

    - **CleanUpRMS.cmd** の場合 - `reg delete HKCU\Software\Microsoft\Office\15.0\Common\DRM /f` という行を探し、そのすぐ下に、次の行を追加します。

            reg delete HKCU\Software\Microsoft\Office\16.0\Common\DRM /f

    - **Redirect_Onprem.cmd** の場合 - `reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM" /t REG_SZ /v "DefaultServer" /d "%CloudRMS%" /F` という行を探し、そのすぐ下に、次の&2; 行を追加します。

            reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\DRM" /t REG_SZ /v "DefaultServerUrl" /d "https://%CloudRMS%/_wmcs/licensing" /F 

            reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\DRM" /t REG_SZ /v "DefaultServer" /d "%CloudRMS%" /F

    省略可能: スクリプトはコメント内の Office 2016 を参照しません。 Office 2016 にこれらの変更を反映するようにコメントを更新する場合は、**Redirect_Onprem.cmd** を次のように変更します。

    - `::     or MSIPC (Office 2013) with on-premises AD RMS` を探し、これを次のように置き換えます。
    
            ::     or MSIPC (Office 2013 and 2016) with on-premises AD RMS

    - `echo Redirect SCP for Office 2013` を探し、これを次のように置き換えます。
    
            echo Redirect SCP for Office versions based on MSIPC

    - `echo Redirect MSIPC for Office 2013` を探し、これを次のように置き換えます。
    
            echo Redirect MSIPC for Office versions based on MSIPC

4.  Windows コンピューターの場合:

    - ユーザーのコンテキストで管理者特権を使用してこれらのスクリプトを実行します。

    モバイル デバイス クライアントおよび Mac コンピューターの場合:

    -  [AD RMS モバイル デバイス拡張機能](http://technet.microsoft.com/library/dn673574.aspx)をデプロイするときに作成した DNS SRV レコードを削除します。

#### <a name="changes-made-by-the-migration-scripts"></a>移行スクリプトによって行われる変更
ここでは、移行スクリプトが行う変更について説明します。 この情報は、参照用、トラブルシューティング用、または変更を自分で行いたい場合に使用できます。

CleanUpRMS_RUN_Elevated.cmd:

-   %userprofile%\AppData\Local\Microsoft\DRM および %userprofile%\AppData\Local\Microsoft\MSIPC フォルダーの内容を、すべてのサブフォルダーおよび長い名前のファイルも含めて削除します。

-   次のレジストリ キーの内容を削除します。

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\SOFTWARE\WoW6432Node\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation

-   次のレジストリ値を追加します。

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd:

-   次の各場所の下に、パラメーターとして指定された各 URL の次のレジストリ値を作成します。

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    各エントリには、**https://OldRMSserverURL/_wmcs/licensing** の REG_SZ 値が含まれ、**https://&lt;YourTenantURL&gt;/_wmcs/licensing** という形式のデータが含まれます。

    > [!NOTE]
    > *&lt;YourTenantURL&gt;* の形式は、**{GUID}.rms.[Region].aadrm.com** です。
    > 
    > 例: 5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > Azure RMS の **Get-AadrmConfiguration** コマンドレットを実行するときに [RightsManagementServiceId](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) 値を識別することによって、この値を見つけることができます。


## <a name="next-steps"></a>次のステップ
移行を続行するには、「[移行フェーズ 3 - サービス構成のサポート](migrate-from-ad-rms-phase3.md)」に進んでください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


