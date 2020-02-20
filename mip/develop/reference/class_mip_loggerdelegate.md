---
title: class mip::LoggerDelegate
description: 'Microsoft Information Protection (MIP) SDK の mip:: loggerdelegate クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: c9e4f4db31c12a84f888964694ffa4c88585c884
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77487737"
---
# <a name="class-miploggerdelegate"></a>class mip::LoggerDelegate 
MIP SDK のロガーに対してインターフェイスを定義するクラス。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
public void Init(const std::string& storagePath)  |  ロガーを初期化します。
public void Flush()  |  ロガーをフラッシュします。
public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const int32_t line)  |  ログ ファイルにログ ステートメントを書き込みます。
  
## <a name="members"></a>Members
  
### <a name="init-function"></a>Init 関数
ロガーを初期化します。

パラメータ:  
* **storagePath**: ログを含む継続状態が格納される可能性のある場所へのパス。


  
### <a name="flush-function"></a>Flush 関数
ロガーをフラッシュします。
  
### <a name="writetolog-function"></a>WriteToLog 関数
ログ ファイルにログ ステートメントを書き込みます。

パラメータ:  
* **level**: ログ ステートメントのログ レベル。 


* **message**: ログ ステートメントのメッセージ。 


* **function**: ログ ステートメントの関数の名前。 


* **file**: ログ ステートメントが生成されたファイル名。 


* **line**: ログ ステートメントが生成された行番号。

