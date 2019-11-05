---
title: class mip::UserRights
description: 'Microsoft Information Protection (MIP) SDK の mip:: userrights クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 1df26089f37b1e89be8749aa1bc862f0d3a729ba
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73558390"
---
# <a name="class-mipuserrights"></a>class mip::UserRights 
ユーザーのグループおよびそれらに関連付けられている権限。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public UserRights (const std:: vector\<std:: string\>& users、const std:: vector\<std:: string\>& 権限)  |  UserRights コンストラクター。
public const std:: vector\<std:: string\>& Users () const  |  権限のセットに関連付けられているユーザーを取得します。
public const std:: vector\<std:: string\>& 権限 () const  |  ユーザーのグループに関連付けられている権限を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="userrights-function"></a>UserRights 関数
UserRights コンストラクター。

パラメーター:  
* **users**: 同じ権限を共有するユーザーのグループ 


* **rights**: ユーザーのグループによって共有されている権限


  
### <a name="users-function"></a>Users 関数
権限のセットに関連付けられているユーザーを取得します。

  
**戻り値**: 権限のセットに関連付けられているユーザー
  
### <a name="rights-function"></a>権限関数
ユーザーのグループに関連付けられている権限を取得します。

  
**戻り値**: ユーザーのグループに関連付けられている権限