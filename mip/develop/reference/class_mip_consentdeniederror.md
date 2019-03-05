---
title: class mip::ConsentDeniedError
description: Mip::consentdeniederror クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 462f124ad4c181880222eecf696617fe8fe53d64
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333273"
---
# <a name="class-mipconsentdeniederror"></a>class mip::ConsentDeniedError 
ユーザーに同意を求めた操作で、同意が得られませんでした。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public char const* what() const  |  エラー メッセージを取得します。
public std::shared_ptr\<エラー\> Clone() 定数  |  エラーを複製します。
public virtual ErrorType GetErrorType() const  |  エラーの種類を取得します。
public virtual const std::string& GetErrorName() const  |  エラー名を取得します。
public virtual const std::string& GetMessage() const  |  エラー メッセージを取得します。
public virtual void SetMessage(const std::string& msg)  |  エラー メッセージを設定します。
  
## <a name="members"></a>メンバー
  
### <a name="what-function"></a>どのような関数
エラー メッセージを取得します。

  
**返します**:エラー メッセージ
  
### <a name="clone-function"></a>Clone 関数
エラーを複製します。

  
**返します**:エラーの複製。
  
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

