---
title: class mip::LoggerDelegate
description: 'Microsoft Information Protection (MIP) SDK の mip:: loggerdelegate クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: f1726c53afb7e398f8921e1cb8fc67e3166fffe8
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73561041"
---
# <a name="class-miploggerdelegate"></a>class mip::LoggerDelegate 
MIP SDK のロガーに対してインターフェイスを定義するクラス。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public void Init(const std::string& storagePath)  |  ロガーを初期化します。
public void Flush()  |  ロガーをフラッシュします。
public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const int32_t line)  |  ログ ファイルにログ ステートメントを書き込みます。
  
## <a name="members"></a>メンバー
  
### <a name="init-function"></a>Init 関数
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

