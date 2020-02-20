---
title: class mip::PolicyEngine::Settings
description: Microsoft Information Protection (MIP) SDK の mip::p olicyengine クラスについて説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 620775649ee0fa593f141b1a4f983ad8b52caafe
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77487618"
---
# <a name="class-mippolicyenginesettings"></a>class mip::PolicyEngine::Settings 
PolicyEngine に関連付けられた設定を定義します。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
パブリック設定 (const std:: string & engineId、const std:: string & clientData、const std:: string & locale、bool loadSensitivityTypes)  |  既存のエンジンを読み込むための PolicyEngine:: Settings コンストラクター。
パブリック設定 (定数 Id & id、const std:: string & clientData、const std:: string & locale、bool loadSensitivityTypes)  |  新しいエンジンを作成するための PolicyEngine:: Settings コンストラクター。
public const std::string& GetEngineId() const  |  エンジン ID を取得します。
public void SetEngineId(const std::string& id)  |  エンジン ID を設定します。
public const Identity& GetIdentity() const  |  ID オブジェクトを取得します。
public void SetIdentity(const Identity& identity)  |  ID オブジェクトを設定します。
public const std::string& GetClientData() const  |  設定で設定されたクライアント データを取得します。
public void SetClientData(const std::string& clientData)  |  クライアント データ文字列を設定します。
public const std::string& GetLocale() const  |  設定で設定されたロケールを取得します。
public void SetCustomSettings (const std:: vector\<std::p air\<std:: string、std:: string\>\>& customSettings)  |  機能のゲーティングとテストに使用するカスタム設定を設定します。
public const std:: vector\<std::p air\<std:: string、std:: string\>\>& GetCustomSettings () const  |  機能のゲーティングとテストに使用するカスタム設定を取得します。
public void SetSessionId(const std::string& sessionId)  |  クライアントによって定義されたテレメトリに使用するセッション ID を設定します。
public const std::string& GetSessionId() const  |  セッション ID、一意識別子を取得します。
public bool IsLoadSensitivityTypesEnabled() const  |  読み込み感度ラベルが有効かどうかを示すフラグを取得します。
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  必要に応じて、クラウド エンドポイントのベース URL を設定します。
public const std::string& GetCloudEndpointBaseUrl() const  |  すべてのサービス要求で使用されるクラウド ベースの URL を取得します (指定されている場合)。
public void SetDelegatedUserEmail (const std:: string & delegatedUserEmail)  |  委任されたユーザーを設定します。
public const std:: string & GetDelegatedUserEmail () const  |  委任されたユーザーを取得します。
public void SetLabelFilter (const std:: vector\<LabelFilterType\>& labelFilter)  |  ラベルフィルターを設定します。
public const std:: vector\<LabelFilterType\>& GetLabelFilter () const  |  ラベルフィルターを取得します。
public void Setバリエーション Abmarkextmarkingtype (可変 abている extmarkmarkingtype)  |  変数テキストのマークの種類を設定します。
パブリック型のバリエーション Abmarkextmarkingtype () const。  |  変数のテキストのマーク付けの種類を取得します。
  
## <a name="members"></a>Members
  
### <a name="settings-function"></a>Settings 関数
既存のエンジンを読み込むための PolicyEngine:: Settings コンストラクター。

パラメータ:  
* **engineId**: AddEngineAsync によって生成されたか、または自分で生成した一意のエンジン ID に設定します。 既存のエンジンを読み込む場合は ID を再利用し、それ以外の場合は新しいエンジンが作成されます。 


* **clientData**: アンロード時にエンジンと共に格納でき、読み込まれたエンジンから取得できるカスタマイズ可能なクライアント データ。 


* **locale**: エンジンのローカライズ可能な出力はこのロケールで提供されます。 


* **省略可能**: エンジンが読み込まれるときに、カスタム感度の種類も読み込む必要があることを示すフラグです。 true の場合、カスタム感度の種類の更新とポリシーの変更に対して、プロファイルに対して true が呼び出されます。 false の場合、ListSensitivityTypes call は常に空のリストを返します。


  
### <a name="settings-function"></a>Settings 関数
新しいエンジンを作成するための PolicyEngine:: Settings コンストラクター。

パラメータ:  
* **identity**: 新しいエンジンに関連付けられているユーザーの ID 情報。 


* **clientData**: アンロード時にエンジンと共に格納でき、読み込まれたエンジンから取得できるカスタマイズ可能なクライアント データ。 


* **locale**: エンジンのローカライズ可能な出力はこのロケールで提供されます。 


