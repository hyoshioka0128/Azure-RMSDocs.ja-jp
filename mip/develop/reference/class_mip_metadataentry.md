---
title: クラス MetadataEntry
description: 'Microsoft Information Protection (MIP) SDK の metadataentry:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 026fecc8da2008a2798ca8bc44951bc97ec5455a
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566787"
---
# <a name="class-metadataentry"></a>クラス MetadataEntry 
メタデータエントリの抽象クラス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック MetadataEntry (const std:: string& key、const std:: string& value、uint32_t version)  |  MetadataEntry 抽象化の場合は、c' tor です。
パブリック MetadataEntry (const std:: string& key、const std:: string& value、const Metadataentry& version)  |  MetadataEntry 抽象化の場合は、c' tor です。
パブリック MetadataEntry (const std:: string& key, const std:: string& value)  |  MetadataEntry 抽象化の場合、バージョンは既定値の0に設定されます。
public const std:: string& GetKey () const  |  メタデータエントリキーを取得します。
public const std:: string& GetValue () const  |  メタデータエントリの値を取得します。
パブリック MetadataVersion GetVersion () const  |  メタデータエントリのバージョンを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="metadataentry-function"></a>MetadataEntry 関数
MetadataEntry 抽象化の場合は、c' tor です。

パラメーター:  
* **キー**: メタデータキーのエントリ。 


* **値**: メタデータ値のエントリ 


* **バージョン**: メタデータバージョンの値


  
### <a name="metadataentry-function"></a>MetadataEntry 関数
MetadataEntry 抽象化の場合は、c' tor です。

パラメーター:  
* **キー**: メタデータキーのエントリ。 


* **値**: メタデータ値のエントリ 


* **バージョン**: メタデータバージョンの値


  
### <a name="metadataentry-function"></a>MetadataEntry 関数
MetadataEntry 抽象化の場合、バージョンは既定値の0に設定されます。

パラメーター:  
* **キー**: メタデータキーのエントリ。 


* **値**: メタデータ値のエントリ


  
### <a name="getkey-function"></a>GetKey 関数
メタデータエントリキーを取得します。

  
**戻り値**: メタデータエントリキー。
  
### <a name="getvalue-function"></a>GetValue 関数
メタデータエントリの値を取得します。

  
は、メタデータエントリの値 **を返し** ます。
  
### <a name="getversion-function"></a>GetVersion 関数
メタデータエントリのバージョンを取得します。

  
は、メタデータエントリのバージョン **を返し** ます。