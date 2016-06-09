---
# required metadata

title: RMS 対応アプリケーションの ADAL 認証 | Azure RMS
description: ADAL での認証プロセスの概要を説明します。
keywords: authentication, RMS, ADAL
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f89f59b7-33d1-4ab3-bb64-1e9bda269935

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** この SDK コンテンツは最新のものではありません。 しばらくの間、[最新版](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx)の文書は MSDN でご覧ください。 **
# RMS 対応アプリケーションの ADAL 認証

Azure ADAL を使用したアプリに対する Azure RMS での認証は、RMS クライアント 2.1 の一部になっています。

Microsoft Online サインイン アシスタントではなく、ADAL 認証を使用するようにアプリケーションを更新すると、ユーザーと顧客は以下を利用できるようになります。

- 多要素認証を使用する
- コンピューターの管理者特権なしで RMS 2.1 クライアントをインストールする
- Windows 10 向けアプリケーションの認定

## 2 つの認証方法

このトピックでは、2 種類の認証方法とそれに対応するコード例を示します。

- **内部認証** - RMS SDK によって管理された OAuth 認証。 認証が必要なときに RMS クライアントに ADAL 認証プロンプトを表示させる場合は、この方法を使用します。 アプリケーションの構成方法の詳細については、「内部認証」セクションを参照してください。

> [!NOTE] 現在、アプリケーションがサインイン アシスタント付きの AD RMS SDK 2.1 を使用している場合は、アプリケーション移行パスとして内部認証方法を使用することをお勧めします。

- **外部認証** - アプリケーションによって管理される OAuth 認証。 アプリケーションで独自の OAuth 認証を管理する場合は、この方法を使用します。 この方法では、認証が必要なとき、RMS クライアントはアプリケーション定義のコールバックを実行します。 詳細な例については、このトピックの最後の「外部認証」を参照してください。

> [!NOTE] 外部認証は、ユーザーを変更できるということではありません。RMS クライアントは、常に特定の RMS テナントの既定のユーザーを使用します。

### 内部認証

以下のものが必要です。

