---
title: クラス UserRoles
description: 'Microsoft Information Protection (MIP) SDK の userroles:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: ef881f184fd370665006c8fb4d73138b7c5e2f3c
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214135"
---
# <a name="class-userroles"></a>クラス UserRoles 
ユーザーのグループおよびそれらに関連付けられているロール。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public UserRoles (const std:: vector \<std::string\>& users、const std:: vector \<std::string\>& ロール)  |  UserRoles コンストラクター。
public const std:: vector \<std::string\>& Users () const  |  ロールのセットに関連付けられているユーザーを取得します。
public const std:: vector \<std::string\>& Roles () const  |  ユーザーのグループに関連付けられているロールを取得します。
  
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