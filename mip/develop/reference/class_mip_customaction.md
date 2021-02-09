---
title: CustomAction クラス
description: 'Microsoft Information Protection (MIP) SDK の customaction:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: d1fb231d76ba2b5f076d42bbeeff95618c7386f3
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211704"
---
# <a name="class-customaction"></a>CustomAction クラス 
CustomAction は、アクションのすべてのサブプロパティをプロパティバッグとしてキャプチャする汎用アクションクラスです。 呼び出し元は、アクションの意味を理解する必要があります。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  アクション名を取得します。
public const std:: vector \<std::pair\<std::string, std::string\> \>& GetProperties () const  |  プロパティ キーと値のペアの一覧を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getname-function"></a>GetName 関数
アクション名を取得します。

  
**戻り値**: 存在する場合はアクション名。それ以外の場合、空の文字列。
  
### <a name="getproperties-function"></a>GetProperties 関数
プロパティ キーと値のペアの一覧を取得します。

  
**戻り値**: キーと値のペアの一覧。