---
title: 'クラス PolicyEngine:: Settings'
description: 'Microsoft Information Protection (MIP) SDK の policyengine:: settings クラスに関するドキュメントを示します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 4e40bccefa523e18dfdb99a8ef0adacad9f9d4cf
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215104"
---
# <a name="class-policyenginesettings"></a>クラス PolicyEngine:: Settings 
PolicyEngine に関連付けられている設定を定義します。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック設定 (const std:: string& engineId、const std:: shared_ptr \<AuthDelegate\>& authDelegate、const std:: string& clientData、const std:: string& locale、Bool loadSensitivityTypes)  |  既存のエンジンを読み込むための PolicyEngine::Settings コンストラクター。
パブリック設定 (const Id& id、const std:: shared_ptr \<AuthDelegate\>& authDelegate、const std:: string& clientData、const std:: string& locale、Bool loadSensitivityTypes)  |  新しいエンジンを作成するための PolicyEngine::Settings コンストラクター。
public const std::string& GetEngineId() const  |  エンジン ID を取得します。
public void SetEngineId(const std::string& id)  |  エンジン ID を設定します。
public const Identity& GetIdentity() const  |  ID オブジェクトを取得します。
public void SetIdentity(const Identity& identity)  |  ID オブジェクトを設定します。
public const std::string& GetClientData() const  |  設定で設定されたクライアント データを取得します。
public void SetClientData(const std::string& clientData)  |  クライアント データ文字列を設定します。
public const std::string& GetLocale() const  |  設定で設定されたロケールを取得します。
public void SetCustomSettings (const std:: vector \<std::pair\<std::string, std::string\> \>& customsettings)  |  機能のゲーティングとテストに使用するカスタム設定を設定します。
public const std:: vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings () const  |  機能のゲーティングとテストに使用するカスタム設定を取得します。
public void SetSessionId(const std::string& sessionId)  |  クライアントによって定義されたテレメトリに使用するセッション ID を設定します。
public const std::string& GetSessionId() const  |  セッション ID、一意識別子を取得します。
public bool IsLoadSensitivityTypesEnabled () const  |  読み込み感度ラベルが有効かどうかを示すフラグを取得します。
パブリック void SetCloud (クラウドクラウド)  |  必要に応じて、ターゲットクラウドを設定します。
パブリッククラウドの GetCloud () const  |  すべてのサービス要求によって使用されるターゲットクラウドを取得します。
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  カスタムクラウドのクラウドエンドポイントベース URL を設定します。
public const std::string& GetCloudEndpointBaseUrl() const  |  すべてのサービス要求で使用されるクラウド ベースの URL を取得します (指定されている場合)。
public void SetDelegatedUserEmail (const std:: string& delegatedUserEmail)  |  委任されたユーザーを設定します。
public const std:: string& GetDelegatedUserEmail () const  |  委任されたユーザーを取得します。
public void SetLabelFilter (const std:: vector \<LabelFilterType\>& deprecatedLabelFilters)  |  ラベルフィルターを設定します。
public const std:: vector \<LabelFilterType\>& getlabelfilter () const  |  非推奨の関数 SetLabelFilter によって設定されたラベルフィルターを取得します。
public void ConfigureFunctionality (FunctionalityFilterType functionalityFilterType, bool enabled)  |  機能を有効または無効にします。
public const std:: map \<FunctionalityFilterType, bool\>& GetConfiguredFunctionality () const  |  構成済みの機能を取得します。
public void Setバリエーション Abmarkextmarkingtype (可変 abている extmarkmarkingtype)  |  変数テキストのマークの種類を設定します。
パブリック型のバリエーション Abmarkextmarkingtype () const。  |  変数のテキストのマーク付けの種類を取得します。
public void SetAuthDelegate (const std:: shared_ptr \<AuthDelegate\>& authdelegate)  |  エンジン認証デリゲートを設定します。
public std::shared_ptr\<AuthDelegate\> GetAuthDelegate() const  |  エンジン認証デリゲートを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="settings-function"></a>Settings 関数
既存のエンジンを読み込むための PolicyEngine::Settings コンストラクター。

