---
title: class mip::Stream
description: Mip::stream クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: cc7d803e572be16a817292c702c5990b7720ddd8
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252131"
---
# <a name="class-mipstream"></a>class mip::Stream 
MIP SDK とストリーム ベースのコンテンツの間のインターフェイスを定義するクラス。
  
## <a name="summary"></a>まとめ
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



  
**返します**:読み取られたバイト数。
  
### <a name="write-function"></a>Write 関数
バッファーからストリームに書き込みます。

パラメーター:  
* **buffer**: バッファーへのポインター 


* **bufferLength**: バッファー サイズ。 



  
**返します**:書き込まれたバイト数。
  
### <a name="flush-function"></a>Flush 関数
ストリームをフラッシュします。

  
**返します**:成功した場合は true。 他は false。
  
### <a name="seek-function"></a>Seek 関数
ストリーム内の特定の位置をシークします。

パラメーター:  
* **position**: ストリームをシークする位置。


  
### <a name="canread-function"></a>CanRead 関数
ストリームから読み込めるかどうかのチェックです。

  
**返します**:読み取り可能な場合は true。 他は false。
  
### <a name="canwrite-function"></a>CanWrite 関数
ストリームに書き込めるかどうかのチェックです。

  
**返します**:書き込み可能な場合は true。 他は false。
  
### <a name="position-function"></a>Position 関数
ストリーム内の現在の位置を取得します。

  
**返します**:ストリーム内の位置。
  
### <a name="size-function"></a>サイズ関数
ストリーム内のコンテンツのサイズを取得します。

  
**返します**:ストリームのサイズ。
  
### <a name="size-function"></a>サイズ関数
ストリームのサイズを設定します。

パラメーター:  
* **stream**: ストリームのサイズ。

