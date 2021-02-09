---
title: TelemetryEvent クラス
description: 'Microsoft Information Protection (MIP) SDK の telemetryevent:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 8776eff24a889a1132fc71d11c38b02c49822263
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98225031"
---
# <a name="class-telemetryevent"></a>TelemetryEvent クラス 
単一のテレメトリイベント。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std::string& GetName() const  |  イベント名を取得します。
パブリック EventLevel GetLevel () const  |  イベントのレベルを取得します。これは、必要なサービスデータ (NSD) であるかどうかを示します。
public const std:: chrono:: steady_clock:: time_point& GetStartTime () const  |  イベントの開始時刻を取得します。
public void AddProperty (const std:: shared_ptr \<EventProperty\>& prop)  |  イベントにプロパティを追加します。
public void AddProperty (const std:: string& name, bool value)  |  ブール型のプロパティをイベントに追加します。
public void AddProperty (const std:: string& name、double value、Pii pii)  |  イベントに double プロパティを追加します。
public void AddProperty (const std:: string& name、int64_t value、Pii pii)  |  Int64 プロパティをイベントに追加します。
public void AddProperty (const std:: string& name、const std:: string& value、Pii pii)  |  イベントに文字列プロパティを追加します。
public void Addauditono プロパティ (const std:: string& name, const std:: string& value)  |  監査のみの文字列プロパティをイベントに追加します。
public std:: vector \<std::shared_ptr\<EventProperty\> \> GetProperties () const  |  すべてのイベントプロパティを取得します。
public std:: shared_ptr \<EventProperty\> GetProperty (const std:: string& name)  |  指定された名前を持つプロパティを取得します (存在する場合)。
  
## <a name="members"></a>メンバー
  
### <a name="getname-function"></a>GetName 関数
イベント名を取得します。

  
**戻り値**: イベント名
  
### <a name="getlevel-function"></a>GetLevel 関数
イベントのレベルを取得します。これは、必要なサービスデータ (NSD) であるかどうかを示します。

  
**戻り値**: イベントのレベル
  
### <a name="getstarttime-function"></a>GetStartTime 関数
イベントの開始時刻を取得します。

  
**戻り値**: イベントの開始時刻
  
### <a name="addproperty-function"></a>AddProperty 関数
イベントにプロパティを追加します。

パラメーター:  
* **prop**: 追加するプロパティ


  
### <a name="addproperty-function"></a>AddProperty 関数
ブール型のプロパティをイベントに追加します。

パラメーター:  
* **名前**: プロパティ名 


* **値**: プロパティ値


  
### <a name="addproperty-function"></a>AddProperty 関数
イベントに double プロパティを追加します。

パラメーター:  
* **名前**: プロパティ名 


* **値**: プロパティ値 


* **pii**: pii の分類


  
### <a name="addproperty-function"></a>AddProperty 関数
Int64 プロパティをイベントに追加します。

パラメーター:  
* **名前**: プロパティ名 


* **値**: プロパティ値 


* **pii**: pii の分類


  
### <a name="addproperty-function"></a>AddProperty 関数
イベントに文字列プロパティを追加します。

パラメーター:  
* **名前**: プロパティ名 


* **値**: プロパティ値 


* **pii**: pii の分類


  
### <a name="addauditonlyproperty-function"></a>Addauditonをプロパティ関数
監査のみの文字列プロパティをイベントに追加します。

パラメーター:  
* **名前**: プロパティ名 


* **値**: プロパティ値


監査のみのプロパティには機密情報が含まれており、手動でスキャンされされるまで、監査専用のプロパティにはファイルログやパイプラインへの書き込みを行わないでください。
  
### <a name="getproperties-function"></a>GetProperties 関数
すべてのイベントプロパティを取得します。

  
**戻り値**: イベントプロパティ
  
### <a name="getproperty-function"></a>GetProperty 関数
指定された名前を持つプロパティを取得します (存在する場合)。

パラメーター:  
* **名前**: 取得するプロパティの名前



  
は、指定された名前のプロパティ、または nullptr がない場合は nullptr を **返し** ます。