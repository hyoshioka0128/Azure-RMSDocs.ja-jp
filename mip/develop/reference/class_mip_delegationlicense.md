---
title: DelegationLicense クラス
description: 'Microsoft Information Protection (MIP) SDK の delegationlicense:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: cfb719a68650b2159574dd6f8d92fb3d0c15a2c1
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98225071"
---
# <a name="class-delegationlicense"></a>DelegationLicense クラス 
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: vector \<uint8_t\>& GetSerializedDelegationJsonLicense ()  |  委任ライセンスを取得します。
public const std:: vector \<uint8_t\>& GetSerializedUserLicense (ProtectionHandler::P reLicenseFormat 形式)  |  要求された場合は、ユーザーライセンスを取得します。
public const std:: string& GetUser ()  |  このライセンスが作成されたユーザーを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getserializeddelegationjsonlicense-function"></a>GetSerializedDelegationJsonLicense 関数
委任ライセンスを取得します。

  
**戻り値**: シリアル化されたライセンスこのライセンスは、要求を行ったユーザーの id にバインドされます
  
### <a name="getserializeduserlicense-function"></a>GetSerializedUserLicense 関数
要求された場合は、ユーザーライセンスを取得します。

パラメーター:  
* **形式**: ライセンスの形式



  
は、要求された場合はシリアル化されたユーザーライセンスを **返し** ます。それ以外の場合は、このライセンスは要求内の委任されたユーザーにバインドされます
  
### <a name="getuser-function"></a>GetUser 関数
このライセンスが作成されたユーザーを取得します。

  
**戻り値**: ユーザー