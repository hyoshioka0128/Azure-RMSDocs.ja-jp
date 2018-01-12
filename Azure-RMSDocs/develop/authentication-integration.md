---
title: "Azure AD でアプリを登録する方法 - AIP"
description: "RMS 対応アプリケーションのユーザー認証の基本について説明します。"
keywords: 
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 03/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 200D9B23-F35D-4165-9AC4-C482A5CE1D28
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.openlocfilehash: 1d7a5a41c16a8a1354933b13449875de7ec0902e
ms.sourcegitcommit: 93124ef58e471277c7793130f1a82af33dabcea9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2018
---
# <a name="how-to-register-and-rms-enable-your-app-with-azure-ad"></a>Azure AD でアプリの登録と RMS の有効化を行う方法

このトピックでは、Azure ポータルによるアプリ登録と RMS 有効化の基本事項を説明した後、Azure Active Directory Authentication Library (ADAL) によるユーザー認証について説明します。

## <a name="what-is-user-authentication"></a>ユーザー認証とは
ユーザー認証は、デバイス アプリケーションと RMS インフラストラクチャ間の通信を確立するために不可欠な手順です。 この認証プロセスでは、標準の OAuth 2.0 プロトコルを使用します。これには、現在のユーザーと認証要求に関する重要な情報が必要になります。

## <a name="registration-via-azure-portal"></a>Azure ポータルでの登録
まず、Azure ポータルでアプリの登録を構成するためのガイド「[Configure Azure RMS for ADAL authentication (Azure RMS の ADAL 認証を構成する)](adal-auth.md)」に従ってください。 後で使用するために、このプロセスでの**クライアント ID** と**リダイレクト URI** をコピーして保存しておいてください。

## <a name="complete-your-information-protection-integration-agreement-ipia"></a>Information Protection Integration Agreement (IPIA) を完了する
アプリケーションを展開する前に、Microsoft Information Protection チームとの IPIA を完了する必要があります。 完全な詳細については、トピック「[運用環境にデプロイする](deploying-your-application.md)」の最初のセクションを参照してください。

## <a name="implement-user-authentication-for-your-app"></a>アプリのユーザー認証の実装
各 RMS API には、ユーザーの認証を有効にするために実装する必要があるコールバックがあります。 RMS SDK 4.2 は、アクセス トークンを指定しなかった場合、アクセス トークンを更新する必要がある場合、またはアクセス トークンの有効期限が切れている場合に、このコールバックの実装を使用します。