- [Microsoft Azure のサブスクリプション](https://azure.microsoft.com/en-us/) (無料評価版で十分です)。
- Microsoft Azure Rights Management のサブスクリプション (無料の[個人向け RMS](https://technet.microsoft.com/en-us/library/dn592127.aspx) アカウントで十分です)。

> [!NOTE] IT 管理者に、Microsoft Azure Rights Management のサブスクリプションがあるかどうかを問い合わせ、以下の手順の実行を依頼します。 組織にサブスクリプションがない場合、IT 管理者に作成してもらいます。 また、IT 管理者は、Microsoft アカウント (Hotmail など) ではなく、職場または学校アカウントでサブスクライブする必要があります。

Microsoft Azure にサインアップした後:

- 管理者特権を持つアカウントを使用して、組織の [Microsoft Azure の管理ポータル](https://manage.windowsazure.com)にログインします。

![Azure にログインする](../media/AzurePortalLogin.png)

- ポータルの左下にある **[Active Directory]** アプリケーションを参照します。

![[Active Directory] を選択する](../media/AzureADPick.png)

- ディレクトリをまだ作成していない場合は、ポータルの左下隅にある **[新規]** ボタンを選択します。

![[新規] を選択する](../media/AzureNewBtn.png)

- **[Rights Management]** タブを選択し、**[Rights Management のステータス]** が **[アクティブ]**、**[不明]**、または **[許可されていません]** であることを確認します。 ステータスが **[非アクティブ]** の場合は、ポータル中央下部にある **[アクティブ化]** ボタンを選択し、選択を確認します。

![[アクティブ化] を選択する](../media/RMTab.png)

- 次に、ディレクトリを選択して [アプリケーション] を選択し、ディレクトリに新しい*ネイティブ アプリケーション*を作成します。

![[アプリケーション] を選択する](../media/CreateNativeApp.png)

- ポータル中央下部の **[追加]** ボタンを選択します。

![[追加] を選択する](../media/AddAppBtn.png)

- メッセージが表示されたら、**[組織で開発中のアプリケーションを追加]** を選択します。

![[組織で開発中のアプリケーションを追加] の選択](../media/AddAnAppPick.png)

- **[ネイティブ クライアント アプリケーション]** を選択して **[次へ]** ボタンを選択し、アプリケーションの名前を指定します。

![アプリの名前を指定する](../media/TellUsInput.png)

- リダイレクト URI を追加し、[次へ] を選択します。 リダイレクト URI は、有効な URI で、ディレクトリに対して一意である必要があります。 たとえば、`com.mycompany.myapplication://authorize` のような URI を使用します。

![リダイレクト URI を追加する](../media/RedirectURI.png)

- ディレクトリでアプリケーションを選択し、**[構成]** を選択します。

![[構成] を選択する](../media/ConfigYourApp.png)

>[!NOTE] **[クライアント ID]** と **[リダイレクト URI]** をコピーし、後で RMS クライアントを構成するときのために保存します。

- アプリケーション設定下部で **[他のアプリケーションに対するアクセス許可]** の **[アプリケーションの追加]** ボタンを選択します。

![[アプリケーションの追加] を選択する](../media/PermissionsToOtherBtn.png)

- この GUID `00000012-0000-0000-c000-000000000000` を **[次で始まる]** 編集ボックスに追加し、チェック ボタンを選択します。

![GUID を追加する](../media/AddGUID.png)

- **[Microsoft Rights Management]** の隣の [+] ボタンを選択します。

![[+] ボタンの選択](../media/ChoosePlusBtn.png)

- ダイアログの左下隅にあるチェック マークを選択します。

![チェック マークを選択する](../media/ChooseCheck.png)

- Azure RMS 用アプリケーションに依存関係を追加する準備ができました。 依存関係を追加するには、**[他のアプリケーションに対するアクセス許可]** で新しい **[Microsoft Rights Management サービス]** エントリを選択し、**[デリゲートされたアクセス許可]** ドロップ ボックスで **[ユーザー用の保護されたコンテンツを作成してアクセスする]** チェック ボックスをオンにします。

![アクセス許可を設定する](../media/AddDependency.png)

- ポータル中央下部の **[保存]** アイコンを選択して、アプリケーションを保存します。

![[保存] を選択する](../media/SaveApplication.png)

- RMS SDK 2.1 で提供される内部 ADAL 認証を使用するようにアプリケーションを構成する準備が整いました。 RMS クライアントを構成するには、[IpcInitialize](/rights-management/sdk/2.1/api/win/IpcInitialize) の呼び出しの直後に [IpcSetGlobalProperty](/rights-management/sdk/2.1/api/win/IpcSetGlobalProperty) の呼び出しを追加します。 次のコード スニペットを例として使用できます。


    IpcInitialize();

    IPC_AAD_APPLICATION_ID applicationId = { 0 };   applicationId.cbSize = sizeof(IPC_AAD_APPLICATION_ID);   applicationId.wszClientId = L"GUID-provided-by-AAD-for-your-app-(no-brackets)";   applicationId.wszRedirectUri = L"RedirectionUriWeProvidedAADForOurApp://authorize";

    HRESULT hr = IpcSetGlobalProperty(IPC_EI_APPLICATION_ID, &amp;applicationId);

    if (FAILED(hr)) {    //Handle the error   }

### 外部認証

- 独自の認証トークンの管理方法のコード例を次に示します。


    extern HRESULT GetADALToken(LPVOID pContext, const IPC_NAME_VALUE_LIST&amp; Parameters, __out wstring wstrToken) throw();

    HRESULT GetLicenseKey(PCIPC_BUFFER pvLicense, __in LPVOID pContextForAdal, __out IPC_KEY_HANDLE &amp;hKey) { IPC_OAUTH2_CALLBACK pfGetADALToken =         [](LPVOID pvContext, PIPC_NAME_VALUE_LIST pParameters, IPC_AUTH_TOKEN_HANDLE* phAuthToken) -&gt; HRESULT { wstring wstrToken; HRESULT hr = GetADALToken(pvContext, *pParameters, wstrToken); return SUCCEEDED(hr) ? IpcCreateOAuth2Token(wstrToken.c_str(), OUT phAuthToken) : hr; };

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
      credentialContext.pcOAuth2 = &amp;callbackCredentialContext;

      IPC_PROMPT_CTX promptContext =
      {
        sizeof(IPC_PROMPT_CTX),
        NULL,
        IPC_PROMPT_FLAG_SILENT | IPC_PROMPT_FLAG_HAS_USER_CONSENT,
        NULL,
        &amp;credentialContext
      };

      hKey = 0L;
      return IpcGetKey(pvLicense, 0, &amp;promptContext, NULL, &amp;hKey);
  }

### 関連項目
- [データ型](/rights-management/sdk/2.1/api/win/Data%20types)
- [Environment properties (環境プロパティ)](/rights-management/sdk/2.1/api/win/Environment%20properties)
- [IpcCreateOAuth2Token](/rights-management/sdk/2.1/api/win/IpcCreateOAuth2Token)
- [IpcGetKey](/rights-management/sdk/2.1/api/win/IpcGetKey)
- [IpcInitialize](/rights-management/sdk/2.1/api/win/IpcInitialize)
- [IPC_CREDENTIAL](/rights-management/sdk/2.1/api/win/IPC\_CREDENTIAL)
- [IPC_NAME_VALUE_LIST](/rights-management/sdk/2.1/api/win/IPC\_NAME\_VALUE\_LIST)
- [IPC_OAUTH2_CALLBACK_INFO](/rights-management/sdk/2.1/api/win/IPC\_OAUTH2\_CALLBACK\_INFO)
- [IPC_PROMPT_CTX](/rights-management/sdk/2.1/api/win/IPC\_PROMPT\_CTX)
- [IPC_AAD_APPLICATION_ID](/rights-management/sdk/2.1/api/win/IPC\_AAD\_APPLICATION\_ID)


<!--HONumber=Jun16_HO1-->


