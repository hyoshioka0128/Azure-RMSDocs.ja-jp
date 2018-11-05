---
title: class mip CustomAction
description: class mip CustomAction のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a94a41c0e7f7848201e2af44187cce2540579b27
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47444725"
---
# <a name="class-mipcustomaction"></a>class mip::CustomAction 
[CustomAction](class_mip_customaction.md) は、アクションのすべてのサブプロパティをプロパティ バッグとしてキャプチャする汎用アクション クラスです。 呼び出し元は、アクションの意味を理解する必要があります。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const std::string& GetName() const  |  アクション名を取得します。
public const std::vector<std::pair<std::string, std::string>>& GetProperties() const  |  プロパティ キーと値のペアの一覧を取得します。
 public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getname"></a>GetName
アクション名を取得します。

  
**戻り値**: 存在する場合はアクション名。それ以外の場合、空の文字列。
  
### <a name="getproperties"></a>GetProperties
プロパティ キーと値のペアの一覧を取得します。

  
**戻り値**: キーと値のペアの一覧。
  
### <a name="actiontype"></a>ActionType
[アクション](class_mip_action.md)の種類を取得します。

  
**戻り値**: ActionType: この基底クラスをキャストできる派生アクションの種類。