---
title: 'クラス FileEngine:: Settings'
description: 'Microsoft Information Protection (MIP) SDK の fileengine:: settings クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 5a992c81b4d32a876f5f047a98b229aace7cb075
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763270"
---
# <a name="class-fileenginesettings"></a>クラス FileEngine:: Settings 
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック設定 (const std:: string& engineId、const std:: shared_ptr\<authdelegate\>& authdelegate、const std:: string& clientdata、const std:: string& locale、bool loadSensitivityTypes)  |  既存のエンジンを読み込むための FileEngine::Settings コンストラクター。
パブリック設定 (const Id& id、const std:: shared_ptr\<authdelegate\>& authdelegate、const std:: string& clientdata、const std:: string& locale、bool loadSensitivityTypes)  |  新しいエンジンを作成するための FileProfile::Settings コンストラクター。
public const std::string& GetEngineId() const  |  エンジン ID を返します。
public void SetEngineId(const std::string& id)  |  エンジン ID を設定します。
public const Identity& GetIdentity() const  |  エンジン ID を返します。
public void SetIdentity(const Identity& identity)  |  エンジン ID を設定します。
public const std::string& GetClientData() const  |  エンジンのクライアント データを返します。
public const std::string& GetLocale() const  |  エンジンのロケールを返します。
public void setcustomsettings (const std:: vector\<std::p air\<std:: string, std:: string\> \>& 値)  |  テストや実験に使用する名前と値のペアの一覧を設定します。
public const std:: vector\<std::p air\<std:: string、std:: string\> \>& GetCustomSettings () const  |  テストや実験に使用する名前と値のペアの一覧を取得します。
public void SetSessionId(const std::string& sessionId)  |  エンジンのセッション ID を設定します。
public const std::string& GetSessionId() const  |  エンジンのセッション ID を返します。
パブリック void SetCloud (クラウドクラウド)  |  必要に応じて、ターゲットクラウドを設定します。
パブリッククラウドの GetCloud () const  |  すべてのサービス要求によって使用されるターゲットクラウドを取得します。
public void SetProtectionCloudEndpointBaseUrl(const std::string& protectionCloudEndpointBaseUrl)  |  カスタムクラウドの保護クラウドエンドポイントベース URL を設定します。
public const std::string& GetProtectionCloudEndpointBaseUrl() const  |  保護クラウドエンドポイントのベース url を取得します。
public void SetPolicyCloudEndpointBaseUrl (const std:: string& policyCloudEndpointBaseUrl)  |  カスタムクラウドのポリシークラウドエンドポイントベース URL を設定します。
public const std:: string& GetPolicyCloudEndpointBaseUrl () const  |  ポリシークラウドエンドポイントのベース url を取得します。
public void SetProtectionOnlyEngine (bool protectionOnly)  |  保護のみのエンジン インジケーターを設定します (ポリシー/ラベルなし)。
public const bool IsProtectionOnlyEngine() const  |  保護のみのエンジン インジケーターを返します (ポリシー/ラベルなし)。
public bool IsLoadSensitivityTypesEnabled () const  |  読み込み感度ラベルが有効かどうかを示すフラグを取得します。
public void EnablePFile (bool 値)  |  が PFiles を生成するかどうかを示すフラグを設定します。
public const bool IsPFileEnabled ()  |  が PFiles を生成するかどうかを示すフラグを取得します。
public void SetDelegatedUserEmail (const std:: string& delegatedUserEmail)  |  委任されたユーザーを設定します。
public const std:: string& GetDelegatedUserEmail () const  |  委任されたユーザーを取得します。
public void SetLabelFilter (const std:: vector\<LabelFilterType\>& labelfilter)  |  ラベルフィルターを設定します。
public const std:: vector\<LabelFilterType\>& getlabelfilter () const  |  ラベルフィルターを取得します。
public void SetAuthDelegate (const std:: shared_ptr\<authdelegate\>& authdelegate)  |  エンジン認証デリゲートを設定します。
public std:: shared_ptr\<authdelegate\> getauthdelegate () const  |  エンジン認証デリゲートを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="settings-function"></a>Settings 関数
既存のエンジンを読み込むための FileEngine::Settings コンストラクター。

パラメーター:  
* **engineId**: AddEngineAsync によって生成される一意のエンジン ID に設定します。 


* **Authdelegate**: 認証トークンを取得するために SDK によって使用される認証デリゲートは、両方が指定されている場合は policyprofile:: Settings:: authdelegate をオーバーライドします 


* **clientData**: アンロード時にエンジンと共に格納でき、読み込まれたエンジンから取得できるカスタマイズ可能なクライアント データ。 


* **locale**: エンジンのローカライズ可能な出力はこのロケールで提供されます。 


* **loadSensitivityTypes**: エンジンが読み込まれるときに、カスタム感度の種類も読み込む必要があることを示す省略可能なフラグです。 true の場合は、カスタム感度の種類の更新とポリシーの変更に対して、プロファイルに対して true が呼び出されます。 false の場合、ListSensitivityTypes call は常に空のリストを返します。


  
### <a name="settings-function"></a>Settings 関数
新しいエンジンを作成するための FileProfile::Settings コンストラクター。

