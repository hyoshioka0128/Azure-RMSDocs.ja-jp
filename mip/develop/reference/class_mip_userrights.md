---
title: class mip::UserRights
description: Mip::userrights クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: aadf12606f74d508ba3ebdc1ce0770febd49e142
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2019
ms.locfileid: "56251304"
---
# <a name="class-mipuserrights"></a>class mip::UserRights 
ユーザーのグループおよびそれらに関連付けられている権限。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック UserRights (const std::vector\<std::string\>(& a) ユーザー、const std::vector\<std::string\>& rights)  |  [UserRights](class_mip_userrights.md) コンストラクター。
public const std::vector\<std::string\>& Users() const  |  権限のセットに関連付けられているユーザーを取得します。
public const std::vector\<std::string\>& Rights() const  |  ユーザーのグループに関連付けられている権限を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="userrights-function"></a>UserRights 関数
[UserRights](class_mip_userrights.md) コンストラクター。

パラメーター:  
* **ユーザー**:同じ権限を共有するユーザーのグループ 


* **rights**:ユーザーのグループによって共有されている権限


  
### <a name="users-function"></a>ユーザー関数
権限のセットに関連付けられているユーザーを取得します。

  
**返します**:権限のセットに関連付けられているユーザー
  
### <a name="rights-function"></a>Rights 関数
ユーザーのグループに関連付けられている権限を取得します。

  
**返します**:ユーザーのグループに関連付けられている権限
