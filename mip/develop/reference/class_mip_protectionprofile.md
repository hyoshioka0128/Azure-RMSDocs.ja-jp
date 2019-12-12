---
title: class mip::ProtectionProfile
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionprofile クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: a6c78e7311f3af3920df19d7a3a6ca92bb09e819
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560050"
---
# <a name="class-mipprotectionprofile"></a>class mip::ProtectionProfile 
ProtectionProfile は、保護操作を実行するためのルートクラスです。
アプリケーションは、保護操作を実行する前に ProtectionProfile を作成する必要があります。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  初期化中および有効期間全体にわたって ProtectionProfile によって使用される設定を取得します。
public void ListEnginesAsync (const std:: shared_ptr\<void\>& context)  |  エンジンの一覧操作を開始します。
public std:: vector\<std:: string\> ListEngines ()  |  エンジンを一覧表示します。
public void AddEngineAsync (const ProtectionEngine:: Settings & settings, const std:: shared_ptr\<void\>& context)  |  プロファイルへの新しい保護エンジンの追加を開始します。
public std:: shared_ptr\<ProtectionEngine\> AddEngine (const ProtectionEngine:: Settings & settings)  |  プロファイルに新しい保護エンジンを追加します。
public void DeleteEngineAsync (const std:: string & engineId、const std:: shared_ptr\<void\>& context)  |  指定した ID を持つ保護エンジンの削除を開始します。 指定したエンジンのすべてのデータが削除されます。
public void DeleteEngine(const std::string& engineId)  |  指定した ID を持つ保護エンジンを削除します。 指定したエンジンのすべてのデータが削除されます。
public static MIP_API void __CDECL MIP::P rotectionProfile:: LoadAsync | 初期化中および有効期間全体にわたって ProtectionProfile によって使用される設定
public static MIP_API std:: shared_ptr&lt;ProtectionProfile&gt; __CDECL MIP::P rotectionProfile:: Load | 指定された設定に基づいてプロファイルを読み込んでいます。
public static const MIP_API char * __CDECL MIP::P rotectionProfile:: GetVersion | ライブラリのバージョンを取得します。
public static MIP_API std:: shared_ptr&lt;発行 Licenseinfo&gt; __CDECL MIP::P rotectionProfile:: Get発行 Licenseinfo | 発行ライセンスの詳細のホルダーを作成し、保護ハンドラーを作成するために使用できます。 

## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
初期化中および有効期間全体にわたって ProtectionProfile によって使用される設定を取得します。

  
**戻り値**: の初期化中および有効期間全体にわたって protectionprofile によって使用される設定
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 関数
エンジンの一覧操作を開始します。

パラメーター:  
* **context**: オブザーバーに不透明に返されるクライアント コンテキスト


ProtectionProfile:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="listengines-function"></a>ListEngines 関数
エンジンを一覧表示します。

  
**戻り値**: キャッシュされたエンジン ID
  
### <a name="addengineasync-function"></a>AddEngineAsync 関数
プロファイルへの新しい保護エンジンの追加を開始します。

パラメーター:  
* **設定**: エンジンの設定を指定する mip::P rotectionengine:: settings オブジェクト。 


* **context**: オブザーバーに不透明に返されるクライアント コンテキスト


ProtectionProfile:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="addengine-function"></a>AddEngine 関数
プロファイルに新しい保護エンジンを追加します。

パラメーター:  
* **設定**: エンジンの設定を指定する mip::P rotectionengine:: settings オブジェクト。



  
**戻り値**: 新しく作成された protectionengine
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 関数
指定した ID を持つ保護エンジンの削除を開始します。 指定したエンジンのすべてのデータが削除されます。

パラメーター:  
* **id**: 一意のエンジン ID。 


* **context**: オブザーバーに不透明に返されるクライアント コンテキスト


ProtectionProfile:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="deleteengine-function"></a>DeleteEngine 関数
指定した ID を持つ保護エンジンを削除します。 指定したエンジンのすべてのデータが削除されます。

パラメーター:  
* **id**: 一意のエンジン ID。

### <a name="loadasync-function"></a>LoadAsync 関数
初期化中および有効期間全体にわたって ProtectionProfile によって使用される設定 

[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) は成功または失敗時に呼び出されます。

パラメーター:
* **設定**: 初期化中および有効期間全体にわたって protectionprofile によって使用される設定。
* **コンテキスト**: この同じコンテキストは、protectionprofile:: observer:: OnLoadSuccess または protectionprofile:: observer:: Onloadsuccess にそのように転送されます。

### <a name="load-function"></a>Load 関数
指定された設定に基づいてプロファイルを読み込んでいます。

[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) は成功または失敗時に呼び出されます。

パラメーター:
* **設定**: 初期化中および有効期間全体にわたって protectionprofile によって使用される設定。

は、新しく作成されたプロファイル**を返し**ます。

### <a name="getversion-function"></a>GetVersion 関数
ライブラリのバージョンを取得します。 

**戻り値**: ライブラリのバージョン。

### <a name="getpublishinglicenseinfo-function"></a>Get発行 Licenseinfo 関数
発行ライセンスの詳細のホルダーを作成し、保護ハンドラーを作成するために使用できます。 

パラメーター:
* **serializedPublishingLicense**: シリアル化された公開ライセンス。

**を返し**ます: 発行ライセンスの詳細のホルダー 