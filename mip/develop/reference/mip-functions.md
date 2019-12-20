---
title: クラス
description: 関数
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.date: 01/28/2019
ms.author: mbaldwin
ms.openlocfilehash: 4479cd9419d51e841906e6268427e184d4e1b4d3
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558002"
---
# <a name="functions"></a>関数



## <a name="namespace-mip"></a>名前空間 mip

| 名前空間スコープ別の関数   | 説明                                |
|--------------------------------|---------------------------------------------|
public std:: string GetAssignmentMethodString (メソッドの指定)       |  指定されたメソッドの列挙型を文字列の説明に変換します。
public static std:: string GetActionSourceString (ActionSource actionSource)       |  アクションのソース名を取得します。
public static std:: string GetDataStateString (mip::D ataState state)       |  コンテンツの状態名を取得します。
public const std::string& GetCustomSettingPolicyDataName()       |  ポリシー データを明示的に指定する設定の名前。
public const std::string& GetCustomSettingExportPolicyFileName()       |  SCC ポリシー データをエクスポートするファイルのパスを明示的に指定する設定の名前。
public const std::string& GetCustomSettingSensitivityTypesDataName()       |  秘密度データを明示的に指定する設定の名前。
public const std::string& GetCustomSettingPolicyDataFile()       |  ポリシー データのファイルのパスを明示的に指定する設定の名前。
public const std::string& GetCustomSettingSensitivityTypesDataFile()       |  感度の種類のデータファイルパスを明示的に指定する設定の名前。
public const std:: string & GetCustomSettingLabelCustomPropertiesSyncEnabled ()       |  ラベル機能によってカスタムプロパティとカスタムプロパティによってラベルを有効にできる設定の名前。
public const std:: map\<、GetDefaultFeatureSettings () のように、フライト機能、bool\>& ます。       |  機能が既定で有効になっているかどうかを取得します。
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std:: istream\>& stdIStream)       |  Std:: istream からストリームを作成します。
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std:: ostream\>& stdOStream)       |  Std:: ostream からストリームを作成します。
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std:: iostream\>& stdIOStream)       |  Std:: iostream からストリームを作成します。
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromBuffer (uint8_t * buffer、const int64_t size)       |  バッファーからストリームを作成します。
public MIP_API std:: vector\<uint8_t\> ReadFromStream (const std:: shared_ptr\<MIP:: Stream\>& stream)       |  ストリームのすべてのバイトを読み取ります。
public ActionType operator & (ActionType a、ActionType b)       |  アクションの種類が enum の and (&) 演算子。
public ActionType operator ^ (ActionType a, ActionType b)       |  アクションの種類の列挙型に対する Xor (^) 演算子。

### <a name="getassignmentmethodstring-function"></a>GetAssignmentMethodString 関数
指定されたメソッドの列挙型を文字列の説明に変換します。

パラメーター:  
* **メソッド**: 割り当てメソッド。 



  
**戻り値**: 割り当てメソッドの文字列の説明。
  
### <a name="getactionsourcestring-function"></a>GetActionSourceString 関数
アクションのソース名を取得します。

パラメーター:  
* **actionsource**: アクションのソース。 



  
は、アクションソースの文字列形式を**返し**ます。
  
### <a name="getdatastatestring-function"></a>GetDataStateString 関数
コンテンツの状態名を取得します。

パラメーター:  
* **Actionsource**: 作業中のコンテンツの状態。 



  
**戻り値**: コンテンツの状態の文字列形式。
  
### <a name="getcustomsettingpolicydataname-function"></a>GetCustomSettingPolicyDataName 関数
ポリシー データを明示的に指定する設定の名前。

  
**戻り値**: カスタムの設定キー。
  
### <a name="getcustomsettingexportpolicyfilename-function"></a>GetCustomSettingExportPolicyFileName 関数
SCC ポリシー データをエクスポートするファイルのパスを明示的に指定する設定の名前。

  
**戻り値**: カスタムの設定キー。
  
### <a name="getcustomsettingsensitivitytypesdataname-function"></a>GetCustomSettingSensitivityTypesDataName 関数
秘密度データを明示的に指定する設定の名前。

  
**戻り値**: カスタムの設定キー。
  
