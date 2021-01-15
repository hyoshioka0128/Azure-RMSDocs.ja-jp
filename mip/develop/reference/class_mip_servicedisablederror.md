---
title: ServiceDisabledError クラス
description: 'Microsoft Information Protection (MIP) SDK の servicedisablederror:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: e7f3ec6e3e02047607f696acd0a14cd632b5b0e9
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214288"
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

サービスを無効にする範囲について説明します。

 値                         | 説明                                
--------------------------------|---------------------------------------------
User            | ユーザーのサービスが無効になっています。
Device            | デバイスのサービスが無効になっています。
プラットフォーム            | プラットフォームでサービスが無効になっています。
Tenant            | テナントのサービスが無効になっています。
