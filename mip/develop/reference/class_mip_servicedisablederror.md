---
title: ServiceDisabledError クラス
description: 'Microsoft Information Protection (MIP) SDK の servicedisablederror:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: b4ccba889ce025f343293d458f76ae7d63457f4f
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567050"
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