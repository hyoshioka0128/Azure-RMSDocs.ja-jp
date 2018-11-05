---
title: class mip PolicyEngine Settings
description: class mip PolicyEngine Settings のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 6ac94d1e34615a0248dac85f28c55154b127574f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446347"
---
# <a name="class-mippolicyenginesettings"></a>class mip::PolicyEngine::Settings 
[PolicyEngine](class_mip_policyengine.md) に関連付けられている設定を定義します。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  既存のエンジンを読み込むための [PolicyEngine::Settings](class_mip_policyengine_settings.md) コンストラクター。
 public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  新しいエンジンを作成するための [PolicyEngine::Settings](class_mip_policyengine_settings.md) コンストラクター。
 public const std::string& GetEngineId() const  |  エンジン ID を取得します。
 public void SetEngineId(const std::string& id)  |  エンジン ID を設定します。
 public const Identity& GetIdentity() const  |  ID オブジェクトを取得します。
 public void SetIdentity(const Identity& identity)  |  ID オブジェクトを設定します。
 public const std::string& GetClientData() const  |  設定で設定されたクライアント データを取得します。
 public void SetClientData(const std::string& clientData)  |  クライアント データ文字列を設定します。
 public const std::string& GetLocale() const  |  設定で設定されたロケールを取得します。
public void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& customSettings)  |  機能のゲーティングとテストに使用するカスタム設定を設定します。
public const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  機能のゲーティングとテストに使用するカスタム設定を取得します。
 public void SetSessionId(const std::string& sessionId)  |  クライアントによって定義されたテレメトリに使用するセッション ID を設定します。
 public const std::string& GetSessionId() const  |  セッション ID、一意識別子を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
既存のエンジンを読み込むための [PolicyEngine::Settings](class_mip_policyengine_settings.md) コンストラクター。

パラメーター:  
* **engineId**: AddEngineAsync によって生成されたか、または自分で生成した一意のエンジン ID に設定します。 既存のエンジンを読み込む場合は ID を再利用し、それ以外の場合は新しいエンジンが作成されます。 


* **clientData**: アンロード時にエンジンと共に格納でき、読み込まれたエンジンから取得できるカスタマイズ可能なクライアント データ。 


* **locale**: エンジンのローカライズ可能な出力はこのロケールで提供されます。


  
### <a name="settings"></a>Settings
新しいエンジンを作成するための [PolicyEngine::Settings](class_mip_policyengine_settings.md) コンストラクター。

パラメーター:  
* **identity**: 新しいエンジンに関連付けられているユーザーの ID 情報。 


* **clientData**: アンロード時にエンジンと共に格納でき、読み込まれたエンジンから取得できるカスタマイズ可能なクライアント データ。 


* **locale**: エンジンのローカライズ可能な出力はこのロケールで提供されます。


  
### <a name="getengineid"></a>GetEngineId
エンジン ID を取得します。

  
**戻り値**: エンジンを識別する一意の文字列。
  
### <a name="setengineid"></a>SetEngineId
エンジン ID を設定します。

パラメーター:  
* **id**: エンジン ID。


  
### <a name="getidentity"></a>GetIdentity
ID オブジェクトを取得します。

  
**戻り値**: 設定オブジェクト内の ID への参照。 
  
**関連項目**: mip::Identity
  
### <a name="setidentity"></a>SetIdentity
ID オブジェクトを設定します。

パラメーター:  
* **identity**: ユーザーの一意の ID。 


  
**関連項目**: mip::Identity
  
### <a name="getclientdata"></a>GetClientData
設定で設定されたクライアント データを取得します。

  
**戻り値**: クライアントで指定されたデータの文字列。
  
### <a name="setclientdata"></a>SetClientData
クライアント データ文字列を設定します。

パラメーター:  
* **clientData**: ユーザーが指定したデータ。


  
### <a name="getlocale"></a>GetLocale
設定で設定されたロケールを取得します。

  
**戻り値**: ロケール。
  
### <a name="setcustomsettings"></a>SetCustomSettings
機能のゲーティングとテストに使用するカスタム設定を設定します。

パラメーター:  
* **customSettings**: 名前と値のペアの一覧。


  
### <a name="getcustomsettings"></a>GetCustomSettings
機能のゲーティングとテストに使用するカスタム設定を取得します。

  
**戻り値**: 名前と値のペアのリスト。
  
### <a name="setsessionid"></a>SetSessionId
クライアントによって定義されたテレメトリに使用するセッション ID を設定します。

パラメーター:  
* **sessionId**: テレメトリ イベントを接続する一意の文字列。


  
### <a name="getsessionid"></a>GetSessionId
セッション ID、一意識別子を取得します。

  
**戻り値**: セッション ID。