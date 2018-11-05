---
title: class mip ProtectionEngine Settings
description: class mip ProtectionEngine Settings のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: f61e86a87ecfea21bc9d02f4e55f3fbe663e9b80
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446704"
---
# <a name="class-mipprotectionenginesettings"></a>class mip::ProtectionEngine::Settings 
作成時および有効期間全体にわたって [ProtectionEngine](class_mip_protectionengine.md) によって使用される[設定](class_mip_protectionengine_settings.md)。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public Settings(const Identity& identity, const std::string& clientData, const std::string& locale)  |  新しいエンジンを作成するための [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) コンストラクター。
 public Settings(const std::string& engineId, const std::string& clientData, const std::string& locale)  |  既存のエンジンを読み込むための [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) コンストラクター。
 public const std::string& GetEngineId() const  |  エンジン ID を取得します。
 public void SetEngineId(const std::string& engineId)  |  エンジン ID を設定します。
 public const Identity& GetIdentity() const  |  エンジンに関連付けられたユーザー ID を取得します。
 public void SetIdentity(const Identity& identity)  |  エンジンに関連付けられるユーザー ID を設定します。
 public const std::string& GetClientData() const  |  クライアントに指定されたカスタム データを取得します。
 public void SetClientData(const std::string& clientData)  |  クライアントに指定されたカスタム データを設定します。
 public const std::string& GetLocale() const  |  エンジン データが書き込まれるロケールを取得します。
public void SetCustomSettings(const std::vector<std::pair<std::string, std::string>>& value)  |  テストや実験に使用する名前と値のペアを設定します。
public const std::vector<std::pair<std::string, std::string>>& GetCustomSettings() const  |  テストや実験に使用する名前と値のペアを取得します。
 public void SetSessionId(const std::string& sessionId)  |  ログ/テレメトリの相関関係に使用する、エンジンのセッション ID を設定します。
 public const std::string& GetSessionId() const  |  エンジンのセッション ID を取得します。
 public void SetCloudEndpointBaseUrl(const std::string& cloudEndpointBaseUrl)  |  必要に応じて、クラウド エンドポイントのベース URL を設定します。
 public const std::string& GetCloudEndpointBaseUrl() const  |  すべてのサービス要求で使用されるクラウド ベースの URL を取得します (指定されている場合)。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
新しいエンジンを作成するための [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) コンストラクター。

パラメーター:  
* **identity**: [ProtectionEngine](class_mip_protectionengine.md) に関連付けられる ID


* **clientData**: アンロード時にエンジンと共に保存でき、読み込まれたエンジンから取得できる、カスタマイズ可能なクライアント データ。 


* **locale**: エンジン出力はこのロケールで提供されます。


  
### <a name="settings"></a>Settings
既存のエンジンを読み込むための [ProtectionEngine::Settings](class_mip_protectionengine_settings.md) コンストラクター。

パラメーター:  
* **engineId**: 読み込まれるエンジンの一意識別子 


* **clientData**: アンロード時にエンジンと共に保存でき、読み込まれたエンジンから取得できる、カスタマイズ可能なクライアント データ。 


* **locale**: エンジン出力はこのロケールで提供されます。


  
### <a name="getengineid"></a>GetEngineId
エンジン ID を取得します。

  
**戻り値**: エンジン ID
  
### <a name="setengineid"></a>SetEngineId
エンジン ID を設定します。

パラメーター:  
* **engineId**: エンジン ID。


  
### <a name="getidentity"></a>GetIdentity
エンジンに関連付けられたユーザー ID を取得します。

  
**戻り値**: エンジンに関連付けられたユーザー ID
  
### <a name="setidentity"></a>SetIdentity
エンジンに関連付けられるユーザー ID を設定します。

パラメーター:  
* **identity**: エンジンに関連付けられるユーザー ID


  
### <a name="getclientdata"></a>GetClientData
クライアントに指定されたカスタム データを取得します。

  
**戻り値** クライアントに指定されたカスタム データ
  
### <a name="setclientdata"></a>SetClientData
クライアントに指定されたカスタム データを設定します。

パラメーター:  
* **Custom**: クライアントに指定されたデータ


  
### <a name="getlocale"></a>GetLocale
エンジン データが書き込まれるロケールを取得します。

  
**戻り値**: エンジン データが書き込まれるロケール
  
### <a name="setcustomsettings"></a>SetCustomSettings
テストや実験に使用する名前と値のペアを設定します。

パラメーター:  
* **customSettings**: テストや実験に使用する名前と値のペア


  
### <a name="getcustomsettings"></a>GetCustomSettings
テストや実験に使用する名前と値のペアを取得します。

  
**戻り値**: テストや実験に使用する名前と値のペア
  
### <a name="setsessionid"></a>SetSessionId
ログ/テレメトリの相関関係に使用する、エンジンのセッション ID を設定します。

パラメーター:  
* **sessionId**: ログ/テレメトリの相関関係に使用する、エンジンのセッション ID


  
### <a name="getsessionid"></a>GetSessionId
エンジンのセッション ID を取得します。

  
**戻り値**: エンジンのセッション ID
  
### <a name="setcloudendpointbaseurl"></a>SetCloudEndpointBaseUrl
必要に応じて、クラウド エンドポイントのベース URL を設定します。

パラメーター:  
* **cloudEndpointBaseUrl**: すべてのサービス要求で使用されるベース URL (たとえば、"https://api.aadrm.com")


ベース URL が指定されていない場合は、エンジン ID のドメインの DNS 参照によって決定されます。
  
### <a name="getcloudendpointbaseurl"></a>GetCloudEndpointBaseUrl
すべてのサービス要求で使用されるクラウド ベースの URL を取得します (指定されている場合)。

  
**戻り値**: ベース URL