---
# required metadata

title: 方法&#58; アプリに認証を追加する | Azure RMS
description: RMS 対応アプリケーションのユーザー認証の基本について説明します。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 94697eb5-1fab-4591-bd40-b5646daac8a3

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿
# 方法&#58; アプリに認証を追加する

このトピックでは、RMS 対応アプリケーションのユーザー認証の基本について説明します。

## ユーザー認証とは
ユーザー認証は、デバイス アプリケーションと RMS インフラストラクチャ間の通信を確立するために不可欠な手順です。 この認証プロセスでは標準の OAuth 2.0 プロトコルを使用します。ここでは、現在のユーザーおよびその認証要求について、**authority**、**resource**、および **userId** といった情報が必要になります。

**注**  範囲は現在使用されていませんが、今後の使用のために予約されています。

 

**ユーザー認証コールバック** - Microsoft Rights Management SDK 4.2 では、アクセス トークンが指定されなかった場合、また、アクセス トークンを更新する必要があったり、有効期限が切れている場合に認証コールバックの実装が使用されます。

ユーザーの認証を有効にするには、プラットフォームの各 RMS API に含まれるコールバックを実装する必要があります。

-   Android API では [**AuthenticationRequestCallback**](/rights-management/sdk/4.2/api/android/com.microsoft.rightsmanagement#msipcthin2_authenticationrequestcallback_interface_java) および [**AuthenticationCompletionCallback**](/rights-management/sdk/4.2/api/android/authenticationcompletioncallback#msipcthin2_authenticationcompletioncallback_interface_java) インターフェイスを使用します。
-   iOS/OS X API では、[**MSAuthenticationCallback**](/rights-management/sdk/4.2/api/iOS/iOS#msipcthin2_msauthenticationcallback_protocol_objc) プロトコルを使用します。
-   WinPhone API では [**IAuthenticationCallback**](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement#msipcthin2_iauthenticationcallback) インターフェイスを使用します。
-   Linux API では [IAuthenticationCallback](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1IAuthenticationCallback.html) インターフェイスを使用します。

## 認証に使用するライブラリ

認証コールバックを実装するには、適切なライブラリをダウンロードして、それを使用するように開発環境を構成する必要があります。 これらのプラットフォーム用の ADAL ライブラリが GitHub に用意されています。 次の各リソースには、環境をセットアップして、ライブラリを使用するためのガイダンスが含まれています。

-   [Windows Azure Active Directory 認証ライブラリ (ADAL) (iOS 向け)](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [Windows Azure Active Directory 認証ライブラリ (ADAL) (Mac 向け)](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/)
-   [Windows Azure Active Directory 認証ライブラリ (ADAL) (Android 向け)](https://github.com/MSOpenTech/azure-activedirectory-library-for-android)
-   [Windows Azure Active Directory 認証ライブラリ (ADAL) (dotnet 向け)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet)
-   Linux SDK の場合、ADAL ライブラリは SDK ソースでパッケージ化されます ([Github](https://github.com/AzureAD/rms-sdk-for-cpp) で入手可能)。

**注**  他の認証ライブラリも使用できますが、上記の Active Directory 認証ライブラリ (ADAL) のいずれかを使用することをお勧めします。

## Active Directory 認証ライブラリ (ADAL) を使用する認証の入力

ユーザーを Azure RMS (または AD RMS) に認証するには、ADAL にいくつかのパラメーターが必要です。 RMS 対応アプリと同様に、Azure AD アプリの一般的に必要な標準の OAuth 2.0 パラメーターは次のとおりです。 ADAL 使用法の現行のガイドラインについては、前に記載された対応する Github リポジトリの README ファイルをご覧ください。

次のパラメーターとガイドラインが、RMS ワーク フローに必要です。

-   **権限** – 認証エンドポイントの URL。通常は AAD または ADFS です。 このパラメーターは、RMS SDK 認証コールバックによってアプリに提供されます。
-   **リソース** - アクセスしようとしているサービス アプリケーション (通常 Azure RMS または AD RMS) の URL/URI。 このパラメーターは、RMS SDK 認証コールバックによってアプリに提供されます。
-   **ユーザー ID** – UPN。通常は、アプリにアクセスするユーザーの電子メール アドレスです。 このパラメーターは、ユーザーが不明の場合は空にできます。また、ユーザー トークンをキャッシュしたり、キャッシュからトークンを要求したりする場合にも使用できます。 一般的に、ユーザー プロンプトの "ヒント" としても使用されます。
-   **クライアント ID** – クライアント アプリの ID。 有効な Azure AD アプリケーションの ID である必要があります。 詳しくは、「方法: Azure アプリケーション ID を取得する」をご覧ください。
-   **リダイレクト URI** – 認証コードの対象の URI で認証ライブラリを指定します。 iOS および Android には特定の形式が必要なことに注意してください。詳しくは、ADAL の対応する GitHub リポジトリの README ファイルをご覧ください。

    Android: `msauth://packagename/Base64UrlencodedSignature`

    iOS: `<app-scheme>://<bundle-id>`

**注**  アプリがこれらのガイドラインを遵守しない場合、Azure RMS および Azure AD ワークフローが失敗することがあり、Microsoft.com によってサポートされなくなります。 また、運用アプリケーションで無効なクライアント ID を使用した場合、Rights Management License Agreement (RMLA) 違反が発生する可能性があります。

## 認証コールバックの実装の例

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


**iOS/OS X ユーザー認証** - 詳しくは、「[iOS/OS X のコード例](ios-os-x-code-examples.md)」、

最初のシナリオの**ステップ 2**、「RMS 保護ファイルを使用する」をご覧ください。


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



**Linux/C++ ユーザー認証** - 詳しくは、「[Linux のコード例](linux-c-code-examples.md)」をご覧ください。



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



 

 


<!--HONumber=Apr16_HO3-->


