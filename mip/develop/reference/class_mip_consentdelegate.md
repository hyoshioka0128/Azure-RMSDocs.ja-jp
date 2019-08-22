---
title: 'クラス mip:: Conのデリゲート'
description: 'Microsoft Information Protection (MIP) SDK の mip:: conのデリゲートクラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: ea088c9d92712243f3c628c17fadb0e61831103b
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884428"
---
# <a name="class-mipconsentdelegate"></a>クラス mip:: Conのデリゲート 
同意に関連する操作の委任。
この委任は、同意を要求する通知がいつユーザーに表示されるかを把握するために、クライアント アプリケーションによって実装されます。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public Consent GetUserConsent(const std::string& url)  |  SDK でサービス エンドポイントに接続するためのユーザーの同意が求められたときに呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="getuserconsent-function"></a>GetUserConsent 関数
SDK でサービス エンドポイントに接続するためのユーザーの同意が求められたときに呼び出されます。

パラメーター:  
* **url**:SDK がユーザーの同意を必要とする URL



  
次の**値を返し**ます。ユーザーの決定を持つ同意列挙型。
このメソッドを使用して SDK でユーザーの同意が求められる場合、クライアント アプリケーションではユーザーに URL を提示する必要があります。 クライアント アプリケーションでは、ユーザーの同意を取得するための手段を提供し、ユーザーの決定に対応する適切な Consent 列挙型を返す必要があります。