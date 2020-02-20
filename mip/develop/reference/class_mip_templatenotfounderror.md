---
title: 'クラス mip:: Templatenotfound エラー'
description: 'Microsoft Information Protection (MIP) SDK の mip:: templatenotfound error クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: babcf77de224a75b2beec7e0b15c867698b49c15
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489318"
---
# <a name="class-miptemplatenotfounderror"></a>クラス mip:: Templatenotfound エラー 
テンプレート ID は RMS サービスによって認識されません。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
public std:: string mMessage  | _まだ文書化されていません。_
public std:: map\<std:: string, std:: string\> mDebugInfo  | _まだ文書化されていません。_
public char const* what() const  |  エラー メッセージを取得します。
public std:: shared_ptr\<Error\> Clone () const  |  エラーを複製します。
public virtual ErrorType GetErrorType() const  |  エラーの種類を取得します。
public const std:: string & GetErrorName () const  |  エラー名を取得します。
public const std:: string & GetMessage () const  |  エラー メッセージを取得します。
public void SetMessage (const std:: string & msg)  |  エラー メッセージを設定します。
public void AddDebugInfo (const std:: string & key, const std:: string & value)  |  デバッグ情報エントリを追加します。
public const std:: map\<std:: string、std:: string\>& GetDebugInfo () const  |  デバッグ情報を取得します。
  
## <a name="members"></a>Members
  
### <a name="mmessage"></a>mMessage
_まだ文書化されていません。_

  
### <a name="mdebuginfo"></a>mDebugInfo
_まだ文書化されていません。_

  
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

パラメータ:  
* **msg**: エラー メッセージ。


  
### <a name="adddebuginfo-function"></a>AddDebugInfo 関数
デバッグ情報エントリを追加します。

パラメータ:  
* **キー**: デバッグ情報キー 


* **値**: デバッグ情報の値


  
### <a name="getdebuginfo-function"></a>GetDebugInfo 関数
デバッグ情報を取得します。

  
**戻り**値: デバッグ情報 (キー/値)