---
title: class mip::PolicyEngine::Settings
description: Mip::policyengine クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 6ad384768ef876109a6a43237765474345a666bc
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2019
ms.locfileid: "56257537"
---
# <a name="class-mippolicyenginesettings"></a>class mip::PolicyEngine::Settings 
[PolicyEngine](class_mip_policyengine.md) に関連付けられている設定を定義します。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale, bool loadSensitivityTypes)  |  既存のエンジンを読み込むための [PolicyEngine::Settings](class_mip_policyengine_settings.md) コンストラクター。
public Settings(const Identity& identity, const std::string& clientData, const std::string& locale, bool loadSensitivityTypes)  |  新しいエンジンを作成するための [PolicyEngine::Settings](class_mip_policyengine_settings.md) コンストラクター。
public const std::string& GetEngineId() const  |  エンジン ID を取得します。
public void SetEngineId(const std::string& id)  |  エンジン ID を設定します。
public const Identity& GetIdentity() const  |  取得、 [Identity](class_mip_identity.md)オブジェクト。
public void SetIdentity(const Identity& identity)  |  設定、 [Identity](class_mip_identity.md)オブジェクト。
public const std::string& GetClientData() const  |  設定で設定されたクライアント データを取得します。
public void SetClientData(const std::string& clientData)  |  クライアント データ文字列を設定します。
public const std::string& GetLocale() const  |  設定で設定されたロケールを取得します。
public void SetCustomSettings (const std::vector\<std::pair\<std::string, std::string\>\>& customsettings:)  |  機能のゲーティングとテストに使用するカスタム設定を設定します。
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  機能のゲーティングとテストに使用するカスタム設定を取得します。
public void SetSessionId(const std::string& sessionId)  |  クライアントによって定義されたテレメトリに使用するセッション ID を設定します。
public const std::string& GetSessionId() const  |  セッション ID、一意識別子を取得します。
public bool IsLoadSensitivityTypesEnabled() const  |  取得、負荷の機密ラベルが有効になっているかどうかを示すフラグ。
  
## <a name="members"></a>メンバー
  
### <a name="settings-function"></a>ポリシーの設定
既存のエンジンを読み込むための [PolicyEngine::Settings](class_mip_policyengine_settings.md) コンストラクター。

パラメーター:  
* **engineId**:AddEngineAsync または生成された自己によって生成された一意のエンジン ID に設定します。 既存のエンジンを読み込む場合は ID を再利用し、それ以外の場合は新しいエンジンが作成されます。 


* **clientData**: アンロード時にエンジンと共に格納でき、読み込まれたエンジンから取得できるカスタマイズ可能なクライアント データ。 


* **locale**: エンジンのローカライズ可能な出力はこのロケールで提供されます。 


* **省略可能な**: エンジンが読み込まれたときを示すフラグを読み込む必要がありますもカスタムの機密の種類の更新情報をカスタムの機密の種類とポリシーの変更をプロファイルには true。 OnPolicyChange オブザーバーが呼び出される場合。 false ListSensitivityTypes を呼び出す場合は空のリストを常に返します。


  
### <a name="settings-function"></a>ポリシーの設定
新しいエンジンを作成するための [PolicyEngine::Settings](class_mip_policyengine_settings.md) コンストラクター。

パラメーター:  
* **identity**:[Identity](class_mip_identity.md)新しいエンジンに関連付けられているユーザーの情報。 


* **clientData**: アンロード時にエンジンと共に格納でき、読み込まれたエンジンから取得できるカスタマイズ可能なクライアント データ。 


* **locale**: エンジンのローカライズ可能な出力はこのロケールで提供されます。 


* **省略可能な**: エンジンが読み込まれたときを示すフラグを読み込む必要がありますもカスタムの機密の種類の更新情報をカスタムの機密の種類とポリシーの変更をプロファイルには true。 OnPolicyChange オブザーバーが呼び出される場合。 false ListSensitivityTypes を呼び出す場合は空のリストを常に返します。


  
### <a name="getengineid-function"></a>GetEngineId 関数
エンジン ID を取得します。

  
**返します**:エンジンを識別する一意の文字列。
  
### <a name="setengineid-function"></a>SetEngineId 関数
エンジン ID を設定します。

パラメーター:  
* **id**: エンジン ID。


  
### <a name="getidentity-function"></a>GetIdentity 関数
取得、 [Identity](class_mip_identity.md)オブジェクト。

  
**返します**:設定オブジェクト内の id への参照。 
  
**参照してください**: [:identity](class_mip_identity.md)
  
### <a name="setidentity-function"></a>SetIdentity 関数
設定、 [Identity](class_mip_identity.md)オブジェクト。

パラメーター:  
* **identity**: ユーザーの一意の ID。 


  
**参照してください**: [:identity](class_mip_identity.md)
  
### <a name="getclientdata-function"></a>GetClientData 関数
設定で設定されたクライアント データを取得します。

  
**返します**:クライアントによって指定されたデータの文字列。
  
### <a name="setclientdata-function"></a>SetClientData 関数
クライアント データ文字列を設定します。

パラメーター:  
* **clientData**: ユーザーが指定したデータ。


  
### <a name="getlocale-function"></a>GetLocale 関数
設定で設定されたロケールを取得します。

  
**返します**:ロケール。
  
### <a name="setcustomsettings-function"></a>SetCustomSettings 関数
機能のゲーティングとテストに使用するカスタム設定を設定します。

パラメーター:  
* **customsettings:**:名前と値のペアの一覧。


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
機能のゲーティングとテストに使用するカスタム設定を取得します。

  
**返します**:名前と値のペアの一覧。
  
### <a name="setsessionid-function"></a>SetSessionId 関数
クライアントによって定義されたテレメトリに使用するセッション ID を設定します。

パラメーター:  
* **sessionId**: テレメトリ イベントを接続する一意の文字列。


  
### <a name="getsessionid-function"></a>GetSessionId 関数
セッション ID、一意識別子を取得します。

  
**返します**:セッション id。
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled 関数
取得、負荷の機密ラベルが有効になっているかどうかを示すフラグ。

  
**返します**:他の false を有効になっている場合は true。
