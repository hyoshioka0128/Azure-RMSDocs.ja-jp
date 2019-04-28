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
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60175311"
---
# <a name="acquire-an-access-token-powershell"></a>アクセス トークンを取得する (PowerShell)

この例では、OAuth2 トークンを取得する外部の PowerShell スクリプトを呼び出す方法を示します。 有効な OAuth2 アクセス トークンは、認証のデリゲートの実装で必要です。

## <a name="prerequisites"></a>前提条件

- 完全な[(MIP) SDK のセットアップと構成](setup-configure-mip.md)します。 その他のタスク間で、Azure Active Directory (Azure AD) テナント、クライアント アプリケーションを登録します。 Azure AD では、これは、トークンの取得ロジックで使用すると、クライアント ID とも呼ばれる、アプリケーション ID を提供します。

このコードは、運用環境で使用目的としています。 開発と認証の概念についてのみ使用できます。 

## <a name="sampleauthacquiretoken"></a>sample::auth::AcquireToken()

### <a name="authh"></a>auth.h

AcquireToken という単一の関数を作成します。 戻り値になるため、ハードコーディングこのチュートリアルでは、パラメーターを受け付けずお文字列 (トークン) を返します。

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

ソース ファイルは、後の手順で、ハードコーディングされるトークンの値を返します。

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

既に完了している場合は、この手順をスキップすることができます[(MIP) SDK のセットアップと構成](setup-configure-mip.md)します。

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


