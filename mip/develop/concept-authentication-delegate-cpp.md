---
title: 概念 - 認証委任の実装 (C++)
description: この記事は、C++ に認証委任を実装する方法を理解するのに役立ちます。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: e3436acdd6a2900f4a21bb50b283d12065cd659b
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69886261"
---
# <a name="microsoft-information-protection-sdk---implementing-an-authentication-delegate-c"></a>Microsoft Information Protection SDK - 認証委任の実装 (C++)

MIP SDK は認証チャレンジとトークンで応答を処理する、認証委任を実装します。 これ自体では、トークンの取得は実装しません。 トークンの取得手順は開発者次第で、`mip::AuthDelegate` クラスの特に `AcquireOAuth2Token` メンバー関数を拡張することによって実現されます。

## <a name="building-authdelegateimpl"></a>Building AuthDelegateImpl

基底クラス `mip::AuthDelegate` を拡張するには、`sample::auth::AuthDelegateImpl` と呼ばれる新しいクラスを作成します。 このクラスは `AcquireOAuth2Token` 関数を実装し、認証パラメーターを取り入れるコンストラクターを設定します。

### <a name="auth_delegate_implh"></a>auth_delegate_impl.h

この例では、既定のコンストラクターがユーザー名、パスワード、およびアプリケーションの[アプリケーション ID](/azure/active-directory/develop/developer-glossary#application-id-client-id) のみを許可します。 これらは、プライベート変数 `mUserName`、`mPassword`、および `mClientId` に格納されます。

ID プロバイダーやリソース URI などの情報は、少なくとも `AuthDelegateImpl` コンストラクターでは、実装する必要がないということに注意してください。 その情報は、`OAuth2Challenge` オブジェクトの `AcquireOAuth2Token` の一部として渡されます。 代わりに、これらの詳細は、`AcquireOAuth2Token` の `AcquireToken` 呼び出しで渡します。

```cpp
//auth_delegate_impl.h
#include <string.h>
#include "mip/common_types.h"

namespace sample {
namespace auth {
class AuthDelegateImpl final : public mip::AuthDelegate { //extend mip::AuthDelegate base class
public:
  AuthDelegateImpl() = delete;

//constructor accepts username, password, and mip::ApplicationInfo.
  AuthDelegateImpl::AuthDelegateImpl(
    const mip::ApplicationInfo& applicationInfo,
    std::string& username,
    const std::string& password)
    : mApplicationInfo(applicationInfo),
      mUserName(username),
      mPassword(password) {
  }

  bool AcquireOAuth2Token(const mip::Identity& identity, const OAuth2Challenge& challenge, OAuth2Token& token) override;

  private:
    std::string mUserName;
    std::string mPassword;
    std::string mClientId;
    mip::ApplicationInfo mApplicationInfo;
};
}
}
```

### <a name="auth_delegate_implcpp"></a>auth_delegate_impl.cpp

OAuth2 プロバイダーへの呼び出しは、`AcquireOAuth2Token` で行われます。 例の `AcquireToken()` への 2 つの呼び出しを以下に示します。 実際には 1 回の呼び出しのみが行われます。 これらの実装については、「[次の手順](#next-steps)」以下のセクションで扱います。

```cpp
//auth_delegate_impl.cpp
#include "auth_delegate_impl.h"
#include <stdexcept>
#include "auth.h" //contains the auth class used later for token acquisition

using std::runtime_error;
using std::string;

namespace sample {
namespace auth {

AuthDelegateImpl::AuthDelegateImpl(
    const string& userName,
    const string& password,
    const string& clientId)
    : mApplicationInfo(applicationInfo),
    mUserName(userName),
    mPassword(password) {
}

//Here we could simply add our token acquisition code to AcquireOAuth2Token
//Instead, that code is implemented in auth.h/cpp to demonstrate calling an external library
bool AuthDelegateImpl::AcquireOAuth2Token(
    const mip::Identity& /*identity*/, //This won't be used
    const OAuth2Challenge& challenge,
    const OAuth2Token& token) {

      //sample::auth::AcquireToken is the code where the token acquisition routine is implemented.
      //AcquireToken() returns a string that contains the OAuth2 token.

      //Simple example for getting hard coded token. Comment out if not used.
      string accessToken = sample::auth::AcquireToken();

      //Practical example for calling external OAuth2 library with provided authentication details.
      string accessToken = sample::auth::AcquireToken(mUserName, mPassword, mApplicationInfo.applicationId, challenge.GetAuthority(), challenge.GetResource());

      //set the passed in OAuth2Token value to the access token acquired by our provider
      token.SetAccessToken(accessToken);
      return true;
    }
}
}
```

## <a name="next-steps"></a>次の手順

認証の実装を完了するには、`AcquireToken()` 関数の背後のコードを構築する必要があります。 以下の例では、トークンを取得する方法をいくつか説明します。

- [Simple/PowerShell トークンの取得例](concept-authentication-acquire-token-ps.md)
- [Python のトークンの取得例](concept-authentication-acquire-token-py.md)
