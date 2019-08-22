---
title: class mip::FileHandler
description: 'Microsoft Information Protection (MIP) SDK の mip:: filehandler クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: a75187820cea8b806a65eebea937ed091f0c62e0
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884316"
---
# <a name="class-mipfilehandler"></a>class mip::FileHandler 
すべてのファイル処理関数のインターフェイス。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<contentlabel\> getlabel ()  |  ファイルからの機密ラベルの取得を開始します。
public std:: shared_ptr\<protectionhandler\> getprotection ()  |  ファイルからの保護ポリシーの取得を開始します。
public void classid (const std:: shared_ptr\<void\>& context)  |  ハンドラーで規則を実行し、実行するアクションの一覧を返します。
public void InspectAsync (const std:: shared_ptr\<void\>& context)  |  互換性のあるファイル形式からファイルの内容を取得するために使用するファイルインスペクタオブジェクトを作成します。
public void setlabel (const std:: shared_ptr\<ラベル\>& Label、const labelingoptions & labelingoptions、const protectionsettings & protectionsettings)  |  機密ラベルをファイルに設定します。
public void DeleteLabel(const LabelingOptions& labelingOptions)  |  ファイルから機密ラベルを削除します。
public void setprotection (const std:: shared_ptr\<protectiondescriptor\>& protectiondescriptor、const protectiondescriptor & protectiondescriptor)  |  カスタムまたはテンプレート ベースのアクセス許可 (protectionDescriptor->GetProtectionType に従う) のいずれかをファイルに設定します。
public void RemoveProtection()  |  ファイルから保護を削除します。 ファイルにラベルが付いている場合、ラベルは失われます。
public void commitasync (const std:: string & outputfilepath、const std:: shared_ptr\<void\>& context) | \|outputFilePath\ で指定されたファイルに変更を書き込みます。 |  パラメーターを使用して指定します。
public void commitasync (const std:: shared_ptr\<ストリーム\>& outputstream、const std:: shared_ptr\<void\>& context) | \|outputStream\ で指定されたストリームに変更を書き込みます。 |  パラメーターを使用して指定します。
public void GetDecryptedTemporaryFileAsync (const std:: shared_ptr\<void\>& context)  |  復号化されたコンテンツを表す一時ファイル (可能であれば削除される) へのパスを返します。
public void GetDecryptedTemporaryStreamAsync (const std:: shared_ptr\<void\>& context)  |  復号化されたコンテンツを表すストリームを返します。
public void NotifyCommitSuccessful (const std:: string & actualFilePath)  |  変更がディスクにコミットされたときに、呼び出されます。
public std::string GetOutputFileName()  |  元のファイル名および累積された変更に基づいて出力ファイル名と拡張子を計算します。
  
## <a name="members"></a>メンバー
  
### <a name="getlabel-function"></a>GetLabel 関数
ファイルからの機密ラベルの取得を開始します。
  
### <a name="getprotection-function"></a>GetProtection 関数
ファイルからの保護ポリシーの取得を開始します。
  
### <a name="classifyasync-function"></a>Classid 関数の非同期関数
ハンドラーで規則を実行し、実行するアクションの一覧を返します。

  
次の**値を返し**ます。コンテンツに適用する必要があるアクションの一覧。
  
### <a name="inspectasync-function"></a>InspectAsync 関数
互換性のあるファイル形式からファイルの内容を取得するために使用するファイルインスペクタオブジェクトを作成します。

  
次の**値を返し**ます。ファイルインスペクター。
  
### <a name="setlabel-function"></a>SetLabel 関数
機密ラベルをファイルに設定します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。 Privileged および Auto メソッドでは、既存のラベルを API でオーバーライドできます。ラベルの設定に labelingOptions パラメーターを介して正当性を示す操作が必要な場合は、[JustificationRequiredError](class_mip_justificationrequirederror.md) をスローします。
  
### <a name="deletelabel-function"></a>DeleteLabel 関数
ファイルから機密ラベルを削除します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。 Privileged および Auto メソッドでは、既存のラベルを API でオーバーライドできます。ラベルの設定に labelingOptions パラメーターを介して正当性を示す操作が必要な場合は、[JustificationRequiredError](class_mip_justificationrequirederror.md) をスローします。
  
### <a name="setprotection-function"></a>SetProtection 関数
カスタムまたはテンプレート ベースのアクセス許可 (protectionDescriptor->GetProtectionType に従う) のいずれかをファイルに設定します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。
  
### <a name="removeprotection-function"></a>RemoveProtection 関数
ファイルから保護を削除します。 ファイルにラベルが付いている場合、ラベルは失われます。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。
  
### <a name="commitasync-function"></a>CommitAsync 関数
|outputFilePath| パラメーターで指定されたファイルに変更を書き込みます。
[FileHandler::Observer](class_mip_filehandler_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="commitasync-function"></a>CommitAsync 関数
|outputStream| パラメーターで指定されたストリームに変更を書き込みます。
[FileHandler::Observer](class_mip_filehandler_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="getdecryptedtemporaryfileasync-function"></a>GetDecryptedTemporaryFileAsync 関数
復号化されたコンテンツを表す一時ファイル (可能であれば削除される) へのパスを返します。
[FileHandler::Observer](class_mip_filehandler_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="getdecryptedtemporarystreamasync-function"></a>GetDecryptedTemporaryStreamAsync 関数
復号化されたコンテンツを表すストリームを返します。
[FileHandler::Observer](class_mip_filehandler_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="notifycommitsuccessful-function"></a>NotifyCommitSuccessful 関数
変更がディスクにコミットされたときに、呼び出されます。

パラメーター:  
* **Actualfilepath**:出力ファイルの実際のファイルパス 


監査イベントを発生させます
  
### <a name="getoutputfilename-function"></a>GetOutputFileName 関数
元のファイル名および累積された変更に基づいて出力ファイル名と拡張子を計算します。