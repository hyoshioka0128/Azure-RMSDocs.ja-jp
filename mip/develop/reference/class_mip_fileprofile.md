---
title: class mip::FileProfile
description: Mip::fileprofile クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 4bdd96e7f9f414062d969de1ffaf7195ad71d214
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57329405"
---
# <a name="class-mipfileprofile"></a>class mip::FileProfile 
[FileProfile](class_mip_fileprofile.md) クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。
一般的なアプリケーションには、プロファイルが 1 つのみ必要です。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  プロファイル設定を返します。
public void ListEnginesAsync(const std::shared_ptr\<void\>& context)  |  エンジンの一覧操作を開始します。
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr\<void\>& context)  |  指定した ID を持つファイル エンジンのアンロードを開始します。
public void AddEngineAsync(const FileEngine::Settings& settings, const std::shared_ptr\<void\>& context)  |  プロファイルへの新しいファイル エンジンの追加を開始します。
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr\<void\>& context)  |  指定した ID を持つファイル エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
プロファイル設定を返します。
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 関数
エンジンの一覧操作を開始します。
[FileProfile::Observer](class_mip_fileprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync 関数
指定した ID を持つファイル エンジンのアンロードを開始します。
[FileProfile::Observer](class_mip_fileprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="addengineasync-function"></a>AddEngineAsync 関数
プロファイルへの新しいファイル エンジンの追加を開始します。
[FileProfile::Observer](class_mip_fileprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 関数
指定した ID を持つファイル エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。
[FileProfile::Observer](class_mip_fileprofile_observer.md) は成功または失敗時に呼び出されます。
