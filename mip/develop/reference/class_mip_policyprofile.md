---
title: class mip PolicyProfile
description: class mip PolicyProfile のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 387e28780cb0ef02d56050f534d4783fdebc286e
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446863"
---
# <a name="class-mippolicyprofile"></a>class mip::PolicyProfile 
[PolicyProfile](class_mip_policyprofile.md) クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。 一般的なアプリケーションでは [PolicyProfile](class_mip_policyprofile.md) は 1 つしか必要ありませんが、必要に応じて複数のプロファイルを作成できます。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  プロファイルに設定されている設定値を取得します。
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  エンジンの一覧操作を開始します。
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  指定した ID を持つポリシー エンジンのアンロードを開始します。
public void AddEngineAsync(const PolicyEngine::Settings& settings, const std::shared_ptr<void>& context)  |  プロファイルへの新しいポリシー エンジンの追加を開始します。
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  指定した ID を持つポリシー エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
プロファイルに設定されている設定値を取得します。

  
**戻り値**: プロファイルに設定されている設定値。
  
### <a name="listenginesasync"></a>ListEnginesAsync
エンジンの一覧操作を開始します。

パラメーター:  
* **context**: オブザーバー関数に渡されるパラメーター。 


[PolicyProfile::Observer](class_mip_policyprofile_observer.md) は成功時または失敗時に呼び出されます。
  
### <a name="unloadengineasync"></a>UnloadEngineAsync
指定した ID を持つポリシー エンジンのアンロードを開始します。

パラメーター:  
* **id**: 一意のエンジン ID。 


* **context**: オブザーバー関数に不透明に転送されるパラメーター。 


[PolicyProfile::Observer](class_mip_policyprofile_observer.md) は成功時または失敗時に呼び出されます。
  
### <a name="addengineasync"></a>AddEngineAsync
プロファイルへの新しいポリシー エンジンの追加を開始します。

パラメーター:  
* **settings**: エンジンの設定を指定する [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md) オブジェクト。 


* **context**: オブザーバー関数に不透明に転送されるパラメーター。 


[PolicyProfile::Observer](class_mip_policyprofile_observer.md) は成功時または失敗時に呼び出されます。
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
指定した ID を持つポリシー エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。

パラメーター:  
* **id**: 一意のエンジン ID。 


* **context**: オブザーバー関数に渡されるパラメーター。 


[PolicyProfile::Observer](class_mip_policyprofile_observer.md) は成功時または失敗時に呼び出されます。