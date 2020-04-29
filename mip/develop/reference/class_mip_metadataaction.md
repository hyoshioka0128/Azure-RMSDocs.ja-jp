---
title: クラス MetadataAction
description: 'Microsoft Information Protection (MIP) SDK の metadataaction:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: d36a97130fd8a04f8053b6c272cea9af050cb89c
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81761623"
---
# <a name="class-metadataaction"></a>クラス MetadataAction 
コンテンツにメタデータ情報を追加するアクション。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: vector\<std:: String\>& getmetadatatoremove) const  |  コンテンツから削除する必要のあるメタデータの名前の一覧を取得します。
public const std:: vector\<metadataentry\>& GetMetadataToAdd () const  |  コンテンツに追加するメタデータ名と値のペアを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove 関数
コンテンツから削除する必要のあるメタデータの名前の一覧を取得します。

  
**戻り値**: 削除する文字列のベクター。 メタデータを追加する前にメタデータの削除を実行する必要があります。
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd 関数
コンテンツに追加するメタデータ名と値のペアを取得します。

  
**戻り値**: Const std::<MetadataEntry> vector& メタデータの削除は、メタデータを追加する前に行う必要があります。