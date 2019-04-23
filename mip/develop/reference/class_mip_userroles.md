---
title: class mip::UserRoles
description: Mip::userroles クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 7e9e750f5b327dbad5e9b46fa1eca2a3291abdd3
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "60173245"
---
# <a name="class-mipuserroles"></a>class mip::UserRoles 
ユーザーのグループおよびそれらに関連付けられているロール。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
パブリック UserRoles (const std::vector\<std::string\>(& a) ユーザー、const std::vector\<std::string\>(& a) の役割)  |  [UserRoles](class_mip_userroles.md) コンストラクター。
public const std::vector\<std::string\>& Users() const  |  ロールのセットに関連付けられているユーザーを取得します。
public const std::vector\<std::string\>& Roles() const  |  ユーザーのグループに関連付けられているロールを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="userroles-function"></a>UserRoles 関数
[UserRoles](class_mip_userroles.md) コンストラクター。

パラメーター:  
* **ユーザー**:同じロールを共有するユーザーのグループ 


* **ロール**:ユーザーのグループによって共有の役割


  
### <a name="users-function"></a>ユーザー関数
ロールのセットに関連付けられているユーザーを取得します。

  
**返します**:ロールのセットに関連付けられているユーザー
  
### <a name="roles-function"></a>ロール関数
ユーザーのグループに関連付けられているロールを取得します。

  
**返します**:ユーザーのグループに関連付けられているロール