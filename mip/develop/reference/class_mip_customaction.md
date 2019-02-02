---
title: class mip::CustomAction
description: Mip::customaction クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 49840aebf5d49e91671145d0c5dc9e3b6d8e4694
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2019
ms.locfileid: "55650648"
---
# <a name="class-mipcustomaction"></a>class mip::CustomAction 
[CustomAction](class_mip_customaction.md) は、アクションのすべてのサブプロパティをプロパティ バッグとしてキャプチャする汎用アクション クラスです。 呼び出し元は、アクションの意味を理解する必要があります。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  アクション名を取得します。
public const std::vector\<std::pair\<std::string, std::string\>\>& GetProperties() const  |  プロパティ キーと値のペアの一覧を取得します。
public ActionType GetType() const  |  [アクション](class_mip_action.md)の種類を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getname-function"></a>GetName 関数
アクション名を取得します。

  
**返します**:それ以外の場合、空の文字列が存在する場合は、1 つのアクション名。
  
### <a name="getproperties-function"></a>GetProperties 関数
プロパティ キーと値のペアの一覧を取得します。

  
**返します**:キーと値のペアの一覧。
  
### <a name="gettype-function"></a>GetType 関数
[アクション](class_mip_action.md)の種類を取得します。

  
**返します**:ActionType: この基底クラスをキャストできる派生アクションの種類。