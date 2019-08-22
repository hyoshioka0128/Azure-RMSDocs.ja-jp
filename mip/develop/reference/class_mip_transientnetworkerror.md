---
title: class mip::TransientNetworkError
description: 'Microsoft Information Protection (MIP) SDK の mip:: の実行エラークラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 5787c5742edc2daefee00a3c5a9b2bf826b81529
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69882898"
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

