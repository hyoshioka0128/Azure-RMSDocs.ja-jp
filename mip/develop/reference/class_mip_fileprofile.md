---
title: class mip FileProfile
description: class mip FileProfile のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: f317f1eff0266db1da211e164ec5e427ba7ce17d
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445888"
---
# <a name="class-mipfileprofile"></a>class mip::FileProfile 
[FileProfile](class_mip_fileprofile.md) クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。
一般的なアプリケーションには、プロファイルが 1 つのみ必要です。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  プロファイル設定を返します。
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  エンジンの一覧操作を開始します。
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  指定した ID を持つファイル エンジンのアンロードを開始します。
public void AddEngineAsync(const FileEngine::Settings& settings, const std::shared_ptr<void>& context)  |  プロファイルへの新しいファイル エンジンの追加を開始します。
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  指定した ID を持つファイル エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
プロファイル設定を返します。
  
### <a name="listenginesasync"></a>ListEnginesAsync
エンジンの一覧操作を開始します。
[FileProfile::Observer](class_mip_fileprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="unloadengineasync"></a>UnloadEngineAsync
指定した ID を持つファイル エンジンのアンロードを開始します。
[FileProfile::Observer](class_mip_fileprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="addengineasync"></a>AddEngineAsync
プロファイルへの新しいファイル エンジンの追加を開始します。
[FileProfile::Observer](class_mip_fileprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
指定した ID を持つファイル エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。
[FileProfile::Observer](class_mip_fileprofile_observer.md) は成功または失敗時に呼び出されます。