---
title: class mip LoggerDelegate
description: class mip LoggerDelegate のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: b25cdb177735feccfa5c4d344613e4747d18b77f
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445854"
---
# <a name="class-miploggerdelegate"></a>class mip::LoggerDelegate 
MIP SDK のロガーに対してインターフェイスを定義するクラス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public void Init(const std::string& storagePath, LogLevel logLevel)  |  ロガーを初期化します。
 public LogLevel GetLogLevel() const  |  ログ イベントをトリガーする最も低いログ レベルを取得します。
 public void Flush()  |  ロガーをフラッシュします。
 public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const int32_t line)  |  ログ ファイルにログ ステートメントを書き込みます。
  
## <a name="members"></a>メンバー
  
### <a name="init"></a>Init
ロガーを初期化します。

パラメーター:  
* **storagePath**: ログを含む継続状態が格納される可能性のある場所へのパス。 


* **logLevel**: ログ イベントをトリガーする最小のログ レベル。


  
### <a name="loglevel"></a>ログ レベル
ログ イベントをトリガーする最も低いログ レベルを取得します。

  
**戻り値**: ログ イベントをトリガーする最小のログ レベル。
  
### <a name="flush"></a>フラッシュ
ロガーをフラッシュします。
  
### <a name="writetolog"></a>WriteToLog
ログ ファイルにログ ステートメントを書き込みます。

パラメーター:  
* **level**: ログ ステートメントのログ レベル。 


* **message**: ログ ステートメントのメッセージ。 


* **function**: ログ ステートメントの関数の名前。 


* **file**: ログ ステートメントが生成されたファイル名。 


* **line**: ログ ステートメントが生成された行番号。

