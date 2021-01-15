---
title: 概念-Microsoft Information Protection (MIP) SDK C# クライアントの認証シナリオ
description: Microsoft Information Protection SDK C# クライアントアプリケーションの認証シナリオに関する技術的な詳細。
author: Pathak-Aniket
ms.author: v-anikep
ms.date: 09/02/2020
ms.topic: conceptual
ms.service: information-protection
ms.openlocfilehash: bee7cb6854aa58f6d5c3c6781984875c8ee347a1
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212622"
---
# <a name="quickstart-public-and-confidential-clients-c"></a>クイックスタート: パブリックおよび機密クライアント (C#)

MIP SDK を使用してアプリケーションをビルドする場合、2つの一般的なシナリオが使用されます。 最初のシナリオでは、ユーザーが Azure AD に対して直接認証を行っていることを確認します。 2つ目のアプリケーションは、秘密のサービスプリンシパルキーまたは証明書を使用して認証を行います。

## <a name="public-client-applications"></a>パブリッククライアントアプリケーション

これらのアプリケーションは、デバイス上で実行されているアプリケーションがユーザーに認証を求めるメッセージを表示するデスクトップアプリケーションまたはモバイルアプリケーションです。 ユーザーは、バックエンド MIP サービスに直接接続します。 このシナリオでは、認証ライブラリを使用して、ユーザーが Azure AD にサインインできること、多要素または条件付きアクセス要件を満たしていること、および適切なリソースの OAuth2 トークンを取得できることを確認する必要があります。

詳細については、[パブリッククライアントの認証フローに関するドキュメント](/azure/active-directory/develop/msal-net-initializing-client-applications#initializing-a-public-client-application-from-configuration-options)を参照してください。

Microsoft 認証ライブラリ (MSAL) を使用して、Microsoft Information Protection SDK クライアントアプリケーションのパブリッククライアント認証フローを示す、クイックコード領域を次に示します。

```csharp

public string AcquireToken(Identity identity, string authority, string resource, string claims)
{
     var authorityUri = new Uri(authority);
     authority = String.Format("https://{0}/{1}", authorityUri.Host, "<Tenant-GUID>");

     _app = PublicClientApplicationBuilder.Create("<Application-Id>").WithAuthority(authority).WithDefaultRedirectUri().Build();

     var accounts = (_app.GetAccountsAsync()).GetAwaiter().GetResult();

     // Append .default to the resource passed in to AcquireToken().
     string[] scopes = new string[] { resource[resource.Length - 1].Equals('/') ? $"{resource}.default" : $"{resource}/.default" };
     var result = _app.AcquireTokenInteractive(scopes).WithAccount(accounts.FirstOrDefault()).WithPrompt(Prompt.SelectAccount)
                    .ExecuteAsync().ConfigureAwait(false).GetAwaiter().GetResult();

     return result.AccessToken;
}
```

**テナント guid** は、Azure AD テナントの一意のテナント guid です。
**アプリケーション id** は Azure AD ポータルのアプリケーション登録のアプリケーション id です。

## <a name="confidential-client-applications"></a>機密クライアントアプリケーション

これらのアプリケーションは、ユーザーがバックエンド MIP サービスに直接接続していないクラウドまたはサービスベースのアプリケーションです。 このサービスでは、MIP 対応コンテンツのラベル付け、保護、または保護解除を行う必要があります。 このシナリオでは、アプリケーションは証明書またはアプリケーションシークレットを格納する必要があります。 これらのシークレットは、Azure AD するための認証に使用され、そのシークレットを使用してバックエンド MIP サービスのトークンをフェッチします。 その後、MIP SDK の委任機能を使用して、認証されたユーザーの代わりにコンテンツを保護または使用することができます。

MIP SDK とサービスベースのアプリケーションを統合するには、クライアント資格情報付与フローを使用する必要があります。 Microsoft Authentication Library (MSAL) を使用すると、パブリッククライアントアプリケーションに表示されるものと同様のパターンでこれを実装できます。 この記事では、 `IAuthDelegate` このフローを使用してサービスベースのアプリケーションの認証を実行するために、.net で MIP SDK を更新する方法について簡単に説明します。 発行時には、C++ 用の MSAL のバージョンはありませんが、 [DIRECT REST 呼び出し](https://docs.microsoft.com/azure/active-directory/develop/v2-oauth2-client-creds-grant-flow#get-a-token)を使用してこのフローを実装することは可能です。

詳細については、 [confidential クライアント認証フロー](/azure/active-directory/develop/msal-net-initializing-client-applications#initializing-a-confidential-client-application-from-code)に関するドキュメントを参照してください。

次に示すのは、microsoft 認証ライブラリ (MSAL) を使用して Microsoft Information Protection SDK クライアントアプリケーションの機密クライアント認証フローをデモンストレーションするクイックコード領域です。 アプリケーションは、AD 証明書またはクライアントシークレットを使用して認証できます。

> [!NOTE]
> 次のサンプルでは、この行に特に注意を払ってください。 
>
> ```csharp
> string[] scopes = new string[] { resource[resource.Length - 1].Equals('/') ? $"{resource}.default" : $"{resource}/.default" };
> ```
> これにより、メソッドに提供されたリソースから MSAL スコープが構築され `AcquireToken()` ます。 

### <a name="msal-confidential-client-example"></a>MSAL Confidential クライアントの例

```csharp
public string AcquireToken(Identity identity, string authority, string resource, string claim)
{
     AuthenticationResult result;
     var authorityUri = new Uri(authority);
     authority = string.Format("https://{0}/{1}", authorityUri.Host, "<Tenant-GUID>");

     // Certification Based Auth
     if (doCertAuth)
     {
          // Build ConfidentialClientApplication using certificate.
          _app = ConfidentialClientApplicationBuilder.Create("<Application-Id>")
               .WithCertificate(certificate) //Assumption here is Application passes a certificate created using certificate thumbprint
               .WithAuthority(new Uri(authority))
               .Build();
     }

     // Client secret based Auth
     else
     {
          // Build ConfidentialClientApplication using app secret
          _app = ConfidentialClientApplicationBuilder.Create("<Application-Id>")
               .WithClientSecret(clientSecret)
               .WithAuthority(new Uri(authority))
               .Build();
     }

     // Append .default to the resource passed in to AcquireToken().
     string[] scopes = new string[] { resource[resource.Length - 1].Equals('/') ? $"{resource}.default" : $"{resource}/.default" };

     try{
          result = _app.AcquireTokenForClient(scopes).ExecuteAsync().Result;
     }
     catch (MsalServiceException ex) when (ex.Message.Contains("AADSTS70011"))
     {
          // Invalid scope. The scope has to be of the form "https://resourceurl/.default"
          // Mitigation: change the scope to be as expected
          Console.WriteLine("Scope provided is not supported");
          return null;
     }
            return result.AccessToken;
}

```
**テナント guid** は、Azure AD テナントの一意のテナント guid です。
**アプリケーション id** は Azure AD ポータルのアプリケーション登録のアプリケーション id です。