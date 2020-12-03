---
title: struct ApplicationInfo
description: ApplicationInfo 構造体を文書にします。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: d56fdcaccf67f46b2d6632ec6586e2b140717696
ms.sourcegitcommit: 6322f840388067edbe3642661e313ff225be5563
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "96535588"
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