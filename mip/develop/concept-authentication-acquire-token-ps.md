---
title: 概念 - PowerShell を使用してアクセス トークンを取得します。
description: この記事は、PowerShell を使用して OAuth2 アクセス トークンを取得する方法を理解するのに役立ちます。 これは、認証委任の実装で必要になります。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 02/04/2019
ms.author: mbaldwin
ms.openlocfilehash: 68ae6bc02f671f0a4d18c382ccde4f53873b2fd4
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "60175311"
---
# <a name="acquire-an-access-token-powershell"></a>アクセス トークンを取得する (PowerShell)

次の例は、外部 PowerShell スクリプトを呼び出して OAuth2 トークンを取得する方法を示しています。 認証デリゲートの実装では、有効な OAuth2 アクセストークンが必要です。

## <a name="prerequisites"></a>必要条件

- 完成した[(MIP) SDK のセットアップと構成](setup-configure-mip.md)。 他のタスクでは、クライアントアプリケーションを Azure Active Directory (Azure AD) テナントに登録します。 Azure AD は、トークン取得ロジックで使用されるアプリケーション ID (クライアント ID とも呼ばれます) を提供します。

このコードは、運用環境で使用するためのものではありません。 これは、開発と認証の概念を理解するためにのみ使用できます。 

## <a name="sampleauthacquiretoken"></a>sample::auth::AcquireToken()

### <a name="authh"></a>auth.h

AcquireToken という単一の関数を作成します。 このチュートリアルでは戻り値をハードコーディングするため、パラメーターを受け入れず、文字列 (トークン) を返します。

```cpp
//auth.h
#include <string>

namespace sample {
  namespace auth {
    std::string AcquireToken();
  }
}
```

### <a name="authcpp"></a>auth.cpp

ソースファイルは、後の手順でハードコーディングされるトークン値を返します。

```cpp
//auth.cpp
#include <string>
#include "auth.h"

namespace sample {
  namespace auth {
    string AcquireToken() {
      std::string mToken = "your token here";
      return mToken;
    }
  }
}
```

## <a name="mint-a-token"></a>トークンを mint する

最後に、mToken 変数に入れるトークンを mint します。 次の例では、Windows で ADAL および PowerShell を使用して、OAuth2 トークンをすばやく取得するために使用できる PowerShell スクリプトを示します。 このトークンは、Office 365 セキュリティとコンプライアンス センターのエンドポイントに対してのみ付与されます。 そのため、リソース URL が更新されない限り、保護アクションは失敗します。 

### <a name="install-adalpshttpswwwpowershellgallerycompackagesadalps31942-from-ps-gallery"></a>PS ギャラリーから [ADAL.PS](https://www.powershellgallery.com/packages/ADAL.PS/3.19.4.2) をインストールする

以前に[(MIP) SDK のセットアップと構成](setup-configure-mip.md)を完了している場合は、この手順を省略できます。

```PowerShell
Install-Module -Name ADAL.PS
```

### <a name="use-get-adaltoken-to-obtain-the-access-token"></a>Get-ADALToken を使用してアクセス トークンを取得する

```PowerShell
#Install the ADAL.PS package if it's not installed.
if(!(Get-Package adal.ps)) { Install-Package -Name adal.ps }

$authority = "https://login.windows.net/common/oauth2/authorize" 
#this is the security and compliance center endpoint
$resourceUrl = "https://syncservice.o365syncservice.com/"
#replace <application-id> and <redirect-uri>, with the Redirect URI and Application ID from your Azure AD application registration.
$clientId = "<application-id>"
$redirectUri = "<redirect-uri>"

$response = Get-ADALToken -Resource $resourceUrl -ClientId $clientId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:Always
$response.AccessToken | clip
```

`string mToken` の値として、トークンをクリップボードから auth.cpp にコピーして、上記の "your token here" を置き換えます。 次の手順の所要時間に応じて、スクリプトをもう一度実行する必要がある場合があります。