パラメーター:  
* **identity**: 新しいエンジンに関連付けられているユーザーの ID 情報。 


* **Authdelegate**: 認証トークンを取得するために SDK によって使用される認証デリゲートは、両方が指定されている場合は policyprofile:: Settings:: authdelegate をオーバーライドします 


* **clientData**: アンロード時にエンジンと共に格納でき、読み込まれたエンジンから取得できるカスタマイズ可能なクライアント データ。 


* **locale**: エンジンのローカライズ可能な出力はこのロケールで提供されます。 


* **loadSensitivityTypes**: エンジンが読み込まれるときに、カスタム感度の種類も読み込む必要があることを示す省略可能なフラグです。 true の場合は、カスタム感度の種類の更新とポリシーの変更に対して、プロファイルに対して true が呼び出されます。 false の場合、ListSensitivityTypes call は常に空のリストを返します。


  
### <a name="getengineid-function"></a>GetEngineId 関数
エンジン ID を返します。
  
### <a name="setengineid-function"></a>SetEngineId 関数
エンジン ID を設定します。

パラメーター:  
* **id**: エンジン ID。


  
### <a name="getidentity-function"></a>GetIdentity 関数
エンジン ID を返します。
  
### <a name="setidentity-function"></a>SetIdentity 関数
エンジン ID を設定します。
  
### <a name="getclientdata-function"></a>GetClientData 関数
エンジンのクライアント データを返します。
  
### <a name="getlocale-function"></a>GetLocale 関数
エンジンのロケールを返します。
  
### <a name="setcustomsettings-function"></a>SetCustomSettings 関数
テストや実験に使用する名前と値のペアの一覧を設定します。
  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
テストや実験に使用する名前と値のペアの一覧を取得します。
  
### <a name="setsessionid-function"></a>SetSessionId 関数
エンジンのセッション ID を設定します。
  
### <a name="getsessionid-function"></a>GetSessionId 関数
エンジンのセッション ID を返します。
  
### <a name="setcloud-function"></a>SetCloud 関数
必要に応じて、ターゲットクラウドを設定します。

パラメーター:  
* **クラウド**: クラウド


クラウドが指定されていない場合、既定ではグローバルクラウドになります。
  
### <a name="getcloud-function"></a>GetCloud 関数
すべてのサービス要求によって使用されるターゲットクラウドを取得します。

  
**返される値**: クラウド
  
### <a name="setprotectioncloudendpointbaseurl-function"></a>SetProtectionCloudEndpointBaseUrl 関数
カスタムクラウドの保護クラウドエンドポイントベース URL を設定します。

パラメーター:  
* **protectionCloudEndpointBaseUrl**: 保護エンドポイントに関連付けられたベース URL


この値は読み取り専用であり、Cloud = Custom に設定されている必要があります
  
### <a name="getprotectioncloudendpointbaseurl-function"></a>GetProtectionCloudEndpointBaseUrl 関数
保護クラウドエンドポイントのベース url を取得します。

  
**戻り**値: 保護エンドポイントに関連付けられているベース url この値は読み取り専用で、Cloud = Custom に設定する必要があります
  
### <a name="setpolicycloudendpointbaseurl-function"></a>SetPolicyCloudEndpointBaseUrl 関数
カスタムクラウドのポリシークラウドエンドポイントベース URL を設定します。

パラメーター:  
* **policyCloudEndpointBaseUrl**: ポリシーエンドポイントに関連付けられているベース url


  
### <a name="getpolicycloudendpointbaseurl-function"></a>GetPolicyCloudEndpointBaseUrl 関数
ポリシークラウドエンドポイントのベース url を取得します。

  
**戻り値**: ポリシーエンドポイントに関連付けられているベース url
  
### <a name="setprotectiononlyengine-function"></a>SetProtectionOnlyEngine 関数
保護のみのエンジン インジケーターを設定します (ポリシー/ラベルなし)。
  
### <a name="isprotectiononlyengine-function"></a>IsProtectionOnlyEngine 関数
保護のみのエンジン インジケーターを返します (ポリシー/ラベルなし)。
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled 関数
読み込み感度ラベルが有効かどうかを示すフラグを取得します。

  
が**返さ**れます。有効な場合は True、それ以外の場合は false です。
  
### <a name="enablepfile-function"></a>EnablePFile 関数
が PFiles を生成するかどうかを示すフラグを設定します。
  
### <a name="ispfileenabled-function"></a>IsPFileEnabled 関数
が PFiles を生成するかどうかを示すフラグを取得します。

  
が**返さ**れます。有効な場合は True、それ以外の場合は false です。
  
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
ラベルフィルターを取得します。

  
**戻り値**: ラベルフィルター。
ラベルは、既定でスコープにフィルターを適用します。この api は、可能なアクションによってフィルター処理を許可します。
  
### <a name="setauthdelegate-function"></a>SetAuthDelegate 関数
エンジン認証デリゲートを設定します。

パラメーター:  
* **authdelegate**: Auth デリゲート


  
### <a name="getauthdelegate-function"></a>GetAuthDelegate 関数
エンジン認証デリゲートを取得します。

  
**戻り値**: エンジンの認証デリゲート。