---
title: "クラウド ベース RMS でサービス アプリケーション使用を有効化する方法 | Azure RMS"
description: "このトピックでは、Azure Rights Management を使用するようにサービス アプリケーションをセットアップする手順について説明します。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: EA1457D1-282F-4CF3-A23C-46793D2C2F32
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 4c3625676c7e794ef133c75881f666bae80e0513
ms.openlocfilehash: ad8c41c9f3f3515a817d508d8f5a8953daf4b440


---

# 方法: クラウド ベース RMS でのサービス アプリケーション使用の有効化

このトピックでは、Azure Rights Management を使用するようにサービス アプリケーションをセットアップする手順について説明します。 詳細については、「[Azure Rights Management の概要](https://technet.microsoft.com/library/jj585016.aspx)」を参照してください。

**重要**  
Rights Management Services SDK 2.1 サービスを Azure RMS で利用するには、独自のテナントを作成する必要があります。 詳細については、「[Azure RMS の要件: Azure RMS をサポートするクラウド サブスクリプション](../get-started/requirements-subscriptions.md)」を参照してください。

## 必要条件

-   RMS SDK 2.1 をインストールして構成する必要があります。 詳細については、[RMS SDK 2.1 の概要のページ](getting-started-with-ad-rms-2-0.md)を参照してください。
-   対称キーのオプションを使用するかその他の方法で、[ACS を介してサービス ID を作成](https://msdn.microsoft.com/en-us/library/gg185924.aspx)して、その処理中にキー情報をメモします。

## Azure Rights Management サービスへの接続

-   [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize) を呼び出します。
-   [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty) を設定します。

        C++
        int mode = IPC_API_MODE_SERVER;
        IpcSetGlobalProperty(IPC_EI_API_MODE, &(mode));


  **注** 詳細については、「[Setting the API security mode (API セキュリティ モードの設定)](setting-the-api-security-mode-api-mode.md)」を参照してください。

     
-   次の手順は、[**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx) 構造体のインスタンスを作成するためのセットアップです。**pcCredential** ([**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential)) メンバーに Azure Rights Management サービスの接続情報を設定します。
-   [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key) 構造体のインスタンスを作成するときは、対称キーのサービス ID 作成時にメモした情報使用して (このトピックで既に示した前提条件を参照してください)、**wszServicePrincipal**、**wszBposTenantId**、**cbKey** パラメーターを設定します。

**注** 探索サービスの既存の条件により、北米以外の地域では、対称キーの資格情報が他の地域から受け入れられないため、テナント URL を直接指定する必要があります。 この指定には、[**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) または [**IpcGetTemplateIssuerList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist) の [**IPC\_CONNECTION\_INFO**](/rights-management/sdk/2.1/api/win/ipc_connection_info#msipc_ipc_connection_info) パラメーターを使用します。

## 対称キーの生成と必要な情報の収集

### 対称キーを生成する手順

-   [Microsoft Online サインイン アシスタント](http://go.microsoft.com/fwlink/p/?LinkID=286152)をインストールします。
-   [Azure AD PowerShell モジュール](https://bposast.vo.msecnd.net/MSOPMW/8073.4/amd64/AdministrationConfig-en.msi)をインストールします。

**注** Powershell コマンドレットを使用するには、テナントの管理者でなければなりません。

-   PowerShell を起動し、次のコマンドを実行してキー         `Import-Module MSOnline`
            `Connect-MsolService` (管理者資格情報を入力)         `New-MsolServicePrincipal` (表示名を入力) を生成します。
-   対称キーの生成後、キー自体と **AppPrincipalId** を含むキーに関する情報が出力されます。


    The following symmetric key was created as one was not supplied ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

    DisplayName : RMSTestApp ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963} ObjectId : 0ee53770-ec86-409e-8939-6d8239880518 AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963


### **TenantBposId** と **URL** を調べる手順

-   [Azure RMS PowerShell モジュール](https://technet.microsoft.com/en-us/library/jj585012.aspx)をインストールします。
-   Powershell を起動し、次のコマンドを実行してテナントの RMS 構成を取得します。

    `Import-Module aadrm`

    `Connect-AadrmService` (管理者の資格情報を入力します)

    `Get-AadrmConfiguration`


-   [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key) のインスタンスを作成して、いくつかのメンバーを設定します。

    // キーの構造を作成します。
    IPC_CREDENTIAL_SYMMETRIC_KEY symKey = {0};

    // サービス作成時の情報を各メンバーに設定します。
    symKey.wszBase64Key = "your service principal key"; symKey.wszAppPrincipalId = "your app principal identifier"; symKey.wszBposTenantId = "your tenent identifier";


詳細については、「[**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key)」を参照してください。

-   [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key) インスタンスを含む、[**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential) 構造体のインスタンスを作成します。

**注** *connectionInfo* メンバーには、直前に `Get-AadrmConfiguration` を呼び出したときの URL が設定され、ここではそのフィールド名を示します。

    // Create a credential structure.
    IPC_CREDENTIAL cred = {0};

    IPC_CONNECTION_INFO connectionInfo = {0};
    connectionInfo.wszIntranetUrl = LicensingIntranetDistributionPointUrl;
    connectionInfo.wszExtranetUrl = LicensingExtranetDistributionPointUrl;

    // Set each member.
    cred.dwType = IPC_CREDENTIAL_TYPE_SYMMETRIC_KEY;
    cred.pcCertContext = (PCCERT_CONTEXT)&symKey;

    // Create your prompt control.
    IPC_PROMPT_CTX promptCtx = {0};

    // Set each member.
    promptCtx.cbSize = sizeof(IPC_PROMPT_CTX);
    promptCtx.hwndParent = NULL;
    promptCtx.dwflags = IPC_PROMPT_FLAG_SILENT;
    promptCtx.hCancelEvent = NULL;
    promptCtx.pcCredential = &cred;

### テンプレートの識別と暗号化

-   暗号化に使用するテンプレートを選択します
    [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist) を呼び出して、同じ [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx) インスタンスに渡します。


    PCIPC_TIL pTemplates = NULL; IPC_TEMPLATE_ISSUER templateIssuer = (pTemplateIssuerList->aTi)[0];

    hr = IpcGetTemplateList(&(templateIssuer.connectionInfo),        IPC_GTL_FLAG_FORCE_DOWNLOAD,        0,        &promptCtx,        NULL,        &pTemplates);


-   このトピック前半のテンプレートを使用して、[**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile) を呼び出して、同じ [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx) インスタンスに渡します。

[**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile) の使用例:

    LPCWSTR wszContentTemplateId = pTemplates->aTi[0].wszID;
    hr = IpcfEncryptFile(wszInputFilePath,
           wszContentTemplateId,
           IPCF_EF_TEMPLATE_ID,
           IPC_EF_FLAG_KEY_NO_PERSIST,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

[**IpcfDecryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile) の使用例:

    hr = IpcfDecryptFile(wszInputFilePath,
           IPCF_DF_FLAG_DEFAULT,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

アプリケーションでの Azure Rights Management 使用の有効化に必要な手順が完了しました。

## 関連項目

* [Azure Rights Management の概要](https://technet.microsoft.com/en-us/library/jj585016.aspx)
* [RMS SDK 2.1 の概要のページ](getting-started-with-ad-rms-2-0.md)
* [ACS を介したサービス ID 作成のページ](https://msdn.microsoft.com/en-us/library/gg185924.aspx)
* [**IpcSetGlobalProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetglobalproperty)
* [**IpcInitialize**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcinitialize)
* [**IPC\_PROMPT\_CTX**](/rights-management/sdk/2.1/api/win/ipc_prompt_ctx#msipc_ipc_prompt_ctx)
* [**IPC\_CREDENTIAL**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential)
* [**IPC\_CREDENTIAL\_SYMMETRIC\_KEY**](/rights-management/sdk/2.1/api/win/ipc_credential#msipc_ipc_credential_symmetric_key)
* [**IpcGetTemplateIssuerList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplateissuerlist)
* [**IpcGetTemplateList**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcgettemplatelist)
* [**IpcfDecryptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfdecryptfile)
* [**IpcfEncrcyptFile**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcfencryptfile)
* [**IpcCreateLicenseFromScratch**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromscratch)
* [**IpcCreateLicenseFromTemplateID**](/rights-management/sdk/2.1/api/win/functions#msipc_ipccreatelicensefromtemplateid)
 

 



<!--HONumber=Jul16_HO1-->


