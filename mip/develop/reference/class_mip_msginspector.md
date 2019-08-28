---
title: 'クラス mip:: MsgInspector'
description: 'Microsoft Information Protection (MIP) SDK の mip:: msginspector クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 274ada562bae46add2429a2f87442bb77528ea05
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70054260"
---
# <a name="class-mipmsginspector"></a>クラス mip:: MsgInspector 
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: vector\<uint8_t\>& getbody ()  |  メッセージの本文を取得します。 TXT/HTML が utf8 として書式設定されている場合はです。
パブリック BodyType GetBodyType () const  |  本文の種類を取得します。
public const std:: vector\<std:: unique_ptr\<msgattachmentdata\>\>& getattachments () const  |  添付ファイルの一覧を msg 添付データオブジェクトとして取得します。
public InspectorType GetInspectorType () const  |  ファイルの種類を取得します。
public std:: shared_ptr\<ストリーム\> getfilestream () const  |  ファイルストリームを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getbody-function"></a>GetBody 関数
メッセージの本文を取得します。 TXT/HTML が utf8 として書式設定されている場合はです。

  
次の**値を返し**ます。バイトのベクター。
  
### <a name="getbodytype-function"></a>GetBodyType 関数
本文の種類を取得します。

  
次の**値を返し**ます。メッセージの本文の種類。
  
### <a name="getattachments-function"></a>GetAttachments 関数
添付ファイルの一覧を msg 添付データオブジェクトとして取得します。

  
次の**値を返し**ます。Std:: unique_ptr のベクター<MsgAttachmentData>
  
### <a name="getinspectortype-function"></a>GetInspectorType 関数
ファイルの種類を取得します。

  
次の**値を返し**ます。InspectorType.
  
### <a name="getfilestream-function"></a>GetFileStream 関数
ファイルストリームを取得します。

  
次の**値を返し**ます。ファイルストリームへの共有 ptr。