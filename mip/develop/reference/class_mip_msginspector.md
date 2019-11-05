---
title: 'クラス mip:: MsgInspector'
description: 'Microsoft Information Protection (MIP) SDK の mip:: msginspector クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: d1234168e4ce3996077b705e904f5765b761ec4c
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73558610"
---
# <a name="class-mipmsginspector"></a>クラス mip:: MsgInspector 
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: vector\<uint8_t\>& GetBody ()  |  メッセージの本文を取得します。 TXT/HTML が utf8 として書式設定されている場合はです。
パブリック BodyType GetBodyType () const  |  本文の種類を取得します。
public const std:: vector\<std:: unique_ptr\<MsgAttachmentData\>\>& GetAttachments () const  |  添付ファイルの一覧を msg 添付データオブジェクトとして取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getbody-function"></a>GetBody 関数
メッセージの本文を取得します。 TXT/HTML が utf8 として書式設定されている場合はです。

  
は、バイトのベクターを**返し**ます。
  
### <a name="getbodytype-function"></a>GetBodyType 関数
本文の種類を取得します。

  
は、メッセージの本文の種類を**返し**ます。
  
### <a name="getattachments-function"></a>GetAttachments 関数
添付ファイルの一覧を msg 添付データオブジェクトとして取得します。

  
は、std::<MsgAttachmentData> unique_ptr のベクターを**返し**ます。