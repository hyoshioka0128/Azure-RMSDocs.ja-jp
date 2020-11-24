---
title: 'クラス ProtectionEngine:: Settings'
description: 'Microsoft Information Protection (MIP) SDK の protectionengine:: settings クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 47947ed2b9b815204e3843ad64c18ffccf39b913
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95569102"
---
# <a name="class-protectionenginesettings"></a>クラス ProtectionEngine:: Settings 
作成時および有効期間全体にわたって ProtectionEngine によって使用される設定。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック設定 (const Identity& Identity、const std:: shared_ptr \<AuthDelegate\>& authDelegate、const std:: string& clientData、const std:: string& locale)  |  新しいエンジンを作成するための ProtectionEngine::Settings コンストラクター。
パブリック設定 (const std:: string& engineId、const std:: shared_ptr \<AuthDelegate\>& authDelegate、const std:: string& clientData、const std:: string& locale)  |  既存のエンジンを読み込むための ProtectionEngine::Settings コンストラクター。
public const std::string& GetEngineId() const  |  エンジン ID を取得します。
public void SetEngineId(const std::string& engineId)  |  エンジン ID を設定します。
public const Identity& GetIdentity() const  |  エンジンに関連付けられたユーザー ID を取得します。
public void SetIdentity(const Identity& identity)  |  エンジンに関連付けられるユーザー ID を設定します。
public const std::string& GetClientData() const  |  クライアントに指定されたカスタム データを取得します。
public void SetClientData(const std::string& clientData)  |  クライアントに指定されたカスタム データを設定します。
public const std::string& GetLocale() const  |  エンジン データが書き込まれるロケールを取得します。
public void SetCustomSettings (const std:: vector \<std::pair\<std::string, std::string\> \>& value)  |  テストや実験に使用する名前と値のペアを設定します。
public const std:: vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings () const  |  テストや実験に使用する名前と値のペアを取得します。
public void SetSessionId(const std::string& sessionId)  |  ログ/テレメトリの相関関係に使用する、エンジンのセッション ID を設定します。
public const std::string& GetSessionId() const  |  エンジンのセッション ID を取得します。
パブリック void SetCloud (クラウドクラウド)  |  必要に応じて、ターゲットクラウドを設定します。
パブリッククラウドの GetCloud () const  |  すべてのサービス要求によって使用されるターゲットクラウドを取得します。
public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  カスタムクラウドのクラウドエンドポイントベース URL を設定します。
public const std::string& GetCloudEndpointBaseUrl() const  |  すべてのサービス要求で使用されるクラウド ベースの URL を取得します (指定されている場合)。
public void SetAuthDelegate (const std:: shared_ptr \<AuthDelegate\>& authdelegate)  |  エンジン認証デリゲートを設定します。
public std::shared_ptr\<AuthDelegate\> GetAuthDelegate() const  |  エンジン認証デリゲートを取得します。
public const std:: string& GetUnderlyingApplicationId () const  |  基になるアプリケーション ID を取得します。
public void SetUnderlyingApplicationId (const std:: string& underlyingApplicationId)  |  基になるアプリケーション ID を設定します。
  
## <a name="members"></a>メンバー
  
### <a name="settings-function"></a>Settings 関数
新しいエンジンを作成するための ProtectionEngine::Settings コンストラクター。

パラメーター:  
* **identity**: ProtectionEngine に関連付けられる ID


* **Authdelegate**: 認証トークンを取得するために SDK によって使用される認証デリゲートは、両方が指定されている場合は policyprofile:: Settings:: authdelegate をオーバーライドします 


* **clientData**: アンロード時にエンジンと共に保存でき、読み込まれたエンジンから取得できる、カスタマイズ可能なクライアント データ。 


* **locale**: エンジン出力はこのロケールで提供されます。


  
### <a name="settings-function"></a>Settings 関数
既存のエンジンを読み込むための ProtectionEngine::Settings コンストラクター。

パラメーター:  
* **engineId**: 読み込まれるエンジンの一意識別子 


* **Authdelegate**: 認証トークンを取得するために SDK によって使用される認証デリゲートは、両方が指定されている場合は policyprofile:: Settings:: authdelegate をオーバーライドします 


