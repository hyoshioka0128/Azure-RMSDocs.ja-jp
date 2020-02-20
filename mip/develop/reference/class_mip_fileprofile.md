---
title: class mip::FileProfile
description: 'Microsoft Information Protection (MIP) SDK の mip:: fileprofile クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 44d6024473555c0745ff3156ff5cd004f83b6f6b
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77488145"
---
# <a name="class-mipfileprofile"></a>class mip::FileProfile 
FileProfile クラスは、Microsoft Information Protection 操作を使用するためのルートクラスです。
一般的なアプリケーションには、プロファイルが 1 つのみ必要です。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  プロファイル設定を返します。
public std:: shared_ptr\<AsyncControl\> ListEnginesAsync (const std:: shared_ptr\<void\>& context)  |  エンジンの一覧操作を開始します。
public std:: shared_ptr\<AsyncControl\> UnloadEngineAsync (const std:: string & id、const std:: shared_ptr\<void\>& context)  |  指定した ID を持つファイル エンジンのアンロードを開始します。
public std:: shared_ptr\<AsyncControl\> AddEngineAsync (const FileEngine:: Settings & Settings, const std:: shared_ptr\<void\>& context)  |  プロファイルへの新しいファイル エンジンの追加を開始します。
public std:: shared_ptr\<AsyncControl\> DeleteEngineAsync (const std:: string & id、const std:: shared_ptr\<void\>& context)  |  指定した ID を持つファイル エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。
  
## <a name="members"></a>Members
  
### <a name="getsettings-function"></a>GetSettings 関数
プロファイル設定を返します。
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 関数
エンジンの一覧操作を開始します。

  
**戻り値**: Async control オブジェクト。
FileProfile:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync 関数
指定した ID を持つファイル エンジンのアンロードを開始します。

  
**戻り値**: Async control オブジェクト。
FileProfile:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="addengineasync-function"></a>AddEngineAsync 関数
プロファイルへの新しいファイル エンジンの追加を開始します。

  
**戻り値**: Async control オブジェクト。
FileProfile:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 関数
指定した ID を持つファイル エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。

  
**戻り値**: Async control オブジェクト。
FileProfile:: オブザーバーは、成功または失敗時に呼び出されます。