---
title: 関数
description: 関数
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.date: 01/28/2019
ms.author: mbaldwin
ms.openlocfilehash: 80d13de3778648c2e0230ac37c559b0ca1f62a07
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69882800"
---
# <a name="functions"></a>関数

## <a name="summary"></a>Summary 

### <a name="namespace-mip"></a>名前空間 mip
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
public const std:: map\<のフライト機能、bool\>& GetDefaultFeatureSettings ()       |  機能が既定で有効になっているかどうかを取得します。
public MIP_API void __CDECL ReleaseAllResources ()       |  シャットダウンの前にすべてのリソース (スレッドなど) を解放します。
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std:: istream\>& stdistream)       |  std::istream から[ストリーム](class_mip_stream.md)を作成します。
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std:: ostream\>& stdostream)       |  std::ostream から[ストリーム](class_mip_stream.md)を作成します。
public MIP_API std:: shared_ptr\<MIP:: Stream\> CreateStreamFromStdStream (const std:: shared_ptr\<std:: iostream\>& stdIOStream)       |  std::iostream から[ストリーム](class_mip_stream.md)を作成します。
public MIP_API std:: shared_ptr\<MIP:: Stream\> createstreamfrombuffer (uint8_t * buffer, const int64_t size)       |  バッファーから[ストリーム](class_mip_stream.md)を作成します。
public MIP_API std:: vector\<uint8_t\> readfromstream (const std:: shared_ptr\<MIP:: stream\>& stream)       |  ストリームのすべてのバイトを読み取ります。

### <a name="namespace-mipauditmetadatakeys"></a>名前空間 mip:: auditmetadatakeys
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std:: string Sender ()       |  文字列形式のメタデータキーを監査します。
public std:: string Recipients ()       | _まだ文書化されていません。_
public std:: string Lastsystem.string ()       | _まだ文書化されていません。_
public std:: string LastModifiedDate ()       | _まだ文書化されていません。_


### <a name="namespace-miprights"></a>名前空間 mip:: rights

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
public std:: vector\<std:: string\> emailrights ()       |  電子メールに適用される権限の一覧を取得します。
public std:: vector\<std:: string\> editabledocumentrights ()       |  ドキュメントに適用される権限の一覧を取得します。
public std:: vector\<std:: string\> commonrights ()       |  すべてのシナリオで適用される権限の一覧を取得します。

### <a name="namespace-miproles"></a>名前空間 mip:: roles

 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::string Viewer()       |  'ビューアー' ロールの文字列識別子を取得します。
public std::string Reviewer()       |  'レビュー担当者' ロールの文字列識別子を取得します。
public std::string Author()       |  '作成者' ロールの文字列識別子を取得します。
public std::string CoOwner()       |  '共同所有者' ロールの文字列識別子を取得します。

## <a name="namespace-mip"></a>名前空間 mip

### <a name="getassignmentmethodstring-function"></a>GetAssignmentMethodString 関数
指定されたメソッドの列挙型を文字列の説明に変換します。

パラメーター:  
* **メソッド**: 割り当てメソッド。 



  
次の**値を返し**ます。代入メソッドの文字列の説明。
  
### <a name="getactionsourcestring-function"></a>GetActionSourceString 関数
アクションのソース名を取得します。

パラメーター:  
* **Actionsource**:アクションのソース。 



  
次の**値を返し**ます。アクションソースの文字列表現。
  
### <a name="getdatastatestring-function"></a>GetDataStateString 関数
コンテンツの状態名を取得します。

パラメーター:  
* **Actionsource**:作業中のコンテンツの状態。 



  
次の**値を返し**ます。コンテンツの状態の文字列表現。
  
### <a name="getcustomsettingpolicydataname-function"></a>GetCustomSettingPolicyDataName 関数
ポリシー データを明示的に指定する設定の名前。

  
次の**値を返し**ます。カスタム設定キー。
  
