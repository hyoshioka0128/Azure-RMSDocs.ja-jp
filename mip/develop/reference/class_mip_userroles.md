---
title: class mip::UserRoles
description: 'Microsoft Information Protection (MIP) SDK の mip:: userroles クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: c674882145e5c47233224f470d3b038bca9a40b7
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69882808"
---
# <a name="class-mipuserroles"></a>class mip::UserRoles 
ユーザーのグループおよびそれらに関連付けられているロール。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public userroles (const std:: vector\<std:: string\>& users, const std:: vector\<std:: string\>& roles)  |  [UserRoles](class_mip_userroles.md) コンストラクター。
public const std:: vector\<std:: string\>& Users () const  |  ロールのセットに関連付けられているユーザーを取得します。
public const std:: vector\<std:: string\>& Roles () const  |  ユーザーのグループに関連付けられているロールを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="userroles-function"></a>UserRoles 関数
[UserRoles](class_mip_userroles.md) コンストラクター。

パラメーター:  
* **ユーザー**:同じロールを共有するユーザーのグループ 


* **ロール**:ユーザーのグループによって共有されるロール


  
### <a name="users-function"></a>Users 関数
ロールのセットに関連付けられているユーザーを取得します。

  
次の**値を返し**ます。ロールのセットに関連付けられているユーザー
  
### <a name="roles-function"></a>Roles 関数
ユーザーのグループに関連付けられているロールを取得します。

  
次の**値を返し**ます。ユーザーのグループに関連付けられているロール