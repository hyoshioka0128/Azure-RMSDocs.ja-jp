---
title: 概念 - Python を使用してアクセス トークンを取得します。
description: この記事は、Python を使用して OAuth2 アクセス トークンを取得する方法を理解するのに役立ちます。 これは、認証委任の実装で必要になります。
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 02/04/2019
ms.author: bryanla
ms.openlocfilehash: 423ae80df11dcf8031f845fdabf881606daf89c7
ms.sourcegitcommit: fa7551060aaecc62d0c1f9179dd07f035d86651f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/05/2019
ms.locfileid: "55742169"
---
# <a name="acquire-an-access-token-python"></a>アクセス トークンを取得する (Python)

この例では、外部の Python スクリプトを呼び出して OAuth2 トークンを取得する方法を示します。 有効な OAuth2 アクセス トークンは、認証のデリゲートの実装で必要です。

## <a name="prerequisites"></a>前提条件

以下のサンプルを実行します。

- Python 2.7 をインストールします。
- プロジェクトに utils.h/cpp を実装します。 
- Auth.py はプロジェクトに追加する必要があり、ビルドのバイナリと同じディレクトリに存在します。
- 完全な[(MIP) SDK のセットアップと構成](setup-configure-mip.md)します。 その他のタスク間で、Azure Active Directory (Azure AD) テナント、クライアント アプリケーションを登録します。 Azure AD では、これは、トークンの取得ロジックで使用すると、クライアント ID とも呼ばれる、アプリケーション ID を提供します。

このコードは、運用環境で使用目的としています。 開発と認証の概念についてのみ使用できます。 このサンプルは、クロス プラットフォームです。

## <a name="sampleauthacquiretoken"></a>sample::auth::AcquireToken()

単純な認証の例で、単純なお見せしました`AcquireToken()`関数パラメーターがありませんでしたし、ハード コーディングされたトークンの値が返されます。 この例では、AcquireToken() をオーバーロードして、認証パラメータを受け入れ、外部の Python スクリプトを呼び出し、トークンを戻します。

### <a name="authh"></a>auth.h

auth.h では、`AcquireToken()` がオーバーロードされます。オーバーロードされた関数と更新されたパラメーターは次のとおりです。

```cpp
//auth.h
#include <string>

namespace sample {
  namespace auth {
    std::string AcquireToken();

    std::string AcquireToken(
        const std::string& userName, //A string value containing the user's UPN.
        const std::string& password, //The user's password in plaintext
        const std::string& clientId, //The Azure AD client ID (also known as Application ID) of your application.
        const std::string& resource, //The resource URL for which an OAuth2 token is required. Provided by challenge object.
        const std::string& authority); //The authentication authority endpoint. Provided by challenge object.
    }
}
```

最初の 3 つのパラメーターはユーザー入力によって得られるか、アプリケーションにハード コーディングされています。 最後の 2 つのパラメーターは、認証委任に SDK によって提供されます。 


### <a name="authcpp"></a>auth.cpp

auth.cpp では、オーバーロードされた関数定義を追加し、Python スクリプトを呼び出すのに必要なコードを定義しました。 この関数は、提供されているすべてのパラメーターを受け入れ、それを Python スクリプトに渡します。 スクリプトが実行され、トークンが文字列の形式で戻されます。

```cpp
#include "auth.h"
#include "utils.h"

#include <fstream>
#include <functional>
#include <memory>
#include <string>

using std::string;
using std::runtime_error;

namespace sample {
    namespace auth {

    string AcquireToken() { //ignore in this sample
    }

    //This function implements token acquisition in the application by calling an external Python script.
    //The Python script requires username, password, clientId, resource, and authority.
    //Username, Password, and ClientId are provided by the user/developer
    //Resource and Authority are provided as part of the OAuth2Challenge object that is passed in by the SDK to the AuthDelegate.
    string AcquireToken(
        const string& userName,
        const string& password,
        const string& clientId,
        const string& resource,
        const string& authority) {

    string cmd = "python";
    if (sample::FileExists("auth.py"))
        cmd += " auth.py -u ";

    else
        throw runtime_error("Unable to find auth script.");

    cmd += userName;
    cmd += " -p ";
    cmd += password;
    cmd += " -a ";
    cmd += authority;
    cmd += " -r ";
    cmd += resource;
    cmd += " -c ";
    // Replace <application-id> with the Application ID provided during your Azure AD application registration.
    cmd += (!clientId.empty() ? clientId : "<application-id>");

    string result = sample::Execute(cmd.c_str());
    if (result.empty())
        throw runtime_error("Failed to acquire token. Ensure Python is installed correctly.");

    return result;
    }
    }
}

```