### <a name="getcustomsettingexportpolicyfilename-function"></a>GetCustomSettingExportPolicyFileName 関数
SCC ポリシー データをエクスポートするファイルのパスを明示的に指定する設定の名前。

  
次の**値を返し**ます。カスタム設定キー。
  
### <a name="getcustomsettingsensitivitytypesdataname-function"></a>GetCustomSettingSensitivityTypesDataName 関数
秘密度データを明示的に指定する設定の名前。

  
次の**値を返し**ます。カスタム設定キー。
  
### <a name="getcustomsettingpolicydatafile-function"></a>GetCustomSettingPolicyDataFile 関数
ポリシー データのファイルのパスを明示的に指定する設定の名前。

  
次の**値を返し**ます。カスタム設定キー。
  
### <a name="getcustomsettingsensitivitytypesdatafile-function"></a>GetCustomSettingSensitivityTypesDataFile 関数
感度の種類のデータファイルパスを明示的に指定する設定の名前。

  
次の**値を返し**ます。カスタム設定キー。
  
### <a name="getcustomsettingexternallabelsenabled-function"></a>GetCustomSettingExternalLabelsEnabled 関数
が "外部ラベル" 機能を有効にできる設定の名前。

  
次の**値を返し**ます。カスタム設定キー。
  
### <a name="releaseallresources-function"></a>ReleaseAllResources 関数
シャットダウンの前にすべてのリソース (スレッドなど) を解放します。
この関数は、処理を終了する前に1回だけ呼び出す必要があります。 MIP は、依存するライブラリが読み込まれることが保証されていて、スレッドの結合が引き続き可能であることが保証される時点で、それ自体を初期化解除する機会を提供します。 アプリケーションでは、この関数を呼び出す前に、すべての MIP オブジェクト (例: プロファイル、エンジン、ハンドラー) への参照を解放する必要があります。
この関数が呼び出されない場合、MIP は標準的なプロセスの破棄の一部として自然にアンロードされます。 一部のプラットフォームでは、これによりデッドロックが発生する可能性があります (たとえば、プロセスの破棄に応じて win32 でスレッドを結合することはできません)。またはクラッシュ (たとえば、win32 で遅延読み込みされたライブラリの DLL のアンロード順序は MIP によって制御されないため、依存するライブラリがMIP シャットダウンコードの実行時にアンロードされたため、読み取りエラーが無効になります)。
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream 関数
std::istream から[ストリーム](class_mip_stream.md)を作成します。

パラメーター:  
* **Stdistream**:Std:: istream のバックアップ



  
次の**値を返し**ます。Std:: istream をラップする[ストリーム](class_mip_stream.md)
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream 関数
std::ostream から[ストリーム](class_mip_stream.md)を作成します。

パラメーター:  
* **Stdostream**:バッキング std:: ostream



  
次の**値を返し**ます。Std:: ostream をラップする[ストリーム](class_mip_stream.md)
  
### <a name="createstreamfromstdstream-function"></a>CreateStreamFromStdStream 関数
std::iostream から[ストリーム](class_mip_stream.md)を作成します。

パラメーター:  
* **stdIOStream**:バッキング std:: iostream



  
次の**値を返し**ます。Std:: iostream をラップする[ストリーム](class_mip_stream.md)
  
### <a name="createstreamfrombuffer-function"></a>CreateStreamFromBuffer 関数
バッファーから[ストリーム](class_mip_stream.md)を作成します。

パラメーター:  
* **バッファー**:バッファーへのポインター



  
次の**値を返し**ます。バッファーのサイズサイズ
  



## <a name="namespace-mipauditmetadatakeys"></a>名前空間 mip:: auditmetadatakeys

### <a name="sender-function"></a>Sender 関数
文字列形式のメタデータキーを監査します。
  
### <a name="recipients-function"></a>受信者関数
_まだ文書化されていません。_

  
### <a name="lastmodifiedby-function"></a>Lastて関数
_まだ文書化されていません。_

  
### <a name="lastmodifieddate-function"></a>LastModifiedDate 関数
_まだ文書化されていません。_






