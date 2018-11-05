---
title: 関数
description: 関数
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 3bb9cd594022085c24c45bde428cb11f6734caab
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446517"
---
# <a name="functions"></a>関数

| 関数 (スコープ)              | 説明                                |
|--------------------------------|---------------------------------------------|
**共通** |
public const std::string& GetCustomSettingPolicyDataName()       |  ポリシー データを明示的に指定する設定の名前。
public const std::string& GetCustomSettingExportPolicyFileName()       |  SCC ポリシー データをエクスポートするファイルのパスを明示的に指定する設定の名前。
public const std::string& GetCustomSettingPolicyDataFile()       |  ポリシー データのファイルのパスを明示的に指定する設定の名前。
 **mip 関数** |
public std::shared_ptr<mip::Stream> CreateStreamFromBuffer(uint8_t* buffer, const int64_t size)       |  バッファーから[ストリーム](class_mip_stream.md)を作成します。
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::iostream>& stdIOStream)       |  std::iostream から[ストリーム](class_mip_stream.md)を作成します。
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::istream>& stdIStream)       |  std::istream から[ストリーム](class_mip_stream.md)を作成します。
public std::shared_ptr<mip::Stream> CreateStreamFromStdStream(const std::shared_ptr<std::ostream>& stdOStream)       |  std::ostream から[ストリーム](class_mip_stream.md)を作成します。
public void ReleaseAllResources()       |  シャットダウンの前にすべてのリソース (スレッドなど) を解放します。
**mip::Rights 関数**|
public std::string AuditedExtract()       |  '監査済み抽出' 権限の文字列識別子を取得します。
public std::string Comment()       |  'コメント' 権限の文字列識別子を取得します。
public std::vector<std::string> CommonRights()       |  すべてのシナリオで適用される権限の一覧を取得します。
public std::string Edit()       |  '編集' 権限の文字列識別子を取得します。
public std::vector<std::string> EditableDocumentRights()       |  ドキュメントに適用される権限の一覧を取得します。
public std::vector<std::string> EmailRights()       |  電子メールに適用される権限の一覧を取得します。
public std::string Export()       |  'エクスポート' 権限の文字列識別子を取得します。
public std::string Extract()       |  '抽出' 権限の文字列識別子を取得します。
public std::string Forward()       |  '転送' 権限の文字列識別子を取得します。
public std::string Owner()       |  '所有者' 権限の文字列識別子を取得します。
public std::string Print()       |  '印刷' 権限の文字列識別子を取得します。
public std::string Reply()       |  '返信' 権限の文字列識別子を取得します。
public std::string ReplyAll()       |  '全員に返信' 権限の文字列識別子を取得します。
public std::string View()       |  '表示' 権限の文字列識別子を取得します。
**mip::Roles 関数**|
public std::string Author()       |  '作成者' ロールの文字列識別子を取得します。
public std::string CoOwner()       |  '共同所有者' ロールの文字列識別子を取得します。
public std::string Reviewer()       |  'レビュー担当者' ロールの文字列識別子を取得します。
public std::string Viewer()       |  'ビューアー' ロールの文字列識別子を取得します。

  
## <a name="functions-common"></a>関数 (共通)

### <a name="getcustomsettingpolicydataname"></a>GetCustomSettingPolicyDataName
ポリシー データを明示的に指定する設定の名前。

  
**戻り値**: カスタムの設定キー。
  
### <a name="getcustomsettingexportpolicyfilename"></a>GetCustomSettingExportPolicyFileName
SCC ポリシー データをエクスポートするファイルのパスを明示的に指定する設定の名前。

  
**戻り値**: カスタムの設定キー。
  
### <a name="getcustomsettingpolicydatafile"></a>GetCustomSettingPolicyDataFile
ポリシー データのファイルのパスを明示的に指定する設定の名前。

  
**戻り値**: カスタムの設定キー。

## <a name="functions-mip"></a>関数 (mip)

### <a name="mipcreatestreamfrombufferbuffer"></a>mip::CreateStreamFromBuffer(buffer)

バッファーから[ストリーム](class_mip_stream.md)を作成します。

パラメーター:  
* **buffer**: バッファーへのポインター

**戻り値**: バッファーの**サイズ**
  

### <a name="mipcreatestreamfromstdstreamistream"></a>mip::CreateStreamFromStdStream(istream)

std::istream から[ストリーム](class_mip_stream.md)を作成します。

パラメーター:  

* **stdIStream**: std::istream のバッキング
  
**戻り値**: std::istream をラップする[ストリーム](class_mip_stream.md)
  
### <a name="mipcreatestreamfromstdstreamiostream"></a>mip::CreateStreamFromStdStream(iostream)

std::iostream から[ストリーム](class_mip_stream.md)を作成します。

