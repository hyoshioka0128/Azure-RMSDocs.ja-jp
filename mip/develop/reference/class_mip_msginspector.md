---
title: クラス MsgInspector
description: 'Microsoft Information Protection (MIP) SDK の msginspector:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: aaf9cc6803e0111cd37960f356d8a6bb19fd60a5
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215172"
---
# <a name="class-msginspector"></a>クラス MsgInspector 
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: vector \<uint8_t\>& getbody () const  |  メッセージの本文を取得します。 TXT/HTML が utf8 として書式設定されている場合はです。
パブリック unsigned int GetCodePage () const  |  Txt、html 本文形式に関連する、本文エンコードコードページを取得します。
パブリック BodyType GetBodyType () const  |  本文の種類を取得します。
public const std:: vector \<std::shared_ptr\<MsgAttachmentData\> \>& getattachments () const  |  添付ファイルの一覧を msg 添付データオブジェクトとして取得します。
public InspectorType GetInspectorType () const  |  ファイルの種類を取得します。
public std:: shared_ptr \<Stream\> getfilestream () const  |  ファイルストリームを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getbody-function"></a>GetBody 関数
メッセージの本文を取得します。 TXT/HTML が utf8 として書式設定されている場合はです。

  
は、バイトのベクターを **返し** ます。
  
### <a name="getcodepage-function"></a>GetCodePage 関数
Txt、html 本文形式に関連する、本文エンコードコードページを取得します。

  
は、符号なしのコードページ **を返し** ます。 
  
**関連** 項目: [https://docs.microsoft.com/en-us/windows/win32/intl/code-page-identifiers](https://docs.microsoft.com/windows/win32/intl/code-page-identifiers)
  
### <a name="getbodytype-function"></a>GetBodyType 関数
本文の種類を取得します。

  
は、メッセージの本文の種類を **返し** ます。
  
### <a name="getattachments-function"></a>GetAttachments 関数
添付ファイルの一覧を msg 添付データオブジェクトとして取得します。

  
は、std:: unique_ptr のベクターを **返し** ます。<MsgAttachmentData>
  
### <a name="getinspectortype-function"></a>GetInspectorType 関数
ファイルの種類を取得します。

  
は、InspectorType **を返し** ます。
  
### <a name="getfilestream-function"></a>GetFileStream 関数
ファイルストリームを取得します。

  
は、ファイルストリームへの共有 ptr を **返し** ます。