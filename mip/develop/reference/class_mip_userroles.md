---
title: class mip UserRoles
description: class mip UserRoles のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 1cc1da6f443fa22095f216bb2ec2f0e51e75bf78
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445259"
---
# <a name="class-mipuserroles"></a>class mip::UserRoles 
ユーザーのグループおよびそれらに関連付けられているロール。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public UserRoles(const std::vector<std::string>& users, const std::vector<std::string>& roles)  |  [UserRoles](class_mip_userroles.md) コンストラクター。
public const std::vector<std::string>& Users() const  |  ロールのセットに関連付けられているユーザーを取得します。
public const std::vector<std::string>& Roles() const  |  ユーザーのグループに関連付けられているロールを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="userroles"></a>UserRoles
[UserRoles](class_mip_userroles.md) コンストラクター。

パラメーター:  
* **users**: 同じロールを共有するユーザーのグループ 


* **roles**: ユーザーのグループによって共有されているロール


  
### <a name="users"></a>Users
ロールのセットに関連付けられているユーザーを取得します。

  
**戻り値**: ロールのセットに関連付けられているユーザー
  
### <a name="roles"></a>役割
ユーザーのグループに関連付けられているロールを取得します。

  
**戻り値**: ユーザーのグループに関連付けられているロール