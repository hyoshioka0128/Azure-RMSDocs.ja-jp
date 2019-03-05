---
title: class mip::MetadataAction
description: Mip::metadataaction クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: c180072eec94b2f71471c10b4344d65321ef49c6
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57332414"
---
# <a name="class-mipmetadataaction"></a>class mip::MetadataAction 
コンテンツにメタデータ情報を追加する[アクション](class_mip_action.md)。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::vector\<std::string\>& GetMetadataToRemove() const  |  コンテンツから削除する必要のあるメタデータの名前の一覧を取得します。
public const std::vector\<std::pair\<std::string, std::string\>\>& GetMetadataToAdd() const  |  コンテンツに追加するメタデータ名と値のペアを取得します。
public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getmetadatatoremove-function"></a>GetMetadataToRemove 関数
コンテンツから削除する必要のあるメタデータの名前の一覧を取得します。

  
**返します**:削除する文字列のベクトル。 メタデータを追加する前にメタデータの削除を実行する必要があります。
  
### <a name="getmetadatatoadd-function"></a>GetMetadataToAdd 関数
コンテンツに追加するメタデータ名と値のペアを取得します。

  
**返します**:Const std::vector < std::pair < std::string, std::string >> & Removing メタデータは、メタデータを追加する前に行う必要があります。
  
### <a name="gettype-function"></a>GetType 関数
[アクション](class_mip_action.md)の種類を取得します。

  
**返します**:ActionType: この基底クラスをキャストできる派生アクションの種類。
