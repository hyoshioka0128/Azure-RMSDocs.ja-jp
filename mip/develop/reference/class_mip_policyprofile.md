---
title: class mip::PolicyProfile
description: Microsoft Information Protection (MIP) SDK の mip::p olicyprofile クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 5abcca760f89b492f26ed5fa7b46e280e1bfc8ab
ms.sourcegitcommit: 9cedac6569f3a33a22a721da27074a438b1a7882
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71070535"
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
public static MIP_API void __CDECL MIP::P olicyProfile:: LoadAsync | 指定された設定に基づいて、プロファイルの読み込みを開始します。
public static const MIP_API char * __CDECL MIP::P olicyProfile:: GetVersion | ライブラリのバージョンを取得する


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

### <a name="loadasync-function"></a>LoadAsync 関数
指定された設定に基づいて、プロファイルの読み込みを開始します。

パラメーター:  
* **設定**: プロファイルオブジェクトの読み込みに使用されるプロファイル設定。 </para>
* **context**: オブザーバー関数に渡されるコンテキストパラメーター。

### <a name="getversion-function"></a>GetVersion 関数
ライブラリのバージョンを取得する

次の**値を返し**ます。バージョン文字列。

