---
title: class mip RemoveContentFooterAction
description: class mip RemoveContentFooterAction のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: d275e2256c8a65bf63fd16d5761f42563d7a7f07
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445633"
---
# <a name="class-mipremovecontentfooteraction"></a>class mip::RemoveContentFooterAction 
ドキュメントからのコンテンツ フッターの削除を指定するアクション クラス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::vector<std::string>& GetUIElementNames()  |  削除する必要のある UI 要素の検索に使用する必要がある名前の一覧を取得します。
 public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getuielementnames"></a>GetUIElementNames
削除する必要のある UI 要素の検索に使用する必要がある名前の一覧を取得します。

  
**戻り値**: UI 要素名の一覧。
  
### <a name="actiontype"></a>ActionType
[アクション](class_mip_action.md)の種類を取得します。

  
**戻り値**: ActionType: この基底クラスをキャストできる派生アクションの種類。