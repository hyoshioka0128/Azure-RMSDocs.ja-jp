---
title: class mip::PolicyEngine::Settings
description: Microsoft Information Protection (MIP) SDK の mip::p olicyengine クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: db96d00d268158b072d2052a5e98f39bf0efa425
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054313"
---
# <a name="class-mippolicyenginesettings"></a>class mip::PolicyEngine::Settings 
[PolicyEngine](class_mip_policyengine.md) に関連付けられている設定を定義します。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック設定 (const std:: string & engineId、const std:: string & clientData、const std:: string & locale、bool loadSensitivityTypes)  |  既存のエンジンを読み込むための [PolicyEngine::Settings](class_mip_policyengine_settings.md) コンストラクター。
パブリック設定 (定数 Id & id、const std:: string & clientData、const std:: string & locale、bool loadSensitivityTypes)  |  新しいエンジンを作成するための [PolicyEngine::Settings](class_mip_policyengine_settings.md) コンストラクター。
public const std::string& GetEngineId() const  |  エンジン ID を取得します。
public void SetEngineId(const std::string& id)  |  エンジン ID を設定します。
public const Identity& GetIdentity() const  |  [Id](class_mip_identity.md)オブジェクトを取得します。
public void SetIdentity(const Identity& identity)  |  [Id](class_mip_identity.md)オブジェクトを設定します。
public const std::string& GetClientData() const  |  設定で設定されたクライアント データを取得します。
public void SetClientData(const std::string& clientData)  |  クライアント データ文字列を設定します。
public const std::string& GetLocale() const  |  設定で設定されたロケールを取得します。
public void setcustomsettings (const std:: vector\<std::p air\<std:: string, std:: string\>\>& customsettings)  |  機能のゲーティングとテストに使用するカスタム設定を設定します。
public const std:: vector\<std::p air\<std:: string、std:: string\>\>& GetCustomSettings () const  |  機能のゲーティングとテストに使用するカスタム設定を取得します。
public void SetSessionId(const std::string& sessionId)  |  クライアントによって定義されたテレメトリに使用するセッション ID を設定します。
public const std::string& GetSessionId() const  |  セッション ID、一意識別子を取得します。
public bool IsLoadSensitivityTypesEnabled() const  |  読み込み感度ラベルが有効かどうかを示すフラグを取得します。
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  必要に応じて、クラウド エンドポイントのベース URL を設定します。
public const std::string& GetCloudEndpointBaseUrl() const  |  すべてのサービス要求で使用されるクラウド ベースの URL を取得します (指定されている場合)。
public void SetDelegatedUserEmail (const std:: string & delegatedUserEmail)  |  委任されたユーザーを設定します。
public const std:: string & GetDelegatedUserEmail () const  |  委任されたユーザーを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="settings-function"></a>Settings 関数
既存のエンジンを読み込むための [PolicyEngine::Settings](class_mip_policyengine_settings.md) コンストラクター。

パラメーター:  
* **engineId**:AddEngineAsync または自己生成された一意のエンジン ID に設定します。 既存のエンジンを読み込む場合は ID を再利用し、それ以外の場合は新しいエンジンが作成されます。 


* **clientData**: アンロード時にエンジンと共に格納でき、読み込まれたエンジンから取得できるカスタマイズ可能なクライアント データ。 


* **locale**: エンジンのローカライズ可能な出力はこのロケールで提供されます。 


* **省略可能**: エンジンが読み込まれるときに、カスタム感度の種類も読み込む必要があることを示すフラグです。 true の場合、カスタム感度の種類の更新とポリシーの変更に対して、プロファイルに対して true が呼び出されます。 false の場合、ListSensitivityTypes call は常に空のリストを返します。


  
### <a name="settings-function"></a>Settings 関数
新しいエンジンを作成するための [PolicyEngine::Settings](class_mip_policyengine_settings.md) コンストラクター。

