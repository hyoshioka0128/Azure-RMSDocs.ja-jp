---
title: class mip::MetadataAction
description: 'Microsoft Information Protection (MIP) SDK の mip:: metadataaction クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 405bb153527cb3fde346203d3b11c09c97110f12
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73558673"
---
# <a name="class-mipmetadataaction"></a>class mip::MetadataAction 
コンテンツにメタデータ情報を追加するアクション。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: vector\<std:: string\>& GetMetadataToRemove) const  |  コンテンツから削除する必要のあるメタデータの名前の一覧を取得します。
public const std:: vector\<std::p air\<std:: string、std:: string\>\>& GetMetadataToAdd () const  |  コンテンツに追加するメタデータ名と値のペアを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove 関数
コンテンツから削除する必要のあるメタデータの名前の一覧を取得します。

  
**戻り値**: 削除する文字列のベクター。 メタデータを追加する前にメタデータの削除を実行する必要があります。
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd 関数
コンテンツに追加するメタデータ名と値のペアを取得します。

  
**戻り値**: const std::vector<std::pair<std::string, std::string>>& メタデータを追加する前にメタデータの削除を実行する必要があります。