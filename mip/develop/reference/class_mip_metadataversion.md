---
title: クラス MetadataVersion
description: 'Microsoft Information Protection (MIP) SDK の metadataversion:: undefined クラスに関するドキュメントを示します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 35ed3ef28cd4a1a822c11f64b422a474edcd4b53
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213608"
---
# <a name="class-metadataversion"></a>クラス MetadataVersion 
MetadataVersion のインターフェイスです。 MetadataVersion は、アクティブなメタデータとその処理方法を決定します。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック MetadataVersion (uint32_t version、MetadataVersionFormat フラグ)  |  MetadataVersion コンストラクター。
パブリック仮想 uint32_t GetValue () const  |  数値バージョンを取得します。
パブリック仮想 bool HasFlag (MetadataVersionFormat フラグ) const  |  特定のフラグが設定されているかどうかを取得します。
パブリック仮想 MetadataVersionFormat GetFlags () const  |  特定のバージョンのメタデータの処理方法を定義するフラグを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="metadataversion-function"></a>MetadataVersion 関数
MetadataVersion コンストラクター。

パラメーター:  
* **バージョン**: メタデータアクションに使用する数値のバージョン 


* **flags**: バージョンを使用してメタデータアクションを計算する方法を指定するフラグ


  
### <a name="getvalue-function"></a>GetValue 関数
数値バージョンを取得します。

  
は、数値のバージョンを **返し** ます。
  
### <a name="hasflag-function"></a>HasFlag 関数
特定のフラグが設定されているかどうかを取得します。

  
は、フラグが設定されている場合は True **を返し** ます。
  
### <a name="getflags-function"></a>GetFlags 関数
特定のバージョンのメタデータの処理方法を定義するフラグを取得します。

  
は、メタデータの処理方法を指定するフラグを **返し** ます。