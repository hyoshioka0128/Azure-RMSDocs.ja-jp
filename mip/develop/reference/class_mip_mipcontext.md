---
title: 'クラス mip:: MipContext'
description: 'Microsoft Information Protection (MIP) SDK の mip:: mipcontext クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: f6bc8d5a61ec259b85ae9e2479afeb9a2f00412f
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054578"
---
# <a name="class-mipmipcontext"></a>クラス mip:: MipContext 
MipContext は、すべてのプロファイル、エンジン、ハンドラー間で共有される状態を表します。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public void ShutDown ()  |  MIP を終了します。
public bool IsFeatureEnabled (フライト Ingfeature 機能) const  |  機能が有効かどうかを取得します。
public const ApplicationInfo& GetApplicationInfo() const  |  アプリケーションの説明を取得します。
public const std:: string & GetMipPath () const  |  ログ、キャッシュなどのファイルパスを取得します。
public std:: shared_ptr\<LoggerDelegate\> GetLoggerDelegate ()  |  Logger の実装を取得します。
public LoggerDelegate * GetRawLoggerDelegate ()  |  Logger の実装を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="shutdown-function"></a>ShutDown 関数
MIP を終了します。
プロセス/DLL をシャットダウンする前に、このメソッドを呼び出す必要があります。
  
### <a name="isfeatureenabled-function"></a>IsFeatureEnabled 関数
機能が有効かどうかを取得します。

パラメーター:  
* **機能**:有効/無効にする機能



  
次の**値を返し**ます。FeatureFlightingDelegate がアプリケーションによって提供されていない場合、機能が有効になっているかどうかにかかわらず、常に true が返されます。
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo 関数
アプリケーションの説明を取得します。

  
次の**値を返し**ます。アプリケーションの説明
  
### <a name="getmippath-function"></a>GetMipPath 関数
ログ、キャッシュなどのファイルパスを取得します。

  
次の**値を返し**ます。ファイルパス ("mip" リーフディレクトリを含む)
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate 関数
Logger の実装を取得します。

  
次の**値を返し**ます。Lnm
  
### <a name="getrawloggerdelegate-function"></a>GetRawLoggerDelegate 関数
Logger の実装を取得します。

  
次の**値を返し**ます。Lnm