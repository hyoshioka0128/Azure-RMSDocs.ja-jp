---
title: 'クラス mip:: Conのデリゲート'
description: 'Microsoft Information Protection (MIP) SDK の mip:: conのデリゲートクラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: bbeca67a1ffcd5a7b159883c97a2eb3a08bfb3e2
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490321"
---
# <a name="class-mipconsentdelegate"></a>クラス mip:: Conのデリゲート 
同意に関連する操作の委任。
この委任は、同意を要求する通知がいつユーザーに表示されるかを把握するために、クライアント アプリケーションによって実装されます。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public Consent GetUserConsent(const std::string& url)  |  SDK でサービス エンドポイントに接続するためのユーザーの同意が求められたときに呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="getuserconsent-function"></a>GetUserConsent 関数
SDK でサービス エンドポイントに接続するためのユーザーの同意が求められたときに呼び出されます。

パラメータ:  
* **url**: SDK でユーザーの同意が求められる URL



  
**戻り値**: ユーザーの決定を含む Consent 列挙型。
このメソッドを使用して SDK でユーザーの同意が求められる場合、クライアント アプリケーションではユーザーに URL を提示する必要があります。 クライアント アプリケーションでは、ユーザーの同意を取得するための手段を提供し、ユーザーの決定に対応する適切な Consent 列挙型を返す必要があります。