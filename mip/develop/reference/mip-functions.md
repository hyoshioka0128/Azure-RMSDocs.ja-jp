---
title: 関数
description: 関数
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.date: 01/28/2019
ms.author: mbaldwin
ms.openlocfilehash: ced8339fa93ec349644a1f9e386489bb02c8eff0
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60173421"
---
# <a name="functions"></a>関数

## <a name="summary"></a>まとめ 

### <a name="namespace-mip"></a>Namespace mip
| 名前空間スコープ関数   | [説明]                                |
|--------------------------------|---------------------------------------------|
public std::string GetAssignmentMethodString (AssignmentMethod メソッド)       |  AssignmentMethod 列挙型を説明する文字列に変換します。
パブリック静的な std::string GetActionSourceString (ActionSource actionSource)       |  アクションのソース名を取得します。
public static std::string GetDataStateString(mip::DataState state)       |  コンテンツの状態の名前を取得します。
public const std::string& GetCustomSettingPolicyDataName()       |  ポリシー データを明示的に指定する設定の名前。
public const std::string& GetCustomSettingExportPolicyFileName()       |  SCC ポリシー データをエクスポートするファイルのパスを明示的に指定する設定の名前。
public const std::string& GetCustomSettingSensitivityTypesDataName()       |  機密データを明示的に指定する設定の名前。
public const std::string& GetCustomSettingPolicyDataFile()       |  ポリシー データのファイルのパスを明示的に指定する設定の名前。
public const std::string& GetCustomSettingSensitivityTypesDataFile()       |  小文字の区別の種類のデータ ファイルのパスを明示的に指定する設定の名前。
public const std::string& GetCustomSettingExternalLabelsEnabled()       |  「外部ラベル」機能を有効にできる設定の名前。
public MIP_API void __CDECL ReleaseAllResources()       |  シャット ダウンする前にすべてのリソース (スレッドなど) を解放します。
public MIP_API std::shared_ptr\<mip::Stream\> CreateStreamFromStdStream (const std::shared_ptr\<std::istream\>& stdIStream)       |  std::istream から[ストリーム](class_mip_stream.md)を作成します。
public MIP_API std::shared_ptr\<mip::Stream\> CreateStreamFromStdStream (const std::shared_ptr\<std::ostream\>& stdOStream)       |  std::ostream から[ストリーム](class_mip_stream.md)を作成します。
public MIP_API std::shared_ptr\<mip::Stream\> CreateStreamFromStdStream (const std::shared_ptr\<std::iostream\>& stdIOStream)       |  std::iostream から[ストリーム](class_mip_stream.md)を作成します。
public MIP_API std::shared_ptr\<mip::Stream\> CreateStreamFromBuffer(uint8_t* buffer, const int64_t size)       |  バッファーから[ストリーム](class_mip_stream.md)を作成します。


### <a name="namespace-mipauditmetadatakeys"></a>Namespace mip::auditmetadatakeys
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public std::string Sender()       |  文字列形式のメタデータのキーを監査します。
public std::string Recipients()       | _まだ文書化されていません。_
public std::string LastModifiedBy()       | _まだ文書化されていません。_
public std::string LastModifiedDate()       | _まだ文書化されていません。_


### <a name="namespace-miprights"></a>Namespace mip::rights

 メンバー                        | [説明]                                
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
public std::vector\<std::string\> EmailRights()       |  電子メールに適用される権限の一覧を取得します。
public std::vector\<std::string\> EditableDocumentRights()       |  ドキュメントに適用される権限の一覧を取得します。
public std::vector\<std::string\> CommonRights()       |  すべてのシナリオで適用される権限の一覧を取得します。

### <a name="namespace-miproles"></a>Namespace mip::roles

 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public std::string Viewer()       |  'ビューアー' ロールの文字列識別子を取得します。
public std::string Reviewer()       |  'レビュー担当者' ロールの文字列識別子を取得します。
public std::string Author()       |  '作成者' ロールの文字列識別子を取得します。
public std::string CoOwner()       |  '共同所有者' ロールの文字列識別子を取得します。

## <a name="namespace-mip"></a>Namespace mip

