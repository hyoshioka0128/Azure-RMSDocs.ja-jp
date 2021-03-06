---
title: mip::ServiceDisabledError をクラスします。
description: Mip::servicedisablederror クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 1373d9ecc03f69267af631216a04d358e8be7af3
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60173373"
---
# <a name="class-mipservicedisablederror"></a>mip::ServiceDisabledError をクラスします。 
ユーザーは、サービスを無効になっているため、コンテンツへのアクセスを取得できませんでした。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public Extent GetExtent() const  |  サービスが無効になっているエクステントを取得します。
エクステントの列挙型  |  サービスが無効になっているエクステントをについて説明します。
public char const* what() const  |  エラー メッセージを取得します。
public std::shared_ptr\<エラー\> Clone() 定数  |  エラーを複製します。
public virtual ErrorType GetErrorType() const  |  エラーの種類を取得します。
public virtual const std::string& GetErrorName() const  |  エラー名を取得します。
public virtual const std::string& GetMessage() const  |  エラー メッセージを取得します。
public virtual void SetMessage(const std::string& msg)  |  エラー メッセージを設定します。
  
## <a name="members"></a>メンバー
  
### <a name="getextent-function"></a>GetExtent 関数
サービスが無効になっているエクステントを取得します。

  
**返します**:エクステントは、サービスが無効になっています
  
### <a name="extent-enum"></a>Extent 列挙型

サービスが無効になっているエクステントをについて説明します。

 値                         | [説明]                                
--------------------------------|---------------------------------------------
ユーザー            | サービスは、ユーザーに対して無効です。
デバイス            | デバイスのサービスは無効です。
プラットフォーム            | プラットフォームのサービスは無効です。
テナント            | サービスは、テナントに対して無効です。



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