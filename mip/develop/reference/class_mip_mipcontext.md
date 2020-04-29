---
title: MipContext クラス
description: 'Microsoft Information Protection (MIP) SDK の mipcontext:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: cf191a1e770d13d84603fe593d63dedb98bbb14b
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81761468"
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
public std:: shared_ptr\<LoggerDelegate\> GetLoggerDelegate ()  |  Logger の実装を取得します。
public LoggerDelegate * GetRawLoggerDelegate ()  |  Logger の実装を取得します。
public const std:: map\<のフライト機能、Bool\>& get観光 ingfeatures () const  |  フライト機能セットを取得します。
  
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

  
**戻り**値: しきい値ログレベル
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate 関数
Logger の実装を取得します。

  
**戻り値**: ロガー
  
### <a name="getrawloggerdelegate-function"></a>GetRawLoggerDelegate 関数
Logger の実装を取得します。

  
**戻り値**: ロガー
  
### <a name="getflightingfeatures-function"></a>Getフライト機能関数
フライト機能セットを取得します。

  
**戻り値**: flighting 機能マップ