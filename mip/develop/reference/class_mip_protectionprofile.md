---
title: class mip ProtectionProfile
description: class mip ProtectionProfile のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a7dffb4a6b1490ef185eb9a5062f394f4509f00a
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446687"
---
# <a name="class-mipprotectionprofile"></a>class mip::ProtectionProfile 
[ProtectionProfile](class_mip_protectionprofile.md) は、保護操作を実行するためのルート クラスです。
アプリケーションでは、保護操作を実行する前に [ProtectionProfile](class_mip_protectionprofile.md) を作成する必要があります
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  初期化時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される設定を取得します。
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  エンジンの一覧操作を開始します。
public std::vector<std::string> ListEngines()  |  エンジンを一覧表示します。
public void AddEngineAsync(const ProtectionEngine::Settings& settings, const std::shared_ptr<void>& context)  |  プロファイルへの新しい保護エンジンの追加を開始します。
public std::shared_ptr<ProtectionEngine> AddEngine(const ProtectionEngine::Settings& settings)  |  プロファイルに新しい保護エンジンを追加します。
public void DeleteEngineAsync(const std::string& engineId, const std::shared_ptr<void>& context)  |  指定した ID を持つ保護エンジンの削除を開始します。 指定したエンジンのすべてのデータが削除されます。
 public void DeleteEngine(const std::string& engineId)  |  指定した ID を持つ保護エンジンを削除します。 指定したエンジンのすべてのデータが削除されます。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
初期化時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される設定を取得します。

  
**戻り値**: 初期化時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される [Settings](class_mip_protectionprofile_settings.md)
  
### <a name="listenginesasync"></a>ListEnginesAsync
エンジンの一覧操作を開始します。

パラメーター:  
* **context**: オブザーバーに不透明に返されるクライアント コンテキスト


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="listengines"></a>ListEngines
エンジンを一覧表示します。

  
**戻り値**: キャッシュされたエンジン ID
  
### <a name="addengineasync"></a>AddEngineAsync
プロファイルへの新しい保護エンジンの追加を開始します。

パラメーター:  
* **settings**: エンジンの設定を指定する [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) オブジェクト。 


* **context**: オブザーバーに不透明に返されるクライアント コンテキスト


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="protectionengine"></a>ProtectionEngine
プロファイルに新しい保護エンジンを追加します。

パラメーター:  
* **settings**: エンジンの設定を指定する [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) オブジェクト。



  
**戻り値**: 新しく作成された [ProtectionEngine](class_mip_protectionengine.md)
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
指定した ID を持つ保護エンジンの削除を開始します。 指定したエンジンのすべてのデータが削除されます。

パラメーター:  
* **id**: 一意のエンジン ID。 


* **context**: オブザーバーに不透明に返されるクライアント コンテキスト


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="deleteengine"></a>DeleteEngine
指定した ID を持つ保護エンジンを削除します。 指定したエンジンのすべてのデータが削除されます。

パラメーター:  
* **id**: 一意のエンジン ID。

