---
title: クラウド ベース RMS でサービス アプリケーション使用を有効化する方法 | Azure RMS
description: このトピックでは、Azure Rights Management を使用するようにサービス アプリケーションをセットアップする手順について説明します。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: EA1457D1-282F-4CF3-A23C-46793D2C2F32
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: a760f59effa09cf55f7618e6ab965c5e95f015d3
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "95570662"
---
# <a name="how-to-enable-your-service-application-to-work-with-cloud-based-rms"></a>方法: クラウド ベース RMS でのサービス アプリケーション使用の有効化

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

このトピックでは、Azure Rights Management を使用するようにサービス アプリケーションをセットアップする手順について説明します。 詳細については、「[Azure Rights Management の概要](../requirements.md)」を参照してください。

**重要**  
Rights Management Services SDK 2.1 サービスを Azure RMS で利用するには、独自のテナントを作成する必要があります。 詳細については、「 [Azure RMS の要件: Azure RMS をサポートするクラウドサブスクリプション](../requirements.md)」を参照してください。

## <a name="prerequisites"></a>前提条件

-   RMS SDK 2.1 をインストールして構成する必要があります。 詳細については、[RMS SDK 2.1 の概要のページ](getting-started-with-ad-rms-2-0.md)を参照してください。
-   対称キーのオプションを使用するかその他の方法で、[ACS を介してサービス ID を作成](/previous-versions/azure/azure-services/gg185924(v=azure.100))して、その処理中にキー情報をメモします。

## <a name="connecting-to-the-azure-rights-management-service"></a>Azure Rights Management サービスへの接続

- [IpcInitialize](/previous-versions/windows/desktop/msipc/ipcinitialize) を呼び出します。
- [IpcSetGlobalProperty](/previous-versions/windows/desktop/msipc/ipcsetglobalproperty) を設定します。

  ```cpp
  int mode = IPC_API_MODE_SERVER;
  IpcSetGlobalProperty(IPC_EI_API_MODE, &(mode));
  ```

  **注** 詳細については、「[Setting the API security mode (API セキュリティ モードの設定)](setting-the-api-security-mode-api-mode.md)」を参照してください。


-   次の手順は、 [ipc \_ PROMPT \_ CTX](/previous-versions/windows/desktop/msipc/ipc-prompt-ctx) 構造体のインスタンスを作成するためのセットアップです。 *pccredential*  ([IPC \_ credential](/previous-versions/windows/desktop/msipc/ipc-credential)) メンバーに Azure Rights Management サービスからの接続情報が設定されています。
-   [IPC \_ CREDENTIAL \_ symmetric \_ key](/previous-versions/windows/desktop/msipc/ipc-credential-symmetric-key)構造のインスタンスを作成するときに、 *WszServicePrincipal*、 *wszBposTenantId*、および *cbkey* パラメーターを設定するには、対称キーサービス id の作成に関する情報を使用します (このトピックで前述した「前提条件」を参照してください)。

**注** - 探索サービスの既存の条件により、北米以外の地域では、対称キーの資格情報が他の地域から受け入れられないため、テナント URL を直接指定する必要があります。 これを行うには、*pConnectionInfo* パラメーターの [IpcGetTemplateList](/previous-versions/windows/desktop/msipc/ipcgettemplatelist) または [IpcGetTemplateIssuerList](/previous-versions/windows/desktop/msipc/ipcgettemplateissuerlist) に [IPC\_CONNECTION\_INFO](/previous-versions/windows/desktop/msipc/ipc-connection-info) を入力します。

## <a name="generate-a-symmetric-key-and-collect-the-needed-information"></a>対称キーの生成と必要な情報の収集

### <a name="instructions-to-generate-a-symmetric-key"></a>対称キーを生成する手順

