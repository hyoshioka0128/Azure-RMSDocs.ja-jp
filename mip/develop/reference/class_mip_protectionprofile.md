---
title: class mip::ProtectionProfile
description: Mip::protectionprofile クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: d789250d2ab91ca6e65181e216f260db8d44d496
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184367"
---
# <a name="class-mipprotectionprofile"></a>class mip::ProtectionProfile 
[ProtectionProfile](class_mip_protectionprofile.md) は、保護操作を実行するためのルート クラスです。
アプリケーションでは、保護操作を実行する前に [ProtectionProfile](class_mip_protectionprofile.md) を作成する必要があります
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  初期化時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される設定を取得します。
public void ListEnginesAsync(const std::shared_ptr\<void\>& context)  |  エンジンの一覧操作を開始します。
public std::vector\<std::string\> ListEngines()  |  エンジンを一覧表示します。
public void AddEngineAsync(const ProtectionEngine::Settings& settings, const std::shared_ptr\<void\>& context)  |  プロファイルへの新しい保護エンジンの追加を開始します。
public std::shared_ptr\<ProtectionEngine\> AddEngine(const ProtectionEngine::Settings& settings)  |  プロファイルに新しい保護エンジンを追加します。
public void DeleteEngineAsync(const std::string& engineId, const std::shared_ptr\<void\>& context)  |  指定した ID を持つ保護エンジンの削除を開始します。 指定したエンジンのすべてのデータが削除されます。
public void DeleteEngine(const std::string& engineId)  |  指定した ID を持つ保護エンジンを削除します。 指定したエンジンのすべてのデータが削除されます。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
初期化時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される設定を取得します。

  
**返します**:初期化時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される[設定](class_mip_protectionprofile_settings.md)
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 関数
エンジンの一覧操作を開始します。

パラメーター:  
* **コンテキスト**:オブザーバーに不透明渡されるクライアント コンテキスト


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="listengines-function"></a>ListEngines 関数
エンジンを一覧表示します。

  
**返します**:キャッシュされたエンジン Id
  
### <a name="addengineasync-function"></a>AddEngineAsync 関数
プロファイルへの新しい保護エンジンの追加を開始します。

パラメーター:  
* **settings**: エンジンの設定を指定する [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) オブジェクト。 


* **コンテキスト**:オブザーバーに不透明渡されるクライアント コンテキスト


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="addengine-function"></a>AddEngine 関数
プロファイルに新しい保護エンジンを追加します。

パラメーター:  
* **settings**: エンジンの設定を指定する [mip::ProtectionEngine::Settings](class_mip_protectionengine_settings.md) オブジェクト。



  
**返します**:新しく作成された[ProtectionEngine](class_mip_protectionengine.md)
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 関数
指定した ID を持つ保護エンジンの削除を開始します。 指定したエンジンのすべてのデータが削除されます。

パラメーター:  
* **id**: 一意のエンジン ID。 


* **コンテキスト**:オブザーバーに不透明渡されるクライアント コンテキスト


[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="deleteengine-function"></a>DeleteEngine 関数
指定した ID を持つ保護エンジンを削除します。 指定したエンジンのすべてのデータが削除されます。

パラメーター:  
* **id**: 一意のエンジン ID。

