---
title: クラス DocumentState
description: 'Microsoft Information Protection (MIP) SDK の documentstate:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 674e43b89a43fe90fa1fb38fb7c6d1d51a7326e0
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763320"
---
# <a name="class-documentstate"></a>クラス DocumentState 
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::string GetContentIdentifier() const  |  ドキュメントを説明するコンテンツの説明を取得します。 ファイルの例: [表し] 電子メールの例: [件名: 送信者]。
パブリック仮想 DataState GetDataState () const  |  アプリケーションで操作中のコンテンツの状態を取得します。
public std:: vector\<metadataentry\> getcontentmetadata (const std:: vector\<std:: string\>& names, const std:: vector\<std:: string\>& nameprefixes) const  |  コンテンツからメタデータ項目を取得します。
public std:: shared_ptr\<protectiondescriptor\> getprotectiondescriptor () const  |  保護記述子を取得します。
public ContentFormat GetContentFormat() const  |  コンテンツの形式を取得します。
パブリック仮想署名なし int GetContentMetadataVersion () const  |  テナントのアプリケーションでサポートされている最大のメタデータバージョンを取得します。
public virtual std:: shared_ptr\<ClassificationResults\> GetClassificationResults (const std:: vector\<std:: shared_ptr\<ClassificationRequest\> \> &) const  |  分類結果のマップを返します。
public virtual std:: map\<std:: string、std:: string\> getauditmetadata () const  |  アプリケーション固有のキーと値のペアのマップを返します。
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

  
**戻り値**: コンテンツに適用されるメタデータ。 
  
「Mip:: MetadataEntry **」も参照してください**。
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor 関数
保護記述子を取得します。

  
**戻り値**: 保護記述子
  
### <a name="getcontentformat-function"></a>GetContentFormat 関数
コンテンツの形式を取得します。

  
**戻り値**: DEFAULT、EMAIL 
  
**次も参照**: mip::ContentFormat
  
### <a name="getcontentmetadataversion-function"></a>GetContentMetadataVersion 関数
テナントのアプリケーションでサポートされている最大のメタデータバージョンを取得します。

  
は、コンテンツメタデータのバージョン**を返し**ます。 0の場合、メタデータはバージョンが解除されます。 ファイル形式で複数のメタデータがサポートされている場合、MIP はすべてのメタデータを理解し、バージョンごとに詳細なメタデータの変更を報告できます。
  
### <a name="getclassificationresults-function"></a>GetClassificationResults 関数
分類結果のマップを返します。

パラメーター:  
* **classificationIds**: 分類 id の一覧。 



  
**戻り値**: 分類結果の一覧。 分類サイクルが実行されていない場合は nullptr を返します。
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata 関数
アプリケーション固有のキーと値のペアのマップを返します。

  
**戻り**値: アプリケーション固有の監査メタデータの登録済みキー: 値のペア送信者: 送信者受信者の電子メール id: 電子メールの受信者の JSON 配列: コンテンツを最後に変更したユーザーの電子メール id LastModifiedDate: コンテンツが最後に変更された日付
  
### <a name="getlastmodifiedtime-function"></a>GetLastModifiedTime 関数
ドキュメントが最後に変更された時刻までの時間を返します。

  
**戻り値**: ドキュメントのタイムポイントの最終更新時刻。