---
title: 'クラス mip:: MipContext'
description: 'Microsoft Information Protection (MIP) SDK の mip:: mipcontext クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 9efbe9330014458a26f62e4dfac9ea24ad5d4475
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73561031"
---
# <a name="class-mipmipcontext"></a>クラス mip:: MipContext 
MipContext は、すべてのプロファイル、エンジン、ハンドラー間で共有される状態を表します。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public void ShutDown ()  |  MIP を終了します。
public bool IsFeatureEnabled (フライト Ingfeature 機能) const  |  機能が有効かどうかを取得します。
public const ApplicationInfo& GetApplicationInfo() const  |  アプリケーションの説明を取得します。
public const std:: string & GetMipPath () const  |  ログ、キャッシュなどのファイルパスを取得します。
public bool IsOfflineOnly ()  |  オフラインのみの設定を取得します。
public std:: shared_ptr\<LoggerDelegate\> GetLoggerDelegate ()  |  Logger の実装を取得します。
public LoggerDelegate * GetRawLoggerDelegate ()  |  Logger の実装を取得します。
public static MIP_API std:: shared_ptr&lt;MipContext&gt; __CDECL MIP:: MipContext:: Create | プロファイルを初期化するときに使用する新しい MipContext インスタンスを作成します。
public static MIP_API std:: shared_ptr&lt;MipContext&gt; __CDECL MIP:: MipContext:: CreateWithCustomFeatureSettings | カスタム機能設定を使用して、新しい MipContext インスタンスを作成します。

## <a name="members"></a>メンバー
  
### <a name="shutdown-function"></a>ShutDown 関数
MIP を終了します。
プロセス/DLL をシャットダウンする前に、このメソッドを呼び出す必要があります。
  
### <a name="isfeatureenabled-function"></a>IsFeatureEnabled 関数
機能が有効かどうかを取得します。

パラメーター:  
* **機能**: 有効/無効にする機能



  
**戻り値**: FeatureFlightingDelegate がアプリケーションによって提供されていない場合、機能が有効になっているかどうかにかかわらず、常に true が返されます。
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo 関数
アプリケーションの説明を取得します。

  
**戻り値**: アプリケーションの説明
  
### <a name="getmippath-function"></a>GetMipPath 関数
ログ、キャッシュなどのファイルパスを取得します。

  
**戻り値**: ファイルパス ("mip" リーフディレクトリ)
  
### <a name="isofflineonly-function"></a>IsOfflineOnly 関数
オフラインのみの設定を取得します。

  
**戻り値**: アプリケーションがオフライン専用モードで実行されているかどうか
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate 関数
Logger の実装を取得します。

  
**戻り値**: ロガー
  
### <a name="getrawloggerdelegate-function"></a>GetRawLoggerDelegate 関数
Logger の実装を取得します。

  
**戻り値**: ロガー

### <a name="create-function"></a>関数の作成
プロファイルを初期化するときに使用する新しい MipContext インスタンスを作成します。

は、MipContext インスタンス**を返し**ます。

### <a name="createwithcustomfeaturesettings-function"></a>CreateWithCustomFeatureSettings 関数
カスタム機能設定を使用して、新しい MipContext インスタンスを作成します。

は、MipContext インスタンス**を返し**ます。