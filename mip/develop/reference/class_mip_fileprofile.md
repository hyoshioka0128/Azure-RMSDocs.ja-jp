---
title: class mip::FileProfile
description: 'Microsoft Information Protection (MIP) SDK の mip:: fileprofile クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: a436024aefe58a73ea03747fce5c5f2f4b4fc4b1
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73558803"
---
# <a name="class-mipfileprofile"></a>class mip::FileProfile 
FileProfile クラスは、Microsoft Information Protection 操作を使用するためのルートクラスです。
一般的なアプリケーションには、プロファイルが 1 つのみ必要です。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  プロファイル設定を返します。
public void ListEnginesAsync (const std:: shared_ptr\<void\>& context)  |  エンジンの一覧操作を開始します。
public void UnloadEngineAsync (const std:: string & id、const std:: shared_ptr\<void\>& context)  |  指定した ID を持つファイル エンジンのアンロードを開始します。
public void AddEngineAsync (const FileEngine:: Settings & settings, const std:: shared_ptr\<void\>& context)  |  プロファイルへの新しいファイル エンジンの追加を開始します。
public void DeleteEngineAsync (const std:: string & id、const std:: shared_ptr\<void\>& context)  |  指定した ID を持つファイル エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。
public static FILE_API void __CDECL mip:: FileProfile:: LoadAsync | 指定された設定に基づいてプロファイルの読み込みを開始します
public static const FILE_API char * __CDECL mip:: FileProfile:: GetVersion | ライブラリのバージョンを取得します。

## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
プロファイル設定を返します。
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 関数
エンジンの一覧操作を開始します。
FileProfile:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync 関数
指定した ID を持つファイル エンジンのアンロードを開始します。
FileProfile:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="addengineasync-function"></a>AddEngineAsync 関数
プロファイルへの新しいファイル エンジンの追加を開始します。
FileProfile:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 関数
指定した ID を持つファイル エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。
FileProfile:: オブザーバーは、成功または失敗時に呼び出されます。

### <a name="loadasync-function"></a>LoadAsync 関数
指定された設定に基づいて、プロファイルの読み込みを開始します。

[FileProfile::Observer](class_mip_fileprofile_observer.md) は成功または失敗時に呼び出されます。

### <a name="getversion-function"></a>GetVersion 関数
ライブラリのバージョンを取得します。