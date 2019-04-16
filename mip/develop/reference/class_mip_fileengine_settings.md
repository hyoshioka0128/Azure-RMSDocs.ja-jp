---
title: class mip::FileEngine::Settings
description: Mip::fileengine クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 2481ee7d42f00ce5b33529b15e17b22ba6556b0e
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574042"
---
# <a name="class-mipfileenginesettings"></a>class mip::FileEngine::Settings 
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale, bool loadSensitivityTypes)  |  既存のエンジンを読み込むための [FileEngine::Settings](class_mip_fileengine_settings.md) コンストラクター。
public Settings(const Identity& identity, const std::string& clientData, const std::string& locale, bool loadSensitivityTypes)  |  新しいエンジンを作成するための [FileProfile::Settings](class_mip_fileprofile_settings.md) コンストラクター。
public const std::string& GetEngineId() const  |  エンジン ID を返します。
public void SetEngineId(const std::string& id)  |  エンジン ID を設定します。
public const Identity& GetIdentity() const  |  エンジンを返します[Identity](class_mip_identity.md)します。
public void SetIdentity(const Identity& identity)  |  エンジン ID を設定します。
public const std::string& GetClientData() const  |  エンジンのクライアント データを返します。
public const std::string& GetLocale() const  |  エンジンのロケールを返します。
public void SetCustomSettings(const std::vector\<std::pair\<std::string, std::string\>\>& value)  |  テストや実験に使用する名前と値のペアの一覧を設定します。
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  テストや実験に使用する名前と値のペアの一覧を取得します。
public void SetSessionId(const std::string& sessionId)  |  エンジンのセッション ID を設定します。
public const std::string& GetSessionId() const  |  エンジンのセッション ID を返します。
public void SetProtectionCloudEndpointBaseUrl(const std::string& protectionCloudEndpointBaseUrl)  |  クラウド境界を指定するために使用する、保護クラウド エンドポイント ベース URL を設定します。
public const std::string& GetProtectionCloudEndpointBaseUrl() const  |  保護クラウド エンドポイントのベース url を取得します。
public void SetPolicyCloudEndpointBaseUrl(const std::string& policyCloudEndpointBaseUrl)  |  ポリシー クラウド エンドポイント ベースの url を設定、クラウドの境界を指定するために使用します。
public const std::string& GetPolicyCloudEndpointBaseUrl() const  |  ポリシーのクラウド エンドポイントのベース url を取得します。
public void SetProtectionOnlyEngine(const bool protectionOnly)  |  保護のみのエンジン インジケーターを設定します (ポリシー/ラベルなし)。
public const bool IsProtectionOnlyEngine() const  |  保護のみのエンジン インジケーターを返します (ポリシー/ラベルなし)。
public bool IsLoadSensitivityTypesEnabled() const  |  取得、負荷の機密ラベルが有効になっているかどうかを示すフラグ。
  
## <a name="members"></a>メンバー
  
### <a name="settings-function"></a>ポリシーの設定
既存のエンジンを読み込むための [FileEngine::Settings](class_mip_fileengine_settings.md) コンストラクター。

パラメーター:  
* **engineId**:AddEngineAsync によって生成された一意のエンジン ID に設定します。 


* **clientData**: アンロード時にエンジンと共に格納でき、読み込まれたエンジンから取得できるカスタマイズ可能なクライアント データ。 


* **locale**: エンジンのローカライズ可能な出力はこのロケールで提供されます。 


* **loadSensitivityTypes**:エンジンが読み込まれるときを示す省略可能なフラグ読み込む必要がありますもカスタムの機密の種類の更新情報をカスタムの機密の種類とポリシーの変更をプロファイルには true。 OnPolicyChange オブザーバーが呼び出される場合。 false ListSensitivityTypes を呼び出す場合は空のリストを常に返します。


  
### <a name="settings-function"></a>ポリシーの設定
新しいエンジンを作成するための [FileProfile::Settings](class_mip_fileprofile_settings.md) コンストラクター。

パラメーター:  
* **identity**:[Identity](class_mip_identity.md)新しいエンジンに関連付けられているユーザーの情報。 


* **clientData**: アンロード時にエンジンと共に格納でき、読み込まれたエンジンから取得できるカスタマイズ可能なクライアント データ。 


* **locale**: エンジンのローカライズ可能な出力はこのロケールで提供されます。 


* **loadSensitivityTypes**:エンジンが読み込まれるときを示す省略可能なフラグ読み込む必要がありますもカスタムの機密の種類の更新情報をカスタムの機密の種類とポリシーの変更をプロファイルには true。 OnPolicyChange オブザーバーが呼び出される場合。 false ListSensitivityTypes を呼び出す場合は空のリストを常に返します。


  
### <a name="getengineid-function"></a>GetEngineId 関数
エンジン ID を返します。
  
### <a name="setengineid-function"></a>SetEngineId 関数
エンジン ID を設定します。

パラメーター:  
* **id**: エンジン ID。


  
### <a name="getidentity-function"></a>GetIdentity 関数
エンジンを返します[Identity](class_mip_identity.md)します。
  
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

パラメーター:  
* **protectionCloudEndpointBaseUrl**:保護のエンドポイントに関連付けられているベース url


  
### <a name="getprotectioncloudendpointbaseurl-function"></a>GetProtectionCloudEndpointBaseUrl function
保護クラウド エンドポイントのベース url を取得します。

  
**返します**:保護のエンドポイントに関連付けられているベース url
  
### <a name="setpolicycloudendpointbaseurl-function"></a>SetPolicyCloudEndpointBaseUrl 関数
ポリシー クラウド エンドポイント ベースの url を設定、クラウドの境界を指定するために使用します。

パラメーター:  
* **policyCloudEndpointBaseUrl**:ポリシーのエンドポイントに関連付けられているベース url


  
### <a name="getpolicycloudendpointbaseurl-function"></a>GetPolicyCloudEndpointBaseUrl function
ポリシーのクラウド エンドポイントのベース url を取得します。

  
**返します**:ポリシーのエンドポイントに関連付けられているベース url
  
### <a name="setprotectiononlyengine-function"></a>SetProtectionOnlyEngine 関数
保護のみのエンジン インジケーターを設定します (ポリシー/ラベルなし)。
  
### <a name="isprotectiononlyengine-function"></a>IsProtectionOnlyEngine 関数
保護のみのエンジン インジケーターを返します (ポリシー/ラベルなし)。
  
### <a name="isloadsensitivitytypesenabled-function"></a>IsLoadSensitivityTypesEnabled 関数
取得、負荷の機密ラベルが有効になっているかどうかを示すフラグ。

  
**返します**:他の false を有効になっている場合は true。