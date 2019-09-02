---
title: クラス mip::D ocumentState
description: Microsoft Information Protection (MIP) SDK の mip::d ocumentstate クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: d76da1fa15027abbac56b9432ef67c8d1b0996d9
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055156"
---
# <a name="class-mipdocumentstate"></a>クラス mip::D ocumentState 
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::string GetContentIdentifier() const  |  ドキュメントを説明するコンテンツの説明を取得します。 ファイルの例: [表し] 電子メールの例: [件名: 送信者]。
パブリック仮想 DataState GetDataState () const  |  アプリケーションで操作中のコンテンツの状態を取得します。
public std:: vector\<std::p air\<std:: string、std:: string\> \> getcontentmetadata (const std:: vector\<std:: string\>& names、const std:: vector\<std:: string\>& nameprefixes) const  |  コンテンツからメタデータ項目を取得します。
public std:: shared_ptr\<protectiondescriptor\> getprotectiondescriptor () const  |  保護記述子を取得します。
public ContentFormat GetContentFormat() const  |  コンテンツの形式を取得します。
public virtual std:: shared_ptr\<ClassificationResults\> GetClassificationResults (const std:: vector\<std:: shared_ptr\<ClassificationRequest\> \> &) const  |  分類結果のマップを返します。
public virtual std::map\<std::string, std::string\> GetAuditMetadata() const  |  アプリケーション固有のキーと値のペアのマップを返します。
  
## <a name="members"></a>メンバー
  
### <a name="getcontentidentifier-function"></a>GetContentIdentifier 関数
ドキュメントを説明するコンテンツの説明を取得します。 ファイルの例: [表し] 電子メールの例: [件名: 送信者]。

  
次の**値を返し**ます。コンテンツに適用されるコンテンツの説明。
この値は、人間が判読できるコンテンツの説明として監査で使用されます。
  
### <a name="getdatastate-function"></a>GetDataState 関数
アプリケーションで操作中のコンテンツの状態を取得します。

  
次の**値を返し**ます。コンテンツデータの状態
  
### <a name="getcontentmetadata-function"></a>GetContentMetadata 関数
コンテンツからメタデータ項目を取得します。

  
次の**値を返し**ます。コンテンツに適用されるメタデータ。 各メタデータ項目は名前と値のペアです。
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor 関数
保護記述子を取得します。

  
次の**値を返し**ます。保護記述子
  
### <a name="getcontentformat-function"></a>GetContentFormat 関数
コンテンツの形式を取得します。

  
次の**値を返し**ます。既定、電子メール 
  
**関連**項目: [Mip:: contentformat](mip-enums-and-structs.md#contentformat-enum)
  
### <a name="getclassificationresults-function"></a>GetClassificationResults 関数
分類結果のマップを返します。

パラメーター:  
* **classificationIds**: 分類 id の一覧。 



  
次の**値を返し**ます。分類結果の一覧。 分類サイクルが実行されていない場合は nullptr を返します。
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata 関数
アプリケーション固有のキーと値のペアのマップを返します。

  
次の**値を返し**ます。アプリケーション固有の監査メタデータの登録済みキー: 値のペア送信者:送信者受信者の電子メール Id:電子メールの受信者の JSON 配列を表します。コンテンツ LastModifiedDate を最後に変更したユーザーの電子メール Id:コンテンツが最後に変更された日付