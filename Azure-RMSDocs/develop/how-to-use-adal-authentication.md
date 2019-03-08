---
title: RMS 対応アプリケーションの ADAL 認証 | Azure RMS
description: ADAL での認証プロセスの概要を説明します。
keywords: 認証、RMS、ADAL
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 0f143a27942604b6a8cfa664fc53be217118fd51
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57331547"
---
# <a name="how-to-use-adal-authentication"></a>方法: ADAL 認証の使用

Azure Active Directory Authentication Library (ADAL) を利用し、アプリに対して Azure RMS で認証を実行する。

Microsoft Online サインイン アシスタントではなく、ADAL 認証を使用するようにアプリケーションを更新すると、ユーザーと顧客は以下を利用できるようになります。

- 多要素認証を使用する
- コンピューターの管理者特権なしで RMS 2.1 クライアントをインストールする
- Windows 10 向けアプリケーションの認定

## <a name="two-approaches-to-authentication"></a>2 つの認証方法

このトピックでは、2 種類の認証方法とそれに対応するコード例を示します。

- **内部認証** - RMS SDK によって管理された OAuth 認証。

  認証が必要なときに RMS クライアントに ADAL 認証プロンプトを表示させる場合は、この方法を使用します。 アプリケーションの構成方法の詳細については、「内部認証」セクションを参照してください。

  > [!Note]
  > 現在、アプリケーションがサインイン アシスタント付きの AD RMS SDK 2.1 を使用している場合は、アプリケーション移行パスとして内部認証方法を使用することをお勧めします。

- **外部認証** - アプリケーションによって管理される OAuth 認証。

  アプリケーションで独自の OAuth 認証を管理する場合は、この方法を使用します。 この方法では、認証が必要なとき、RMS クライアントはアプリケーション定義のコールバックを実行します。 詳細な例については、このトピックの最後の「外部認証」を参照してください。

  > [!Note]
  > 外部認証は、ユーザーを変更できるということではありません。RMS クライアントは、常に特定の RMS テナントの既定のユーザーを使用します。

## <a name="internal-authentication"></a>内部認証

1. 「[Configure Azure RMS for ADAL authentication](adal-auth.md)」 (Azure RMS の ADAL 認証を構成する) の Azure 構成手順に従い、その後、次のアプリ初期化手順に戻ります。
2. RMS SDK 2.1 で提供される内部 ADAL 認証を使用するようにアプリケーションを構成する準備が整いました。

RMS クライアントを構成するには、[IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx) の呼び出しの直後に [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) に呼び出しを追加し、RMS クライアントを構成します。 次のコード スニペットを例として使用できます。

      C++
      IpcInitialize();

      IPC_AAD_APPLICATION_ID applicationId = { 0 };
      applicationId.cbSize = sizeof(IPC_AAD_APPLICATION_ID);
      applicationId.wszClientId = L"GUID-provided-by-AAD-for-your-app-(no-brackets)";
      applicationId.wszRedirectUri = L"RedirectionUriWeProvidedAADForOurApp://authorize";
      HRESULT hr = IpcSetGlobalProperty(IPC_EI_APPLICATION_ID, &applicationId);
      if (FAILED(hr)) {
        //Handle the error
      }

## <a name="external-authentication"></a>外部認証

独自の認証トークンの管理方法のコード例を次に示します。
C++ extern HRESULT GetADALToken(LPVOID pContext, const IPC_NAME_VALUE_LIST& Parameters, __out wstring wstrToken) throw();

      HRESULT GetLicenseKey(PCIPC_BUFFER pvLicense, __in LPVOID pContextForAdal, __out IPC_KEY_HANDLE &hKey)
      {
          IPC_OAUTH2_CALLBACK pfGetADALToken =
          [](LPVOID pvContext, PIPC_NAME_VALUE_LIST pParameters, IPC_AUTH_TOKEN_HANDLE* phAuthToken) -> HRESULT
          {
              wstring wstrToken;
              HRESULT hr = GetADALToken(pvContext, *pParameters, wstrToken);
              return SUCCEEDED(hr) ? IpcCreateOAuth2Token(wstrToken.c_str(), OUT phAuthToken) : hr;
          };

          IPC_OAUTH2_CALLBACK_INFO callbackCredentialContext =
          {
              sizeof(IPC_OAUTH2_CALLBACK_INFO),
              pfGetADALToken,
              pContextForAdal
          };

          IPC_CREDENTIAL credentialContext =
          {
              IPC_CREDENTIAL_TYPE_OAUTH2,
              NULL
          };
          credentialContext.pcOAuth2 = &callbackCredentialContext;

          IPC_PROMPT_CTX promptContext =
          {
              sizeof(IPC_PROMPT_CTX),
              NULL,
              IPC_PROMPT_FLAG_SILENT | IPC_PROMPT_FLAG_HAS_USER_CONSENT,
              NULL,
              &credentialContext
          };

          hKey = 0L;
          return IpcGetKey(pvLicense, 0, &promptContext, NULL, &hKey);
      }

## <a name="related-topics"></a>関連項目

- [データ型](https://msdn.microsoft.com/library/hh535288.aspx)
- [Environment properties (環境プロパティ)](https://msdn.microsoft.com/library/hh535247.aspx)
- [IpcCreateOAuth2Token](https://msdn.microsoft.com/library/mt661866.aspx)
- [IpcGetKey](https://msdn.microsoft.com/library/hh535263.aspx)
- [IpcInitialize](https://msdn.microsoft.com/library/jj127295.aspx)
- [IPC_CREDENTIAL](https://msdn.microsoft.com/library/hh535275.aspx)
- [IPC_NAME_VALUE_LIST](https://msdn.microsoft.com/library/hh535277.aspx)
- [IPC_OAUTH2_CALLBACK_INFO](https://msdn.microsoft.com/library/mt661868.aspx)
- [IPC_PROMPT_CTX](https://msdn.microsoft.com/library/hh535278.aspx)
- [IPC_AAD_APPLICATION_ID](https://msdn.microsoft.com/library/mt661867.aspx)
