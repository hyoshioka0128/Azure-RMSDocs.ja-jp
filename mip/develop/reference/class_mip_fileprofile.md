---
title: class mip::FileProfile
description: 'Microsoft Information Protection (MIP) SDK の mip:: fileprofile クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 00b56c5b45c8c05bf50229c3b462611ce48945c4
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884287"
---
# <a name="class-mipfileprofile"></a>class mip::FileProfile 
[FileProfile](class_mip_fileprofile.md) クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。
一般的なアプリケーションには、プロファイルが 1 つのみ必要です。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  プロファイル設定を返します。
public void ListEnginesAsync (const std:: shared_ptr\<void\>& context)  |  エンジンの一覧操作を開始します。
public void UnloadEngineAsync (const std:: string & id、const std:: shared_ptr\<void\>& context)  |  指定した ID を持つファイル エンジンのアンロードを開始します。
public void AddEngineAsync (const fileengine:: settings & settings, const std:: shared_ptr\<void\>& context)  |  プロファイルへの新しいファイル エンジンの追加を開始します。
public void DeleteEngineAsync (const std:: string & id、const std:: shared_ptr\<void\>& context)  |  指定した ID を持つファイル エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。
  
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