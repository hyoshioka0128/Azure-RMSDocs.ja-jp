---
title: クラスストリーム
description: 'Microsoft Information Protection (MIP) SDK の stream:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: a370d6917306f2865c1d91eb7fa90c2880497a04
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566625"
---
# <a name="class-stream"></a>クラスストリーム 
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


* **Bufferlength**: バッファーサイズ。 



  
**戻り値**: 読み込まれたバイト数。
  
### <a name="write-function"></a>Write 関数
バッファーからストリームに書き込みます。

パラメーター:  
* **buffer**: バッファーへのポインター 


* **Bufferlength**: バッファーサイズ。 



  
**戻り値**: 書き込まれたバイト数。
  
### <a name="flush-function"></a>Flush 関数
ストリームをフラッシュします。

  
**戻り値**: 正常終了した場合は true、それ以外の場合は false。
  
### <a name="seek-function"></a>Seek 関数
ストリーム内の特定の位置をシークします。

パラメーター:  
* **position**: ストリームをシークします。


  
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
* **ストリーム**: サイズ。

