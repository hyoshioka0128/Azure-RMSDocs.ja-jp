---
title: 'クラス ProtectionHandler:: ConsumptionSettings'
description: 'Microsoft Information Protection (MIP) SDK の protectionhandler:: consumptionsettings クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 8ac0e4d3067528d6e860244abca2d70f0cf6a530
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214594"
---
# <a name="class-protectionhandlerconsumptionsettings"></a>クラス ProtectionHandler:: ConsumptionSettings 
既存のコンテンツを使用する ProtectionHandler を作成するために使用される設定。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public ConsumptionSettings (const std:: vector \<uint8_t\>& serializedPublishingLicense)  |  新しいハンドラーを作成するための ProtectionHandler:: ConsumptionSettings コンストラクター。
public ConsumptionSettings (const std:: vector \<uint8_t\>& serializedPreLicense、const std:: vector \<uint8_t\>& serializedPublishingLicense)  |  新しいハンドラーを作成するための ProtectionHandler:: ConsumptionSettings コンストラクター。
public ConsumptionSettings (const std:: shared_ptr \<PublishingLicenseInfo\>& licenseinfo)  |  新しいハンドラーを作成するための ProtectionHandler:: ConsumptionSettings コンストラクター。
public std:: shared_ptr \<PublishingLicenseInfo\> get発行 licenseinfo () const  |  保護されたコンテンツに関連付けられている公開ライセンスを取得します。
public bool GetIsOfflineOnly () const  |  ProtectionHandler の作成でオンライン HTTP 操作が許可されているかどうかを取得します。
public void SetIsOfflineOnly (bool isOfflineOnly)  |  ProtectionHandler の作成でオンライン HTTP 操作が許可されるかどうかを設定します。
public void SetDelegatedUserEmail (const std:: string& delegatedUserEmail)  |  委任されたユーザーを設定します。
public void SetContentName (const std:: string& contentName)  | _まだ文書化されていません。_
public const std:: string& GetDelegatedUserEmail () const  |  委任されたユーザーを取得します。
public const std:: string& GetContentName () const  | _まだ文書化されていません。_
  
## <a name="members"></a>メンバー
  
### <a name="consumptionsettings-function"></a>ConsumptionSettings 関数
新しいハンドラーを作成するための ProtectionHandler:: ConsumptionSettings コンストラクター。

パラメーター:  
* **serializedPublishingLicense**: 保護されたコンテンツからのシリアル化された公開ライセンス


  
### <a name="consumptionsettings-function"></a>ConsumptionSettings 関数
新しいハンドラーを作成するための ProtectionHandler:: ConsumptionSettings コンストラクター。

パラメーター:  
* **serializedPreLicense**: シリアル化されたプレライセンスをコンテンツに添付します。 


* **serializedPublishingLicense**: 保護されたコンテンツからのシリアル化された公開ライセンス


  
### <a name="consumptionsettings-function"></a>ConsumptionSettings 関数
新しいハンドラーを作成するための ProtectionHandler:: ConsumptionSettings コンストラクター。

パラメーター:  
* **licenseinfo**: 保護されたコンテンツからライセンス情報を公開しています


(シリアル化された未処理の発行ライセンスだけではなく) 発行 Licenseinfo を指定すると、公開ライセンスを解析するための MIP SDK が不要になります。
  
### <a name="getpublishinglicenseinfo-function"></a>Get発行 Licenseinfo 関数
保護されたコンテンツに関連付けられている公開ライセンスを取得します。

  
**返品**: ライセンス情報の発行
  
### <a name="getisofflineonly-function"></a>GetIsOfflineOnly 関数
ProtectionHandler の作成でオンライン HTTP 操作が許可されているかどうかを取得します。

  
は、HTTP 操作が許可されていない場合は true を **返し** ます。それ以外の場合は false に設定されている場合は、コンテンツが既に暗号化解除され、その unexpired ライセンスがキャッシュされている場合にのみ、protectionhandler の作成が成功します。 キャッシュされたコンテンツが見つからない場合は、mip:: NetworkError がスローされます。
  
### <a name="setisofflineonly-function"></a>SetIsOfflineOnly 関数
ProtectionHandler の作成でオンライン HTTP 操作が許可されるかどうかを設定します。

パラメーター:  
* **Isofflineonly**: HTTP 操作が許可されていない場合は True、それ以外の場合は false


これが true に設定されている場合、コンテンツが既に復号化されていて、その unexpired ライセンスがキャッシュされている場合にのみ、ProtectionHandler の作成が成功します。 キャッシュされたコンテンツが見つからない場合は、mip:: NetworkError がスローされます。
  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail 関数
委任されたユーザーを設定します。

パラメーター:  
* **delegatedUserEmail**: 委任の電子メール。


委任されたユーザーは、他のユーザーの代理として認証を行うユーザーまたはアプリケーションが動作するときに指定します。
  
### <a name="setcontentname-function"></a>SetContentName 関数
_まだ文書化されていません。_

  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail 関数
委任されたユーザーを取得します。

  
**戻り値**: 委任されたユーザー: 認証を行っているユーザーまたはアプリケーションが別のユーザーの代理で動作しているときに、委任されたユーザーを指定します。
  
### <a name="getcontentname-function"></a>GetContentName 関数
_まだ文書化されていません。_
