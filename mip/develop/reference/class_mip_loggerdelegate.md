---
title: class mip::LoggerDelegate
description: Mip::loggerdelegate クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 511c8dabc8ff31c70c8343a80d423b76c43fa946
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184622"
---
# <a name="class-miploggerdelegate"></a>class mip::LoggerDelegate 
MIP SDK のロガーに対してインターフェイスを定義するクラス。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
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

  
**返します**:ログ イベントをトリガーする最小のログ レベル。
  
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

