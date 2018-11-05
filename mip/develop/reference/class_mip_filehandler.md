---
title: class mip FileHandler
description: class mip FileHandler のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: efae18bdc10f8878f255f35c608a50482a29887b
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446126"
---
# <a name="class-mipfilehandler"></a>class mip::FileHandler 
すべてのファイル処理関数のインターフェイス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public void GetLabelAsync(const std::shared_ptr<void>& context)  |  ファイルからの機密ラベルの取得を開始します。
public void GetProtectionAsync(const std::shared_ptr<void>& context)  |  ファイルからの保護ポリシーの取得を開始します。
 public void SetLabel(const std::string& labelId, const LabelingOptions& labelingOptions)  |  機密ラベルをファイルに設定します。
 public void DeleteLabel(const LabelingOptions& labelingOptions)  |  ファイルから機密ラベルを削除します。
public void SetProtection(const std::shared_ptr<ProtectionDescriptor>& protectionDescriptor)  |  カスタムまたはテンプレート ベースのアクセス許可 (protectionDescriptor->GetProtectionType に従う) のいずれかをファイルに設定します。
 public void RemoveProtection()  |  ファイルから保護を削除します。 ファイルにラベルが付いている場合、ラベルは失われます。
public void CommitAsync(const std::string& outputFilePath, const std::shared_ptr<void>& context) | \|outputFilePath\ で指定されたファイルに変更を書き込みます。 |  パラメーターに渡します。
public void CommitAsync(const std::shared_ptr<Stream>& outputStream, const std::shared_ptr<void>& context) | \|outputStream\ で指定されたストリームに変更を書き込みます。 |  パラメーターに渡します。
 public void NotifyCommitSuccessful(const std::string& contentIdentifier)  |  変更がディスクにコミットされたときに、呼び出されます。
 public std::string GetOutputFileName()  |  元のファイル名および累積された変更に基づいて出力ファイル名と拡張子を計算します。
  
## <a name="members"></a>メンバー
  
### <a name="getlabelasync"></a>GetLabelAsync
ファイルからの機密ラベルの取得を開始します。
[FileHandler::Observer](class_mip_filehandler_observer.md) は成功または失敗時に呼び出されます。

パラメーター:  
* **context**: オブザーバーに不透明に渡されるクライアント コンテキスト。


  
### <a name="getprotectionasync"></a>GetProtectionAsync
ファイルからの保護ポリシーの取得を開始します。
[FileHandler::Observer](class_mip_filehandler_observer.md) は成功または失敗時に呼び出されます。

パラメーター:  
* **context**: オブザーバーに不透明に渡されるクライアント コンテキスト。


  
### <a name="setlabel"></a>SetLabel
機密ラベルをファイルに設定します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。 Privileged および Auto メソッドでは、既存のラベルを API でオーバーライドできます。ラベルの設定に labelingOptions パラメーターを介して正当性を示す操作が必要な場合は、[JustificationRequiredError](class_mip_justificationrequirederror.md) をスローします。
  
### <a name="deletelabel"></a>DeleteLabel
ファイルから機密ラベルを削除します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。 Privileged および Auto メソッドでは、既存のラベルを API でオーバーライドできます。ラベルの設定に labelingOptions パラメーターを介して正当性を示す操作が必要な場合は、[JustificationRequiredError](class_mip_justificationrequirederror.md) をスローします。
  
### <a name="setprotection"></a>SetProtection
カスタムまたはテンプレート ベースのアクセス許可 (protectionDescriptor->GetProtectionType に従う) のいずれかをファイルに設定します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。
  
### <a name="removeprotection"></a>RemoveProtection
ファイルから保護を削除します。 ファイルにラベルが付いている場合、ラベルは失われます。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。
  
### <a name="commitasync"></a>CommitAsync
|outputFilePath| パラメーターで指定されたファイルに変更を書き込みます。
[FileHandler::Observer](class_mip_filehandler_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="commitasync"></a>CommitAsync
|outputStream| パラメーターで指定されたストリームに変更を書き込みます。
[FileHandler::Observer](class_mip_filehandler_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="notifycommitsuccessful"></a>NotifyCommitSuccessful
変更がディスクにコミットされたときに、呼び出されます。

パラメーター:  
* **contentIdentifier**: ファイルの例: "C:\mip-sdk-for-cpp\files\audit.docx" [パス] 電子メールの例: "RE: 監査 design:user1@contoso.com" [件名:送信者] 


監査イベントを発生させます
  
### <a name="getoutputfilename"></a>GetOutputFileName
元のファイル名および累積された変更に基づいて出力ファイル名と拡張子を計算します。