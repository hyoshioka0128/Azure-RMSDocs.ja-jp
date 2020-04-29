---
title: クラス MsgInspector
description: 'Microsoft Information Protection (MIP) SDK の msginspector:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 79a044099c09d799d77f4af11eb0b80ecc21d6d6
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81761479"
---
# <a name="class-msginspector"></a>クラス MsgInspector 
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: vector\<Uint8_t\>& getbody ()  |  メッセージの本文を取得します。 TXT/HTML が utf8 として書式設定されている場合はです。
パブリック BodyType GetBodyType () const  |  本文の種類を取得します。
public const std:: vector\<std:: shared_ptr\<msgattachmentdata\> \>& getattachments () const  |  添付ファイルの一覧を msg 添付データオブジェクトとして取得します。
public InspectorType GetInspectorType () const  |  ファイルの種類を取得します。
public std:: shared_ptr\<Stream\> getfilestream () const  |  ファイルストリームを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getbody-function"></a>GetBody 関数
メッセージの本文を取得します。 TXT/HTML が utf8 として書式設定されている場合はです。

  
は、バイトのベクターを**返し**ます。
  
### <a name="getbodytype-function"></a>GetBodyType 関数
本文の種類を取得します。

  
は、メッセージの本文の種類を**返し**ます。
  
### <a name="getattachments-function"></a>GetAttachments 関数
添付ファイルの一覧を msg 添付データオブジェクトとして取得します。

  
は、std:: unique_ptr のベクターを**返し**ます。<MsgAttachmentData>
  
### <a name="getinspectortype-function"></a>GetInspectorType 関数
ファイルの種類を取得します。

  
は、InspectorType**を返し**ます。
  
### <a name="getfilestream-function"></a>GetFileStream 関数
ファイルストリームを取得します。

  
は、ファイルストリームへの共有 ptr を**返し**ます。