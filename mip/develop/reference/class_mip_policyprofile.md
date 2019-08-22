---
title: class mip::PolicyProfile
description: Microsoft Information Protection (MIP) SDK の mip::p olicyprofile クラスについて説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 13d24afe87bc04f7a92dde8daf88c1ada38cedc2
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883750"
---
# <a name="class-mippolicyprofile"></a>class mip::PolicyProfile 
[PolicyProfile](class_mip_policyprofile.md) クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。 一般的なアプリケーションでは [PolicyProfile](class_mip_policyprofile.md) は 1 つしか必要ありませんが、必要に応じて複数のプロファイルを作成できます。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  プロファイルに設定されている設定値を取得します。
public void ListEnginesAsync (const std:: shared_ptr\<void\>& context)  |  エンジンの一覧操作を開始します。
public void UnloadEngineAsync (const std:: string & id、const std:: shared_ptr\<void\>& context)  |  指定した ID を持つポリシー エンジンのアンロードを開始します。
public void AddEngineAsync (const policyengine:: settings & settings, const std:: shared_ptr\<void\>& context)  |  プロファイルへの新しいポリシー エンジンの追加を開始します。
public void DeleteEngineAsync (const std:: string & id、const std:: shared_ptr\<void\>& context)  |  指定した ID を持つポリシー エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
プロファイルに設定されている設定値を取得します。

  
次の**値を返し**ます。プロファイルに設定された設定。
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 関数
エンジンの一覧操作を開始します。

パラメーター:  
* **context**: オブザーバー関数に渡されるパラメーター。 


[PolicyProfile::Observer](class_mip_policyprofile_observer.md) は成功時または失敗時に呼び出されます。
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync 関数
指定した ID を持つポリシー エンジンのアンロードを開始します。

パラメーター:  
* **id**: 一意のエンジン ID。 


* **context**: オブザーバー関数に不透明に転送されるパラメーター。 


[PolicyProfile::Observer](class_mip_policyprofile_observer.md) は成功時または失敗時に呼び出されます。
  
### <a name="addengineasync-function"></a>AddEngineAsync 関数
プロファイルへの新しいポリシー エンジンの追加を開始します。

パラメーター:  
* **settings**: エンジンの設定を指定する [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md) オブジェクト。 


* **context**: オブザーバー関数に不透明に転送されるパラメーター。 


[PolicyProfile::Observer](class_mip_policyprofile_observer.md) は成功時または失敗時に呼び出されます。
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 関数
指定した ID を持つポリシー エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。

パラメーター:  
* **id**: 一意のエンジン ID。 


* **context**: オブザーバー関数に渡されるパラメーター。 


[PolicyProfile::Observer](class_mip_policyprofile_observer.md) は成功時または失敗時に呼び出されます。