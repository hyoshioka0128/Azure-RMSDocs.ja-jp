---
title: クラス ExecutionState
description: 'Microsoft Information Protection (MIP) SDK の executionstate:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 543b46f8ceb731e7ea7c4e513f1a42c25a080521
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215461"
---
# <a name="class-executionstate"></a>クラス ExecutionState 
エンジンの実行に必要なすべての状態のインターフェイス。
クライアントでは、必要な状態を取得するメソッドのみを呼び出す必要があります。 そのため、効率を高めるために、クライアントは対応する状態が事前に計算されるのではなく動的に計算されるようにこのインターフェイスを実装できます。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std:: shared_ptr \<Label\> getnewlabel () const  |  ドキュメントに適用される必要のある機密ラベル ID を取得します。
public std::string GetContentIdentifier() const  |  ドキュメントを説明するコンテンツの説明を取得します。 ファイルの例: [表し] 電子メールの例: [件名: 送信者]。
パブリック仮想 DataState GetDataState () const  |  アプリケーションで操作中のコンテンツの状態を取得します。
public std::p air \<bool, std::string\> IsDowngradeJustified () const  |  実装では、既存のラベルのダウングレードの理由が示されたかどうかを渡す必要があります。
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  新しいラベルの割り当て方法を取得します。
パブリック仮想 std:: vector \<std::pair\<std::string, std::string\> \> getnewlabelextendedproperties () const  |  新しいラベルの拡張プロパティを返します。
public std:: vector \<MetadataEntry\> getcontentmetadata (const std:: vector \<std::string\>& names, const std:: Vector \<std::string\>& nameprefixes) const  |  コンテンツからメタデータ項目を取得します。
public std::shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor() const  |  保護記述子を取得します。
public std:: string GetContentFormat () const  |  コンテンツの形式を取得します。
パブリック仮想 MetadataVersion GetContentMetadataVersion () const  |  テナントのアプリケーションでサポートされている最大のメタデータバージョンを取得します。
public ActionType GetSupportedActions() const  |  サポートされているすべてのアクションの種類を表すマスクされた列挙型を取得します。
public virtual std:: shared_ptr \<ClassificationResults\> GetClassificationResults (const std:: vector \<std::shared_ptr\<ClassificationRequest\> \> &) const  |  分類結果のマップを返します。
public virtual std:: map \<std::string, std::string\> getauditmetadata () const  |  アプリケーション固有のキーと値のペアのマップを返します。
  
## <a name="members"></a>メンバー
  
### <a name="getnewlabel-function"></a>GetNewLabel 関数
ドキュメントに適用される必要のある機密ラベル ID を取得します。

  
**戻り値**: コンテンツに適用される機密ラベル ID が存在する場合はその ID、それ以外でラベルを削除する場合は空。
  
### <a name="getcontentidentifier-function"></a>GetContentIdentifier 関数
ドキュメントを説明するコンテンツの説明を取得します。 ファイルの例: [表し] 電子メールの例: [件名: 送信者]。

  
は、コンテンツに適用されるコンテンツの説明を **返し** ます。
この値は、人間が判読できるコンテンツの説明として監査で使用されます。
  
### <a name="getdatastate-function"></a>GetDataState 関数
アプリケーションで操作中のコンテンツの状態を取得します。

  
**戻り値**: コンテンツ データの状態
  
### <a name="isdowngradejustified-function"></a>IsDowngradeJustified 関数
実装では、既存のラベルのダウングレードの理由が示されたかどうかを渡す必要があります。

  
**戻り値**: ダウングレードの正当性が理由メッセージと共に示される場合は true、それ以外の場合は false。 
  
**関連** 項目: mip:: ジャスト Ifyaction
  
### <a name="getnewlabelassignmentmethod-function"></a>Getnewlabelのメソッド関数
新しいラベルの割り当て方法を取得します。

  
**戻り値**: 割り当て方法: STANDARD、PRIVILEGED、AUTO。 
  
**関連項目**: mip::AssignmentMethod
  
### <a name="getnewlabelextendedproperties-function"></a>GetNewLabelExtendedProperties 関数
新しいラベルの拡張プロパティを返します。

  
**戻り値**: コンテンツに適用される拡張プロパティ。
  
### <a name="getcontentmetadata-function"></a>GetContentMetadata 関数
コンテンツからメタデータ項目を取得します。

  
**戻り値**: コンテンツに適用されるメタデータ。 各メタデータ項目は名前と値のペアです。
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor 関数
保護記述子を取得します。

  
**戻り値**: 保護記述子
  
### <a name="getcontentformat-function"></a>GetContentFormat 関数
コンテンツの形式を取得します。

  
**戻り値**: コンテンツ形式
  
### <a name="getcontentmetadataversion-function"></a>GetContentMetadataVersion 関数
テナントのアプリケーションでサポートされている最大のメタデータバージョンを取得します。

  
は、コンテンツメタデータのバージョン **を返し** ます。 0の場合、メタデータはバージョンが解除されます。 ファイル形式で複数のメタデータがサポートされている場合、MIP はすべてのメタデータを理解し、バージョンごとに詳細なメタデータの変更を報告できます。
  
### <a name="getsupportedactions-function"></a>GetSupportedActions 関数
サポートされているすべてのアクションの種類を表すマスクされた列挙型を取得します。

  
**戻り値**: サポートされているすべてのアクションの種類を表すマスクされた列挙型。
ActionType::Justify must be supported. ポリシーとラベルの変更に理由が必要な場合、常に理由アクションが返されます。
  
### <a name="getclassificationresults-function"></a>GetClassificationResults 関数
分類結果のマップを返します。

パラメーター:  
* **classificationIds**: 分類 id の一覧。 



  
**戻り値**: 分類結果の一覧。 分類サイクルが実行されていない場合は nullptr を返します。
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata 関数
アプリケーション固有のキーと値のペアのマップを返します。

  
**戻り** 値: アプリケーション固有の監査メタデータの登録済みキー: 値のペア送信者: 送信者受信者の電子メール id: 電子メールの受信者の JSON 配列: コンテンツを最後に変更したユーザーの電子メール id LastModifiedDate: コンテンツが最後に変更された日付