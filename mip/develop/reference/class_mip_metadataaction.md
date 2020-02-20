---
title: class mip::MetadataAction
description: 'Microsoft Information Protection (MIP) SDK の mip:: metadataaction クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 85d2742d5602dc2e36d9370a33fd04050fbeee9d
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77487720"
---
# <a name="class-mipmetadataaction"></a>class mip::MetadataAction 
コンテンツにメタデータ情報を追加するアクション。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
public const std:: vector\<std:: string\>& GetMetadataToRemove) const  |  コンテンツから削除する必要のあるメタデータの名前の一覧を取得します。
public const std:: vector\<std::p air\<std:: string、std:: string\>\>& GetMetadataToAdd () const  |  コンテンツに追加するメタデータ名と値のペアを取得します。
  
## <a name="members"></a>Members
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove 関数
コンテンツから削除する必要のあるメタデータの名前の一覧を取得します。

  
**戻り値**: 削除する文字列のベクター。 メタデータを追加する前にメタデータの削除を実行する必要があります。
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd 関数
コンテンツに追加するメタデータ名と値のペアを取得します。

  
**戻り値**: const std::vector<std::pair<std::string, std::string>>& メタデータを追加する前にメタデータの削除を実行する必要があります。