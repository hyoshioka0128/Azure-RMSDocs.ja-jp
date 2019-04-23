---
title: クラスの:identity
description: :Identity クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 75d11fae7d79cadc4dd8909be371cbde2e87f289
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "60173543"
---
# <a name="class-mipidentity"></a>クラスの:identity 
Id の抽象化です。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
パブリック Identity()  |  既定の[Identity](class_mip_identity.md)ユーザーの電子メール アドレスが不明の場合に使用されるコンス トラクター。
public Identity(const Identity& other)  |  [Identity](class_mip_identity.md)コピー コンス トラクター。
パブリックの明示的な Id (const std::string & 電子メール)  |  [Identity](class_mip_identity.md)ユーザーの電子メール アドレスがわかっている場合に使用されるコンス トラクター。
public const std::string& GetEmail() const  |  電子メールを取得します。
public void SetDelegatedEmail(const std::string& delegatedEmail)  |  On behalf of、opertations の実行をユーザーが委任された電子メール、委任された電子メール アドレスを設定します。
public const std::string& GetDelegatedEmail() const  |  委任された電子メールを取得、委任された電子メール アドレスを on behalf of ユーザー、opertations が実行されます。
  
## <a name="members"></a>メンバー
  
### <a name="identity-function"></a>Identity 関数
既定の[Identity](class_mip_identity.md)ユーザーの電子メール アドレスが不明の場合に使用されるコンス トラクター。
  
### <a name="identity-function"></a>Identity 関数
[Identity](class_mip_identity.md)コピー コンス トラクター。

パラメーター:  
* **[Identity](class_mip_identity.md)**: コピーを作成するために使用します。


  
### <a name="identity-function"></a>Identity 関数
[Identity](class_mip_identity.md)ユーザーの電子メール アドレスがわかっている場合に使用されるコンス トラクター。

パラメーター:  
* **電子メール**: ユーザーの電子メール アドレス。


  
### <a name="getemail-function"></a>GetEmail 関数
電子メールを取得します。

  
**返します**:電子メール アドレス。
  
### <a name="setdelegatedemail-function"></a>SetDelegatedEmail 関数
On behalf of、opertations の実行をユーザーが委任された電子メール、委任された電子メール アドレスを設定します。

パラメーター:  
* **delegatedEmail**: 委任電子メール。


  
### <a name="getdelegatedemail-function"></a>GetDelegatedEmail 関数
委任された電子メールを取得、委任された電子メール アドレスを on behalf of ユーザー、opertations が実行されます。

  
**返します**:委任された電子メール アドレス。