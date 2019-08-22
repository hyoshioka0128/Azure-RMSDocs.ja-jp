---
title: class mip::UserRights
description: 'Microsoft Information Protection (MIP) SDK の mip:: userrights クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: c26c7d1aa31cf8fb2ea562582a2ebaad8417615d
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884986"
---
# <a name="class-mipuserrights"></a>class mip::UserRights 
ユーザーのグループおよびそれらに関連付けられている権限。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public userrights (const std:: vector\<std:: string\>& users, const std:: vector\<std:: string\>& 権限)  |  [UserRights](class_mip_userrights.md) コンストラクター。
public const std:: vector\<std:: string\>& Users () const  |  権限のセットに関連付けられているユーザーを取得します。
public const std:: vector\<std:: string\>& 権限 () const  |  ユーザーのグループに関連付けられている権限を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="userrights-function"></a>UserRights 関数
[UserRights](class_mip_userrights.md) コンストラクター。

パラメーター:  
* **ユーザー**:同じ権限を共有するユーザーのグループ 


* **権限**:ユーザーのグループによって共有される権限


  
### <a name="users-function"></a>Users 関数
権限のセットに関連付けられているユーザーを取得します。

  
次の**値を返し**ます。権限のセットに関連付けられているユーザー
  
### <a name="rights-function"></a>権限関数
ユーザーのグループに関連付けられている権限を取得します。

  
次の**値を返し**ます。ユーザーのグループに関連付けられている権限