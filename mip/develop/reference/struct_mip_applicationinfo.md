---
title: struct ApplicationInfo
description: Microsoft Information Protection (MIP) SDK に関連付けられているドキュメント構造。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 4971d7cf0891308733dafd0dc64d58c02343f1e4
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566553"
---
# <a name="struct-applicationinfo"></a>struct ApplicationInfo 
アプリケーション固有の情報を含む構造体。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::string applicationId  |  AAD ポータルで設定されたアプリケーション id (角かっこなしの GUID である必要があります)。
public std::string applicationName  |  アプリケーション名 ('; ' を除く有効な ASCII 文字のみを含める必要があります)
public std::string applicationVersion  |  使用されているアプリケーションのバージョン ('; ' を除く有効な ASCII 文字のみを含める必要があります)
  
## <a name="members"></a>メンバー
  
### <a name="applicationid-struct-member"></a>applicationId 構造体メンバー
AAD ポータルで設定されたアプリケーション id (角かっこなしの GUID である必要があります)。
  
### <a name="applicationname-struct-member"></a>applicationName 構造体メンバー
アプリケーション名 ('; ' を除く有効な ASCII 文字のみを含める必要があります)
  
### <a name="applicationversion-struct-member"></a>applicationVersion 構造体メンバー
使用されているアプリケーションのバージョン ('; ' を除く有効な ASCII 文字のみを含める必要があります)