* **省略可能**: エンジンが読み込まれるときに、カスタム感度の種類も読み込む必要があることを示すフラグです。 true の場合、カスタム感度の種類の更新とポリシーの変更に対して、プロファイルに対して true が呼び出されます。 false の場合、ListSensitivityTypes call は常に空のリストを返します。


  
### <a name="getengineid-function"></a>GetEngineId 関数
エンジン ID を取得します。

  
**戻り値**: エンジンを識別する一意の文字列。
  
### <a name="setengineid-function"></a>SetEngineId 関数
エンジン ID を設定します。

パラメータ:  
* **id**: エンジン ID。


  
### <a name="getidentity-function"></a>GetIdentity 関数
ID オブジェクトを取得します。

  
**戻り値**: 設定オブジェクト内の ID への参照。 
  
**関連項目**: mip::Identity
  
### <a name="setidentity-function"></a>SetIdentity 関数
ID オブジェクトを設定します。

パラメータ:  
* **identity**: ユーザーの一意の ID。 


  
**関連項目**: mip::Identity
  
### <a name="getclientdata-function"></a>GetClientData 関数
設定で設定されたクライアント データを取得します。

  
**戻り値**: クライアントで指定されたデータの文字列。
  
### <a name="setclientdata-function"></a>SetClientData 関数
クライアント データ文字列を設定します。

パラメータ:  
* **clientData**: ユーザーが指定したデータ。


  
### <a name="getlocale-function"></a>GetLocale 関数
設定で設定されたロケールを取得します。

  
**戻り値**: ロケール。
  
### <a name="setcustomsettings-function"></a>SetCustomSettings 関数
機能のゲーティングとテストに使用するカスタム設定を設定します。

パラメータ:  
* **customSettings**: 名前と値のペアの一覧。


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
機能のゲーティングとテストに使用するカスタム設定を取得します。

  
**戻り値**: 名前と値のペアのリスト。
  
### <a name="setsessionid-function"></a>SetSessionId 関数
クライアントによって定義されたテレメトリに使用するセッション ID を設定します。

パラメータ:  
* **sessionId**: テレメトリ イベントを接続する一意の文字列。


  
### <a name="getsessionid-function"></a>GetSessionId 関数
セッション ID、一意識別子を取得します。

  
**戻り値**: セッション ID。
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled 関数
読み込み感度ラベルが有効かどうかを示すフラグを取得します。

  
が**返さ**れます。有効な場合は True、それ以外の場合は false です。
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl 関数
必要に応じて、クラウド エンドポイントのベース URL を設定します。

パラメータ:  
* **cloudEndpointBaseUrl**: すべてのサービス要求で使用されるベース URL (たとえば、"https://dataservice.protection.outlook.com")


  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl 関数
すべてのサービス要求で使用されるクラウド ベースの URL を取得します (指定されている場合)。

  
**戻り値**: ベース URL
  
### <a name="setdelegateduseremail-function"></a>SetDelegatedUserEmail 関数
委任されたユーザーを設定します。

パラメータ:  
* **delegatedUserEmail**: 委任の電子メール。


委任されたユーザーは、他のユーザーの代理として認証を行うユーザーまたはアプリケーションが動作するときに指定します。
  
### <a name="getdelegateduseremail-function"></a>GetDelegatedUserEmail 関数
委任されたユーザーを取得します。

  
**戻り値**: 委任されたユーザー: 認証を行っているユーザーまたはアプリケーションが別のユーザーの代理で動作しているときに、委任されたユーザーを指定します。
  
### <a name="setlabelfilter-function"></a>SetLabelFilter 関数
ラベルフィルターを設定します。

パラメータ:  
* **labelfilter**: ラベルフィルター。


ラベルは、既定でスコープにフィルターを適用します。この api は、可能なアクションによってフィルター処理を許可します。
  
### <a name="getlabelfilter-function"></a>GetLabelFilter 関数
ラベルフィルターを取得します。

  
**戻り値**: ラベルフィルター。
ラベルは、既定でスコープにフィルターを適用します。この api は、可能なアクションによってフィルター処理を許可します。
  
### <a name="setvariabletextmarkingtype-function"></a>Setバリエーション Abmarkextmarkingtype 関数
変数テキストのマークの種類を設定します。

パラメータ:  
* 可変**Abmarkextmarkingtype**: 変数テキストのマーク付けの種類。


  
### <a name="getvariabletextmarkingtype-function"></a>Getバリエーション Abmarkextmarkingtype 関数
変数のテキストのマーク付けの種類を取得します。

  
は、変数テキストのマーク付けの種類を**返し**ます。