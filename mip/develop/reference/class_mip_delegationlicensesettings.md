---
title: DelegationLicenseSettings クラス
description: 'Microsoft Information Protection (MIP) SDK の delegationlicensesettings:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 947accd8104f8eda9f7b7320a1fbdb956810f34d
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98224987"
---
# <a name="class-delegationlicensesettings"></a>DelegationLicenseSettings クラス 
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std:: shared_ptr \<const PublishingLicenseInfo\> getlicenseinfo () const  |  発行ライセンスを取得します。
public const std:: vector \<std::string\>& getusers () const  |  要求のユーザーの一覧を取得します。
public bool GetAquireEndUserLicenses () const  |  デリゲートライセンスに加えてエンドユーザーライセンスを取得するかどうかを示すブール値を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getlicenseinfo-function"></a>GetLicenseInfo 関数
発行ライセンスを取得します。

  
**戻り値**: 発行 licenseinfo
  
### <a name="getusers-function"></a>GetUsers 関数
要求のユーザーの一覧を取得します。

  
**戻り値**: ユーザー
  
### <a name="getaquireenduserlicenses-function"></a>GetAquireEndUserLicenses 関数
デリゲートライセンスに加えてエンドユーザーライセンスを取得するかどうかを示すブール値を取得します。

  
**戻り値**: エンドユーザーライセンスを取得するかどうか