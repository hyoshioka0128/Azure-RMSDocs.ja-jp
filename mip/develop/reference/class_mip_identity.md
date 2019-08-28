---
title: 'クラス mip:: Identity'
description: 'Microsoft Information Protection (MIP) SDK の mip:: identity クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 8bb4e30398e6f12214605df6f5ad194334d3eeff
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054779"
---
# <a name="class-mipidentity"></a>クラス mip:: Identity 
Id の抽象化。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック Id ()  |  ユーザーの電子メールアドレスが不明な場合に使用される既定の[id](class_mip_identity.md)コンストラクター。
パブリック Id (const Identity & その他)  |  [Id](class_mip_identity.md)コピーコンストラクター。
パブリック明示的な Id (const std:: string & email)  |  ユーザーの電子メールアドレスがわかっている場合に使用される[id](class_mip_identity.md)コンストラクター。
public const std::string& GetEmail() const  |  電子メールを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="identity-function"></a>Identity 関数
ユーザーの電子メールアドレスが不明な場合に使用される既定の[id](class_mip_identity.md)コンストラクター。
  
### <a name="identity-function"></a>Identity 関数
[Id](class_mip_identity.md)コピーコンストラクター。

パラメーター:  
* **[Id](class_mip_identity.md)** : コピーの作成に使用されます。


  
### <a name="identity-function"></a>Identity 関数
ユーザーの電子メールアドレスがわかっている場合に使用される[id](class_mip_identity.md)コンストラクター。

パラメーター:  
* **email**: ユーザーの電子メールアドレス。


  
### <a name="getemail-function"></a>GetEmail 関数
電子メールを取得します。

  
次の**値を返し**ます。電子メール。