-   [Microsoft Online サインイン アシスタント](https://go.microsoft.com/fwlink/p/?LinkID=286152)をインストールします。
-   [Azure AD PowerShell モジュール](https://bposast.vo.msecnd.net/MSOPMW/8073.4/amd64/AdministrationConfig-en.msi)をインストールします。

**注** - Powershell コマンドレットを使用するには、テナントの管理者でなければなりません。

- Powershell を起動し、次のコマンドを実行してキーを生成します。

    `Import-Module MSOnline`

    `Connect-MsolService` (管理者の資格情報を入力します)

    `New-MsolServicePrincipal` (表示名を入力します)

- 対称キーの生成後、キー自体と *AppPrincipalId* を含むキーに関する情報が出力されます。

  ```output
  The following symmetric key was created as one was not supplied
  ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

  DisplayName : RMSTestApp
  ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963}
  ObjectId : 0ee53770-ec86-409e-8939-6d8239880518
  AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963
  ```


### <a name="instructions-to-find-out-tenantbposid-and-urls"></a>**TenantBposId** と **URL** を調べる手順

-   [Azure RMS PowerShell モジュール](../install-powershell.md)をインストールします。
-   Powershell を起動し、次のコマンドを実行してテナントの RMS 構成を取得します。

    `Import-Module AIPService`

    `Connect-AipService` (管理者の資格情報を入力します)

    `Get-AipServiceConfiguration`


- [IPC \_ CREDENTIAL \_ SYMMETRIC \_ KEY](/previous-versions/windows/desktop/msipc/ipc-credential-symmetric-key)のインスタンスを作成し、いくつかのメンバーを設定します。

  ```cpp
  // Create a key structure.
  IPC_CREDENTIAL_SYMMETRIC_KEY symKey = {0};

  // Set each member with information from service creation.
  symKey.wszBase64Key = "your service principal key";
  symKey.wszAppPrincipalId = "your app principal identifier";
  symKey.wszBposTenantId = "your tenant identifier";
  ```

詳細については、「 [IPC \_ CREDENTIAL \_ SYMMETRIC \_ KEY](/previous-versions/windows/desktop/msipc/ipc-credential-symmetric-key)」を参照してください。

- [Ipc \_ credential \_ SYMMETRIC \_ KEY](/previous-versions/windows/desktop/msipc/ipc-credential-symmetric-key)インスタンスを含む[ipc \_ credential](/previous-versions/windows/desktop/msipc/ipc-credential)構造体のインスタンスを作成します。

  **メモ**  - *ConnectionInfo* メンバーは、以前のの呼び出しからの url で設定され、 `Get-AipServiceConfiguration` ここではこれらのフィールド名を使用しています。

  ```cpp
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
  ```

### <a name="identify-a-template-and-then-encrypt"></a>テンプレートの識別と暗号化

- 暗号化に使用するテンプレートを選択します
    [Ipcgettemplatelist](/previous-versions/windows/desktop/msipc/ipcgettemplatelist)を呼び出して、同じ[IPC \_ PROMPT \_ CTX](/previous-versions/windows/desktop/msipc/ipc-prompt-ctx)インスタンスに渡します。

  ```cpp
  PCIPC_TIL pTemplates = NULL;
  IPC_TEMPLATE_ISSUER templateIssuer = (pTemplateIssuerList->aTi)[0];

  hr = IpcGetTemplateList(&(templateIssuer.connectionInfo),
         IPC_GTL_FLAG_FORCE_DOWNLOAD,
         0,
         &promptCtx,
         NULL,
         &pTemplates);
  ```

- このトピックで既に説明したテンプレートを使用して、 [Ipcfencrcyptfile](/previous-versions/windows/desktop/msipc/ipcfencryptfile)を呼び出し、同じ [IPC \_ PROMPT \_ CTX](/previous-versions/windows/desktop/msipc/ipc-prompt-ctx)インスタンスに渡します。

  [IpcfEncrcyptFile](/previous-versions/windows/desktop/msipc/ipcfencryptfile) の使用例:

  ```cpp
  LPCWSTR wszContentTemplateId = pTemplates->aTi[0].wszID;
  hr = IpcfEncryptFile(wszInputFilePath,
         wszContentTemplateId,
         IPCF_EF_TEMPLATE_ID,
         IPC_EF_FLAG_KEY_NO_PERSIST,
         &promptCtx,
         NULL,
         &wszOutputFilePath);
  ```

  [IpcfDecryptFile](/previous-versions/windows/desktop/msipc/ipcfdecryptfile) の使用例:

  ```cpp
  hr = IpcfDecryptFile(wszInputFilePath,
         IPCF_DF_FLAG_DEFAULT,
         &promptCtx,
         NULL,
         &wszOutputFilePath);
  ```

アプリケーションでの Azure Rights Management 使用の有効化に必要な手順が完了しました。

## <a name="related-topics"></a>関連トピック

* [Azure Rights Management の概要](../requirements.md)
* [RMS SDK 2.1 の概要のページ](getting-started-with-ad-rms-2-0.md)
* [ACS を介したサービス ID 作成のページ](/previous-versions/azure/azure-services/gg185924(v=azure.100))
* [IpcSetGlobalProperty](/previous-versions/windows/desktop/msipc/ipcsetglobalproperty)
* [IpcInitialize](/previous-versions/windows/desktop/msipc/ipcinitialize)
* [IPC \_ プロンプト \_ CTX](/previous-versions/windows/desktop/msipc/ipc-prompt-ctx)
* [IPC \_ 資格情報](/previous-versions/windows/desktop/msipc/ipc-credential)
* [IPC \_ 資格情報の \_ 対称 \_ キー](/previous-versions/windows/desktop/msipc/ipc-credential-symmetric-key)
* [IpcGetTemplateIssuerList](/previous-versions/windows/desktop/msipc/ipcgettemplateissuerlist)
* [IpcGetTemplateList](/previous-versions/windows/desktop/msipc/ipcgettemplatelist)
* [IpcfDecryptFile](/previous-versions/windows/desktop/msipc/ipcfdecryptfile)
* [IpcfEncrcyptFile](/previous-versions/windows/desktop/msipc/ipcfencryptfile)
* [IpcCreateLicenseFromScratch](/previous-versions/windows/desktop/msipc/ipccreatelicensefromscratch)
* [IpcCreateLicenseFromTemplateID](/previous-versions/windows/desktop/msipc/ipccreatelicensefromtemplateid)