### <a name="getassignmentmethodstring-function"></a>GetAssignmentMethodString 関数
AssignmentMethod 列挙型を説明する文字列に変換します。

パラメーター:  
* **メソッド**: 割り当て方法。 



  
**返します**:割り当て方法の文字列説明。
  
### <a name="getactionsourcestring-function"></a>GetActionSourceString 関数
アクションのソース名を取得します。

パラメーター:  
* **actionSource**:操作のソース。 



  
**返します**:操作のソースの文字列形式。
  
### <a name="getdatastatestring-function"></a>GetDataStateString 関数
コンテンツの状態の名前を取得します。

パラメーター:  
* **actionSource**:時に作業しているコンテンツの状態。 



  
**返します**:コンテンツの状態の文字列形式。
  
### <a name="getcustomsettingpolicydataname-function"></a>GetCustomSettingPolicyDataName 関数
ポリシー データを明示的に指定する設定の名前。

  
**返します**:カスタム設定のキー。
  
### <a name="getcustomsettingexportpolicyfilename-function"></a>GetCustomSettingExportPolicyFileName 関数
SCC ポリシー データをエクスポートするファイルのパスを明示的に指定する設定の名前。

  
**返します**:カスタム設定のキー。
  
### <a name="getcustomsettingsensitivitytypesdataname-function"></a>GetCustomSettingSensitivityTypesDataName 関数
機密データを明示的に指定する設定の名前。

  
**返します**:カスタム設定のキー。
  
### <a name="getcustomsettingpolicydatafile-function"></a>GetCustomSettingPolicyDataFile 関数
ポリシー データのファイルのパスを明示的に指定する設定の名前。

  
**返します**:カスタム設定のキー。
  
### <a name="getcustomsettingsensitivitytypesdatafile-function"></a>GetCustomSettingSensitivityTypesDataFile 関数
小文字の区別の種類のデータ ファイルのパスを明示的に指定する設定の名前。

  
**返します**:カスタム設定のキー。
  
### <a name="getcustomsettingexternallabelsenabled-function"></a>GetCustomSettingExternalLabelsEnabled 関数
「外部ラベル」機能を有効にできる設定の名前。

  
**返します**:カスタム設定のキー。
  
### <a name="releaseallresources-function"></a>ReleaseAllResources 関数
シャット ダウンする前にすべてのリソース (スレッドなど) を解放します。
この関数は、プロセスが終了する前に 1 回だけ呼び出す必要があります。 ここでその依存するライブラリが読み込まれる保証も、引き続き可能はスレッドへの参加後すぐに自体を初期化する機会 MIP を提供します。 アプリケーションでは、この関数を呼び出す前に、すべての MIP オブジェクト (例: プロファイル、エンジン、ハンドラー) への参照を解放する必要があります。
この関数が呼び出されない場合は、MIP は標準的なプロセスの終了処理の一部として自然なアンロードできません。 プラットフォームによっては、デッドロックになる可能性があります (たとえば、スレッドを破棄を処理する応答で win32 では参加できません) またはクラッシュした (たとえば、win32 上のライブラリの遅延読み込みの DLL のアンロード順序によって制御されていない MIP、ため、その依存するライブラリの可能性がありますによってがアンロードされた無効な読み取り障害の結果として、MIP シャット ダウン コードの実行時間)。
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream 関数
std::istream から[ストリーム](class_mip_stream.md)を作成します。

パラメーター:  
* **stdIStream**:バッキング std::istream



  
**返します**:[Stream](class_mip_stream.md) std::istream の折り返し
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream 関数
std::ostream から[ストリーム](class_mip_stream.md)を作成します。

パラメーター:  
* **stdOStream**:バッキング std::ostream



  
**返します**:[Stream](class_mip_stream.md) std::ostream の折り返し
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream 関数
std::iostream から[ストリーム](class_mip_stream.md)を作成します。

パラメーター:  
* **stdIOStream**:バッキング std::iostream



  
**返します**:[Stream](class_mip_stream.md) std::iostream の折り返し
  
### <a name="createstreamfrombuffer-function"></a>CreateStreamFromBuffer 関数
バッファーから[ストリーム](class_mip_stream.md)を作成します。

