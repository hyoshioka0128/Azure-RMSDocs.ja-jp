---
title: 'クラス mip:: ServiceDisabledError'
description: 'Microsoft Information Protection (MIP) SDK の mip:: servicedisablederror クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 1481e81707e84d7ba977d36bec152ba86b5e60b6
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489420"
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
ユーザー            | ユーザーのサービスが無効になっています。
デバイス            | デバイスのサービスが無効になっています。
プラットフォーム            | プラットフォームでサービスが無効になっています。
テナント            | テナントのサービスが無効になっています。
サービスを無効にする範囲について説明します。