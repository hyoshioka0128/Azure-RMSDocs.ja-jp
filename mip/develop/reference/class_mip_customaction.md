---
title: class mip::CustomAction
description: Mip::customaction クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 12ecba0f442ee3e51a5cb58e77bee546ac262deb
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333570"
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