### <a name="getcustomsettingpolicydatafile-function"></a>GetCustomSettingPolicyDataFile 関数
ポリシー データのファイルのパスを明示的に指定する設定の名前。

  
**戻り値**: カスタムの設定キー。
  
### <a name="getcustomsettingsensitivitytypesdatafile-function"></a>GetCustomSettingSensitivityTypesDataFile 関数
感度の種類のデータファイルパスを明示的に指定する設定の名前。

  
**戻り値**: カスタムの設定キー。
  
### <a name="getcustomsettinglabelcustompropertiessyncenabled-function"></a>GetCustomSettingLabelCustomPropertiesSyncEnabled 関数
ラベル機能によってカスタムプロパティとカスタムプロパティによってラベルを有効にできる設定の名前。

  
**戻り値**: カスタムの設定キー。
  
### <a name="getdefaultfeaturesettings-function"></a>GetDefaultFeatureSettings 関数
機能が既定で有効になっているかどうかを取得します。

  
**戻り**値: フライト機能の既定の状態
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream 関数
Std:: istream からストリームを作成します。

パラメーター:  
* **stdIStream**: std::istream のバッキング



  
**戻り値**: std:: istream をラップするストリーム
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream 関数
Std:: ostream からストリームを作成します。

パラメーター:  
* **stdOStream**: std::ostream のバッキング



  
**戻り値**: std:: ostream をラップするストリーム
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream 関数
Std:: iostream からストリームを作成します。

パラメーター:  
* **stdIOStream**: std::iostream のバッキング



  
は、std:: iostream をラップするストリームを**返し**ます。
  
### <a name="createstreamfrombuffer-function"></a>CreateStreamFromBuffer 関数
バッファーからストリームを作成します。

パラメーター:  
* **buffer**: バッファーへのポインター



  
**戻り値**: バッファーのサイズ
  
### <a name="readfromstream-function"></a>ReadFromStream 関数
ストリームのすべてのバイトを読み取ります。

パラメーター:  
* **ポインター**: ストリームへのポインター。



  
は、バイトのベクターを**返し**ます。
  
### <a name="operator-function"></a>operator |プロシージャ
アクションの種類の列挙型の or (|) 演算子。
  
### <a name="operator-function"></a>operator & 関数
アクションの種類が enum の and (&) 演算子。
  
### <a name="operator-function"></a>operator ^ 関数
アクションの種類の列挙型に対する Xor (^) 演算子。

## <a name="namespace-mipauditmetadatakeys"></a>名前空間 mip:: auditmetadatakeys

 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std:: string Sender ()       |  文字列形式のメタデータキーを監査します。
public std:: string Recipients ()       | まだ文書化されていません。
public std:: string Lastsystem.string ()       | まだ文書化されていません。
public std:: string LastModifiedDate ()       | まだ文書化されていません。
  
### <a name="sender-function"></a>Sender 関数
文字列形式のメタデータキーを監査します。
  
### <a name="recipients-function"></a>受信者関数
_まだ文書化されていません。_

  
### <a name="lastmodifiedby-function"></a>Lastて関数
_まだ文書化されていません。_

  
### <a name="lastmodifieddate-function"></a>LastModifiedDate 関数
_まだ文書化されていません。_


## <a name="namespace-miprights"></a>名前空間の `mip::rights` 
  
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::string Owner()       |  '所有者' 権限の文字列識別子を取得します。
public std::string View()       |  '表示' 権限の文字列識別子を取得します。
public std::string AuditedExtract()       |  '監査済み抽出' 権限の文字列識別子を取得します。
public std::string Edit()       |  '編集' 権限の文字列識別子を取得します。
public std::string Export()       |  'エクスポート' 権限の文字列識別子を取得します。
public std::string Extract()       |  '抽出' 権限の文字列識別子を取得します。
public std::string Print()       |  '印刷' 権限の文字列識別子を取得します。
public std::string Comment()       |  'コメント' 権限の文字列識別子を取得します。
public std::string Reply()       |  '返信' 権限の文字列識別子を取得します。
public std::string ReplyAll()       |  '全員に返信' 権限の文字列識別子を取得します。
public std::string Forward()       |  '転送' 権限の文字列識別子を取得します。
public std:: vector\<std:: string\> EmailRights ()       |  電子メールに適用される権限の一覧を取得します。
public std:: vector\<std:: string\> EditableDocumentRights ()       |  ドキュメントに適用される権限の一覧を取得します。
public std:: vector\<std:: string\> CommonRights ()       |  すべてのシナリオで適用される権限の一覧を取得します。
  

