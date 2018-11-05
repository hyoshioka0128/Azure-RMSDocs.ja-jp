---
title: class mip MetadataAction
description: class mip MetadataAction のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 8f7480775a0226c7161c9ad770184e54427a5084
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47444621"
---
# <a name="class-mipmetadataaction"></a>class mip::MetadataAction 
コンテンツにメタデータ情報を追加する[アクション](class_mip_action.md)。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::vector<std::string>& GetMetadataToRemove() const  |  コンテンツから削除する必要のあるメタデータの名前の一覧を取得します。
public const std::vector<std::pair<std::string, std::string>>& GetMetadataToAdd() const  |  コンテンツに追加するメタデータ名と値のペアを取得します。
 public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getmetadatatoremove"></a>GetMetadataToRemove
コンテンツから削除する必要のあるメタデータの名前の一覧を取得します。

  
**戻り値**: 削除する文字列のベクター。 メタデータを追加する前にメタデータの削除を実行する必要があります。
  
### <a name="getmetadatatoadd"></a>GetMetadataToAdd
コンテンツに追加するメタデータ名と値のペアを取得します。

  
**戻り値**: const std::vector<std::pair<std::string, std::string>>& メタデータを追加する前にメタデータの削除を実行する必要があります。
  
### <a name="actiontype"></a>ActionType
[アクション](class_mip_action.md)の種類を取得します。

  
**戻り値**: ActionType: この基底クラスをキャストできる派生アクションの種類。