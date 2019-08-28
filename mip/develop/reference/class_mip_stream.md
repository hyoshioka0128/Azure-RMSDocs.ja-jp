---
title: class mip::Stream
description: 'Microsoft Information Protection (MIP) SDK の mip:: stream クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: c799708931103c595ce1ad66a41accb9f0dcfc85
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056843"
---
# <a name="class-mipstream"></a>class mip::Stream 
MIP SDK とストリーム ベースのコンテンツの間のインターフェイスを定義するクラス。
  
## <a name="summary"></a>Summary
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



  
次の**値を返し**ます。読み取ったバイト数。
  
### <a name="write-function"></a>Write 関数
バッファーからストリームに書き込みます。

パラメーター:  
* **buffer**: バッファーへのポインター 


* **bufferLength**: バッファー サイズ。 



  
次の**値を返し**ます。書き込まれたバイト数。
  
### <a name="flush-function"></a>Flush 関数
ストリームをフラッシュします。

  
次の**値を返し**ます。成功した場合は True、それ以外の場合は false。
  
### <a name="seek-function"></a>Seek 関数
ストリーム内の特定の位置をシークします。

パラメーター:  
* **position**: ストリームをシークする位置。


  
### <a name="canread-function"></a>CanRead 関数
ストリームから読み込めるかどうかのチェックです。

  
次の**値を返し**ます。読み取り可能な場合は True。それ以外の場合は false。
  
### <a name="canwrite-function"></a>CanWrite 関数
ストリームに書き込めるかどうかのチェックです。

  
次の**値を返し**ます。書き込み可能な場合は false。
  
### <a name="position-function"></a>Position 関数
ストリーム内の現在の位置を取得します。

  
次の**値を返し**ます。ストリーム内の位置。
  
### <a name="size-function"></a>Size 関数
ストリーム内のコンテンツのサイズを取得します。

  
次の**値を返し**ます。ストリームのサイズ。
  
### <a name="size-function"></a>Size 関数
ストリームのサイズを設定します。

パラメーター:  
* **stream**: ストリームのサイズ。

