---
title: クラス UserRights
description: 'Microsoft Information Protection (MIP) SDK の userrights:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 37943d284eaa00524797605158e320c25e52e17b
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95569446"
---
# <a name="class-userrights"></a>クラス UserRights 
ユーザーのグループおよびそれらに関連付けられている権限。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public UserRights (const std:: vector \<std::string\>& users, const std:: vector \<std::string\>& 権限)  |  UserRights コンストラクター。
public const std:: vector \<std::string\>& Users () const  |  権限のセットに関連付けられているユーザーを取得します。
public const std:: vector \<std::string\>& 権限 () const  |  ユーザーのグループに関連付けられている権限を取得します。
  
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