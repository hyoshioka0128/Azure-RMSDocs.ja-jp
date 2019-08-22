---
title: class mip::ProtectionProfile
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionprofile クラスについて説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: cc69e167a5b5a8dc46157443c13d70732ace62c0
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883322"
---
# <a name="class-mipprotectionprofile"></a>class mip::ProtectionProfile 
[ProtectionProfile](class_mip_protectionprofile.md) は、保護操作を実行するためのルート クラスです。
アプリケーションでは、保護操作を実行する前に [ProtectionProfile](class_mip_protectionprofile.md) を作成する必要があります
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  初期化時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される設定を取得します。
public void ListEnginesAsync (const std:: shared_ptr\<void\>& context)  |  エンジンの一覧操作を開始します。
public std:: vector\<std:: string\> listengines ()  |  エンジンを一覧表示します。
public void AddEngineAsync (const protectionengine:: settings & settings, const std:: shared_ptr\<void\>& context)  |  プロファイルへの新しい保護エンジンの追加を開始します。
public std:: shared_ptr\<protectionengine\> addengine (const protectionengine:: settings & settings)  |  プロファイルに新しい保護エンジンを追加します。
public void DeleteEngineAsync (const std:: string & engineId、const std:: shared_ptr\<void\>& context)  |  指定した ID を持つ保護エンジンの削除を開始します。 指定したエンジンのすべてのデータが削除されます。
public void DeleteEngine(const std::string& engineId)  |  指定した ID を持つ保護エンジンを削除します。 指定したエンジンのすべてのデータが削除されます。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
初期化時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される設定を取得します。

  
次の**値を返し**ます。初期化時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される[設定](class_mip_protectionprofile_settings.md)
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 関数
エンジンの一覧操作を開始します。

パラメーター:  
* **コンテキスト**:オブザーバーに戻される不透明クライアントコンテキスト


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="listengines-function"></a>ListEngines 関数
エンジンを一覧表示します。

  
次の**値を返し**ます。キャッシュされたエンジン Id
  
### <a name="addengineasync-function"></a>AddEngineAsync 関数
プロファイルへの新しい保護エンジンの追加を開始します。

パラメーター:  
* **settings**: エンジンの設定を指定する [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) オブジェクト。 


* **コンテキスト**:オブザーバーに戻される不透明クライアントコンテキスト


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="addengine-function"></a>AddEngine 関数
プロファイルに新しい保護エンジンを追加します。

パラメーター:  
* **settings**: エンジンの設定を指定する [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) オブジェクト。



  
次の**値を返し**ます。新しく作成された[Protectionengine](class_mip_protectionengine.md)
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 関数
指定した ID を持つ保護エンジンの削除を開始します。 指定したエンジンのすべてのデータが削除されます。

パラメーター:  
* **id**: 一意のエンジン ID。 


* **コンテキスト**:オブザーバーに戻される不透明クライアントコンテキスト


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="deleteengine-function"></a>DeleteEngine 関数
指定した ID を持つ保護エンジンを削除します。 指定したエンジンのすべてのデータが削除されます。

パラメーター:  
* **id**: 一意のエンジン ID。

