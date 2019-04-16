---
title: mip::NoPermissionsError をクラスします。
description: Mip::nopermissionserror クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: ac10820e1fa167888b857043219711a485632c00
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573702"
---
# <a name="class-mipnopermissionserror"></a>mip::NoPermissionsError をクラスします。 
ユーザーがコンテンツにアクセスできませんでした。 例: アクセス許可がない、コンテンツが取り消された。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public std::string GetReferrer() const  |  ドキュメントに対する権限の不足が発生した場合の連絡先を取得します。
public std::string GetOwner() const  | _まだ文書化されていません。_
public char const* what() const  |  エラー メッセージを取得します。
public std::shared_ptr\<エラー\> Clone() 定数  |  エラーを複製します。
public virtual ErrorType GetErrorType() const  |  エラーの種類を取得します。
public virtual const std::string& GetErrorName() const  |  エラー名を取得します。
public virtual const std::string& GetMessage() const  |  エラー メッセージを取得します。
public virtual void SetMessage(const std::string& msg)  |  エラー メッセージを設定します。
  
## <a name="members"></a>メンバー

### <a name="getreferrer-function"></a>GetReferrer 関数
ドキュメントに対する権限の不足が発生した場合の連絡先を取得します。

  
**返します**:ドキュメントに対する権限の不足が発生した場合にお問い合わせください。
  
### <a name="getowner-function"></a>GetOwner 関数
_まだ文書化されていません。_

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