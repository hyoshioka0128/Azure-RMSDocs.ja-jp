---
title: class mip::FileHandler
description: Mip::filehandler クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 664478f074334196b78b5583867224e1a9f482d2
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2019
ms.locfileid: "56253069"
---
# <a name="class-mipfilehandler"></a>class mip::FileHandler 
すべてのファイル処理関数のインターフェイス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::shared_ptr\<ContentLabel\> GetLabel()  |  ファイルからの機密ラベルの取得を開始します。
public std::shared_ptr\<ProtectionHandler\> GetProtection()  |  ファイルからの保護ポリシーの取得を開始します。
public void ClassifyAsync(const std::shared_ptr\<void\>& context)  |  ハンドラーでルールを実行し、実行するアクションの一覧を返します。
public void SetLabel(const std::string& labelId, const LabelingOptions& labelingOptions)  |  機密ラベルをファイルに設定します。
public void DeleteLabel(const LabelingOptions& labelingOptions)  |  ファイルから機密ラベルを削除します。
public void SetProtection(const std::shared_ptr\<ProtectionDescriptor\>& protectionDescriptor)  |  カスタムまたはテンプレート ベースのアクセス許可 (protectionDescriptor->GetProtectionType に従う) のいずれかをファイルに設定します。
public void SetProtection(const std::vector\<uint8_t\>& serializedPublishingLicense, const std::vector\<uint8_t\>& serializedProtectionInfo)  |  ファイルには、(serializedPublishingLicense および serializedProtectionInfo) に従って、カスタムまたはテンプレート ベースのアクセス許可を設定します。
public void RemoveProtection()  |  ファイルから保護を削除します。 ファイルにラベルが付いている場合、ラベルは失われます。
public void CommitAsync(const std::string& outputFilePath, const std::shared_ptr\<void\>& context) | \|outputFilePath\ で指定されたファイルに変更を書き込みます。 |  パラメーター。
public void CommitAsync(const std::shared_ptr\<Stream\>& outputStream, const std::shared_ptr\<void\>& context) | \|outputStream\ で指定されたストリームに変更を書き込みます。 |  パラメーター。
public void GetDecryptedTemporaryFileAsync(const std::shared_ptr\<void\>& context)  |  一時ファイル (可能であれば削除されます) - 復号化されたコンテンツを表すパスを返します。
public void NotifyCommitSuccessful(const std::string& contentIdentifier)  |  変更がディスクにコミットされたときに、呼び出されます。
public std::string GetOutputFileName()  |  元のファイル名および累積された変更に基づいて出力ファイル名と拡張子を計算します。
  
## <a name="members"></a>メンバー
  
### <a name="getlabel-function"></a>GetLabel 関数
ファイルからの機密ラベルの取得を開始します。
  
### <a name="getprotection-function"></a>GetProtection 関数
ファイルからの保護ポリシーの取得を開始します。
  
### <a name="classifyasync-function"></a>ClassifyAsync 関数
ハンドラーでルールを実行し、実行するアクションの一覧を返します。

  
**返します**:コンテンツに適用されるアクションの一覧。
  
### <a name="setlabel-function"></a>SetLabel 関数
機密ラベルをファイルに設定します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。 Privileged および Auto メソッドでは、既存のラベルを API でオーバーライドできます。ラベルの設定に labelingOptions パラメーターを介して正当性を示す操作が必要な場合は、[JustificationRequiredError](class_mip_justificationrequirederror.md) をスローします。
  
### <a name="deletelabel-function"></a>DeleteLabel 関数
ファイルから機密ラベルを削除します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。 Privileged および Auto メソッドでは、既存のラベルを API でオーバーライドできます。ラベルの設定に labelingOptions パラメーターを介して正当性を示す操作が必要な場合は、[JustificationRequiredError](class_mip_justificationrequirederror.md) をスローします。
  
### <a name="setprotection-function"></a>SetProtection 関数
カスタムまたはテンプレート ベースのアクセス許可 (protectionDescriptor->GetProtectionType に従う) のいずれかをファイルに設定します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。
  
### <a name="setprotection-function"></a>SetProtection 関数
ファイルには、(serializedPublishingLicense および serializedProtectionInfo) に従って、カスタムまたはテンプレート ベースのアクセス許可を設定します。
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
一時ファイル (可能であれば削除されます) - 復号化されたコンテンツを表すパスを返します。
[FileHandler::Observer](class_mip_filehandler_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="notifycommitsuccessful-function"></a>NotifyCommitSuccessful 関数
変更がディスクにコミットされたときに、呼び出されます。

パラメーター:  
* **contentIdentifier**: ファイルの例。電子メールの"C:\mip-sdk-for-cpp\files\audit.docx"[&] 例:"RE:監査design:user1@contoso.com"[サブジェクト: 送信者] 


監査イベントを発生させます
  
### <a name="getoutputfilename-function"></a>GetOutputFileName 関数
元のファイル名および累積された変更に基づいて出力ファイル名と拡張子を計算します。
