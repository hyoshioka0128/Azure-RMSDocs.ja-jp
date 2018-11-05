---
title: class mip Stream
description: class mip Stream のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: e6296c5e15590741e008979dcf12373ff5fcdf00
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445225"
---
# <a name="class-mipstream"></a>class mip::Stream 
MIP SDK とストリーム ベースのコンテンツの間のインターフェイスを定義するクラス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public int64_t Read(uint8_t* buffer, int64_t bufferLength)  |  ストリームからバッファーに読み取ります。
 public int64_t Write(const uint8_t* buffer, int64_t bufferLength)  |  バッファーからストリームに書き込みます。
 public bool Flush()  |  ストリームをフラッシュします。
 public void Seek(int64_t position)  |  ストリーム内の特定の位置をシークします。
 public bool CanRead() const  |  ストリームから読み込めるかどうかのチェックです。
 public bool CanWrite() const  |  ストリームに書き込めるかどうかのチェックです。
 public int64_t Position()  |  ストリーム内の現在の位置を取得します。
 public int64_t Size()  |  ストリーム内のコンテンツのサイズを取得します。
 public void Size(int64_t value)  |  ストリームのサイズを設定します。
  
## <a name="members"></a>メンバー
  
### <a name="read"></a>読み取り
ストリームからバッファーに読み取ります。

パラメーター:  
* **buffer**: バッファーへのポインター 


* **bufferLength**: バッファー サイズ。 



  
**戻り値**: 読み込まれたバイト数。
  
### <a name="write"></a>書き込み
バッファーからストリームに書き込みます。

パラメーター:  
* **buffer**: バッファーへのポインター 


* **bufferLength**: バッファー サイズ。 



  
**戻り値**: 書き込まれたバイト数。
  
### <a name="flush"></a>フラッシュ
ストリームをフラッシュします。

  
**戻り値**: 正常終了した場合は true、それ以外の場合は false。
  
### <a name="seek"></a>Seek
ストリーム内の特定の位置をシークします。

パラメーター:  
* **position**: ストリームをシークする位置。


  
### <a name="canread"></a>CanRead
ストリームから読み込めるかどうかのチェックです。

  
**戻り値**: 読み取り可能な場合は true、それ以外の場合は false。
  
### <a name="canwrite"></a>CanWrite
ストリームに書き込めるかどうかのチェックです。

  
**戻り値**: 書き出し可能な場合は true、それ以外の場合は false。
  
### <a name="position"></a>位置
ストリーム内の現在の位置を取得します。

  
**戻り値**: ストリーム内の位置。
  
### <a name="size"></a>Size
ストリーム内のコンテンツのサイズを取得します。

  
**戻り値**: ストリームのサイズ。
  
### <a name="size"></a>Size
ストリームのサイズを設定します。

パラメーター:  
* **stream**: ストリームのサイズ。

