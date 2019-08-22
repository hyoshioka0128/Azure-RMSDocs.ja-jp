---
title: class mip::MetadataAction
description: 'Microsoft Information Protection (MIP) SDK の mip:: metadataaction クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 26a189d714001f4145ce328c163a052313923136
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885413"
---
# <a name="class-mipmetadataaction"></a>class mip::MetadataAction 
コンテンツにメタデータ情報を追加する[アクション](class_mip_action.md)。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::vector\<std::string\>& GetMetadataToRemove() const  |  コンテンツから削除する必要のあるメタデータの名前の一覧を取得します。
public const std::vector\<std::pair\<std::string, std::string\>\>& GetMetadataToAdd() const  |  コンテンツに追加するメタデータ名と値のペアを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove 関数
コンテンツから削除する必要のあるメタデータの名前の一覧を取得します。

  
次の**値を返し**ます。削除する文字列のベクター。 メタデータを追加する前にメタデータの削除を実行する必要があります。
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd 関数
コンテンツに追加するメタデータ名と値のペアを取得します。

  
次の**値を返し**ます。Const std:: vector < std::p air < std:: string、std:: string > > メタデータの削除 & メタデータを追加する前に実行する必要があります。