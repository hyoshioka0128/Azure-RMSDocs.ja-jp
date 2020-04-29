---
title: ServiceDisabledError クラス
description: 'Microsoft Information Protection (MIP) SDK の servicedisablederror:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: ef521d9330df410bc14ad6ae856b837fc615cfbb
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81760684"
---
# <a name="class-servicedisablederror"></a>ServiceDisabledError クラス 
サービスが無効になっているため、ユーザーはコンテンツにアクセスできませんでした。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリックエクステント GetExtent () const  |  サービスが無効になっている範囲を取得します。
範囲の列挙  |  サービスを無効にする範囲について説明します。
  
## <a name="members"></a>メンバー
  
### <a name="getextent-function"></a>GetExtent 関数
サービスが無効になっている範囲を取得します。

  
**戻り値**: サービスが無効になっているエクステント
  
### <a name="extent-enum"></a>エクステント列挙型
 値                         | 説明                                
--------------------------------|---------------------------------------------
User            | ユーザーのサービスが無効になっています。
Device            | デバイスのサービスが無効になっています。
プラットフォーム            | プラットフォームでサービスが無効になっています。
Tenant            | テナントのサービスが無効になっています。
サービスを無効にする範囲について説明します。