パラメーター:  
* **engineId**: AddEngineAsync または自己生成された1つのエンジン ID に設定します。 既存のエンジンを読み込む場合は ID を再利用し、それ以外の場合は新しいエンジンが作成されます。 


* **Authdelegate**: 認証トークンを取得するために SDK によって使用される認証デリゲートは、両方が指定されている場合は policyprofile:: Settings:: authdelegate をオーバーライドします 


* **clientData**: アンロード時にエンジンと共に格納でき、読み込まれたエンジンから取得できるカスタマイズ可能なクライアント データ。 


* **locale**: エンジンのローカライズ可能な出力はこのロケールで提供されます。 


* **省略可能**: エンジンが読み込まれるときに、カスタム感度の種類も読み込む必要があることを示すフラグです。 true の場合、カスタム感度の種類の更新とポリシーの変更に対して、プロファイルに対して true が呼び出されます。 false の場合、ListSensitivityTypes call は常に空のリストを返します。


  
### <a name="settings-function"></a>Settings 関数
新しいエンジンを作成するための PolicyEngine::Settings コンストラクター。

パラメーター:  
* **identity**: 新しいエンジンに関連付けられているユーザーの ID 情報。 


* **Authdelegate**: 認証トークンを取得するために SDK によって使用される認証デリゲートは、両方が指定されている場合は policyprofile:: Settings:: authdelegate をオーバーライドします 


* **clientData**: アンロード時にエンジンと共に格納でき、読み込まれたエンジンから取得できるカスタマイズ可能なクライアント データ。 


* **locale**: エンジンのローカライズ可能な出力はこのロケールで提供されます。 


* **省略可能**: エンジンが読み込まれるときに、カスタム感度の種類も読み込む必要があることを示すフラグです。 true の場合、カスタム感度の種類の更新とポリシーの変更に対して、プロファイルに対して true が呼び出されます。 false の場合、ListSensitivityTypes call は常に空のリストを返します。


  
### <a name="getengineid-function"></a>GetEngineId 関数
エンジン ID を取得します。

  
**戻り値**: エンジンを識別する一意の文字列。
  
### <a name="setengineid-function"></a>SetEngineId 関数
エンジン ID を設定します。

パラメーター:  
* **id**: エンジン ID。


  
### <a name="getidentity-function"></a>GetIdentity 関数
ID オブジェクトを取得します。

  
**戻り値**: 設定オブジェクト内の ID への参照。 
  
**関連項目**: mip::Identity
  
### <a name="setidentity-function"></a>SetIdentity 関数
ID オブジェクトを設定します。

パラメーター:  
* **id**: ユーザーの一意の id。 


  
**関連項目**: mip::Identity
  
### <a name="getclientdata-function"></a>GetClientData 関数
設定で設定されたクライアント データを取得します。

  
**戻り値**: クライアントで指定されたデータの文字列。
  
### <a name="setclientdata-function"></a>SetClientData 関数
クライアント データ文字列を設定します。

パラメーター:  
* **clientdata**: ユーザーが指定したデータ。


  
### <a name="getlocale-function"></a>GetLocale 関数
設定で設定されたロケールを取得します。

  
**戻り値**: ロケール。
  
### <a name="setcustomsettings-function"></a>SetCustomSettings 関数
機能のゲーティングとテストに使用するカスタム設定を設定します。

パラメーター:  
* **Customsettings**: 名前と値のペアの一覧。


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
機能のゲーティングとテストに使用するカスタム設定を取得します。

  
**戻り値**: 名前と値のペアのリスト。
  
### <a name="setsessionid-function"></a>SetSessionId 関数
クライアントによって定義されたテレメトリに使用するセッション ID を設定します。

