---
title: class mip::CustomAction
description: 'Microsoft Information Protection (MIP) SDK の mip:: customaction クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: e71adc9c791f71b73c9386955d6b9606f2554f83
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884385"
---
# <a name="class-mipcustomaction"></a>class mip::CustomAction 
[CustomAction](class_mip_customaction.md) は、アクションのすべてのサブプロパティをプロパティ バッグとしてキャプチャする汎用アクション クラスです。 呼び出し元は、アクションの意味を理解する必要があります。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  アクション名を取得します。
public const std:: vector\<std::p air\<std:: string、std:: string\>\>& GetProperties () const  |  プロパティ キーと値のペアの一覧を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getname-function"></a>GetName 関数
アクション名を取得します。

  
次の**値を返し**ます。アクション名が存在する場合は、それ以外の場合は空の文字列。
  
### <a name="getproperties-function"></a>GetProperties 関数
プロパティ キーと値のペアの一覧を取得します。

  
次の**値を返し**ます。キーと値のペアの一覧。