* **clientData**: アンロード時にエンジンと共に保存でき、読み込まれたエンジンから取得できる、カスタマイズ可能なクライアント データ。 


* **locale**: エンジン出力はこのロケールで提供されます。


  
### <a name="getengineid-function"></a>GetEngineId 関数
エンジン ID を取得します。

  
**戻り値**: エンジン ID
  
### <a name="setengineid-function"></a>SetEngineId 関数
エンジン ID を設定します。

パラメーター:  
* **engineId**: エンジン ID。


  
### <a name="getidentity-function"></a>GetIdentity 関数
エンジンに関連付けられたユーザー ID を取得します。

  
**戻り値**: エンジンに関連付けられたユーザー ID
  
### <a name="setidentity-function"></a>SetIdentity 関数
エンジンに関連付けられるユーザー ID を設定します。

パラメーター:  
* **identity**: エンジンに関連付けられるユーザー ID


  
### <a name="getclientdata-function"></a>GetClientData 関数
クライアントに指定されたカスタム データを取得します。

  
**戻り値** クライアントに指定されたカスタム データ
  
### <a name="setclientdata-function"></a>SetClientData 関数
クライアントに指定されたカスタム データを設定します。

パラメーター:  
* **Custom**: クライアントに指定されたデータ


  
### <a name="getlocale-function"></a>GetLocale 関数
エンジン データが書き込まれるロケールを取得します。

  
**戻り値**: エンジン データが書き込まれるロケール
  
### <a name="setcustomsettings-function"></a>SetCustomSettings 関数
テストや実験に使用する名前と値のペアを設定します。

パラメーター:  
* **customSettings**: テストや実験に使用する名前と値のペア


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
テストや実験に使用する名前と値のペアを取得します。

  
**戻り値**: テストや実験に使用する名前と値のペア
  
### <a name="setsessionid-function"></a>SetSessionId 関数
ログ/テレメトリの相関関係に使用する、エンジンのセッション ID を設定します。

パラメーター:  
* **sessionId**: ログ/テレメトリの関連付けに使用されるエンジンセッション ID


  
### <a name="getsessionid-function"></a>GetSessionId 関数
エンジンのセッション ID を取得します。

  
**戻り値**: エンジンのセッション ID
  
### <a name="setcloud-function"></a>SetCloud 関数
必要に応じて、ターゲットクラウドを設定します。

パラメーター:  
* **クラウド**: クラウド


クラウドが指定されていない場合は、可能であれば、エンジンの id ドメインの DNS 参照によって決定されます。それ以外の場合は、グローバルクラウドにフォールバックします。
  
### <a name="getcloud-function"></a>GetCloud 関数
すべてのサービス要求によって使用されるターゲットクラウドを取得します。

  
**返される値**: クラウド
  
### <a name="setcloudendpointbaseurl-function"></a>SetCloudEndpointBaseUrl 関数
カスタムクラウドのクラウドエンドポイントベース URL を設定します。

パラメーター:  
* **cloudEndpointBaseUrl**: すべてのサービス要求で使用されるベース URL (たとえば、"https://api.aadrm.com")


この値は読み取り専用であり、Cloud = Custom に設定されている必要があります
  
### <a name="getcloudendpointbaseurl-function"></a>GetCloudEndpointBaseUrl 関数
すべてのサービス要求で使用されるクラウド ベースの URL を取得します (指定されている場合)。

  
**戻り値**: ベース URL
  
### <a name="setauthdelegate-function"></a>SetAuthDelegate 関数
エンジン認証デリゲートを設定します。

パラメーター:  
* **authdelegate**: Auth デリゲート


  
### <a name="getauthdelegate-function"></a>GetAuthDelegate 関数
エンジン認証デリゲートを取得します。

  
**戻り値**: エンジンの認証デリゲート。
  
### <a name="getunderlyingapplicationid-function"></a>GetUnderlyingApplicationId 関数
基になるアプリケーション ID を取得します。

  
**戻り値**: 基になるアプリケーション ID
  
### <a name="setunderlyingapplicationid-function"></a>SetUnderlyingApplicationId 関数
基になるアプリケーション ID を設定します。

パラメーター:  
* **UnderlyingApplicationId**: 基になるアプリケーション ID。