パラメーター:  
* **sessionId**: テレメトリイベントを接続する一意の文字列。


  
### <a name="getsessionid-function"></a>GetSessionId 関数
セッション ID、一意識別子を取得します。

  
**戻り値**: セッション ID。
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled 関数
読み込み感度ラベルが有効かどうかを示すフラグを取得します。

  
が **返さ** れます。有効な場合は True、それ以外の場合は false です。
  
### <a name="setcloud-function"></a>SetCloud 関数
必要に応じて、ターゲットクラウドを設定します。

パラメーター:  
* **クラウド**: クラウド


クラウドが指定されていない場合、既定では商用クラウドになります。
  
### <a name="getcloud-function"></a>GetCloud 関数
すべてのサービス要求によって使用されるターゲットクラウドを取得します。

  
**返される値**: クラウド
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl 関数
カスタムクラウドのクラウドエンドポイントベース URL を設定します。

パラメーター:  
* **cloudEndpointBaseUrl**: すべてのサービス要求で使用されるベース URL (たとえば、"https://dataservice.protection.outlook.com")


この値は読み取り専用であり、Cloud = Custom に設定されている必要があります
  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl 関数
すべてのサービス要求で使用されるクラウド ベースの URL を取得します (指定されている場合)。

  
**戻り値**: ベース URL
  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail 関数
委任されたユーザーを設定します。

パラメーター:  
* **delegatedUserEmail**: 委任の電子メール。


委任されたユーザーは、他のユーザーの代理として認証を行うユーザーまたはアプリケーションが動作するときに指定します。
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail 関数
委任されたユーザーを取得します。

  
**戻り値**: 委任されたユーザー: 認証を行っているユーザーまたはアプリケーションが別のユーザーの代理で動作しているときに、委任されたユーザーを指定します。
  
### <a name="setlabelfilter-function"></a>SetLabelFilter 関数
ラベルフィルターを設定します。

パラメーター:  
* **labelfilter**: ラベルフィルター。


ラベルは、既定でスコープにフィルターを適用します。この api は、可能なアクションによってフィルター処理を許可します。 HyokProtection と DoubleKeyProtection が設定されていない場合は、フィルター処理されます。
  
### <a name="getlabelfilter-function"></a>GetLabelFilter 関数
非推奨の関数 SetLabelFilter によって設定されたラベルフィルターを取得します。

  
**戻り値**: ラベルフィルター。
ラベルは、既定でスコープにフィルターを適用します。この api は、可能なアクションによってフィルター処理を許可します。
  
### <a name="configurefunctionality-function"></a>ConfigureFunctionality 関数
機能を有効または無効にします。

パラメーター:  
* **functionalityFilterType**: 機能の種類。 


* **enabled**: 有効にする場合は True、無効にする場合は false


HyokProtection、DoubleKeyProtection、DoubleKeyUserDefinedProtection は既定で無効になっているため、有効にする必要があります。
  
### <a name="getconfiguredfunctionality-function"></a>GetConfiguredFunctionality 関数
構成済みの機能を取得します。

  
**戻り** 値: 型が有効になっているかどうかを示すブール値へのマップ。
  
### <a name="setvariabletextmarkingtype-function"></a>Setバリエーション Abmarkextmarkingtype 関数
変数テキストのマークの種類を設定します。

パラメーター:  
* 可変 **Abmarkextmarkingtype**: 変数テキストのマーク付けの種類。


  
### <a name="getvariabletextmarkingtype-function"></a>Getバリエーション Abmarkextmarkingtype 関数
変数のテキストのマーク付けの種類を取得します。

  
は、変数テキストのマーク付けの種類を **返し** ます。
  
### <a name="setauthdelegate-function"></a>SetAuthDelegate 関数
エンジン認証デリゲートを設定します。

パラメーター:  
* **authdelegate**: Auth デリゲート


  
### <a name="getauthdelegate-function"></a>GetAuthDelegate 関数
エンジン認証デリゲートを取得します。

  
**戻り値**: エンジンの認証デリゲート。