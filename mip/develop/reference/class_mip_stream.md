---
title: class mip::Stream
description: 'Microsoft Information Protection (MIP) SDK の mip:: stream クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: f1bd4220369d036c2071453412844e0691efb2ec
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559971"
---
# <a name="class-mipstream"></a>class mip::Stream 
MIP SDK とストリーム ベースのコンテンツの間のインターフェイスを定義するクラス。
  
## <a name="summary"></a>要約
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
  
### <a name="read-function"></a>Read 関数
ストリームからバッファーに読み取ります。

パラメーター:  
* **buffer**: バッファーへのポインター 


* **bufferLength**: バッファー サイズ。 



  
**戻り値**: 読み込まれたバイト数。
  
### <a name="write-function"></a>Write 関数
バッファーからストリームに書き込みます。

パラメーター:  
* **buffer**: バッファーへのポインター 


* **bufferLength**: バッファー サイズ。 



  
**戻り値**: 書き込まれたバイト数。
  
### <a name="flush-function"></a>Flush 関数
ストリームをフラッシュします。

  
**戻り値**: 正常終了した場合は true、それ以外の場合は false。
  
### <a name="seek-function"></a>Seek 関数
ストリーム内の特定の位置をシークします。

パラメーター:  
* **position**: ストリームをシークする位置。


  
### <a name="canread-function"></a>CanRead 関数
ストリームから読み込めるかどうかのチェックです。

  
**戻り値**: 読み取り可能な場合は true、それ以外の場合は false。
  
### <a name="canwrite-function"></a>CanWrite 関数
ストリームに書き込めるかどうかのチェックです。

  
**戻り値**: 書き出し可能な場合は true、それ以外の場合は false。
  
### <a name="position-function"></a>Position 関数
ストリーム内の現在の位置を取得します。

  
**戻り値**: ストリーム内の位置。
  
### <a name="size-function"></a>Size 関数
ストリーム内のコンテンツのサイズを取得します。

  
**戻り値**: ストリームのサイズ。
  
### <a name="size-function"></a>Size 関数
ストリームのサイズを設定します。

パラメーター:  
* **stream**: ストリームのサイズ。

