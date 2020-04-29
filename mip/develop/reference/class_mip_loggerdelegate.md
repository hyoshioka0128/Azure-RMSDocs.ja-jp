---
title: LoggerDelegate クラス
description: 'Microsoft Information Protection (MIP) SDK の loggerdelegate:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: e213f243a0e46bb804b224c7a0752a0b9b270103
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81761817"
---
# <a name="class-loggerdelegate"></a>LoggerDelegate クラス 
MIP SDK のロガーに対してインターフェイスを定義するクラス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public void Init(const std::string& storagePath)  |  ロガーを初期化します。
public void Flush()  |  ロガーをフラッシュします。
public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const int32_t line)  |  ログ ファイルにログ ステートメントを書き込みます。
  
## <a name="members"></a>メンバー
  
### <a name="init-function"></a>init 関数
ロガーを初期化します。

パラメーター:  
* **storagePath**: ログを含む継続状態が格納される可能性のある場所へのパス。


  
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

