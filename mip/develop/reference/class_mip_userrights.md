---
title: class mip::UserRights
description: Mip::userrights クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 148b1b1a9f70cc87c3297c69e1e9ffa67af34cf4
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184248"
---
# <a name="class-mipuserrights"></a>class mip::UserRights 
ユーザーのグループおよびそれらに関連付けられている権限。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
パブリック UserRights (const std::vector\<std::string\>(& a) ユーザー、const std::vector\<std::string\>& rights)  |  [UserRights](class_mip_userrights.md) コンストラクター。
public const std::vector\<std::string\>& Users() const  |  権限のセットに関連付けられているユーザーを取得します。
public const std::vector\<std::string\>& Rights() const  |  ユーザーのグループに関連付けられている権限を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="userrights-function"></a>UserRights 関数
[UserRights](class_mip_userrights.md) コンストラクター。

パラメーター:  
* **ユーザー**:同じ権限を共有するユーザーのグループ 


* **rights**:ユーザーのグループによって共有されている権限


  
### <a name="users-function"></a>ユーザー関数
権限のセットに関連付けられているユーザーを取得します。

  
**返します**:権限のセットに関連付けられているユーザー
  
### <a name="rights-function"></a>Rights 関数
ユーザーのグループに関連付けられている権限を取得します。

  
**返します**:ユーザーのグループに関連付けられている権限