## <a name="python-script"></a>Python スクリプト

このスクリプトは、シンプルな http 要求を使用して、認証トークンを取得します。 これは、サンプル アプリが認証トークンを取得するためのみに含まれており、実稼働のコードで使用されることは意図していません。 このスクリプトは、単純な古いユーザー名/パスワード http 認証をサポートするテナントに対してのみ動作します。 MFA または証明書ベースの認証は失敗します。

```python
import getopt
import sys
import json
import urllib
import urllib2
import re

def printUsage():
  print('auth.py -u <username> -p <password> -a <authority> -r <resource> -c <clientId>')

def main(argv):
  try:
    options, args = getopt.getopt(argv, 'hu:p:a:r:c:')
  except getopt.GetoptError:
    printUsage()
    sys.exit(-1)

  username = ''
  password = ''
  authority = ''
  resource = ''
  clientId = ''

  for option, arg in options:
    if option == '-h':
      printUsage()
      sys.exit()
    elif option == '-u':
      username = arg
    elif option == '-p':
      password = arg
    elif option == '-a':
      authority = arg
    elif option == '-r':
      resource = arg
    elif option == '-c':
      clientId = arg

  if username == '' or password == '' or authority == '' or resource == '' or clientId == '':
    printUsage()
    sys.exit(-1)

  # Find everything after the last '/' and replace it with 'token'
  if not authority.endswith('token'):
    regex = re.compile('^(.*[\/])')
    match = regex.match(authority)
    authority = match.group()
    authority = authority + 'token'

  # Build REST call
  headers = {
    'Content-Type': 'application/x-www-form-urlencoded',
    'Accept': 'application/json'
  }

  params = {
    'resource': resource,
    'client_id': clientId,
    'grant_type': 'password',
    'username': username,
    'password': password
  }

  req = urllib2.Request(
    url = authority,
    headers = headers,
    data = urllib.urlencode(params))

  f = urllib2.urlopen(req)
  response = f.read()
  f.close()
  sys.stdout.write(json.loads(response)['access_token'])

if __name__ == '__main__':
  main(sys.argv[1:])
```

## <a name="update-acquireoauth2token"></a>AcquireOAuth2Token の更新

最後に、`AuthDelegateImpl` の `AcquireOAuth2Token` 関数を更新し、オーバーロードされた `AcquireToken` 関数を呼び出します。 リソースおよび権限 URL は、`challenge.GetResource()` と `challenge.GetAuthority()` を読むことによって取得されます。 エンジンの追加時に、`OAuth2Challenge` は認証委任に渡されます。 この作業は SDK が行います。開発者側では他に何も行う必要はありません。 

```cpp
bool AuthDelegateImpl::AcquireOAuth2Token(
    const mip::Identity& /*identity*/,
    const OAuth2Challenge& challenge,
    OAuth2Token& token) {

    //call our AcquireToken function, passing in username, password, clientId, and getting the resource/authority from the OAuth2Challenge object
    string accessToken = sample::auth::AcquireToken(mUserName, mPassword, mClientId, challenge.GetResource(), challenge.GetAuthority());
    token.SetAccessToken(accessToken);
    return true;
}
```

`engine` が追加されると、SDK が `AcquireOAuth2Token 関数を呼び出し、チャレンジを渡し、Python スクリプトを実行し、トークンを受け取り、トークンをサービスに提示します。


