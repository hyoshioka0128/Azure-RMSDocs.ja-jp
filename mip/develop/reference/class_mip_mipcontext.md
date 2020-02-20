---
title: 'クラス mip:: MipContext'
description: 'Microsoft Information Protection (MIP) SDK の mip:: mipcontext クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 82c39cd6f716bde9232f6a5a461b2ffbfbae1dd0
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489913"
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
public LogLevel GetThresholdLogLevel () const  |  しきい値ログレベルを取得します。
public std:: shared_ptr\<LoggerDelegate\> GetLoggerDelegate ()  |  Logger の実装を取得します。
public LoggerDelegate * GetRawLoggerDelegate ()  |  Logger の実装を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="shutdown-function"></a>ShutDown 関数
MIP を終了します。
プロセス/DLL をシャットダウンする前に、このメソッドを呼び出す必要があります。
  
### <a name="isfeatureenabled-function"></a>IsFeatureEnabled 関数
機能が有効かどうかを取得します。

パラメータ:  
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
  
### <a name="getthresholdloglevel-function"></a>GetThresholdLogLevel 関数
しきい値ログレベルを取得します。

  
**戻り**値: しきい値ログレベル
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate 関数
Logger の実装を取得します。

  
**戻り値**: ロガー
  
### <a name="getrawloggerdelegate-function"></a>GetRawLoggerDelegate 関数
Logger の実装を取得します。

  
**戻り値**: ロガー