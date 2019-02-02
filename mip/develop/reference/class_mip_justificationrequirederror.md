---
title: class mip::JustificationRequiredError
description: Mip::justificationrequirederror クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 721037296ecc7d92fae6747a408ce84bfda4b34a
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650920"
---
# <a name="class-mipjustificationrequirederror"></a>class mip::JustificationRequiredError 
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual std::shared_ptr\<Error\> Clone() const  |  エラーを複製します。
public char const* what() const  |  エラー メッセージを取得します。
public virtual ErrorType GetErrorType() const  |  エラーの種類を取得します。
public virtual const std::string& GetErrorName() const  |  エラー名を取得します。
public virtual const std::string& GetMessage() const  |  エラー メッセージを取得します。
public virtual void SetMessage(const std::string& msg)  |  エラー メッセージを設定します。
  
## <a name="members"></a>メンバー
  
### <a name="clone-function"></a>Clone 関数
エラーを複製します。

  
**返します**:エラーの複製。
  
### <a name="what-function"></a>どのような関数
エラー メッセージを取得します。

  
**返します**:エラー メッセージ
  
### <a name="geterrortype-function"></a>GetErrorType 関数
エラーの種類を取得します。

  
**返します**:エラーの種類。
  
### <a name="geterrorname-function"></a>GetErrorName 関数
エラー名を取得します。

  
**返します**:エラー名です。
  
### <a name="getmessage-function"></a>GetMessage 関数
エラー メッセージを取得します。

  
**返します**:エラー メッセージ。
  
### <a name="setmessage-function"></a>SetMessage 関数
エラー メッセージを設定します。

パラメーター:  
* **msg**: エラー メッセージ。

