---
title: クラス FileProfile
description: 'Microsoft Information Protection (MIP) SDK の fileprofile:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: cf5950b37953dc32100e8ae2700b6111783cb612
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81762922"
---
# <a name="class-fileprofile"></a>クラス FileProfile 
FileProfile クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。
一般的なアプリケーションには、プロファイルが 1 つのみ必要です。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  プロファイル設定を返します。
public std:: shared_ptr\<asynccontrol\> ListEnginesAsync (const std:: shared_ptr\<void\>& context)  |  エンジンの一覧操作を開始します。
public std:: shared_ptr\<asynccontrol\> UnloadEngineAsync (const std:: string& id、const std:: shared_ptr\<void\>& context)  |  指定した ID を持つファイル エンジンのアンロードを開始します。
public std:: shared_ptr\<asynccontrol\> AddEngineAsync (const Fileengine:: Settings& settings, const std:: shared_ptr\<void\>& context)  |  プロファイルへの新しいファイル エンジンの追加を開始します。
public std:: shared_ptr\<asynccontrol\> DeleteEngineAsync (const std:: string& id、const std:: shared_ptr\<void\>& context)  |  指定した ID を持つファイル エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。
public void AcquirePolicyAuthToken (クラウドクラウド、const std:: shared_ptr\<authdelegate\>& authdelegate) const  |  ポリシーの認証コールバックをトリガーします。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
プロファイル設定を返します。
  
### <a name="listenginesasync-function"></a>ListEnginesAsync 関数
エンジンの一覧操作を開始します。

  
**戻り値**: Async control オブジェクト。
FileProfile::Observer は成功または失敗時に呼び出されます。
  
### <a name="unloadengineasync-function"></a>UnloadEngineAsync 関数
指定した ID を持つファイル エンジンのアンロードを開始します。

  
**戻り値**: Async control オブジェクト。
FileProfile::Observer は成功または失敗時に呼び出されます。
  
### <a name="addengineasync-function"></a>AddEngineAsync 関数
プロファイルへの新しいファイル エンジンの追加を開始します。

  
**戻り値**: Async control オブジェクト。
FileProfile::Observer は成功または失敗時に呼び出されます。
  
### <a name="deleteengineasync-function"></a>DeleteEngineAsync 関数
指定した ID を持つファイル エンジンの削除を開始します。 指定したプロファイルのデータがすべて削除されます。

  
**戻り値**: Async control オブジェクト。
FileProfile::Observer は成功または失敗時に呼び出されます。
  
### <a name="acquirepolicyauthtoken-function"></a>AcquirePolicyAuthToken 関数
ポリシーの認証コールバックをトリガーします。

パラメーター:  
* **クラウド**: Azure クラウド 


* **Authdelegate**: 呼び出される認証コールバック


MIP は、auth デリゲートによって返された値を使用してキャッシュしたり他の操作を実行したりすることはありません。 この関数は、MIP が認証トークンを要求するまで "ログイン" されていないアプリケーションに推奨されます。 これにより、アプリケーションは、MIP が実際に必要とする前にトークンをフェッチできます。