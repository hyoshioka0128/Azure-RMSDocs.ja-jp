---
title: 'クラス mip:: MsgAttachmentData'
description: 'Microsoft Information Protection (MIP) SDK の mip:: msgattachmentdata クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: f9f47ca1503c912840fe1ed43542b5a4b4f2d0ec
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77487669"
---
# <a name="class-mipmsgattachmentdata"></a>クラス mip:: MsgAttachmentData 
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
public const std:: vector\<uint8_t\>& GetBytes ()  |  バイナリバイトベクトルとして添付ファイルを取得します。
public std:: shared_ptr\<Stream\> System.resources.resourcemanager.getstream () const  |  バイナリストリームとして添付ファイルを取得します。
public const std::string& GetName() const  |  添付ファイルの名前を文字列として取得します。
public const std:: string & GetLongName () const  |  添付ファイルの長い名前を文字列として取得します。
public const std::string& GetPath() const  |  添付ファイルのパス名を文字列として取得します。 パスが空でない場合は、添付ファイルを参照します。
public const std:: string & GetLongPath () const  |  添付ファイルの長いパス名を文字列として取得します。 パスが空でない場合は、添付ファイルを参照します。
  
## <a name="members"></a>Members
  
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