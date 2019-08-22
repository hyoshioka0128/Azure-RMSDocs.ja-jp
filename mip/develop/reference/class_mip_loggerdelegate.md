---
title: class mip::LoggerDelegate
description: 'Microsoft Information Protection (MIP) SDK の mip:: loggerdelegate クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: effba9bc41907c477cea7e3cf6a8688187538068
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883903"
---
# <a name="class-miploggerdelegate"></a>class mip::LoggerDelegate 
MIP SDK のロガーに対してインターフェイスを定義するクラス。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public void Init(const std::string& storagePath, LogLevel logLevel)  |  ロガーを初期化します。
public LogLevel GetLogLevel() const  |  ログ イベントをトリガーする最も低いログ レベルを取得します。
public void Flush()  |  ロガーをフラッシュします。
public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const int32_t line)  |  ログ ファイルにログ ステートメントを書き込みます。
  
## <a name="members"></a>メンバー
  
### <a name="init-function"></a>Init 関数
ロガーを初期化します。

パラメーター:  
* **storagePath**: ログを含む継続状態が格納される可能性のある場所へのパス。 


* **logLevel**: ログ イベントをトリガーする最小のログ レベル。


  
### <a name="getloglevel-function"></a>GetLogLevel 関数
ログ イベントをトリガーする最も低いログ レベルを取得します。

  
次の**値を返し**ます。ログイベントをトリガーする最も低いログレベル。
  
### <a name="flush-function"></a>Flush 関数
ロガーをフラッシュします。
  
### <a name="writetolog-function"></a>WriteToLog 関数
ログ ファイルにログ ステートメントを書き込みます。

パラメーター:  
* **level**: ログ ステートメントのログ レベル。 


* **message**: ログ ステートメントのメッセージ。 


* **function**: ログ ステートメントの関数の名前。 


* **file**: ログ ステートメントが生成されたファイル名。 


* **line**: ログ ステートメントが生成された行番号。

