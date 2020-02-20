---
title: クラス mip::D ocumentState
description: Microsoft Information Protection (MIP) SDK の mip::d ocumentstate クラスについて説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: a49683730f120b3d43e2c8f9381a86f0df1a400d
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490134"
---
# <a name="class-mipdocumentstate"></a>クラス mip::D ocumentState 
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::string GetContentIdentifier() const  |  ドキュメントを説明するコンテンツの説明を取得します。 ファイルの例: [表し] 電子メールの例: [件名: 送信者]。
パブリック仮想 DataState GetDataState () const  |  アプリケーションで操作中のコンテンツの状態を取得します。
public std:: vector\<std::p air\<std:: string、std:: string\>\> GetContentMetadata (const std:: vector\<std:: string\>& names、const std:: vector\<std:: string\>& namePrefixes) const  |  コンテンツからメタデータ項目を取得します。
public std:: shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor () const  |  保護記述子を取得します。
public ContentFormat GetContentFormat() const  |  コンテンツの形式を取得します。
public virtual std:: shared_ptr\<ClassificationResults\> GetClassificationResults (const std:: vector\<std:: shared_ptr\<ClassificationRequest\>\> &) const  |  分類結果のマップを返します。
パブリック仮想 std:: map\<std:: string、std:: string\> GetAuditMetadata () const  |  アプリケーション固有のキーと値のペアのマップを返します。
public virtual std:: chrono:: time_point\<std:: chrono:: system_clock\> GetLastModifiedTime () const  |  ドキュメントが最後に変更された時刻までの時間を返します。
  
## <a name="members"></a>メンバー
  
### <a name="getcontentidentifier-function"></a>GetContentIdentifier 関数
ドキュメントを説明するコンテンツの説明を取得します。 ファイルの例: [表し] 電子メールの例: [件名: 送信者]。

  
は、コンテンツに適用されるコンテンツの説明を**返し**ます。
この値は、人間が判読できるコンテンツの説明として監査で使用されます。
  
### <a name="getdatastate-function"></a>GetDataState 関数
アプリケーションで操作中のコンテンツの状態を取得します。

  
**戻り値**: コンテンツ データの状態
  
### <a name="getcontentmetadata-function"></a>GetContentMetadata 関数
コンテンツからメタデータ項目を取得します。

  
**戻り値**: コンテンツに適用されるメタデータ。 各メタデータ項目は名前と値のペアです。
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor 関数
保護記述子を取得します。

  
**戻り値**: 保護記述子
  
### <a name="getcontentformat-function"></a>GetContentFormat 関数
コンテンツの形式を取得します。

  
**戻り値**: DEFAULT、EMAIL 
  
**関連**項目: [Mip:: contentformat](mip-enums-and-structs.md#contentformat-enum)
  
### <a name="getclassificationresults-function"></a>GetClassificationResults 関数
分類結果のマップを返します。

パラメータ:  
* **classificationIds**: 分類 id の一覧。 



  
**戻り値**: 分類結果の一覧。 分類サイクルが実行されていない場合は nullptr を返します。
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata 関数
アプリケーション固有のキーと値のペアのマップを返します。

  
**戻り**値: アプリケーション固有の監査メタデータの登録済みキー: 値のペア送信者: 送信者受信者の電子メール id: 電子メールの受信者の JSON 配列: コンテンツを最後に変更したユーザーの電子メール id LastModifiedDate: コンテンツが最後に変更された日付
  
### <a name="getlastmodifiedtime-function"></a>GetLastModifiedTime 関数
ドキュメントが最後に変更された時刻までの時間を返します。

  
**戻り値**: ドキュメントのタイムポイントの最終更新時刻。