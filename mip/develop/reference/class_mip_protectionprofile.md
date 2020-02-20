---
title: class mip::ProtectionProfile
description: Microsoft Information Protection (MIP) SDK の mip::p rotectionprofile クラスについて説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 14d52de8ff87a75aaf2c777eb55c427bbde72a12
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77486734"
---
# <a name="class-mipprotectionprofile"></a>class mip::ProtectionProfile 
ProtectionProfile は、保護操作を実行するためのルートクラスです。
アプリケーションは、保護操作を実行する前に ProtectionProfile を作成する必要があります。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  初期化中および有効期間全体にわたって ProtectionProfile によって使用される設定を取得します。
public std:: shared_ptr\<AsyncControl\> ListEnginesAsync (const std:: shared_ptr\<void\>& context)  |  エンジンの一覧操作を開始します。
public std:: vector\<std:: string\> ListEngines ()  |  エンジンを一覧表示します。
public std:: shared_ptr\<AsyncControl\> AddEngineAsync (const ProtectionEngine:: Settings & Settings, const std:: shared_ptr\<void\>& context)  |  プロファイルへの新しい保護エンジンの追加を開始します。
public std:: shared_ptr\<ProtectionEngine\> AddEngine (const ProtectionEngine:: Settings & settings)  |  プロファイルに新しい保護エンジンを追加します。
public std:: shared_ptr\<AsyncControl\> DeleteEngineAsync (const std:: string & engineId、const std:: shared_ptr\<void\>& context)  |  指定した ID を持つ保護エンジンの削除を開始します。 指定したエンジンのすべてのデータが削除されます。
public void DeleteEngine(const std::string& engineId)  |  指定した ID を持つ保護エンジンを削除します。 指定したエンジンのすべてのデータが削除されます。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
初期化中および有効期間全体にわたって ProtectionProfile によって使用される設定を取得します。

  
**戻り値**: の初期化中および有効期間全体にわたって protectionprofile によって使用される設定
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 関数
エンジンの一覧操作を開始します。

パラメータ:  
* **context**: オブザーバーに不透明に返されるクライアント コンテキスト



  
**戻り値**: Async control オブジェクト。
ProtectionProfile:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="listengines-function"></a>ListEngines 関数
エンジンを一覧表示します。

  
**戻り値**: キャッシュされたエンジン ID
  
### <a name="addengineasync-function"></a>AddEngineAsync 関数
プロファイルへの新しい保護エンジンの追加を開始します。

パラメータ:  
* **設定**: エンジンの設定を指定する mip::P rotectionengine:: settings オブジェクト。 


* **context**: オブザーバーに不透明に返されるクライアント コンテキスト



  
**戻り値**: Async control オブジェクト。
ProtectionProfile:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="addengine-function"></a>AddEngine 関数
プロファイルに新しい保護エンジンを追加します。

パラメータ:  
* **設定**: エンジンの設定を指定する mip::P rotectionengine:: settings オブジェクト。



  
**戻り値**: 新しく作成された protectionengine
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 関数
指定した ID を持つ保護エンジンの削除を開始します。 指定したエンジンのすべてのデータが削除されます。

パラメータ:  
* **id**: 一意のエンジン ID。 


* **context**: オブザーバーに不透明に返されるクライアント コンテキスト



  
**戻り値**: Async control オブジェクト。
ProtectionProfile:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="deleteengine-function"></a>DeleteEngine 関数
指定した ID を持つ保護エンジンを削除します。 指定したエンジンのすべてのデータが削除されます。

パラメータ:  
* **id**: 一意のエンジン ID。

