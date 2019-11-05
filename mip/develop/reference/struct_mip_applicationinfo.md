---
title: 'struct mip:: ApplicationInfo'
description: Microsoft Information Protection (MIP) SDK に関連付けられているドキュメント構造。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 6bee61bc72de35aeaefd9ef1e7639450392b70a7
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73567427"
---
# <a name="struct-mipapplicationinfo"></a>struct mip:: ApplicationInfo 
アプリケーション固有の情報を含む構造体。
  
## <a name="summary"></a>要約
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