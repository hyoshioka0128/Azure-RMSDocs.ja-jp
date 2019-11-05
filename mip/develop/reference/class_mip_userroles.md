---
title: class mip::UserRoles
description: 'Microsoft Information Protection (MIP) SDK の mip:: userroles クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: e77ed6ae4d4b5467964f855a081cc22780d9869c
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560461"
---
# <a name="class-mipuserroles"></a>class mip::UserRoles 
ユーザーのグループおよびそれらに関連付けられているロール。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public UserRoles (const std:: vector\<std:: string\>& users、const std:: vector\<std:: string\>& roles)  |  UserRoles コンストラクター。
public const std:: vector\<std:: string\>& Users () const  |  ロールのセットに関連付けられているユーザーを取得します。
public const std:: vector\<std:: string\>& Roles () const  |  ユーザーのグループに関連付けられているロールを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="userroles-function"></a>UserRoles 関数
UserRoles コンストラクター。

パラメーター:  
* **users**: 同じロールを共有するユーザーのグループ 


* **roles**: ユーザーのグループによって共有されているロール


  
### <a name="users-function"></a>Users 関数
ロールのセットに関連付けられているユーザーを取得します。

  
**戻り値**: ロールのセットに関連付けられているユーザー
  
### <a name="roles-function"></a>Roles 関数
ユーザーのグループに関連付けられているロールを取得します。

  
**戻り値**: ユーザーのグループに関連付けられているロール