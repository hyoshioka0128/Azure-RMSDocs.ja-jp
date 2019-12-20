---
title: class mip::PolicyProfile
description: Microsoft Information Protection (MIP) SDK の mip::p olicyprofile クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 8feb0b93982a00c4843ea914f969ef27cf8e5ca2
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560907"
---
# <a name="class-mippolicyprofile"></a>class mip::PolicyProfile 
PolicyProfile クラスは、Microsoft Information Protection 操作を使用するためのルートクラスです。 一般的なアプリケーションで必要な PolicyProfile は1つだけですが、必要に応じて複数のプロファイルを作成できます。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  プロファイルに設定されている設定値を取得します。
public void ListEnginesAsync (const std:: shared_ptr\<void\>& context)  |  エンジンの一覧操作を開始します。
public std:: vector\<std:: string\> ListEngines ()  |  エンジンの一覧。
public void UnloadEngineAsync (const std:: string & id、const std:: shared_ptr\<void\>& context)  |  指定した ID を持つポリシー エンジンのアンロードを開始します。
public void UnloadEngine (const std:: string & id)  |  指定した ID を持つポリシー エンジンのアンロードを開始します。
public void AddEngineAsync (const PolicyEngine:: Settings & settings, const std:: shared_ptr\<void\>& context)  |  プロファイルへの新しいポリシー エンジンの追加を開始します。
public std:: shared_ptr\<PolicyEngine\> AddEngine (const PolicyEngine:: Settings & settings、const std:: shared_ptr\<void\>& context)  |  プロファイルに新しいポリシーエンジンを追加します。
public void DeleteEngineAsync (const std:: string & id、const std:: shared_ptr\<void\>& context)  |  指定した ID を持つポリシー エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。
public void DeleteEngine(const std::string& engineId)  |  指定された ID を持つポリシーエンジンを削除します。 指定したエンジンのすべてのデータが削除されます。
public static MIP_API void __CDECL MIP::P olicyProfile:: LoadAsync | 指定された設定に基づいて、プロファイルの読み込みを開始します。
public static const MIP_API char * __CDECL MIP::P olicyProfile:: GetVersion | ライブラリのバージョンを取得する

## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
プロファイルに設定されている設定値を取得します。

  
**戻り値**: プロファイルに設定されている設定値。
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 関数
エンジンの一覧操作を開始します。

パラメーター:  
* **context**: オブザーバー関数に渡されるパラメーター。 


PolicyProfile:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="listengines-function"></a>ListEngines 関数
エンジンの一覧。

  
**戻り値**: キャッシュされたエンジン ID
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync 関数
指定した ID を持つポリシー エンジンのアンロードを開始します。

パラメーター:  
* **id**: 一意のエンジン ID。 


* **context**: オブザーバー関数に不透明に転送されるパラメーター。 


PolicyProfile:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="unloadengine-function"></a>UnloadEngine 関数
指定した ID を持つポリシー エンジンのアンロードを開始します。

パラメーター:  
* **id**: 一意のエンジン ID。


  
### <a name="addengineasync-function"></a>AddEngineAsync 関数
プロファイルへの新しいポリシー エンジンの追加を開始します。

パラメーター:  
* **設定**: エンジンの設定を指定する mip::P olicyEngine:: settings オブジェクト。 


* **context**: オブザーバー関数とオプションの httpdelegate に不透明するために指定されたパラメーター。 


PolicyProfile:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="addengine-function"></a>AddEngine 関数
プロファイルに新しいポリシーエンジンを追加します。

パラメーター:  
* **設定**: エンジンの設定を指定する mip::P olicyEngine:: settings オブジェクト。 


* **context**: オプションの httpdelegate に不透明転送されるパラメーター



  
**戻り値**: 新しく作成された policyengine
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 関数
指定した ID を持つポリシー エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。

パラメーター:  
* **id**: 一意のエンジン ID。 


* **context**: オブザーバー関数に渡されるパラメーター。 


PolicyProfile:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="deleteengine-function"></a>DeleteEngine 関数
指定された ID を持つポリシーエンジンを削除します。 指定したエンジンのすべてのデータが削除されます。

パラメーター:  
* **id**: 一意のエンジン ID。

### <a name="loadasync-function"></a>LoadAsync 関数
指定された設定に基づいて、プロファイルの読み込みを開始します。

パラメーター:  
* **設定**: プロファイルオブジェクトの読み込みに使用されるプロファイル設定。 </para>
* **context**: オブザーバー関数に渡されるコンテキストパラメーター。

### <a name="getversion-function"></a>GetVersion 関数
ライブラリのバージョンを取得する

は、バージョン文字列を**返し**ます。