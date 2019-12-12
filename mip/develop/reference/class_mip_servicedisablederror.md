---
title: 'クラス mip:: ServiceDisabledError'
description: 'Microsoft Information Protection (MIP) SDK の mip:: servicedisablederror クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 766d3747c2dbe6a9fdecc6cb6e21eb3d4000d3ec
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558201"
---
# <a name="class-mipservicedisablederror"></a>クラス mip:: ServiceDisabledError 
サービスが無効になっているため、ユーザーはコンテンツにアクセスできませんでした。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public Extent GetExtent() const  |  サービスが無効になっている範囲を取得します。
範囲の列挙  |  サービスを無効にする範囲について説明します。
  
## <a name="members"></a>メンバー
  
### <a name="getextent-function"></a>GetExtent 関数
サービスが無効になっている範囲を取得します。

  
**戻り値**: サービスが無効になっているエクステント
  
### <a name="extent-enum"></a>エクステント列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
User            | ユーザーのサービスが無効になっています。
デバイス            | デバイスのサービスが無効になっています。
プラットフォーム            | プラットフォームでサービスが無効になっています。
テナント            | テナントのサービスが無効になっています。
サービスを無効にする範囲について説明します。