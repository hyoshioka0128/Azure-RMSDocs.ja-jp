---
title: クラス MetadataAction
description: 'Microsoft Information Protection (MIP) SDK の metadataaction:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 082a4332482bce35a436b70d4fa86ee7320d6f52
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566781"
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