- Android - [AuthenticationRequestCallback](https://msdn.microsoft.com/library/dn758255.aspx) および [AuthenticationCompletionCallback](https://msdn.microsoft.com/library/dn758250.aspx) インターフェイス。
- iOS / OS X - [MSAuthenticationCallback](https://msdn.microsoft.com/library/dn758312.aspx) プロトコル。
-  Windows Phone / Window RT - [IAuthenticationCallback](https://msdn.microsoft.com/library/microsoft.rightsmanagement.iauthenticationcallback.aspx) インターフェイス。
- Linux - [IAuthenticationCallback](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1IAuthenticationCallback.html) インターフェイス。

### <a name="what-library-to-use-for-authentication"></a>認証に使用するライブラリ
認証コールバックを実装するには、適切なライブラリをダウンロードして、それを使用するように開発環境を構成する必要があります。 これらのプラットフォーム用の ADAL ライブラリが GitHub に用意されています。

次の各リソースには、環境をセットアップして、ライブラリを使用するためのガイダンスが含まれています。

-   [Windows Azure Active Directory 認証ライブラリ (ADAL) (iOS 向け)](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [Windows Azure Active Directory 認証ライブラリ (ADAL) (Mac 向け)](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [Windows Azure Active Directory 認証ライブラリ (ADAL) (Android 向け)](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)
-   [Windows Azure Active Directory 認証ライブラリ (ADAL) (dotnet 向け)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)
-   Linux SDK の場合、ADAL ライブラリは SDK ソースでパッケージ化されます ([Github](https://github.com/AzureAD/rms-sdk-for-cpp) で入手可能)。

>[!NOTE]  
> 他の認証ライブラリも使用できますが、ADAL のいずれかを使用することをお勧めします。

### <a name="authentication-parameters"></a>認証パラメーター

ADAL は、Azure RMS (または AD RMS) に対してユーザーを認証するために、いくつかの情報を必要とします。 これらの情報は標準の OAuth 2.0 パラメーターであり、一般にどの Azure AD アプリにも求められます。 ADAL 使用法の現行のガイドラインについては、前に記載された対応する Github リポジトリの README ファイルをご覧ください。

- **権限** – 認証エンドポイントの URL。通常は AAD または ADFS です。
- **リソース** - アクセスしようとしているサービス アプリケーション (通常 Azure RMS または AD RMS) の URL/URI。
- **ユーザー ID** – UPN。通常は、アプリにアクセスするユーザーの電子メール アドレスです。 このパラメーターは、ユーザーが不明の場合は空にできます。また、ユーザー トークンをキャッシュしたり、キャッシュからトークンを要求したりする場合にも使用できます。 一般的に、ユーザー プロンプトの*ヒント*としても使用されます。
- **クライアント ID** – クライアント アプリの ID。 有効な Azure AD アプリケーションの ID である必要があります。
また、前述の Azure ポータルでの登録手順で取得したものです。
- **リダイレクト URI** – 認証コードの対象の URI で認証ライブラリを指定します。 iOS および Android では、特定の形式が必要になります。 これらの形式については、ADAL の対応する GitHub リポジトリの README ファイルで説明されています。 この値は、前述の Azure ポータルでの登録手順で取得したものです。

>[!NOTE]
> **範囲**は現在使用されていませんが、今後の使用のために予約されています。

    Android: `msauth://packagename/Base64UrlencodedSignature`

    iOS: `<app-scheme>://<bundle-id>`

>[!NOTE] 
> アプリがこれらのガイドラインを遵守しない場合、Azure RMS および Azure AD ワークフローが失敗することがあり、Microsoft.com によってサポートされなくなります。また、運用アプリケーションで無効なクライアント ID を使用した場合、Rights Management License Agreement (RMLA) 違反が発生する可能性があります。

### <a name="what-should-an-authentication-callback-implementation-look-like"></a>認証コールバックの実装の例
**認証コード例** - この SDK には、認証コールバックの使用を示すコード例が含まれています。 ご参考のためにここに、また以下のリンクされたトピックでいくつかのコード例を紹介します。

**Android ユーザー認証** - 詳しくは、「[Android のコード例](android-code.md)、最初のシナリオの**ステップ 2**、「RMS 保護ファイルを使用する」をご覧ください。


    class MsipcAuthenticationCallback implements AuthenticationRequestCallback
    {
    ...

    @Override
    public void getToken(Map<String, String> authenticationParametersMap,
                         final AuthenticationCompletionCallback authenticationCompletionCallbackToMsipc)
    {
        String authority = authenticationParametersMap.get("oauth2.authority");
        String resource = authenticationParametersMap.get("oauth2.resource");
        String userId = authenticationParametersMap.get("userId");
        mClientId = “12345678-ABCD-ABCD-ABCD-ABCDEFGHIJ”; // get your registered Azure AD application ID here
        mRedirectUri = “urn:ietf:wg:oauth:2.0:oob”;
        final String userHint = (userId == null)? "" : userId;
        AuthenticationContext authenticationContext = App.getInstance().getAuthenticationContext();
        if (authenticationContext == null || !authenticationContext.getAuthority().equalsIgnoreCase(authority))
        {
            try
            {
                authenticationContext = new AuthenticationContext(App.getInstance().getApplicationContext(), authority, …);
                App.getInstance().setAuthenticationContext(authenticationContext);
            }
            catch (NoSuchAlgorithmException e)
            {
                …
                authenticationCompletionCallbackToMsipc.onFailure();
            }
            catch (NoSuchPaddingException e)
            {
                …
                authenticationCompletionCallbackToMsipc.onFailure();
            }
       }
        App.getInstance().getAuthenticationContext().acquireToken(mParentActivity, resource, mClientId, mRedirectURI, userId, mPromptBehavior,
                       "&USERNAME=" + userHint, new AuthenticationCallback<AuthenticationResult>()
                        {
                            @Override
                            public void onError(Exception exc)
                            {
                                …
                                if (exc instanceof AuthenticationCancelError)
                                {
                                     …
                                    authenticationCompletionCallbackToMsipc.onCancel();
                                }
                                else
                                {
                                     …
                                    authenticationCompletionCallbackToMsipc.onFailure();
                                }
                            }

                            @Override
                            public void onSuccess(AuthenticationResult result)
                            {
                                …
                                if (result == null || result.getAccessToken() == null
                                        || result.getAccessToken().isEmpty())
                                {
                                     …
                                }
                                else
                                {
                                    // request is successful
                                    …
                                    authenticationCompletionCallbackToMsipc.onSuccess(result.getAccessToken());
                                }
                            }
                        });
                         }


**iOS/OS X ユーザー認証** - 詳しくは、「[iOS/OS X のコード例](ios-os-x-code-examples.md)」の*最初のシナリオ「RMS 保護ファイルを使用する」のステップ 2* をご覧ください。


    // AuthenticationCallback holds the necessary information to retrieve an access token.
    @interface MsipcAuthenticationCallback : NSObject<MSAuthenticationCallback>

    @end

    @implementation MsipcAuthenticationCallback

    - (void)accessTokenWithAuthenticationParameters:
         (MSAuthenticationParameters *)authenticationParameters
                                completionBlock:
         (void(^)(NSString *accessToken, NSError *error))completionBlock
    {
    ADAuthenticationError *error;
    ADAuthenticationContext* context = [ADAuthenticationContext authenticationContextWithAuthority:authenticationParameters.authority error:&error];

    NSString *appClientId = @”12345678-ABCD-ABCD-ABCD-ABCDEFGHIJ”;

    // get your registered Azure AD application ID here

    NSURL *redirectURI = [NSURL URLWithString:@”ms-sample://com.microsoft.sampleapp”];

    // get your <app-scheme>://<bundle-id> here
    // Retrieve token using ADAL
    [context acquireTokenWithResource:authenticationParameters.resource
                             clientId:appClientId
                          redirectUri:redirectURI
                               userId:authenticationParameters.userId
                      completionBlock:^(ADAuthenticationResult *result)
                      {
                          if (result.status != AD_SUCCEEDED)
                          {
                              NSLog(@"Auth Failed");
                              completionBlock(nil, result.error);
                          }
                          else
                          {
                              completionBlock(result.accessToken, result.error);
                          }
                      }

        ];
    }



**Linux ユーザー認証** - 詳しくは、「[Linux のコード例](linux-c-code-examples.md)」をご覧ください。



    // Class Header
    class AuthCallback : public IAuthenticationCallback {
    private:

      std::shared_ptr<rmsauth::FileCache> FileCachePtr;
      std::string clientId_;
      std::string redirectUrl_;

      public:

      AuthCallback(const std::string& clientId,
               const std::string& redirectUrl);
      virtual std::string GetToken(shared_ptr<AuthenticationParameters>& ap) override;
    };

    class ConsentCallback : public IConsentCallback {
      public:

      virtual ConsentList Consents(ConsentList& consents) override;
    };

    // Class Implementation
    AuthCallback::AuthCallback(const string& clientId, const string& redirectUrl)
    : clientId_(clientId), redirectUrl_(redirectUrl) {
      FileCachePtr = std::make_shared<FileCache>();
    }

    string AuthCallback::GetToken(shared_ptr<AuthenticationParameters>& ap)
    {
      string redirect =
      ap->Scope().empty() ? redirectUrl_ : ap->Scope();

      try
      {
        if (redirect.empty()) {
        throw rmscore::exceptions::RMSInvalidArgumentException(
              "redirect Url is empty");
      }

      if (clientId_.empty()) {
      throw rmscore::exceptions::RMSInvalidArgumentException("client Id is empty");
      }

      AuthenticationContext authContext(
        ap->Authority(), AuthorityValidationType::False, FileCachePtr);

      auto result = authContext.acquireToken(ap->Resource(),
                                           clientId_, redirect,
                                           PromptBehavior::Auto,
                                           ap->UserId());
      return result->accessToken();
      }

      catch (const rmsauth::Exception& ex)
      {
        // out logs
        throw;
      }
    }

[!INCLUDE[Commenting house rules](../includes/houserules.md)]