パラメーター:  
* **id**:新しいエンジンに関連付けられているユーザーの[id](class_mip_identity.md)情報。 


* **clientData**: アンロード時にエンジンと共に格納でき、読み込まれたエンジンから取得できるカスタマイズ可能なクライアント データ。 


* **locale**: エンジンのローカライズ可能な出力はこのロケールで提供されます。 


* **省略可能**: エンジンが読み込まれるときに、カスタム感度の種類も読み込む必要があることを示すフラグです。 true の場合、カスタム感度の種類の更新とポリシーの変更に対して、プロファイルに対して true が呼び出されます。 false の場合、ListSensitivityTypes call は常に空のリストを返します。


  
### <a name="getengineid-function"></a>GetEngineId 関数
エンジン ID を取得します。

  
次の**値を返し**ます。エンジンを識別する一意の文字列。
  
### <a name="setengineid-function"></a>SetEngineId 関数
エンジン ID を設定します。

パラメーター:  
* **id**: エンジン ID。


  
### <a name="getidentity-function"></a>GetIdentity 関数
[Id](class_mip_identity.md)オブジェクトを取得します。

  
次の**値を返し**ます。設定オブジェクト内の id への参照。 
  
**関連**項目: [Mip:: Identity](class_mip_identity.md)
  
### <a name="setidentity-function"></a>SetIdentity 関数
[Id](class_mip_identity.md)オブジェクトを設定します。

パラメーター:  
* **identity**: ユーザーの一意の ID。 


  
**関連**項目: [Mip:: Identity](class_mip_identity.md)
  
### <a name="getclientdata-function"></a>GetClientData 関数
設定で設定されたクライアント データを取得します。

  
次の**値を返し**ます。クライアントによって指定されたデータの文字列。
  
### <a name="setclientdata-function"></a>SetClientData 関数
クライアント データ文字列を設定します。

パラメーター:  
* **clientData**: ユーザーが指定したデータ。


  
### <a name="getlocale-function"></a>GetLocale 関数
設定で設定されたロケールを取得します。

  
次の**値を返し**ます。ロケール。
  
### <a name="setcustomsettings-function"></a>SetCustomSettings 関数
機能のゲーティングとテストに使用するカスタム設定を設定します。

パラメーター:  
* **Customsettings**:名前と値のペアの一覧。


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
機能のゲーティングとテストに使用するカスタム設定を取得します。

  
次の**値を返し**ます。名前と値のペアの一覧。
  
### <a name="setsessionid-function"></a>SetSessionId 関数
クライアントによって定義されたテレメトリに使用するセッション ID を設定します。

パラメーター:  
* **sessionId**: テレメトリ イベントを接続する一意の文字列。


  
### <a name="getsessionid-function"></a>GetSessionId 関数
セッション ID、一意識別子を取得します。

  
次の**値を返し**ます。セッション ID。
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled 関数
読み込み感度ラベルが有効かどうかを示すフラグを取得します。

  
次の**値を返し**ます。有効な場合は True、それ以外の場合は false。
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl 関数
必要に応じて、クラウド エンドポイントのベース URL を設定します。

パラメーター:  
* **cloudEndpointBaseUrl**: すべてのサービス要求で使用されるベース URL (たとえば、"https://dataservice.protection.outlook.com")


  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl 関数
すべてのサービス要求で使用されるクラウド ベースの URL を取得します (指定されている場合)。

  
次の**値を返し**ます。[基本 URL]
  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail 関数
委任されたユーザーを設定します。

パラメーター:  
* **delegatedUserEmail**: 委任の電子メール。


委任されたユーザーは、他のユーザーの代理として認証を行うユーザーまたはアプリケーションが動作するときに指定します。
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail 関数
委任されたユーザーを取得します。

  
次の**値を返し**ます。委任されたユーザー認証を行っているユーザーまたはアプリケーションが別のユーザーの代理で動作しているときに、委任されたユーザーを指定します。