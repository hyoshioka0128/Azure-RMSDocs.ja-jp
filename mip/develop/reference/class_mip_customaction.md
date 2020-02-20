---
title: class mip::CustomAction
description: 'Microsoft Information Protection (MIP) SDK の mip:: customaction クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 9dfbd444684f68b954dd577c9ccdd208f55f9a89
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490197"
---
# <a name="class-mipcustomaction"></a>class mip::CustomAction 
CustomAction は、アクションのすべてのサブプロパティをプロパティバッグとしてキャプチャする汎用アクションクラスです。 呼び出し元は、アクションの意味を理解する必要があります。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  アクション名を取得します。
public const std:: vector\<std::p air\<std:: string、std:: string\>\>& GetProperties () const  |  プロパティ キーと値のペアの一覧を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getname-function"></a>GetName 関数
アクション名を取得します。

  
**戻り値**: 存在する場合はアクション名。それ以外の場合、空の文字列。
  
### <a name="getproperties-function"></a>GetProperties 関数
プロパティ キーと値のペアの一覧を取得します。

  
**戻り値**: キーと値のペアの一覧。