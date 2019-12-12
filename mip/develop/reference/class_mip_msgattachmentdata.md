---
title: 'クラス mip:: MsgAttachmentData'
description: 'Microsoft Information Protection (MIP) SDK の mip:: msgattachmentdata クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: bef08b98e09f9c6802ac9e39de293e9ec25bd380
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558632"
---
# <a name="class-mipmsgattachmentdata"></a>クラス mip:: MsgAttachmentData 
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: vector\<uint8_t\>& GetBytes ()  |  バイナリバイトベクトルとして添付ファイルを取得します。
public std:: shared_ptr\<Stream\> System.resources.resourcemanager.getstream () const  |  バイナリストリームとして添付ファイルを取得します。
public const std::string& GetName() const  |  添付ファイルの名前を文字列として取得します。
public const std:: string & GetLongName () const  |  添付ファイルの長い名前を文字列として取得します。
public const std::string& GetPath() const  |  添付ファイルのパス名を文字列として取得します。 パスが空でない場合は、添付ファイルを参照します。
public const std:: string & GetLongPath () const  |  添付ファイルの長いパス名を文字列として取得します。 パスが空でない場合は、添付ファイルを参照します。
  
## <a name="members"></a>メンバー
  
### <a name="getbytes-function"></a>GetBytes 関数
バイナリバイトベクトルとして添付ファイルを取得します。
  
### <a name="getstream-function"></a>System.resources.resourcemanager.getstream 関数
バイナリストリームとして添付ファイルを取得します。
  
### <a name="getname-function"></a>GetName 関数
添付ファイルの名前を文字列として取得します。
  
### <a name="getlongname-function"></a>GetLongName 関数
添付ファイルの長い名前を文字列として取得します。
  
### <a name="getpath-function"></a>GetPath 関数
添付ファイルのパス名を文字列として取得します。 パスが空でない場合は、添付ファイルを参照します。
  
### <a name="getlongpath-function"></a>GetLongPath 関数
添付ファイルの長いパス名を文字列として取得します。 パスが空でない場合は、添付ファイルを参照します。