### <a name="owner-function"></a>Owner 関数
'所有者' 権限の文字列識別子を取得します。

  
**戻り値**: '所有者' 権限の文字列識別子
  
### <a name="view-function"></a>関数の表示
'表示' 権限の文字列識別子を取得します。

  
**戻り値**: '表示' 権限の文字列識別子
  
### <a name="auditedextract-function"></a>AuditedExtract 関数
'監査済み抽出' 権限の文字列識別子を取得します。

  
**戻り値**: '監査済み抽出' 権限の文字列識別子
  
### <a name="edit-function"></a>関数の編集
'編集' 権限の文字列識別子を取得します。

  
**戻り値**: '編集' 権限の文字列識別子
  
### <a name="export-function"></a>Export 関数
'エクスポート' 権限の文字列識別子を取得します。

  
**戻り値**: 'エクスポート' 権限の文字列識別子
  
### <a name="extract-function"></a>Extract 関数
'抽出' 権限の文字列識別子を取得します。

  
**戻り値**: '抽出' 権限の文字列識別子
  
### <a name="print-function"></a>Print 関数
'印刷' 権限の文字列識別子を取得します。

  
**戻り値**: '印刷' 権限の文字列識別子
  
### <a name="comment-function"></a>Comment 関数
'コメント' 権限の文字列識別子を取得します。

  
**戻り値**: 'コメント' 権限の文字列識別子
  
### <a name="reply-function"></a>Reply 関数
'返信' 権限の文字列識別子を取得します。

  
**戻り値**: '返信' 権限の文字列識別子
  
### <a name="replyall-function"></a>ReplyAll 関数
'全員に返信' 権限の文字列識別子を取得します。

  
**戻り値**: '全員に返信' 権限の文字列識別子
  
### <a name="forward-function"></a>Forward 関数
'転送' 権限の文字列識別子を取得します。

  
**戻り値**: '転送' 権限の文字列識別子
  
### <a name="emailrights-function"></a>EmailRights 関数
電子メールに適用される権限の一覧を取得します。

  
**戻り値**: 電子メールに適用される権限の一覧
  
### <a name="editabledocumentrights-function"></a>EditableDocumentRights 関数
ドキュメントに適用される権限の一覧を取得します。

  
**戻り値**: ドキュメントに適用される権限の一覧
  
### <a name="commonrights-function"></a>CommonRights 関数
すべてのシナリオで適用される権限の一覧を取得します。

  
**戻り値**: すべてのシナリオで適用される権限の一覧

## <a name="namespace-miproles"></a>名前空間 mip:: roles
  
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::string Viewer()       |  'ビューアー' ロールの文字列識別子を取得します。
public std::string Reviewer()       |  'レビュー担当者' ロールの文字列識別子を取得します。
public std::string Author()       |  '作成者' ロールの文字列識別子を取得します。
public std::string CoOwner()       |  '共同所有者' ロールの文字列識別子を取得します。
  
### <a name="viewer-function"></a>ビューアー関数
'ビューアー' ロールの文字列識別子を取得します。

  
**戻り値**: 'ビューアー' ロールの文字列識別子。ビューアーが実行できるのはコンテンツの表示のみです。 編集、コピー、印刷は実行できません。
  
### <a name="reviewer-function"></a>レビュー担当者関数
'レビュー担当者' ロールの文字列識別子を取得します。

  
**戻り値**: 'レビュー担当者' ロールの文字列識別子。レビュー担当者はコンテンツの表示と編集を実行できます。 コピーや印刷は実行できません。
  
### <a name="author-function"></a>Author 関数
'作成者' ロールの文字列識別子を取得します。

  
**戻り値**: '作成者' ロールの文字列識別子。作成者はコンテンツの表示、編集、コピー、印刷を実行できます。
  
### <a name="coowner-function"></a>CoOwner 関数
'共同所有者' ロールの文字列識別子を取得します。

  
**戻り値**: '共同所有者' ロールの文字列識別子。共同所有者はすべてのアクセス許可を持ちます。

