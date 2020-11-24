---
title: class ConsentDelegate
description: 'Microsoft Information Protection (MIP) SDK の conの delegate:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 5f31be6cfd6b9c15bda74a731f0774f786d97f5f
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95569199"
---
# <a name="class-consentdelegate"></a>class ConsentDelegate 
同意に関連する操作の委任。
この委任は、同意を要求する通知がいつユーザーに表示されるかを把握するために、クライアント アプリケーションによって実装されます。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public Consent GetUserConsent(const std::string& url)  |  SDK でサービス エンドポイントに接続するためのユーザーの同意が求められたときに呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="getuserconsent-function"></a>GetUserConsent 関数
SDK でサービス エンドポイントに接続するためのユーザーの同意が求められたときに呼び出されます。

パラメーター:  
* **url**: SDK でユーザーの同意が求められる URL



  
**戻り値**: ユーザーの決定を含む Consent 列挙型。
このメソッドを使用して SDK でユーザーの同意が求められる場合、クライアント アプリケーションではユーザーに URL を提示する必要があります。 クライアント アプリケーションでは、ユーザーの同意を取得するための手段を提供し、ユーザーの決定に対応する適切な Consent 列挙型を返す必要があります。