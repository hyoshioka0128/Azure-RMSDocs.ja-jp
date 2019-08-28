---
title: 'クラス mip:: MsgAttachmentData'
description: 'Microsoft Information Protection (MIP) SDK の mip:: msgattachmentdata クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 88ac473dd20db6499ab818adf47ddc5cb788e960
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055868"
---
# <a name="class-mipmsgattachmentdata"></a>クラス mip:: MsgAttachmentData 
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: vector\<uint8_t\>& GetBytes ()  |  バイナリバイトベクトルとして添付ファイルを取得します。
public std:: shared_ptr\<Stream\> system.resources.resourcemanager.getstream () const  |  バイナリストリームとして添付ファイルを取得します。
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