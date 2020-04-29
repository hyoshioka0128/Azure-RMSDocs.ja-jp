---
title: クラス UserRights
description: 'Microsoft Information Protection (MIP) SDK の userrights:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 1a3bf2c6c8f417d30fac24263f672f2603347960
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764255"
---
# <a name="class-userrights"></a>クラス UserRights 
ユーザーのグループおよびそれらに関連付けられている権限。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public UserRights (const std:: vector\<std:: string\>& users, const std:: vector\<std:: string\>& 権限)  |  UserRights コンストラクター。
public const std:: vector\<std:: String\>& Users () const  |  権限のセットに関連付けられているユーザーを取得します。
public const std:: vector\<std:: String\>& 権限 () const  |  ユーザーのグループに関連付けられている権限を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="userrights-function"></a>UserRights 関数
UserRights コンストラクター。

パラメーター:  
* **users**: 同じ権限を共有するユーザーのグループ 


* **rights**: ユーザーのグループによって共有されている権限


  
### <a name="users-function"></a>Users 関数
権限のセットに関連付けられているユーザーを取得します。

  
**戻り値**: 権限のセットに関連付けられているユーザー
  
### <a name="rights-function"></a>権限関数
ユーザーのグループに関連付けられている権限を取得します。

  
**戻り値**: ユーザーのグループに関連付けられている権限