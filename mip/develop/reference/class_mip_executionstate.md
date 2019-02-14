---
title: class mip::ExecutionState
description: Mip::executionstate クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 7e036938923a3736dc184046049f30a04f1eb87f
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2019
ms.locfileid: "56251740"
---
# <a name="class-mipexecutionstate"></a>class mip::ExecutionState 
エンジンの実行に必要なすべての状態のインターフェイス。
クライアントでは、必要な状態を取得するメソッドのみを呼び出す必要があります。 そのため、効率を高めるために、クライアントは対応する状態が事前に計算されるのではなく動的に計算されるようにこのインターフェイスを実装できます。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::string GetNewLabelId() const  |  ドキュメントに適用される必要のある機密ラベル ID を取得します。
public ActionSource GetNewLabelActionSource() const  |  新しいラベル アクションのソースを取得します。
public std::string GetContentIdentifier() const  |  ドキュメントを説明するコンテンツ識別子を取得します。 ファイルの例: 電子メールの [&] 例: [サブジェクト: 送信者]。
public ContentState GetContentState() const  |  アプリケーションで操作中のコンテンツの状態を取得します。
public std::pair\<bool、std::string\> IsDowngradeJustified() 定数  |  実装では、既存のラベルのダウングレードの理由が示されたかどうかを渡す必要があります。
public AssignmentMethod GetNewLabelAssignmentMethod() const  |  新しいラベルの割り当て方法を取得します。
public std::vector\<std::pair\<std::string, std::string\>\> GetNewLabelExtendedProperties() const  |  新しいラベルの拡張プロパティを返します。
public std::vector\<std::pair\<std::string, std::string\>\> GetContentMetadata(const std::vector\<std::string\>& names, const std::vector\<std::string\>& namePrefixes) const  |  コンテンツからメタデータ項目を取得します。
public std::shared_ptr\<ProtectionDescriptor\> GetProtectionDescriptor() const  |  保護記述子を取得します。
public ContentFormat GetContentFormat() const  |  コンテンツの形式を取得します。
public ActionType GetSupportedActions() const  |  サポートされているすべてのアクションの種類を表すマスクされた列挙型を取得します。
public virtual std::map\<std::string, std::shared_ptr\<ClassificationResult\>\> GetClassificationResults(const std::vector\<std::shared_ptr\<ClassificationRequest\>\> &) const  |  分類結果のマップを返します。
public virtual std::map\<std::string, std::string\> GetAuditMetadata() const  |  アプリケーションの特定の監査のキー/値ペアのマップを返します。
  
## <a name="members"></a>メンバー
  
### <a name="getnewlabelid-function"></a>GetNewLabelId 関数
ドキュメントに適用される必要のある機密ラベル ID を取得します。

  
**返します**:場合、コンテンツに適用される機密ラベル ID が存在するラベルを削除するのには、空それ以外の場合。
  
### <a name="getnewlabelactionsource-function"></a>GetNewLabelActionSource 関数
新しいラベル アクションのソースを取得します。

  
**返します**:操作のソース。
  
### <a name="getcontentidentifier-function"></a>GetContentIdentifier 関数
ドキュメントを説明するコンテンツ識別子を取得します。 ファイルの例: 電子メールの [&] 例: [サブジェクト: 送信者]。

  
**返します**:コンテンツに適用するコンテンツ識別子。
この値は、人間が判読できるコンテンツの説明として監査で使用されます。
  
### <a name="getcontentstate-function"></a>GetContentState 関数
アプリケーションで操作中のコンテンツの状態を取得します。

  
**返します**:コンテンツ データの状態
  
### <a name="isdowngradejustified-function"></a>IsDowngradeJustified 関数
実装では、既存のラベルのダウングレードの理由が示されたかどうかを渡す必要があります。

  
**返します**:ダウン グレードが justifiedalong 妥当性の messageelse false の場合は true 
  
**関連項目**: [mip::JustifyAction](class_mip_justifyaction.md)
  
### <a name="getnewlabelassignmentmethod-function"></a>GetNewLabelAssignmentMethod 関数
新しいラベルの割り当て方法を取得します。

  
**返します**:割り当て方法 STANDARD、PRIVILEGED、AUTO。 
  
**参照してください**: [:assignmentmethod](mip-enums-and-structs.md#assignmentmethod-enum)
  
### <a name="getnewlabelextendedproperties-function"></a>GetNewLabelExtendedProperties function
新しいラベルの拡張プロパティを返します。

  
**返します**:拡張プロパティのコンテンツに適用します。
  
### <a name="getcontentmetadata-function"></a>GetContentMetadata 関数
コンテンツからメタデータ項目を取得します。

  
**返します**:コンテンツに適用されるメタデータ。 各メタデータ項目は名前と値のペアです。
  
### <a name="getprotectiondescriptor-function"></a>GetProtectionDescriptor 関数
保護記述子を取得します。

  
**返します**:保護記述子
  
### <a name="getcontentformat-function"></a>GetContentFormat 関数
コンテンツの形式を取得します。

  
**返します**:既定では、電子メール 
  
**参照してください**: [:contentformat](mip-enums-and-structs.md#contentformat-enum)
  
### <a name="getsupportedactions-function"></a>GetSupportedActions 関数
サポートされているすべてのアクションの種類を表すマスクされた列挙型を取得します。

  
**返します**:サポートされているアクションのすべての型を記述する、マスクされた列挙型。
ActionType::Justify must be supported. ポリシーとラベルの変更に理由が必要な場合、常に理由アクションが返されます。
  
### <a name="getclassificationresults-function"></a>GetClassificationResults 関数
分類結果のマップを返します。

パラメーター:  
* **classificationId**: 分類 ID の一覧。 



  
**返します**:分類結果の一覧。
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata 関数
アプリケーションの特定の監査のキー/値ペアのマップを返します。

  
**返します**:アプリケーションの特定の監査メタデータの登録キーと値ペア送信者の一覧:送信者が受信者の電子メール Id:LastModifiedBy、電子メールの受信者の JSON 配列を表します。コンテンツの LastModifiedDate を前回変更したユーザーの電子メール Id:コンテンツの最終変更日
