---
title: "クラウド ベース RMS でサービス アプリケーション使用を有効化する方法 | Azure RMS"
description: "このトピックでは、Azure Rights Management を使用するようにサービス アプリケーションをセットアップする手順について説明します。"
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: EA1457D1-282F-4CF3-A23C-46793D2C2F32
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 06b34002fe3a5558383083a0e0aa3755715f780b
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="how-to-enable-your-service-application-to-work-with-cloud-based-rms"></a>方法: クラウド ベース RMS でのサービス アプリケーション使用の有効化

このトピックでは、Azure Rights Management を使用するようにサービス アプリケーションをセットアップする手順について説明します。 詳細については、「[Azure Rights Management の概要](https://technet.microsoft.com/library/jj585016.aspx)」を参照してください。

**重要**  
Rights Management Services SDK 2.1 サービスを Azure RMS で利用するには、独自のテナントを作成する必要があります。 詳細については、「[Azure RMS の要件: Azure RMS をサポートするクラウド サブスクリプション](../get-started/requirements-subscriptions.md)」を参照してください。

## <a name="prerequisites"></a>必要条件

-   RMS SDK 2.1 をインストールして構成する必要があります。 詳細については、[RMS SDK 2.1 の概要のページ](getting-started-with-ad-rms-2-0.md)を参照してください。
-   対称キーのオプションを使用するかその他の方法で、[ACS を介してサービス ID を作成](https://msdn.microsoft.com/en-us/library/gg185924.aspx)して、その処理中にキー情報をメモします。

## <a name="connecting-to-the-azure-rights-management-service"></a>Azure Rights Management サービスへの接続

-   [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx) を呼び出します。
-   [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) を設定します。

        C++
        int mode = IPC_API_MODE_SERVER;
        IpcSetGlobalProperty(IPC_EI_API_MODE, &(mode));


  **注** 詳細については、「[Setting the API security mode (API セキュリティ モードの設定)](setting-the-api-security-mode-api-mode.md)」を参照してください。

     
-   次の手順は、[IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx) 構造体のインスタンスを作成するためのセットアップです。*pcCredential* ([IPC\_CREDENTIAL](https://msdn.microsoft.com/library/hh535275.aspx)) メンバーに Azure Rights Management サービスの接続情報を設定します。
-   対称キーのサービス ID 作成時にメモした情報 (このトピックの前述の前提条件を参照してください) を使用して、[IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx) 構造体のインスタンスを作成するときに *wszServicePrincipal*、*wszBposTenantId*、*cbKey* パラメーターを設定します。

**注** - 探索サービスの既存の条件により、北米以外の地域では、対称キーの資格情報が他の地域から受け入れられないため、テナント URL を直接指定する必要があります。 これを行うには、*pConnectionInfo* パラメーターの [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx) または [IpcGetTemplateIssuerList](https://msdn.microsoft.com/library/hh535266.aspx) に [IPC\_CONNECTION\_INFO](https://msdn.microsoft.com/library/hh535274.aspx) を入力します。

## <a name="generate-a-symmetric-key-and-collect-the-needed-information"></a>対称キーの生成と必要な情報の収集

### <a name="instructions-to-generate-a-symmetric-key"></a>対称キーを生成する手順

-   [Microsoft Online サインイン アシスタント](http://go.microsoft.com/fwlink/p/?LinkID=286152)をインストールします。
-   [Azure AD PowerShell モジュール](https://bposast.vo.msecnd.net/MSOPMW/8073.4/amd64/AdministrationConfig-en.msi)をインストールします。

**注** - Powershell コマンドレットを使用するには、テナントの管理者でなければなりません。

- Powershell を起動し、次のコマンドを実行してキーを生成します。

    `Import-Module MSOnline`

    `Connect-MsolService` (管理者の資格情報を入力します)

    `New-MsolServicePrincipal` (表示名を入力します)

- 対称キーの生成後、キー自体と *AppPrincipalId* を含むキーに関する情報が出力されます。

      The following symmetric key was created as one was not supplied
      ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

      DisplayName : RMSTestApp
      ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963}
      ObjectId : 0ee53770-ec86-409e-8939-6d8239880518
      AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963


### <a name="instructions-to-find-out-tenantbposid-and-urls"></a>**TenantBposId** と **URL** を調べる手順

-   [Azure RMS PowerShell モジュール](https://technet.microsoft.com/en-us/library/jj585012.aspx)をインストールします。
-   Powershell を起動し、次のコマンドを実行してテナントの RMS 構成を取得します。

    `Import-Module aadrm`

    `Connect-AadrmService` (管理者の資格情報を入力します)

    `Get-AadrmConfiguration`


- [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx) のインスタンスを作成して、いくつかのメンバーを設定します。

      // Create a key structure.
      IPC_CREDENTIAL_SYMMETRIC_KEY symKey = {0};

      // Set each member with information from service creation.
      symKey.wszBase64Key = "your service principal key";
      symKey.wszAppPrincipalId = "your app principal identifier";
      symKey.wszBposTenantId = "your tenant identifier";


詳細については、「[IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx)」を参照してください。

-   [IPC\_CREDENTIAL](https://msdn.microsoft.com/library/hh535275.aspx) 構造体のインスタンスを作成します。この中に [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx) インスタンスが格納されます。

**注** - *connectionInfo* メンバーには、直前に `Get-AadrmConfiguration` を呼び出したときの URL が設定され、ここではそのフィールド名を示します。

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

### <a name="identify-a-template-and-then-encrypt"></a>テンプレートの識別と暗号化

-   暗号化に使用するテンプレートを選択します
    [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx) を呼び出して、[IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx) の同じインスタンスに渡します。


    PCIPC_TIL pTemplates = NULL; IPC_TEMPLATE_ISSUER templateIssuer = (pTemplateIssuerList->aTi)[0];

    hr = IpcGetTemplateList(&(templateIssuer.connectionInfo),        IPC_GTL_FLAG_FORCE_DOWNLOAD,        0,        &promptCtx,        NULL,        &pTemplates);


-   このトピック前半のテンプレートを使用して、[IpcfEncrcyptFile](https://msdn.microsoft.com/library/dn133059.aspx) を呼び出して、[IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx) の同じインスタンスに渡します。

[IpcfEncrcyptFile](https://msdn.microsoft.com/library/dn133059.aspx) の使用例:

    LPCWSTR wszContentTemplateId = pTemplates->aTi[0].wszID;
    hr = IpcfEncryptFile(wszInputFilePath,
           wszContentTemplateId,
           IPCF_EF_TEMPLATE_ID,
           IPC_EF_FLAG_KEY_NO_PERSIST,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

[IpcfDecryptFile](https://msdn.microsoft.com/library/dn133058.aspx) の使用例:

    hr = IpcfDecryptFile(wszInputFilePath,
           IPCF_DF_FLAG_DEFAULT,
           &promptCtx,
           NULL,
           &wszOutputFilePath);

アプリケーションでの Azure Rights Management 使用の有効化に必要な手順が完了しました。

## <a name="related-topics"></a>関連項目

* [Azure Rights Management の作業の開始](https://technet.microsoft.com/en-us/library/jj585016.aspx)
* [RMS SDK 2.1 の概要](getting-started-with-ad-rms-2-0.md)
* [ACS を介したサービス ID の作成](https://msdn.microsoft.com/en-us/library/gg185924.aspx)
* [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)
* [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx)
* [IPC\_PROMPT\_CTX](https://msdn.microsoft.com/library/hh535278.aspx)
* [IPC\_CREDENTIAL](https://msdn.microsoft.com/library/hh535275.aspx)
* [IPC\_CREDENTIAL\_SYMMETRIC\_KEY](https://msdn.microsoft.com/library/dn133062.aspx)
* [IpcGetTemplateIssuerList](https://msdn.microsoft.com/library/hh535266.aspx)
* [IpcGetTemplateList](https://msdn.microsoft.com/library/hh535267.aspx)
* [IpcfDecryptFile](https://msdn.microsoft.com/library/dn133058.aspx)
* [IpcfEncrcyptFile](https://msdn.microsoft.com/library/dn133059.aspx)
* [IpcCreateLicenseFromScratch](https://msdn.microsoft.com/library/hh535256.aspx)
* [IpcCreateLicenseFromTemplateID](https://msdn.microsoft.com/library/hh535257.aspx)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]