---
title: クラス MsgAttachmentData
description: 'Microsoft Information Protection (MIP) SDK の msgattachmentdata:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: c729b2907878aa383b058689c55072e53541a595
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566752"
---
# <a name="class-msgattachmentdata"></a>クラス MsgAttachmentData 
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: vector \<uint8_t\>& GetBytes ()  |  バイナリバイトベクトルとして添付ファイルを取得します。
public std:: shared_ptr \<Stream\> system.resources.resourcemanager.getstream () const  |  バイナリストリームとして添付ファイルを取得します。
public const std::string& GetName() const  |  添付ファイルの名前を文字列として取得します。
public const std:: string& GetLongName () const  |  添付ファイルの長い名前を文字列として取得します。
public const std::string& GetPath() const  |  添付ファイルのパス名を文字列として取得します。 パスが空でない場合は、添付ファイルを参照します。
public const std:: string& GetLongPath () const  |  添付ファイルの長いパス名を文字列として取得します。 パスが空でない場合は、添付ファイルを参照します。
  
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