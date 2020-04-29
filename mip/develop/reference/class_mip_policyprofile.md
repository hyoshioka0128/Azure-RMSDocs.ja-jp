---
title: クラス PolicyProfile
description: 'Microsoft Information Protection (MIP) SDK の policyprofile:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 9f70b8bfa1eee6e994b67c668b5144d6cb74ecad
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81760904"
---
# <a name="class-policyprofile"></a>クラス PolicyProfile 
PolicyProfile クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。 一般的なアプリケーションでは PolicyProfile は 1 つしか必要ありませんが、必要に応じて複数のプロファイルを作成できます。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  プロファイルに設定されている設定値を取得します。
public std:: shared_ptr\<asynccontrol\> ListEnginesAsync (const std:: shared_ptr\<void\>& context)  |  エンジンの一覧操作を開始します。
public std:: vector\<std:: string\> listengines ()  |  エンジンの一覧。
public std:: shared_ptr\<asynccontrol\> UnloadEngineAsync (const std:: string& id、const std:: shared_ptr\<void\>& context)  |  指定した ID を持つポリシー エンジンのアンロードを開始します。
public void UnloadEngine (const std:: string& id)  |  指定した ID を持つポリシー エンジンのアンロードを開始します。
public std:: shared_ptr\<asynccontrol\> AddEngineAsync (const policyengine:: Settings& settings, const std:: shared_ptr\<void\>& context)  |  プロファイルへの新しいポリシー エンジンの追加を開始します。
public std:: shared_ptr\<policyengine\> Addengine (const policyengine:: settings& settings, const std:: shared_ptr\<void\>& context)  |  プロファイルに新しいポリシーエンジンを追加します。
public std:: shared_ptr\<asynccontrol\> DeleteEngineAsync (const std:: string& id、const std:: shared_ptr\<void\>& context)  |  指定した ID を持つポリシー エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。
public void DeleteEngine(const std::string& engineId)  |  指定された ID を持つポリシーエンジンを削除します。 指定したエンジンのすべてのデータが削除されます。
public void AcquireAuthToken (クラウドクラウド、const std:: shared_ptr\<authdelegate\>& authdelegate) const  |  認証コールバックをトリガーします。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
プロファイルに設定されている設定値を取得します。

  
**戻り値**: プロファイルに設定されている設定値。
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 関数
エンジンの一覧操作を開始します。

パラメーター:  
* **context**: オブザーバー関数に渡されるパラメーター。 


PolicyProfile::Observer は成功時または失敗時に呼び出されます。
  
### <a name="listengines-function"></a>ListEngines 関数
エンジンの一覧。

  
**戻り値**: キャッシュされたエンジン ID
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync 関数
指定した ID を持つポリシー エンジンのアンロードを開始します。

パラメーター:  
* **id**: 一意のエンジン id。 


* **context**: オブザーバー関数に不透明に転送されるパラメーター。 


PolicyProfile::Observer は成功時または失敗時に呼び出されます。
  
### <a name="unloadengine-function"></a>UnloadEngine 関数
指定した ID を持つポリシー エンジンのアンロードを開始します。

パラメーター:  
* **id**: 一意のエンジン id。


  
### <a name="addengineasync-function"></a>AddEngineAsync 関数
プロファイルへの新しいポリシー エンジンの追加を開始します。

パラメーター:  
* **settings**: エンジンの設定を指定する mip::PolicyEngine::Settings オブジェクト。 


* **context**: 不透明がオブザーバー関数とオプションの httpdelegate に転送されるパラメーター。 


PolicyProfile::Observer は成功時または失敗時に呼び出されます。
  
### <a name="addengine-function"></a>AddEngine 関数
プロファイルに新しいポリシーエンジンを追加します。

パラメーター:  
* **settings**: エンジンの設定を指定する mip::PolicyEngine::Settings オブジェクト。 


* **context**: オプションの httpdelegate に不透明転送されるパラメーター



  
**戻り値**: 新しく作成された policyengine
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 関数
指定した ID を持つポリシー エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。

パラメーター:  
* **id**: 一意のエンジン id。 


* **context**: オブザーバー関数に渡されるパラメーター。 


PolicyProfile::Observer は成功時または失敗時に呼び出されます。
  
### <a name="deleteengine-function"></a>DeleteEngine 関数
指定された ID を持つポリシーエンジンを削除します。 指定したエンジンのすべてのデータが削除されます。

パラメーター:  
* **id**: 一意のエンジン id。


  
### <a name="acquireauthtoken-function"></a>AcquireAuthToken 関数
認証コールバックをトリガーします。

パラメーター:  
* **クラウド**: Azure クラウド 


* **Authdelegate**: 呼び出される認証コールバック


MIP は、auth デリゲートによって返された値を使用してキャッシュしたり他の操作を実行したりすることはありません。 この関数は、MIP が認証トークンを要求するまで "ログイン" されていないアプリケーションに推奨されます。 これにより、アプリケーションは、MIP が実際に必要とする前にトークンをフェッチできます。