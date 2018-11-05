---
title: class mip ExecutionState
description: class mip ExecutionState のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 976bca60f3f494a0fbf196e6512b00bdcdd63992
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446313"
---
# <a name="class-mipexecutionstate"></a>class mip::ExecutionState 
エンジンの実行に必要なすべての状態のインターフェイス。
クライアントでは、必要な状態を取得するメソッドのみを呼び出す必要があります。 そのため、効率を高めるために、クライアントは対応する状態が事前に計算されるのではなく動的に計算されるようにこのインターフェイスを実装できます。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public std::string GetNewLabelId() const  |  ドキュメントに適用される必要のある機密ラベル ID を取得します。
 public ActionSource GetNewLabelActionSource() const  |  新しいラベル アクションのソースを取得します。
 public std::string GetContentIdentifier() const  |  ドキュメントを説明するコンテンツ識別子を取得します。 ファイルの例: [パス] 電子メールの例: [件名:送信者]。
 public ContentState GetContentState() const  |  アプリケーションで操作中のコンテンツの状態を取得します。
public std::pair<bool, std::string> IsDowngradeJustified() const  |  実装では、既存のラベルのダウングレードの理由が示されたかどうかを渡す必要があります。
 public AssignmentMethod GetNewLabelAssignmentMethod() const  |  新しいラベルの割り当て方法を取得します。
public std::vector<std::pair<std::string, std::string>> GetNewLabelExtendedProperties() const  |  新しいラベルの拡張プロパティを返します。
public std::vector<std::pair<std::string, std::string>> GetContentMetadata(const std::vector<std::string>& names, const std::vector<std::string>& namePrefixes) const  |  コンテンツからメタデータ項目を取得します。
public std::shared_ptr<ProtectionDescriptor> GetProtectionDescriptor() const  |  保護記述子を取得します。
 public ContentFormat GetContentFormat() const  |  コンテンツの形式を取得します。
 public ActionType GetSupportedActions() const  |  サポートされているすべてのアクションの種類を表すマスクされた列挙型を取得します。
public virtual std::map<std::string, std::shared_ptr<ClassificationResult>> GetClassificationResults(const std::vector<std::string> &) const  |  分類結果のマップを返します。
  
## <a name="members"></a>メンバー
  
### <a name="getnewlabelid"></a>GetNewLabelId
ドキュメントに適用される必要のある機密ラベル ID を取得します。

  
**戻り値**: コンテンツに適用される機密ラベル ID が存在する場合はその ID、それ以外でラベルを削除する場合は空。
  
### <a name="getnewlabelactionsource"></a>GetNewLabelActionSource
新しいラベル アクションのソースを取得します。

  
**戻り値**: アクションのソース。
  
### <a name="getcontentidentifier"></a>GetContentIdentifier
ドキュメントを説明するコンテンツ識別子を取得します。 ファイルの例: [パス] 電子メールの例: [件名:送信者]。

  
**戻り値**: コンテンツに適用されるコンテンツ識別子。
この値は、人間が判読できるコンテンツの説明として監査で使用されます。
  
### <a name="getcontentstate"></a>GetContentState
アプリケーションで操作中のコンテンツの状態を取得します。

  
**戻り値**: コンテンツ データの状態
  
### <a name="isdowngradejustified"></a>IsDowngradeJustified
実装では、既存のラベルのダウングレードの理由が示されたかどうかを渡す必要があります。

  
**戻り値**: ダウングレードの正当性が理由メッセージと共に示される場合は true、それ以外の場合は false。 
  
**関連項目**: [mip::JustifyAction](class_mip_justifyaction.md)
  
### <a name="getnewlabelassignmentmethod"></a>GetNewLabelAssignmentMethod
新しいラベルの割り当て方法を取得します。

  
**戻り値**: 割り当て方法: STANDARD、PRIVILEGED、AUTO。 
  
**関連項目**: mip::AssignmentMethod
  
### <a name="getnewlabelextendedproperties"></a>GetNewLabelExtendedProperties
新しいラベルの拡張プロパティを返します。

  
**戻り値**: コンテンツに適用される拡張プロパティ。
  
### <a name="getcontentmetadata"></a>GetContentMetadata
コンテンツからメタデータ項目を取得します。

  
**戻り値**: コンテンツに適用されるメタデータ。 各メタデータ項目は名前と値のペアです。
  
### <a name="protectiondescriptor"></a>ProtectionDescriptor
保護記述子を取得します。

  
**戻り値**: 保護記述子
  
### <a name="getcontentformat"></a>GetContentFormat
コンテンツの形式を取得します。

  
**戻り値**: DEFAULT、EMAIL 
  
**次も参照**: mip::ContentFormat
  
### <a name="actiontype"></a>ActionType
サポートされているすべてのアクションの種類を表すマスクされた列挙型を取得します。

  
**戻り値**: サポートされているすべてのアクションの種類を表すマスクされた列挙型。
ActionType::Justify must be supported. ポリシーとラベルの変更に理由が必要な場合、常に理由アクションが返されます。
  
### <a name="classificationresult"></a>ClassificationResult
分類結果のマップを返します。

パラメーター:  
* **classificationId**: 分類 ID の一覧。 



  
**戻り値**: 分類結果のリスト。