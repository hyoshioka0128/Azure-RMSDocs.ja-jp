---
title: 'クラス mip:: MsgInspector'
description: 'Microsoft Information Protection (MIP) SDK の mip:: msginspector クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: d2c4f85989e5d9d77ebb540b0b4adfd64b8334c1
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489896"
---
# <a name="class-mipmsginspector"></a>クラス mip:: MsgInspector 
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: vector\<uint8_t\>& GetBody ()  |  メッセージの本文を取得します。 TXT/HTML が utf8 として書式設定されている場合はです。
パブリック BodyType GetBodyType () const  |  本文の種類を取得します。
public const std:: vector\<std:: unique_ptr\<MsgAttachmentData\>\>& GetAttachments () const  |  添付ファイルの一覧を msg 添付データオブジェクトとして取得します。
public InspectorType GetInspectorType () const  |  ファイルの種類を取得します。
public std:: shared_ptr\<Stream\> GetFileStream () const  |  ファイルストリームを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getbody-function"></a>GetBody 関数
メッセージの本文を取得します。 TXT/HTML が utf8 として書式設定されている場合はです。

  
は、バイトのベクターを**返し**ます。
  
### <a name="getbodytype-function"></a>GetBodyType 関数
本文の種類を取得します。

  
は、メッセージの本文の種類を**返し**ます。
  
### <a name="getattachments-function"></a>GetAttachments 関数
添付ファイルの一覧を msg 添付データオブジェクトとして取得します。

  
**戻り値**: std:: unique_ptr のベクター<MsgAttachmentData>
  
### <a name="getinspectortype-function"></a>GetInspectorType 関数
ファイルの種類を取得します。

  
は、InspectorType**を返し**ます。
  
### <a name="getfilestream-function"></a>GetFileStream 関数
ファイルストリームを取得します。

  
は、ファイルストリームへの共有 ptr を**返し**ます。