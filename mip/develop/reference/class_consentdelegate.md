---
title: class ConsentDelegate
description: class ConsentDelegate のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 841049b1e6b369eb2f6a34d9701ed34eca028af6
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446364"
---
# <a name="class-consentdelegate"></a>class ConsentDelegate 
同意に関連する操作の委任。
この委任は、同意を要求する通知がいつユーザーに表示されるかを把握するために、クライアント アプリケーションによって実装されます。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public Consent GetUserConsent(const std::string& url)  |  SDK でサービス エンドポイントに接続するためのユーザーの同意が求められたときに呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="consent"></a>同意
SDK でサービス エンドポイントに接続するためのユーザーの同意が求められたときに呼び出されます。

パラメーター:  
* **url**: SDK でユーザーの同意が求められる URL



  
**戻り値**: ユーザーの決定を含む Consent 列挙型。
このメソッドを使用して SDK でユーザーの同意が求められる場合、クライアント アプリケーションではユーザーに URL を提示する必要があります。 クライアント アプリケーションでは、ユーザーの同意を取得するための手段を提供し、ユーザーの決定に対応する適切な Consent 列挙型を返す必要があります。