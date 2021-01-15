---
title: クラス Templatenotfound エラー
description: 'Microsoft Information Protection (MIP) SDK の templatenotfound error:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 48182ae5d821aeed65e8c28b086dce0349b9af03
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212860"
---
# <a name="class-templatenotfounderror"></a>クラス Templatenotfound エラー 
テンプレート ID は RMS サービスによって認識されません。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std:: string mMessage  | _まだ文書化されていません。_
public std:: map \<std::string, std::string\> mDebugInfo  | _まだ文書化されていません。_
public std:: string mName  | _まだ文書化されていません。_
パブリック ErrorCode GetErrorCode () const  |  無効な入力の errorCode を取得します。
public char const* what() const  |  エラー メッセージを取得します。
public std::shared_ptr\<Error\> Clone() const  |  エラーを複製します。
public virtual ErrorType GetErrorType() const  |  エラーの種類を取得します。
public const std:: string& GetErrorName () const  |  エラー名を取得します。
public const std:: string& GetMessage () const  |  エラー メッセージを取得します。
public void SetMessage (const std:: string& msg)  |  エラー メッセージを設定します。
public void AddDebugInfo (const std:: string& key, const std:: string& value)  |  デバッグ情報エントリを追加します。
public const std:: map \<std::string, std::string\>& GetDebugInfo () const  |  デバッグ情報を取得します。
列挙型 ErrorCode  |  無効な入力エラーの ErrorCode。
  
## <a name="members"></a>メンバー
  
### <a name="mmessage"></a>mMessage
_まだ文書化されていません。_

  
### <a name="mdebuginfo"></a>mDebugInfo
_まだ文書化されていません。_

  
### <a name="mname"></a>mName
_まだ文書化されていません。_

  
### <a name="geterrorcode-function"></a>GetErrorCode 関数
無効な入力の errorCode を取得します。

  
**戻り値**: 無効な入力エラーの ErrorCode
  
### <a name="what-function"></a>機能
エラー メッセージを取得します。

  
**戻り値**: エラーメッセージ
  
### <a name="clone-function"></a>Clone 関数
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

  
は、エラーメッセージを **返し** ます。
  
### <a name="setmessage-function"></a>SetMessage 関数
エラー メッセージを設定します。

パラメーター:  
* **msg**: エラー メッセージ。


  
### <a name="adddebuginfo-function"></a>AddDebugInfo 関数
デバッグ情報エントリを追加します。

パラメーター:  
* **キー**: デバッグ情報キー 


* **値**: デバッグ情報の値


  
### <a name="getdebuginfo-function"></a>GetDebugInfo 関数
デバッグ情報を取得します。

  
**戻り** 値: デバッグ情報 (キー/値)
  
### <a name="errorcode-enum"></a>ErrorCode 列挙型

無効な入力エラーの ErrorCode。

 値                         | 説明                                
--------------------------------|---------------------------------------------
全般            | 一般的な無効な入力エラー
FileIsTooLargeForProtection            | ファイルが大きすぎて保護されません
