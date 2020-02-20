---
title: class mip::UserRights
description: 'Microsoft Information Protection (MIP) SDK の mip:: userrights クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: f44ff30c890a5a8ab3dbce2426a6c1898df1f0e5
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489301"
---
# <a name="class-mipuserrights"></a>class mip::UserRights 
ユーザーのグループおよびそれらに関連付けられている権限。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
public UserRights (const std:: vector\<std:: string\>& users、const std:: vector\<std:: string\>& 権限)  |  UserRights コンストラクター。
public const std:: vector\<std:: string\>& Users () const  |  権限のセットに関連付けられているユーザーを取得します。
public const std:: vector\<std:: string\>& 権限 () const  |  ユーザーのグループに関連付けられている権限を取得します。
  
## <a name="members"></a>Members
  
### <a name="userrights-function"></a>UserRights 関数
UserRights コンストラクター。

パラメータ:  
* **users**: 同じ権限を共有するユーザーのグループ 


* **rights**: ユーザーのグループによって共有されている権限


  
### <a name="users-function"></a>Users 関数
権限のセットに関連付けられているユーザーを取得します。

  
**戻り値**: 権限のセットに関連付けられているユーザー
  
### <a name="rights-function"></a>権限関数
ユーザーのグループに関連付けられている権限を取得します。

  
**戻り値**: ユーザーのグループに関連付けられている権限