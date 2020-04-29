---
title: クラス UserRoles
description: 'Microsoft Information Protection (MIP) SDK の userroles:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: bbff817578bb5ba1fe143c850632e25df8f78708
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764205"
---
# <a name="class-userroles"></a>クラス UserRoles 
ユーザーのグループおよびそれらに関連付けられているロール。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public UserRoles (const std:: vector\<std:: string\>& users, const std:: vector\<std:: string\>& roles)  |  UserRoles コンストラクター。
public const std:: vector\<std:: String\>& Users () const  |  ロールのセットに関連付けられているユーザーを取得します。
public const std:: vector\<std:: String\>& Roles () const  |  ユーザーのグループに関連付けられているロールを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="userroles-function"></a>UserRoles 関数
UserRoles コンストラクター。

パラメーター:  
* **ユーザー**: 同じロールを共有するユーザーのグループ 


* **roles**: ユーザーのグループによって共有されているロール


  
### <a name="users-function"></a>Users 関数
ロールのセットに関連付けられているユーザーを取得します。

  
**戻り値**: ロールのセットに関連付けられているユーザー
  
### <a name="roles-function"></a>Roles 関数
ユーザーのグループに関連付けられているロールを取得します。

  
**戻り値**: ユーザーのグループに関連付けられているロール