## <a name="namespace-miprights"></a>名前空間 mip:: rights

### <a name="owner-function"></a>Owner 関数
'所有者' 権限の文字列識別子を取得します。

  
次の**値を返し**ます。' Owner ' 権限の文字列識別子
  
### <a name="view-function"></a>関数の表示
'表示' 権限の文字列識別子を取得します。

  
次の**値を返し**ます。' View ' 権限の文字列識別子
  
### <a name="auditedextract-function"></a>AuditedExtract 関数
'監査済み抽出' 権限の文字列識別子を取得します。

  
次の**値を返し**ます。' 監査済み抽出 ' 権限の文字列識別子
  
### <a name="edit-function"></a>関数の編集
'編集' 権限の文字列識別子を取得します。

  
次の**値を返し**ます。' Edit ' 権限の文字列識別子
  
### <a name="export-function"></a>Export 関数
'エクスポート' 権限の文字列識別子を取得します。

  
次の**値を返し**ます。' Export ' 権限の文字列識別子
  
### <a name="extract-function"></a>Extract 関数
'抽出' 権限の文字列識別子を取得します。

  
次の**値を返し**ます。' Extract ' 権限の文字列識別子
  
### <a name="print-function"></a>Print 関数
'印刷' 権限の文字列識別子を取得します。

  
次の**値を返し**ます。' Print ' 権限の文字列識別子
  
### <a name="comment-function"></a>Comment 関数
'コメント' 権限の文字列識別子を取得します。

  
次の**値を返し**ます。' Comment ' 権限の文字列識別子
  
### <a name="reply-function"></a>Reply 関数
'返信' 権限の文字列識別子を取得します。

  
次の**値を返し**ます。' Reply ' 権限の文字列識別子
  
### <a name="replyall-function"></a>ReplyAll 関数
'全員に返信' 権限の文字列識別子を取得します。

  
次の**値を返し**ます。"全員に返信" 権限の文字列識別子
  
### <a name="forward-function"></a>Forward 関数
'転送' 権限の文字列識別子を取得します。

  
次の**値を返し**ます。' 転送 ' 権限の文字列識別子
  
### <a name="emailrights-function"></a>EmailRights 関数
電子メールに適用される権限の一覧を取得します。

  
次の**値を返し**ます。電子メールに適用される権限の一覧
  
### <a name="editabledocumentrights-function"></a>EditableDocumentRights 関数
ドキュメントに適用される権限の一覧を取得します。

  
次の**値を返し**ます。ドキュメントに適用される権限の一覧
  
### <a name="commonrights-function"></a>CommonRights 関数
すべてのシナリオで適用される権限の一覧を取得します。

  
次の**値を返し**ます。すべてのシナリオに適用される権限の一覧


## <a name="namespace-miproles"></a>名前空間 mip:: roles

### <a name="viewer-function"></a>ビューアー関数
'ビューアー' ロールの文字列識別子を取得します。

  
次の**値を返し**ます。' Viewer ' ロールの文字列識別子。ビューアーで表示できるのはコンテンツのみです。 編集、コピー、印刷は実行できません。
  
### <a name="reviewer-function"></a>レビュー担当者関数
'レビュー担当者' ロールの文字列識別子を取得します。

  
次の**値を返し**ます。' Reviewer ' ロールの文字列識別子。レビュー担当者はコンテンツを表示および編集できます。 コピーや印刷は実行できません。
  
### <a name="author-function"></a>Author 関数
'作成者' ロールの文字列識別子を取得します。

  
次の**値を返し**ます。' Author ' ロールの文字列識別子。作成者は、コンテンツの表示、編集、コピー、および印刷を行うことができます。
  
### <a name="coowner-function"></a>CoOwner 関数
'共同所有者' ロールの文字列識別子を取得します。

  
次の**値を返し**ます。"共同所有者" ロールの文字列識別子。共同所有者にはすべてのアクセス許可があります