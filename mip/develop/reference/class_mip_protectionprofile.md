---
title: class mip::ProtectionProfile
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionprofile クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: dcd50c403f20486e479fc00016ed6c0ef8885efa
ms.sourcegitcommit: 9cedac6569f3a33a22a721da27074a438b1a7882
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71070493"
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
public static MIP_API void __CDECL MIP::P rotectionProfile:: LoadAsync | 初期化中および有効期間全体にわたって ProtectionProfile によって使用される設定
public static MIP_API std:: shared_ptr&lt;protectionprofile&gt; __cdecl MIP::P rotectionprofile:: Load | 指定された設定に基づいてプロファイルを読み込んでいます。
public static const MIP_API char * __CDECL MIP::P rotectionProfile:: GetVersion | ライブラリのバージョンを取得します。
public static MIP_API std:: shared_ptr&lt;発行 licenseinfo&gt; __cdecl MIP::P rotectionprofile:: get licenseinfo | 発行ライセンスの詳細のホルダーを作成し、保護ハンドラーを作成するために使用できます。 


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

### <a name="loadasync-function"></a>LoadAsync 関数
初期化中および有効期間全体にわたって ProtectionProfile によって使用される設定 

[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) は成功または失敗時に呼び出されます。

パラメーター:
* **設定**:初期化中および有効期間全体にわたって ProtectionProfile によって使用される設定。
* **コンテキスト**:この同じコンテキストは、ProtectionProfile:: Observer:: OnLoadSuccess または ProtectionProfile:: Observer:: Onloadsuccess にそのように転送されます。

### <a name="load-function"></a>Load 関数
指定された設定に基づいてプロファイルを読み込んでいます。

[ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) は成功または失敗時に呼び出されます。

パラメーター:
* **設定**:初期化中および有効期間全体にわたって ProtectionProfile によって使用される設定。

次の**値を返し**ます。新しく作成されたプロファイル。

### <a name="getversion-function"></a>GetVersion 関数
ライブラリのバージョンを取得します。 

次の**値を返し**ます。ライブラリのバージョン。

### <a name="getpublishinglicenseinfo-function"></a>Get発行 Licenseinfo 関数
発行ライセンスの詳細のホルダーを作成し、保護ハンドラーを作成するために使用できます。 

パラメーター:
* **serializedPublishingLicense**:シリアル化された公開ライセンス。

次の**値を返し**ます。発行ライセンスの詳細のホルダー 
