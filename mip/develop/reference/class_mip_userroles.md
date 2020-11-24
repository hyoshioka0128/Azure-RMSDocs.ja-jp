---
title: クラス UserRoles
description: 'Microsoft Information Protection (MIP) SDK の userroles:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: fc6e5f77c68ecde2582cfd622624c0c6b986500b
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566620"
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