---
title: class mip::CustomAction
description: 'Microsoft Information Protection (MIP) SDK の mip:: customaction クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 450ae0e455f74c6cb9b1f6b0b6d8aded9b30b2bd
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558900"
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