---
title: class mip::TransientNetworkError
description: 'Microsoft Information Protection (MIP) SDK の mip:: の実行エラークラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: c39c1e512a266009c6cf635f66c5d6cc8a931be1
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056817"
---
# <a name="class-miptransientnetworkerror"></a>class mip::TransientNetworkError 
一時的なネットワーク エラー。 サービス エンドポイントに対するネットワーク呼び出しを作成する際の、予期しない動作によって発生します。 このエラーは一時的なエラーであるため、この操作は再試行できます。
  
## <a name="summary"></a>Summary
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

  
次の**値を返し**ます。エラーメッセージ
  
### <a name="clone-function"></a>複製関数
エラーを複製します。

  
次の**値を返し**ます。エラーの複製。
  
### <a name="geterrortype-function"></a>GetErrorType 関数
エラーの種類を取得します。

  
次の**値を返し**ます。エラーの種類。
  
### <a name="geterrorname-function"></a>GetErrorName 関数
エラー名を取得します。

  
次の**値を返し**ます。エラー名。
  
### <a name="getmessage-function"></a>GetMessage 関数
エラー メッセージを取得します。

  
次の**値を返し**ます。エラーメッセージ。
  
### <a name="setmessage-function"></a>SetMessage 関数
エラー メッセージを設定します。

パラメーター:  
* **msg**: エラー メッセージ。