パラメーター:  
* **バッファー**:バッファーへのポインター



  
**返します**:バッファーのサイズのサイズ
  



## <a name="namespace-mipauditmetadatakeys"></a>Namespace mip::auditmetadatakeys

### <a name="sender-function"></a>送信者関数
文字列形式のメタデータのキーを監査します。
  
### <a name="recipients-function"></a>受信者関数
_まだ文書化されていません。_

  
### <a name="lastmodifiedby-function"></a>LastModifiedBy 関数
_まだ文書化されていません。_

  
### <a name="lastmodifieddate-function"></a>LastModifiedDate 関数
_まだ文書化されていません。_






## <a name="namespace-miprights"></a>Namespace mip::rights

### <a name="owner-function"></a>所有者関数
'所有者' 権限の文字列識別子を取得します。

  
**返します**:右側の「所有者」の文字列の識別子
  
### <a name="view-function"></a>ビュー関数
'表示' 権限の文字列識別子を取得します。

  
**返します**:右文字列抽出"view"の識別子
  
### <a name="auditedextract-function"></a>AuditedExtract 関数
'監査済み抽出' 権限の文字列識別子を取得します。

  
**返します**:右文字列抽出 '監査済み抽出' の識別子
  
### <a name="edit-function"></a>関数を編集します。
'編集' 権限の文字列識別子を取得します。

  
**返します**:[編集] の右側の文字列識別子
  
### <a name="export-function"></a>関数をエクスポートします。
'エクスポート' 権限の文字列識別子を取得します。

  
**返します**:右文字列抽出 'export' の識別子
  
### <a name="extract-function"></a>Extract 関数
'抽出' 権限の文字列識別子を取得します。

  
**返します**:'抽出' 権限への文字列識別子
  
### <a name="print-function"></a>関数 print
'印刷' 権限の文字列識別子を取得します。

  
**返します**:'印刷' の権限の文字列の識別子
  
### <a name="comment-function"></a>コメント関数
'コメント' 権限の文字列識別子を取得します。

  
**返します**:右文字列抽出 'comment' の識別子
  
### <a name="reply-function"></a>返信関数
'返信' 権限の文字列識別子を取得します。

  
**返します**:右文字列抽出 '応答' の識別子
  
### <a name="replyall-function"></a>全員に返信関数
'全員に返信' 権限の文字列識別子を取得します。

  
**返します**:右側の '全員に返信' の文字列の識別子
  
### <a name="forward-function"></a>転送関数
'転送' 権限の文字列識別子を取得します。

  
**返します**:'転送' 権限の文字列の識別子
  
### <a name="emailrights-function"></a>EmailRights 関数
電子メールに適用される権限の一覧を取得します。

  
**返します**:電子メールに適用される権限の一覧
  
### <a name="editabledocumentrights-function"></a>EditableDocumentRights 関数
ドキュメントに適用される権限の一覧を取得します。

  
**返します**:ドキュメントに適用される権限の一覧
  
### <a name="commonrights-function"></a>CommonRights 関数
すべてのシナリオで適用される権限の一覧を取得します。

  
**返します**:すべてのシナリオで適用される権限の一覧


## <a name="namespace-miproles"></a>Namespace mip::roles

### <a name="viewer-function"></a>ビューアー関数
'ビューアー' ロールの文字列識別子を取得します。

  
**返します**:'ビューアー' ロールをビューアーの文字列識別子には、コンテンツのみを表示できます。 編集、コピー、印刷は実行できません。
  
### <a name="reviewer-function"></a>レビュー担当者関数
'レビュー担当者' ロールの文字列識別子を取得します。

  
**返します**:'のレビュー担当者' ロールのレビュー担当者の文字列識別子では、表示でき、コンテンツを編集することができます。 コピーや印刷は実行できません。
  
### <a name="author-function"></a>作成者関数
'作成者' ロールの文字列識別子を取得します。

  
**返します**:作成者の表示、編集、コピーとコンテンツの印刷 'author' ロールの識別子の文字列を指定します。
  
### <a name="coowner-function"></a>CoOwner 関数
'共同所有者' ロールの文字列識別子を取得します。

  
**返します**:「共同所有者」ロール共同所有者の文字列識別子がすべてのアクセス許可