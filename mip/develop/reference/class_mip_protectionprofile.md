---
title: クラス ProtectionProfile
description: 'Microsoft Information Protection (MIP) SDK の protectionprofile:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: d3a2f02a0dab5bba9b74b264348bcfd7e073f783
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81764412"
---
# <a name="class-protectionprofile"></a>クラス ProtectionProfile 
ProtectionProfile は、保護操作を実行するためのルート クラスです。
アプリケーションでは、保護操作を実行する前に ProtectionProfile を作成する必要があります
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  初期化時および有効期間全体にわたって ProtectionProfile によって使用される設定を取得します。
public std:: shared_ptr\<asynccontrol\> ListEnginesAsync (const std:: shared_ptr\<void\>& context)  |  エンジンの一覧操作を開始します。
public std:: vector\<std:: string\> listengines ()  |  エンジンを一覧表示します。
public std:: shared_ptr\<asynccontrol\> AddEngineAsync (const protectionengine:: settings& settings, const std:: shared_ptr\<void\>& context)  |  プロファイルへの新しい保護エンジンの追加を開始します。
public std:: shared_ptr\<protectionengine\> Addengine (const protectionengine:: settings& settings)  |  プロファイルに新しい保護エンジンを追加します。
public std:: shared_ptr\<asynccontrol\> DeleteEngineAsync (const std:: string& engineId、const std:: shared_ptr\<void\>& context)  |  指定した ID を持つ保護エンジンの削除を開始します。 指定したエンジンのすべてのデータが削除されます。
public void DeleteEngine(const std::string& engineId)  |  指定した ID を持つ保護エンジンを削除します。 指定したエンジンのすべてのデータが削除されます。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
初期化時および有効期間全体にわたって ProtectionProfile によって使用される設定を取得します。

  
**戻り値**: の初期化中および有効期間全体にわたって protectionprofile によって使用される設定
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 関数
エンジンの一覧操作を開始します。

パラメーター:  
* **context**: オブザーバーに不透明に返されるクライアント コンテキスト



  
**戻り値**: Async control オブジェクト。
[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="listengines-function"></a>ListEngines 関数
エンジンを一覧表示します。

  
**戻り値**: キャッシュされたエンジン ID
  
### <a name="addengineasync-function"></a>AddEngineAsync 関数
プロファイルへの新しい保護エンジンの追加を開始します。

パラメーター:  
* **settings**: エンジンの設定を指定する mip::ProtectionEngine::Settings オブジェクト。 


* **context**: オブザーバーに不透明に返されるクライアント コンテキスト



  
**戻り値**: Async control オブジェクト。
ProtectionProfile::Observer は成功または失敗時に呼び出されます。
  
### <a name="addengine-function"></a>AddEngine 関数
プロファイルに新しい保護エンジンを追加します。

パラメーター:  
* **settings**: エンジンの設定を指定する mip::ProtectionEngine::Settings オブジェクト。



  
**戻り値**: 新しく作成された ProtectionEngine
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 関数
指定した ID を持つ保護エンジンの削除を開始します。 指定したエンジンのすべてのデータが削除されます。

パラメーター:  
* **id**: 一意のエンジン id。 


* **context**: オブザーバーに不透明に返されるクライアント コンテキスト



  
**戻り値**: Async control オブジェクト。
ProtectionProfile::Observer は成功または失敗時に呼び出されます。
  
### <a name="deleteengine-function"></a>DeleteEngine 関数
指定した ID を持つ保護エンジンを削除します。 指定したエンジンのすべてのデータが削除されます。

パラメーター:  
* **id**: 一意のエンジン id。

