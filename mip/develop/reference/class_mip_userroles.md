---
title: class mip::UserRoles
description: 'Microsoft Information Protection (MIP) SDK の mip:: userroles クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: d22f66c8fff22b54e5e7e30f425adc2c889e5db0
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489284"
---
# <a name="class-mipuserroles"></a>class mip::UserRoles 
ユーザーのグループおよびそれらに関連付けられているロール。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
public UserRoles (const std:: vector\<std:: string\>& users、const std:: vector\<std:: string\>& roles)  |  UserRoles コンストラクター。
public const std:: vector\<std:: string\>& Users () const  |  ロールのセットに関連付けられているユーザーを取得します。
public const std:: vector\<std:: string\>& Roles () const  |  ユーザーのグループに関連付けられているロールを取得します。
  
## <a name="members"></a>Members
  
### <a name="userroles-function"></a>UserRoles 関数
UserRoles コンストラクター。

パラメータ:  
* **users**: 同じロールを共有するユーザーのグループ 


* **roles**: ユーザーのグループによって共有されているロール


  
### <a name="users-function"></a>Users 関数
ロールのセットに関連付けられているユーザーを取得します。

  
**戻り値**: ロールのセットに関連付けられているユーザー
  
### <a name="roles-function"></a>Roles 関数
ユーザーのグループに関連付けられているロールを取得します。

  
**戻り値**: ユーザーのグループに関連付けられているロール