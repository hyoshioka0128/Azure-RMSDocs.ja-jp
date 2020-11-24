---
title: 概念-Microsoft Information Protection (MIP) SDK C# クライアントの認証シナリオ
description: Microsoft Information Protection SDK C# クライアントアプリケーションの認証シナリオに関する技術的な詳細。
author: Pathak-Aniket
ms.author: v-anikep
ms.date: 09/02/2020
ms.topic: conceptual
ms.service: information-protection
ms.openlocfilehash: 10d6f5ce615373f0955c42f2573b7ddd59629734
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "95570150"
---
# <a name="quickstart-public-and-confidential-clients-c"></a>クイックスタート: パブリックおよび機密クライアント (C#)

MIP SDK を使用してアプリケーションをビルドする場合、2つの一般的なシナリオが使用されます。 1つのシナリオでは、ユーザーが Azure AD に対して直接認証することを確認します。この場合、アプリケーションは、秘密のサービスプリンシパルキーまたは証明書を使用して認証を行います。

## <a name="public-client-applications"></a>パブリッククライアントアプリケーション

これらは一般的にデスクトップアプリケーションまたはモバイルアプリケーションで、デバイス上で実行されているアプリケーションがユーザーに認証を求めるプロンプトを表示し、ユーザーはバックエンド MIP サービスに直接接続します。 このシナリオでは、認証ライブラリを使用して、ユーザーが Azure AD にサインインできること、多要素または条件付きアクセス要件を満たしていること、および適切なリソースの OAuth2 トークンを取得できることを確認する必要があります。

詳細については、Azure AD[パブリッククライアントの認証フロー](/azure/active-directory/develop/msal-net-initializing-client-applications#initializing-a-public-client-application-from-configuration-options)に関するドキュメントを参照してください。

Microsoft 認証ライブラリ (MSAL) を使用した Microsoft Information Protection SDK クライアントアプリケーションのパブリッククライアント認証フローを示す、クイックコード領域を次に示します。

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

テナント GUID は Azure AD テナントのテナント GUID を表し、アプリケーション ID は Azure AD ポータルのアプリケーション登録のアプリケーション ID です。

## <a name="confidential-client-applications"></a>機密クライアントアプリケーション

これらは一般に、ユーザーがバックエンド MIP サービスに直接接続しない、クラウドまたはサービスベースのアプリケーションですが、サービスは、MIP 対応コンテンツのラベル付け、保護、または保護解除を行う必要があります。 このシナリオでは、アプリケーションは Azure AD の認証に使用する証明書またはアプリケーションシークレットを格納し、そのシークレットを使用してバックエンド MIP サービスのトークンを取得する必要があります。 その後、MIP SDK の委任機能を使用して、認証されたユーザーの代わりにコンテンツを保護または使用することができます。

詳細については、Azure AD[社外秘クライアント認証フロー](/azure/active-directory/develop/msal-net-initializing-client-applications#initializing-a-confidential-client-application-from-code)に関するドキュメントを参照してください。

次に示すのは、microsoft 認証ライブラリ (MSAL) を使用して Microsoft Information Protection SDK クライアントアプリケーションの機密クライアント認証フローをデモンストレーションするクイックコード領域です。 アプリケーションは、AD 証明書またはクライアントシークレットを使用して認証できます。

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

テナント GUID は Azure AD テナントのテナント GUID を表し、アプリケーション ID は Azure AD ポータルのアプリケーション登録のアプリケーション ID です。