---
title: class mip::ProtectionEngine::Settings
description: Mip::protectionengine クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 841eddc32e5e6928469dc11aba581defae09bc09
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184503"
---
# <a name="class-mipprotectionenginesettings"></a>class mip::ProtectionEngine::Settings 
作成時および有効期間全体にわたって [ProtectionEngine](class_mip_protectionengine.md) によって使用される[設定](class_mip_protectionengine_settings.md)。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  新しいエンジンを作成するための [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) コンストラクター。
public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  既存のエンジンを読み込むための [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) コンストラクター。
public const std::string& GetEngineId() const  |  エンジン ID を取得します。
public void SetEngineId(const std::string& engineId)  |  エンジン ID を設定します。
public const Identity& GetIdentity() const  |  ユーザーを取得します[Identity](class_mip_identity.md)エンジンに関連付けられています。
public void SetIdentity(const Identity& identity)  |  ユーザーを設定します[Identity](class_mip_identity.md)エンジンに関連付けられています。
public const std::string& GetClientData() const  |  クライアントに指定されたカスタム データを取得します。
public void SetClientData(const std::string& clientData)  |  クライアントに指定されたカスタム データを設定します。
public const std::string& GetLocale() const  |  エンジン データが書き込まれるロケールを取得します。
public void SetCustomSettings(const std::vector\<std::pair\<std::string, std::string\>\>& value)  |  テストや実験に使用する名前と値のペアを設定します。
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  テストや実験に使用する名前と値のペアを取得します。
public void SetSessionId(const std::string& sessionId)  |  ログ/テレメトリの相関関係に使用する、エンジンのセッション ID を設定します。
public const std::string& GetSessionId() const  |  エンジンのセッション ID を取得します。
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  必要に応じて、クラウド エンドポイントのベース URL を設定します。
public const std::string& GetCloudEndpointBaseUrl() const  |  すべてのサービス要求で使用されるクラウド ベースの URL を取得します (指定されている場合)。
  
## <a name="members"></a>メンバー
  
### <a name="settings-function"></a>ポリシーの設定
新しいエンジンを作成するための [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) コンストラクター。

パラメーター:  
* **identity**:[Identity](class_mip_identity.md)を関連付けられる[ProtectionEngine](class_mip_protectionengine.md)


* **clientData**: アンロード時にエンジンと共に保存でき、読み込まれたエンジンから取得できる、カスタマイズ可能なクライアント データ。 


* **ロケール**:エンジンの出力は、このロケールで提供されます。


  
### <a name="settings-function"></a>ポリシーの設定
既存のエンジンを読み込むための [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) コンストラクター。

パラメーター:  
* **engineId**:読み込まれるエンジンの一意識別子 


* **clientData**: アンロード時にエンジンと共に保存でき、読み込まれたエンジンから取得できる、カスタマイズ可能なクライアント データ。 


* **ロケール**:エンジンの出力は、このロケールで提供されます。


  
### <a name="getengineid-function"></a>GetEngineId 関数
エンジン ID を取得します。

  
**返します**:エンジン ID
  
### <a name="setengineid-function"></a>SetEngineId 関数
エンジン ID を設定します。

パラメーター:  
* **engineId**: エンジン ID。


  
### <a name="getidentity-function"></a>GetIdentity 関数
ユーザーを取得します[Identity](class_mip_identity.md)エンジンに関連付けられています。

  
**返します**:ユーザー [Identity](class_mip_identity.md)エンジンに関連付けられています。
  
### <a name="setidentity-function"></a>SetIdentity 関数
ユーザーを設定します[Identity](class_mip_identity.md)エンジンに関連付けられています。

パラメーター:  
* **identity**:ユーザー [Identity](class_mip_identity.md)エンジンに関連付けられています。


  
### <a name="getclientdata-function"></a>GetClientData 関数
クライアントに指定されたカスタム データを取得します。

  
**返します**:クライアントで指定されたカスタム データ
  
### <a name="setclientdata-function"></a>SetClientData 関数
クライアントに指定されたカスタム データを設定します。

パラメーター:  
* **Custom**: クライアントに指定されたデータ


  
### <a name="getlocale-function"></a>GetLocale 関数
エンジン データが書き込まれるロケールを取得します。

  
**返します**:ロケール データが書き込まれるエンジン
  
### <a name="setcustomsettings-function"></a>SetCustomSettings 関数
テストや実験に使用する名前と値のペアを設定します。

パラメーター:  
* **customsettings:**:名前/値ペアのテストや実験に使用


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
テストや実験に使用する名前と値のペアを取得します。

  
**返します**:名前/値ペアのテストや実験に使用
  
### <a name="setsessionid-function"></a>SetSessionId 関数
ログ/テレメトリの相関関係に使用する、エンジンのセッション ID を設定します。

パラメーター:  
* **sessionId**:ログ/テレメトリの関連付けに使用される、エンジンのセッション ID


  
### <a name="getsessionid-function"></a>GetSessionId 関数
エンジンのセッション ID を取得します。

  
**返します**:エンジンのセッション ID
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl 関数
必要に応じて、クラウド エンドポイントのベース URL を設定します。

パラメーター:  
* **cloudEndpointBaseUrl**: すべてのサービス要求で使用されるベース URL (たとえば、"https://api.aadrm.com")


ベース URL が指定されていない場合は、エンジン ID のドメインの DNS 参照によって決定されます。
  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl function
すべてのサービス要求で使用されるクラウド ベースの URL を取得します (指定されている場合)。

  
**返します**:ベース URL