---
title: class mip::FileEngine::Settings
description: 'Microsoft Information Protection (MIP) SDK の mip:: fileengine クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 6105a542c3c01b31598796912211f97562b25f08
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488791"
---
# <a name="class-mipfileenginesettings"></a>class mip::FileEngine::Settings 
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
パブリック設定 (const std:: string & engineId、const std:: string & clientData、const std:: string & locale、bool loadSensitivityTypes)  |  既存のエンジンを読み込むための FileEngine:: Settings コンストラクター。
パブリック設定 (定数 Id & id、const std:: string & clientData、const std:: string & locale、bool loadSensitivityTypes)  |  新しいエンジンを作成するための FileProfile:: Settings コンストラクター。
public const std::string& GetEngineId() const  |  エンジン ID を返します。
public void SetEngineId(const std::string& id)  |  エンジン ID を設定します。
public const Identity& GetIdentity() const  |  エンジン ID を返します。
public void SetIdentity(const Identity& identity)  |  エンジン ID を設定します。
public const std::string& GetClientData() const  |  エンジンのクライアント データを返します。
public const std::string& GetLocale() const  |  エンジンのロケールを返します。
public void SetCustomSettings (const std:: vector\<std::p air\<std:: string、std:: string\>\>& value)  |  テストや実験に使用する名前と値のペアの一覧を設定します。
public const std:: vector\<std::p air\<std:: string、std:: string\>\>& GetCustomSettings () const  |  テストや実験に使用する名前と値のペアの一覧を取得します。
public void SetSessionId(const std::string& sessionId)  |  エンジンのセッション ID を設定します。
public const std::string& GetSessionId() const  |  エンジンのセッション ID を返します。
public void SetProtectionCloudEndpointBaseUrl(const std::string& protectionCloudEndpointBaseUrl)  |  クラウド境界を指定するために使用する、保護クラウド エンドポイント ベース URL を設定します。
public const std::string& GetProtectionCloudEndpointBaseUrl() const  |  保護クラウドエンドポイントのベース url を取得します。
public void SetPolicyCloudEndpointBaseUrl(const std::string& policyCloudEndpointBaseUrl)  |  クラウドの境界を指定するために使用されるポリシークラウドエンドポイントのベース url を設定します。
public const std::string& GetPolicyCloudEndpointBaseUrl() const  |  ポリシークラウドエンドポイントのベース url を取得します。
public void SetProtectionOnlyEngine (bool protectionOnly)  |  保護のみのエンジン インジケーターを設定します (ポリシー/ラベルなし)。
public const bool IsProtectionOnlyEngine() const  |  保護のみのエンジン インジケーターを返します (ポリシー/ラベルなし)。
public bool IsLoadSensitivityTypesEnabled() const  |  読み込み感度ラベルが有効かどうかを示すフラグを取得します。
public void EnablePFile (bool 値)  |  が PFiles を生成するかどうかを示すフラグを設定します。
public const bool IsPFileEnabled ()  |  が PFiles を生成するかどうかを示すフラグを取得します。
public void SetDelegatedUserEmail (const std:: string & delegatedUserEmail)  |  委任されたユーザーを設定します。
public const std:: string & GetDelegatedUserEmail () const  |  委任されたユーザーを取得します。
public void SetLabelFilter (const std:: vector\<LabelFilterType\>& labelFilter)  |  ラベルフィルターを設定します。
public const std:: vector\<LabelFilterType\>& GetLabelFilter () const  |  ラベルフィルターを取得します。
  
## <a name="members"></a>Members
  
### <a name="settings-function"></a>Settings 関数
既存のエンジンを読み込むための FileEngine:: Settings コンストラクター。

パラメータ:  
* **engineId**: AddEngineAsync によって生成される一意のエンジン ID に設定します。 


* **clientData**: アンロード時にエンジンと共に格納でき、読み込まれたエンジンから取得できるカスタマイズ可能なクライアント データ。 


* **locale**: エンジンのローカライズ可能な出力はこのロケールで提供されます。 


* **loadSensitivityTypes**: エンジンが読み込まれるときに、カスタム感度の種類も読み込む必要があることを示す省略可能なフラグです。 true の場合は、カスタム感度の種類の更新とポリシーの変更に対して、プロファイルに対して true が呼び出されます。 false の場合、ListSensitivityTypes call は常に空のリストを返します。


  
### <a name="settings-function"></a>Settings 関数
新しいエンジンを作成するための FileProfile:: Settings コンストラクター。

パラメータ:  
* **identity**: 新しいエンジンに関連付けられているユーザーの ID 情報。 


* **clientData**: アンロード時にエンジンと共に格納でき、読み込まれたエンジンから取得できるカスタマイズ可能なクライアント データ。 


* **locale**: エンジンのローカライズ可能な出力はこのロケールで提供されます。 


* **loadSensitivityTypes**: エンジンが読み込まれるときに、カスタム感度の種類も読み込む必要があることを示す省略可能なフラグです。 true の場合は、カスタム感度の種類の更新とポリシーの変更に対して、プロファイルに対して true が呼び出されます。 false の場合、ListSensitivityTypes call は常に空のリストを返します。


  
### <a name="getengineid-function"></a>GetEngineId 関数
エンジン ID を返します。
  
### <a name="setengineid-function"></a>SetEngineId 関数
エンジン ID を設定します。

パラメータ:  
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
  
### <a name="setprotectioncloudendpointbaseurl-function"></a>SetProtectionCloudEndpointBaseUrl 関数
クラウド境界を指定するために使用する、保護クラウド エンドポイント ベース URL を設定します。

パラメータ:  
* **protectionCloudEndpointBaseUrl**: 保護エンドポイントに関連付けられたベース URL


  
### <a name="getprotectioncloudendpointbaseurl-function"></a>GetProtectionCloudEndpointBaseUrl 関数
保護クラウドエンドポイントのベース url を取得します。

  
**戻り値**: 保護エンドポイントに関連付けられたベース URL
  
### <a name="setpolicycloudendpointbaseurl-function"></a>SetPolicyCloudEndpointBaseUrl 関数
クラウドの境界を指定するために使用されるポリシークラウドエンドポイントのベース url を設定します。

パラメータ:  
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