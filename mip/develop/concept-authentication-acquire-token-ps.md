---
title: 概念 - PowerShell を使用してアクセス トークンを取得します。
description: この記事は、PowerShell を使用して OAuth2 アクセス トークンを取得する方法を理解するのに役立ちます。 これは、認証委任の実装で必要になります。
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 3206fb99cd72c5d609375ec673e7798d33c735c3
ms.sourcegitcommit: 823a14784f4b34288f221e3b3cb41bbd1d5ef3a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453386"
---
# <a name="acquire-an-access-token-powershell"></a>アクセス トークンを取得する (PowerShell)

この例では、外部の PowerShell スクリプトを呼び出して OAuth2 トークンを取得する方法を示します。 これは、認証委任の実装で必要になります。

このコードは運用環境で使用するためのものではありませんが、開発に、また、認証概念を理解するために使用できます。 

## <a name="sampleauthacquiretoken"></a>sample::auth::AcquireToken()

### <a name="authh"></a>auth.h

AcquireToken という単一の関数を作成します。 このチュートリアルでは戻り値はハードコーディングされるため、パラメーターは受け入れず、単に文字列 (トークン) を返すようにします。

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

このソース ファイルでは、後の手順でハードコーディングされるトークン値が返されます。

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

最後に、mToken 変数に入れるトークンを mint します。 次の例では、Windows で ADAL および PowerShell を使用して、OAuth2 トークンをすばやく取得するために使用できる PowerShell スクリプトを示します。 このトークンは、Office 365 セキュリティとコンプライアンス センターのエンドポイントに対してのみ付与されます。 そのため、リソース URL が更新されない限り、保護アクションは失敗します。 この時点でラベルと保護の両方でテストしたい場合は、[次の手順](#next-steps)のセクションに進むことをお勧めします。

### <a name="install-adalpshttpswwwpowershellgallerycompackagesadalps31942-from-ps-gallery"></a>PS ギャラリーから [ADAL.PS](https://www.powershellgallery.com/packages/ADAL.PS/3.19.4.2) をインストールする

```PowerShell
Install-Module -Name ADAL.PS
```

### <a name="use-get-adaltoken-to-obtain-the-access-token"></a>Get-ADALToken を使用してアクセス トークンを取得する

```PowerShell
#Install the ADAL.PS package if it's not installed.
if(!(Get-Package adal.ps)) { Install-Package -Name adal.ps }

$authority = "https://login.windows.net/common/oauth2/authorize" 
#this is the security and compliance center endpoint
$resourceUrl = "https://dataservice.o365filtering.com"
#clientId and redirectUri are from the RMS Sharing Application. 
#Once custom app registration is supported, a custom id and uri will be required. 
$clientId = "6b069eef-9dde-4a29-b402-8ce866edc897"
$redirectUri = "com.microsoft.rms-sharing-for-win://authorize"

$response = Get-ADALToken -Resource $resourceUrl -ClientId $clientId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:Always
$response.AccessToken | clip
```

`string mToken` の値として、トークンをクリップボードから auth.cpp にコピーして、上記の "your token here" を置き換えます。 次の手順の所要時間に応じて、スクリプトをもう一度実行する必要がある場合があります。


