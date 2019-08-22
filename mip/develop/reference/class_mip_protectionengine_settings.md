---
title: class mip::ProtectionEngine::Settings
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionengine クラスについて説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: d770f5a613ecf90d6d6d6406b3b017a2f1162993
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883432"
---
# <a name="class-mipprotectionenginesettings"></a>class mip::ProtectionEngine::Settings 
作成時および有効期間全体にわたって [ProtectionEngine](class_mip_protectionengine.md) によって使用される[設定](class_mip_protectionengine_settings.md)。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  新しいエンジンを作成するための [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) コンストラクター。
public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  既存のエンジンを読み込むための [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) コンストラクター。
public const std::string& GetEngineId() const  |  エンジン ID を取得します。
public void SetEngineId(const std::string& engineId)  |  エンジン ID を設定します。
public const Identity& GetIdentity() const  |  エンジンに関連付けられているユーザー [id](class_mip_identity.md)を取得します。
public void SetIdentity(const Identity& identity)  |  エンジンに関連付けられているユーザー [id](class_mip_identity.md)を設定します。
public const std::string& GetClientData() const  |  クライアントに指定されたカスタム データを取得します。
public void SetClientData(const std::string& clientData)  |  クライアントに指定されたカスタム データを設定します。
public const std::string& GetLocale() const  |  エンジン データが書き込まれるロケールを取得します。
public void setcustomsettings (const std:: vector\<std::p air\<std:: string, std:: string\>\>& 値)  |  テストや実験に使用する名前と値のペアを設定します。
public const std:: vector\<std::p air\<std:: string、std:: string\>\>& GetCustomSettings () const  |  テストや実験に使用する名前と値のペアを取得します。
public void SetSessionId(const std::string& sessionId)  |  ログ/テレメトリの相関関係に使用する、エンジンのセッション ID を設定します。
public const std::string& GetSessionId() const  |  エンジンのセッション ID を取得します。
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  必要に応じて、クラウド エンドポイントのベース URL を設定します。
public const std::string& GetCloudEndpointBaseUrl() const  |  すべてのサービス要求で使用されるクラウド ベースの URL を取得します (指定されている場合)。
  
## <a name="members"></a>メンバー
  
### <a name="settings-function"></a>Settings 関数
新しいエンジンを作成するための [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) コンストラクター。

パラメーター:  
* **id**:[Protectionengine](class_mip_protectionengine.md)に関連付けられる[id](class_mip_identity.md)


* **clientData**: アンロード時にエンジンと共に保存でき、読み込まれたエンジンから取得できる、カスタマイズ可能なクライアント データ。 


* **ロケール**:エンジンの出力はこのロケールで提供されます。


  
### <a name="settings-function"></a>Settings 関数
既存のエンジンを読み込むための [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) コンストラクター。

パラメーター:  
* **engineId**:読み込むエンジンの一意識別子 


* **clientData**: アンロード時にエンジンと共に保存でき、読み込まれたエンジンから取得できる、カスタマイズ可能なクライアント データ。 


* **ロケール**:エンジンの出力はこのロケールで提供されます。


  
### <a name="getengineid-function"></a>GetEngineId 関数
エンジン ID を取得します。

  
次の**値を返し**ます。エンジン ID
  
### <a name="setengineid-function"></a>SetEngineId 関数
エンジン ID を設定します。

パラメーター:  
* **engineId**: エンジン ID。


  
### <a name="getidentity-function"></a>GetIdentity 関数
エンジンに関連付けられているユーザー [id](class_mip_identity.md)を取得します。

  
次の**値を返し**ます。エンジンに関連付けられているユーザー [id](class_mip_identity.md)
  
### <a name="setidentity-function"></a>SetIdentity 関数
エンジンに関連付けられているユーザー [id](class_mip_identity.md)を設定します。

パラメーター:  
* **id**:エンジンに関連付けられているユーザー [id](class_mip_identity.md)


  
### <a name="getclientdata-function"></a>GetClientData 関数
クライアントに指定されたカスタム データを取得します。

  
次の**値を返し**ます。クライアントによって指定されたカスタムデータ
  
### <a name="setclientdata-function"></a>SetClientData 関数
クライアントに指定されたカスタム データを設定します。

パラメーター:  
* **Custom**: クライアントに指定されたデータ


  
### <a name="getlocale-function"></a>GetLocale 関数
エンジン データが書き込まれるロケールを取得します。

  
次の**値を返し**ます。エンジンデータが書き込まれるロケール
  
### <a name="setcustomsettings-function"></a>SetCustomSettings 関数
テストや実験に使用する名前と値のペアを設定します。

パラメーター:  
* **Customsettings**:テストと実験に使用される名前と値のペア


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
テストや実験に使用する名前と値のペアを取得します。

  
次の**値を返し**ます。テストと実験に使用される名前と値のペア
  
### <a name="setsessionid-function"></a>SetSessionId 関数
ログ/テレメトリの相関関係に使用する、エンジンのセッション ID を設定します。

パラメーター:  
* **sessionId**:ログ/テレメトリの関連付けに使用されるエンジンセッション ID


  
### <a name="getsessionid-function"></a>GetSessionId 関数
エンジンのセッション ID を取得します。

  
次の**値を返し**ます。エンジンセッション ID
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl 関数
必要に応じて、クラウド エンドポイントのベース URL を設定します。

パラメーター:  
* **cloudEndpointBaseUrl**: すべてのサービス要求で使用されるベース URL (たとえば、"https://api.aadrm.com")


ベース URL が指定されていない場合は、エンジン ID のドメインの DNS 参照によって決定されます。
  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl 関数
すべてのサービス要求で使用されるクラウド ベースの URL を取得します (指定されている場合)。

  
次の**値を返し**ます。[基本 URL]