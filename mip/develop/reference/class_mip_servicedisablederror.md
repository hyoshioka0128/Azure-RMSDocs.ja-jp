---
title: 'クラス mip:: ServiceDisabledError'
description: 'Microsoft Information Protection (MIP) SDK の mip:: servicedisablederror クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 2fb7968ee2443d208ef3370308056eee4832e385
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057025"
---
# <a name="class-mipservicedisablederror"></a>クラス mip:: ServiceDisabledError 
サービスが無効になっているため、ユーザーはコンテンツにアクセスできませんでした。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public Extent GetExtent() const  |  サービスが無効になっている範囲を取得します。
範囲の列挙  |  サービスを無効にする範囲について説明します。
  
## <a name="members"></a>メンバー
  
### <a name="getextent-function"></a>GetExtent 関数
サービスが無効になっている範囲を取得します。

  
次の**値を返し**ます。サービスが無効になっている範囲
  
### <a name="extent-enum"></a>エクステント列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
ユーザー            | ユーザーのサービスが無効になっています。
デバイス            | デバイスのサービスが無効になっています。
プラットフォーム            | プラットフォームでサービスが無効になっています。
テナント            | テナントのサービスが無効になっています。
サービスを無効にする範囲について説明します。