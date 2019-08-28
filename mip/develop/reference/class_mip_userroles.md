---
title: class mip::UserRoles
description: 'Microsoft Information Protection (MIP) SDK の mip:: userroles クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: cda40d4b3a118ff065dc2e3899b39cf8f405dd68
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056702"
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