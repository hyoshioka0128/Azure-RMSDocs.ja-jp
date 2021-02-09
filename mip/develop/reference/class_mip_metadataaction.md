---
title: クラス MetadataAction
description: 'Microsoft Information Protection (MIP) SDK の metadataaction:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 873901994f452f8a1b521653e9fc078ce1933883
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213676"
---
# <a name="class-metadataaction"></a>クラス MetadataAction 
コンテンツにメタデータ情報を追加するアクション。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: vector \<std::string\>& getmetadatatoremove) const  |  コンテンツから削除する必要のあるメタデータの名前の一覧を取得します。
public const std:: vector \<MetadataEntry\>& GetMetadataToAdd () const  |  コンテンツに追加するメタデータ名と値のペアを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove 関数
コンテンツから削除する必要のあるメタデータの名前の一覧を取得します。

  
**戻り値**: 削除する文字列のベクター。 メタデータを追加する前にメタデータの削除を実行する必要があります。
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd 関数
コンテンツに追加するメタデータ名と値のペアを取得します。

  
**戻り値**: Const std:: vector& メタデータ <MetadataEntry> の削除は、メタデータを追加する前に行う必要があります。