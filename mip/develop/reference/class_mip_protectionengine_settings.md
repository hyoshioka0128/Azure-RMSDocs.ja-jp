---
title: class mip::ProtectionEngine::Settings
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionengine クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 746309afc21637c85ec53dd9af7214151c5bb75a
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73557679"
---
# <a name="class-mipprotectionenginesettings"></a>class mip::ProtectionEngine::Settings 
作成時および有効期間全体にわたって ProtectionEngine によって使用される設定。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  新しいエンジンを作成するための ProtectionEngine:: Settings コンストラクター。
public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  既存のエンジンを読み込むための ProtectionEngine:: Settings コンストラクター。
public const std::string& GetEngineId() const  |  エンジン ID を取得します。
public void SetEngineId(const std::string& engineId)  |  エンジン ID を設定します。
public const Identity& GetIdentity() const  |  エンジンに関連付けられたユーザー ID を取得します。
public void SetIdentity(const Identity& identity)  |  エンジンに関連付けられるユーザー ID を設定します。
public const std::string& GetClientData() const  |  クライアントに指定されたカスタム データを取得します。
public void SetClientData(const std::string& clientData)  |  クライアントに指定されたカスタム データを設定します。
public const std::string& GetLocale() const  |  エンジン データが書き込まれるロケールを取得します。
public void SetCustomSettings (const std:: vector\<std::p air\<std:: string、std:: string\>\>& value)  |  テストや実験に使用する名前と値のペアを設定します。
public const std:: vector\<std::p air\<std:: string、std:: string\>\>& GetCustomSettings () const  |  テストや実験に使用する名前と値のペアを取得します。
public void SetSessionId(const std::string& sessionId)  |  ログ/テレメトリの相関関係に使用する、エンジンのセッション ID を設定します。
public const std::string& GetSessionId() const  |  エンジンのセッション ID を取得します。
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  必要に応じて、クラウド エンドポイントのベース URL を設定します。
public const std::string& GetCloudEndpointBaseUrl() const  |  すべてのサービス要求で使用されるクラウド ベースの URL を取得します (指定されている場合)。
  
## <a name="members"></a>メンバー
  
### <a name="settings-function"></a>Settings 関数
新しいエンジンを作成するための ProtectionEngine:: Settings コンストラクター。

パラメーター:  
* **id**: protectionengine に関連付けられる id


* **clientData**: アンロード時にエンジンと共に保存でき、読み込まれたエンジンから取得できる、カスタマイズ可能なクライアント データ。 


* **locale**: エンジン出力はこのロケールで提供されます。


  
### <a name="settings-function"></a>Settings 関数
既存のエンジンを読み込むための ProtectionEngine:: Settings コンストラクター。

パラメーター:  
* **engineId**: 読み込まれるエンジンの一意識別子 


* **clientData**: アンロード時にエンジンと共に保存でき、読み込まれたエンジンから取得できる、カスタマイズ可能なクライアント データ。 


* **locale**: エンジン出力はこのロケールで提供されます。


  
### <a name="getengineid-function"></a>GetEngineId 関数
エンジン ID を取得します。

  
**戻り値**: エンジン ID
  
### <a name="setengineid-function"></a>SetEngineId 関数
エンジン ID を設定します。

パラメーター:  
* **engineId**: エンジン ID。


  
### <a name="getidentity-function"></a>GetIdentity 関数
エンジンに関連付けられたユーザー ID を取得します。

  
**戻り値**: エンジンに関連付けられたユーザー ID
  
### <a name="setidentity-function"></a>SetIdentity 関数
エンジンに関連付けられるユーザー ID を設定します。

パラメーター:  
* **identity**: エンジンに関連付けられるユーザー ID


  
### <a name="getclientdata-function"></a>GetClientData 関数
クライアントに指定されたカスタム データを取得します。

  
**戻り値** クライアントに指定されたカスタム データ
  
### <a name="setclientdata-function"></a>SetClientData 関数
クライアントに指定されたカスタム データを設定します。

パラメーター:  
* **Custom**: クライアントに指定されたデータ


  
### <a name="getlocale-function"></a>GetLocale 関数
エンジン データが書き込まれるロケールを取得します。

  
**戻り値**: エンジン データが書き込まれるロケール
  
### <a name="setcustomsettings-function"></a>SetCustomSettings 関数
テストや実験に使用する名前と値のペアを設定します。

パラメーター:  
* **customSettings**: テストや実験に使用する名前と値のペア


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
テストや実験に使用する名前と値のペアを取得します。

  
**戻り値**: テストや実験に使用する名前と値のペア
  
### <a name="setsessionid-function"></a>SetSessionId 関数
ログ/テレメトリの相関関係に使用する、エンジンのセッション ID を設定します。

パラメーター:  
* **sessionId**: ログ/テレメトリの相関関係に使用する、エンジンのセッション ID


  
### <a name="getsessionid-function"></a>GetSessionId 関数
エンジンのセッション ID を取得します。

  
**戻り値**: エンジンのセッション ID
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl 関数
必要に応じて、クラウド エンドポイントのベース URL を設定します。

パラメーター:  
* **cloudEndpointBaseUrl**: すべてのサービス要求で使用されるベース URL (たとえば、"https://api.aadrm.com")


ベース URL が指定されていない場合は、エンジン ID のドメインの DNS 参照によって決定されます。
  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl 関数
すべてのサービス要求で使用されるクラウド ベースの URL を取得します (指定されている場合)。

  
**戻り値**: ベース URL