パラメーター:  
* **stdIOStream**: std::iostream のバッキング
  
**戻り値**: std::iostream をラップする[ストリーム](class_mip_stream.md)
  
### <a name="mipcreatestreamfromstdstreamostream"></a>mip::CreateStreamFromStdStream(ostream)

std::ostream から[ストリーム](class_mip_stream.md)を作成します。

パラメーター:  
* **stdOStream**: std::ostream のバッキング
  
**戻り値**: std::ostream をラップする[ストリーム](class_mip_stream.md)
  
### <a name="mipreleaseallresources"></a>mip::ReleaseAllResources

シャットダウンの前にすべてのリソース (スレッドなど) を解放します。  

MIP 動的ライブラリは、アプリケーションによって遅延読み込みされる場合、デッドロックを回避するため、それらの MIP ライブラリをアプリケーションで明示的にアンロードする前に、この関数は呼び出される必要があります。 たとえば、Win32 で、この関数は、FreeLibrary または \__FUnloadDelayLoadedDLL2 によって MIP DLL を明示的にアンロードするための任意の呼び出しの前に呼び出される必要があります。 アプリケーションでは、この関数を呼び出す前に、すべての MIP オブジェクト (例: プロファイル、エンジン、ハンドラー) への参照を解放する必要があります。

## <a name="functions-miprights"></a>関数 (mip::rights)

### <a name="owner"></a>Owner
'所有者' 権限の文字列識別子を取得します。

  
**戻り値**: '所有者' 権限の文字列識別子
  
### <a name="auditedextract"></a>AuditedExtract
'監査済み抽出' 権限の文字列識別子を取得します。

  
**戻り値**: '監査済み抽出' 権限の文字列識別子
  
### <a name="comment"></a>コメント
'コメント' 権限の文字列識別子を取得します。

  
**戻り値**: 'コメント' 権限の文字列識別子
  
### <a name="commonrights"></a>CommonRights
すべてのシナリオで適用される権限の一覧を取得します。

  
**戻り値**: すべてのシナリオで適用される権限の一覧

### <a name="edit"></a>編集
'編集' 権限の文字列識別子を取得します。

  
**戻り値**: '編集' 権限の文字列識別子
  
### <a name="editabledocumentrights"></a>EditableDocumentRights
ドキュメントに適用される権限の一覧を取得します。

  
**戻り値**: ドキュメントに適用される権限の一覧
  
### <a name="emailrights"></a>EmailRights
電子メールに適用される権限の一覧を取得します。

  
**戻り値**: 電子メールに適用される権限の一覧
  
### <a name="export"></a>エクスポート
'エクスポート' 権限の文字列識別子を取得します。

  
**戻り値**: 'エクスポート' 権限の文字列識別子
  
### <a name="extract"></a>抽出
'抽出' 権限の文字列識別子を取得します。

  
**戻り値**: '抽出' 権限の文字列識別子
  
### <a name="forward"></a>転送
'転送' 権限の文字列識別子を取得します。

  
**戻り値**: '転送' 権限の文字列識別子
  
### <a name="print"></a>印刷
'印刷' 権限の文字列識別子を取得します。

  
**戻り値**: '印刷' 権限の文字列識別子
  
### <a name="reply"></a>返信
'返信' 権限の文字列識別子を取得します。

  
**戻り値**: '返信' 権限の文字列識別子
  
### <a name="replyall"></a>全員に返信
'全員に返信' 権限の文字列識別子を取得します。

  
**戻り値**: '全員に返信' 権限の文字列識別子
  
### <a name="view"></a>表示
'表示' 権限の文字列識別子を取得します。

  
**戻り値**: '表示' 権限の文字列識別子
  

## <a name="functions-miproles"></a>関数 (mip::roles)

### <a name="author"></a>作成者
'作成者' ロールの文字列識別子を取得します。

作成者は、コンテンツを表示、編集、コピー、および印刷できます。
  
**戻り値**: '作成者' ロールの文字列識別子
  
### <a name="coowner"></a>CoOwner
'共同所有者' ロールの文字列識別子を取得します。

共同所有者にはすべてのアクセス許可があります
  
**戻り値**: '共同所有者' ロールの文字列識別子

### <a name="reviewer"></a>レビュー担当者
'レビュー担当者' ロールの文字列識別子を取得します。

レビュー担当者は、コンテンツを表示および編集できます。 コピーや印刷は実行できません。
  
**戻り値**: 'レビュー担当者' ロールの文字列識別子
  
### <a name="viewer"></a>表示者
'ビューアー' ロールの文字列識別子を取得します。

ビューアーは、コンテンツを表示のみできます。 編集、コピー、印刷は実行できません。
  
**戻り値**: 'ビューアー' ロールの文字列識別子
  
