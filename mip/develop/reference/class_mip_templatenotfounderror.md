---
title: クラス Templatenotfound エラー
description: 'Microsoft Information Protection (MIP) SDK の templatenotfound error:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 0ba4eae1c1c3d846c5e696a55a8a089b18a583ed
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95569447"
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
まだ文書化されていません。

  
### <a name="mdebuginfo"></a>mDebugInfo
まだ文書化されていません。

  
### <a name="mname"></a>mName
まだ文書化されていません。

  
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

 値                         | 説明                                
--------------------------------|---------------------------------------------
全般            | 一般的な無効な入力エラー
FileIsTooLargeForProtection            | ファイルが大きすぎて保護されません

無効な入力エラーの ErrorCode。