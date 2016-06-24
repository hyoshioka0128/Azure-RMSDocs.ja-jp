---
# required metadata

title: AD RMS から Azure Rights Management への移行 - フェーズ 2 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793


# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
# 移行フェーズ 2 - クライアント側の構成

*適用対象: Active Directory Rights Management サービス、Azure Rights Management*

AD RMS から Azure Rights Management (Azure RMS) への移行フェーズ 2 では、次の情報を使用してください。 これらの手順では、「[AD RMS から Azure Rights Management への移行](migrate-from-ad-rms-to-azure-rms.md)」の手順 5. を説明します。.


## 手順 5.  Azure RMS を使用するようにクライアントを再構成する
Windows クライアントの場合:

1.  [移行スクリプトをダウンロードします](http://go.microsoft.com/fwlink/?LinkId=524619)。

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    これらのスクリプトは、AD RMS ではなく Azure RMS サービスを使用するように Windows コンピューター上の構成をリセットします。

2.  リダイレクト スクリプト (Redirect_OnPrem.cmd) の指示に従って、新しい Azure RMS テナントをポイントするようにスクリプトを変更します。

3.  Windows コンピューターで、ユーザーのコンテキストで管理者特権を使用してこれらのスクリプトを実行します。

モバイル デバイス クライアントおよび Mac コンピューターの場合:

-   [AD RMS モバイル デバイス拡張機能](http://technet.microsoft.com/library/dn673574.aspx)をデプロイするときに作成した DNS SRV レコードを削除します。.

#### 移行スクリプトによって行われる変更
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

-   次のレジストリ値を削除します。

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd:

-   次の各場所の下に、パラメーターとして指定された各 URL の次のレジストリ値を作成します。

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    各エントリには、**https://OldRMSserverURL/_wmcs/licensing** の REG_SZ 値が含まれ、**https://&lt;YourTenantURL&gt;/_wmcs/licensing** という形式のデータが含まれます。.

    > [!NOTE]
    > *&lt;YourTenantURL&gt;* の形式は、**{GUID}.rms.[Region].aadrm.com** です。.
    > 
    > 例: 5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > Azure RMS の **Get-AadrmConfiguration** コマンドレットを実行するときに [RightsManagementServiceId](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) 値を識別することによって、この値を見つけることができます。


## 次のステップ
移行を続行するには、「[移行フェーズ 3 - サービス構成のサポート](migrate-from-ad-rms-phase3.md)」に進んでください。.

<!--HONumber=Apr16_HO4-->


