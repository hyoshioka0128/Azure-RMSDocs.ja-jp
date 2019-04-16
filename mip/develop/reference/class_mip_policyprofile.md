---
title: class mip::PolicyProfile
description: Mip::policyprofile クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 45af1f4d072a1d8a690aa8f459950ae500df3db8
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573875"
---
# <a name="class-mippolicyprofile"></a>class mip::PolicyProfile 
[PolicyProfile](class_mip_policyprofile.md) クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。 一般的なアプリケーションでは [PolicyProfile](class_mip_policyprofile.md) は 1 つしか必要ありませんが、必要に応じて複数のプロファイルを作成できます。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  プロファイルに設定されている設定値を取得します。
public void ListEnginesAsync(const std::shared_ptr\<void\>& context)  |  エンジンの一覧操作を開始します。
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr\<void\>& context)  |  指定した ID を持つポリシー エンジンのアンロードを開始します。
public void AddEngineAsync(const PolicyEngine::Settings& settings, const std::shared_ptr\<void\>& context)  |  プロファイルへの新しいポリシー エンジンの追加を開始します。
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr\<void\>& context)  |  指定した ID を持つポリシー エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
プロファイルに設定されている設定値を取得します。

  
**返します**:プロファイルの設定を設定します。
  
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