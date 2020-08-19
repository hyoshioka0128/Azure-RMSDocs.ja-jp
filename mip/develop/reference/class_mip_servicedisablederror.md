---
title: ServiceDisabledError クラス
description: 'Microsoft Information Protection (MIP) SDK の servicedisablederror:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 3dc6d73f12dc1512d1850d465a966e99d13b52c9
ms.sourcegitcommit: dc50f9a6c2f66544893278a7fd16dff38eef88c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/18/2020
ms.locfileid: "88564455"
---
# <a name="class-servicedisablederror"></a>ServiceDisabledError クラス

サービスが無効になっているため、ユーザーはコンテンツにアクセスできませんでした。
  
## <a name="summary"></a>まとめ

| メンバー                          | 説明
|----------------------------------|--------------------------------------------------------
| パブリックエクステント GetExtent () const  | サービスが無効になっている範囲を取得します。
| 範囲の列挙                      | サービスを無効にする範囲について説明します。
  
## <a name="members"></a>メンバー
  
### <a name="getextent-function"></a>GetExtent 関数
サービスが無効になっている範囲を取得します。

**戻り値**: サービスが無効になっているエクステント
  
### <a name="extent-enum"></a>エクステント列挙型

サービスを無効にする範囲について説明します。

| 値   | 説明
|----------|---------------------------------------
| User     | ユーザーのサービスが無効になっています。
| Device   | デバイスのサービスが無効になっています。
| プラットフォーム | プラットフォームでサービスが無効になっています。
| Tenant   | テナントのサービスが無効になっています。
