---
title: MipContext クラス
description: 'Microsoft Information Protection (MIP) SDK の mipcontext:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: c593ebc368b0717d32e873e6924f80af103325ea
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566763"
---
# <a name="class-mipcontext"></a>MipContext クラス 
MipContext は、すべてのプロファイル、エンジン、ハンドラー間で共有される状態を表します。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public void ShutDown ()  |  MIP を終了します。
public bool IsFeatureEnabled (フライト Ingfeature 機能) const  |  機能が有効かどうかを取得します。
public const ApplicationInfo& GetApplicationInfo() const  |  アプリケーションの説明を取得します。
public const std:: string& GetMipPath () const  |  ログ、キャッシュなどのファイルパスを取得します。
public bool IsOfflineOnly ()  |  オフラインのみの設定を取得します。
public LogLevel GetThresholdLogLevel () const  |  しきい値ログレベルを取得します。
public std:: shared_ptr \<LoggerDelegate\> GetLoggerDelegate ()  |  Logger の実装を取得します。
public LoggerDelegate * GetRawLoggerDelegate ()  |  Logger の実装を取得します。
public const std:: map \<FlightingFeature, bool\>& get観光 ingfeatures () const  |  フライト機能セットを取得します。
  
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
  
### <a name="getthresholdloglevel-function"></a>GetThresholdLogLevel 関数
しきい値ログレベルを取得します。

  
**戻り** 値: しきい値ログレベル
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate 関数
Logger の実装を取得します。

  
**戻り値**: ロガー
  
### <a name="getrawloggerdelegate-function"></a>GetRawLoggerDelegate 関数
Logger の実装を取得します。

  
**戻り値**: ロガー
  
### <a name="getflightingfeatures-function"></a>Getフライト機能関数
フライト機能セットを取得します。

  
**戻り値**: flighting 機能マップ