---
title: class mip::PolicyProfile
description: Microsoft Information Protection (MIP) SDK の mip::p olicyprofile クラスについて説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 515f780c269025175e99caed72e8da381ef88104
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489777"
---
# <a name="class-mippolicyprofile"></a>class mip::PolicyProfile 
PolicyProfile クラスは、Microsoft Information Protection 操作を使用するためのルートクラスです。 一般的なアプリケーションで必要な PolicyProfile は1つだけですが、必要に応じて複数のプロファイルを作成できます。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  プロファイルに設定されている設定値を取得します。
public std:: shared_ptr\<AsyncControl\> ListEnginesAsync (const std:: shared_ptr\<void\>& context)  |  エンジンの一覧操作を開始します。
public std:: vector\<std:: string\> ListEngines ()  |  エンジンの一覧。
public std:: shared_ptr\<AsyncControl\> UnloadEngineAsync (const std:: string & id、const std:: shared_ptr\<void\>& context)  |  指定した ID を持つポリシー エンジンのアンロードを開始します。
public void UnloadEngine (const std:: string & id)  |  指定した ID を持つポリシー エンジンのアンロードを開始します。
public std:: shared_ptr\<AsyncControl\> AddEngineAsync (const PolicyEngine:: Settings & Settings, const std:: shared_ptr\<void\>& context)  |  プロファイルへの新しいポリシー エンジンの追加を開始します。
public std:: shared_ptr\<PolicyEngine\> AddEngine (const PolicyEngine:: Settings & settings、const std:: shared_ptr\<void\>& context)  |  プロファイルに新しいポリシーエンジンを追加します。
public std:: shared_ptr\<AsyncControl\> DeleteEngineAsync (const std:: string & id、const std:: shared_ptr\<void\>& context)  |  指定した ID を持つポリシー エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。
public void DeleteEngine(const std::string& engineId)  |  指定された ID を持つポリシーエンジンを削除します。 指定したエンジンのすべてのデータが削除されます。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
プロファイルに設定されている設定値を取得します。

  
**戻り値**: プロファイルに設定されている設定値。
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 関数
エンジンの一覧操作を開始します。

パラメータ:  
* **context**: オブザーバー関数に渡されるパラメーター。 


PolicyProfile:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="listengines-function"></a>ListEngines 関数
エンジンの一覧。

  
**戻り値**: キャッシュされたエンジン ID
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync 関数
指定した ID を持つポリシー エンジンのアンロードを開始します。

パラメータ:  
* **id**: 一意のエンジン ID。 


* **context**: オブザーバー関数に不透明に転送されるパラメーター。 


PolicyProfile:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="unloadengine-function"></a>UnloadEngine 関数
指定した ID を持つポリシー エンジンのアンロードを開始します。

パラメータ:  
* **id**: 一意のエンジン ID。


  
### <a name="addengineasync-function"></a>AddEngineAsync 関数
プロファイルへの新しいポリシー エンジンの追加を開始します。

パラメータ:  
* **設定**: エンジンの設定を指定する mip::P olicyEngine:: settings オブジェクト。 


* **context**: 不透明がオブザーバー関数とオプションの httpdelegate に転送されるパラメーター。 


PolicyProfile:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="addengine-function"></a>AddEngine 関数
プロファイルに新しいポリシーエンジンを追加します。

パラメータ:  
* **設定**: エンジンの設定を指定する mip::P olicyEngine:: settings オブジェクト。 


* **context**: オプションの httpdelegate に不透明転送されるパラメーター



  
**戻り値**: 新しく作成された policyengine
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 関数
指定した ID を持つポリシー エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。

パラメータ:  
* **id**: 一意のエンジン ID。 


* **context**: オブザーバー関数に渡されるパラメーター。 


PolicyProfile:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="deleteengine-function"></a>DeleteEngine 関数
指定された ID を持つポリシーエンジンを削除します。 指定したエンジンのすべてのデータが削除されます。

パラメータ:  
* **id**: 一意のエンジン ID。

