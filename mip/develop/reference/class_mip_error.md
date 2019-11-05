---
title: class mip::Error
description: 'Microsoft Information Protection (MIP) SDK の mip:: error クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: f59a2b394cbf0bfa5deb555e2c4cdd8c427ed7ea
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560294"
---
# <a name="class-miperror"></a>class mip::Error 
MIP SDK からレポートされる (スローまたは返される) すべてのエラーの基底クラス。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public char const* what() const  |  エラー メッセージを取得します。
public std:: shared_ptr\<Error\> Clone () const  |  エラーを複製します。
public virtual ErrorType GetErrorType() const  |  エラーの種類を取得します。
public virtual const std::string& GetErrorName() const  |  エラー名を取得します。
public virtual const std::string& GetMessage() const  |  エラー メッセージを取得します。
public virtual void SetMessage(const std::string& msg)  |  エラー メッセージを設定します。
  
## <a name="members"></a>メンバー
  
### <a name="what-function"></a>機能
エラー メッセージを取得します。

  
**戻り値**: エラー メッセージ
  
### <a name="clone-function"></a>複製関数
エラーを複製します。

  
**戻り値**: エラーの複製。
  
### <a name="geterrortype-function"></a>GetErrorType 関数
エラーの種類を取得します。

  
**戻り値**: エラーの種類。
  
### <a name="geterrorname-function"></a>GetErrorName 関数
エラー名を取得します。

  
**戻り値**: エラー名。
  
### <a name="getmessage-function"></a>GetMessage 関数
エラー メッセージを取得します。

  
**戻り値**: エラー メッセージ。
  
### <a name="setmessage-function"></a>SetMessage 関数
エラー メッセージを設定します。

パラメーター:  
* **msg**: エラー メッセージ。

