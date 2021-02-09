---
title: EventProperty クラス
description: 'Microsoft Information Protection (MIP) SDK の eventproperty:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 5ee28e454aa5d7854c572df8ef6e4642482c1104
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98225061"
---
# <a name="class-eventproperty"></a>EventProperty クラス 
1つの監査/テレメトリプロパティ。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public EventPropertyType GetPropertyType () const  |  このプロパティの基になるデータ型を取得します。
public const std::string& GetName() const  |  プロパティの名前を取得します。
パブリック Pii GetPii () const  |  個人を特定できる情報 (PII) の分類 (存在する場合) を取得します。
public bool IsAuditOnly () const  |  このプロパティが監査パイプラインに限定されているかどうかを取得します。
public double GetDouble () const  |  プロパティ値の取得 (double)
public int64_t GetInt64 () const  |  プロパティ値の取得 (int64)
public const std:: string& GetString () const  |  プロパティ値の取得 (文字列)
  
## <a name="members"></a>メンバー
  
### <a name="getpropertytype-function"></a>GetPropertyType 関数
このプロパティの基になるデータ型を取得します。

  
**戻り値**: 基になるデータ型
  
### <a name="getname-function"></a>GetName 関数
プロパティの名前を取得します。

  
**戻り値**: プロパティの名前
  
### <a name="getpii-function"></a>GetPii 関数
個人を特定できる情報 (PII) の分類 (存在する場合) を取得します。

  
**戻り値**: PII 分類
  
### <a name="isauditonly-function"></a>IsAuditOnly 関数
このプロパティが監査パイプラインに限定されているかどうかを取得します。

  
は、このプロパティが監査パイプラインに限定されているかどう **かを示します。これ** が True の場合、このプロパティには機密情報が含まれており、手動でスキャンされされるまで監査を除き、ファイルログやパイプラインに書き込むことはできません。
  
### <a name="getdouble-function"></a>GetDouble 関数
プロパティ値の取得 (double)

  
**戻り** 値: プロパティ値
  
### <a name="getint64-function"></a>GetInt64 関数
プロパティ値の取得 (int64)

  
**戻り** 値: プロパティ値
  
### <a name="getstring-function"></a>GetString 関数
プロパティ値の取得 (文字列)

  
**戻り** 値: プロパティ値