---
title: class mip::FileHandler
description: 'Microsoft Information Protection (MIP) SDK の mip:: filehandler クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: b2a6e3cd6de886c3e3983442a1ec7185b688b662
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73558834"
---
# <a name="class-mipfilehandler"></a>class mip::FileHandler 
すべてのファイル処理関数のインターフェイス。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<ContentLabel\> GetLabel ()  |  ファイルからの機密ラベルの取得を開始します。
public std:: shared_ptr\<ProtectionHandler\> GetProtection ()  |  ファイルからの保護ポリシーの取得を開始します。
public void Classid (定数) (const std:: shared_ptr\<void\>& context)  |  ハンドラーで規則を実行し、実行するアクションの一覧を返します。
public void InspectAsync (const std:: shared_ptr\<void\>& context)  |  互換性のあるファイル形式からファイルの内容を取得するために使用するファイルインスペクタオブジェクトを作成します。
public void SetLabel (const std:: shared_ptr\<Label\>& label、const LabelingOptions & labelingOptions、const ProtectionSettings & protectionSettings)  |  機密ラベルをファイルに設定します。
public void DeleteLabel(const LabelingOptions& labelingOptions)  |  ファイルから機密ラベルを削除します。
public void SetProtection (const std:: shared_ptr\<ProtectionDescriptor\>& protectionDescriptor、const Protectiondescriptor & Protectiondescriptor)  |  カスタムまたはテンプレート ベースのアクセス許可 (protectionDescriptor->GetProtectionType に従う) のいずれかをファイルに設定します。
public void SetProtection (const std:: shared_ptr\<ProtectionHandler\>& protectionHandler)  |  既存の保護ハンドラーを使用して、ドキュメントの保護を設定します。
public void RemoveProtection()  |  ファイルから保護を削除します。 ファイルにラベルが付いている場合、ラベルは失われます。
public void CommitAsync (const std:: string & outputFilePath、const std:: shared_ptr\<void\>& context) | \|outputFilePath\ で指定されたファイルに変更を書き込みます。 |  パラメーターに渡します。
public void CommitAsync (const std:: shared_ptr\<Stream\>& outputStream、const std:: shared_ptr\<void\>& context) | \|outputStream\ で指定されたストリームに変更を書き込みます。 |  パラメーターに渡します。
public bool IsModified ()  |  ファイルにコミットする変更があるかどうかを確認します。
public void GetDecryptedTemporaryFileAsync (const std:: shared_ptr\<void\>& context)  |  復号化されたコンテンツを表す一時ファイル (可能であれば削除される) へのパスを返します。
public void GetDecryptedTemporaryStreamAsync (const std:: shared_ptr\<void\>& context)  |  復号化されたコンテンツを表すストリームを返します。
public void NotifyCommitSuccessful (const std:: string & actualFilePath)  |  変更がディスクにコミットされたときに、呼び出されます。
public std::string GetOutputFileName()  |  元のファイル名および累積された変更に基づいて出力ファイル名と拡張子を計算します。
public static bool IsProtected (const std:: string & filePath、const std:: shared_ptr<MipContext>& mipContext) | ファイルが保護されているかどうかを確認します。
public static FILE_API std:: vector&lt;uint8_t&gt; __CDECL mip:: FileHandler:: GetSerializedPublishingLicense | ファイルに公開ライセンスがある場合は、それを返します。

## <a name="members"></a>メンバー
  
### <a name="getlabel-function"></a>GetLabel 関数
ファイルからの機密ラベルの取得を開始します。
  
### <a name="getprotection-function"></a>GetProtection 関数
ファイルからの保護ポリシーの取得を開始します。
  
### <a name="classifyasync-function"></a>Classid 関数の非同期関数
ハンドラーで規則を実行し、実行するアクションの一覧を返します。

  
**戻り値**: コンテンツに適用する必要のあるアクションの一覧。
  
### <a name="inspectasync-function"></a>InspectAsync 関数
互換性のあるファイル形式からファイルの内容を取得するために使用するファイルインスペクタオブジェクトを作成します。

  
は、ファイルインスペクターを**返し**ます。
  
### <a name="setlabel-function"></a>SetLabel 関数
機密ラベルをファイルに設定します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。 Privileged および Auto メソッドを使用すると、API で既存のラベルを上書きすることができます。ラベルを設定する場合は、(labelingOptions パラメーターを使用して) 操作を正当化する必要があります。
  
### <a name="deletelabel-function"></a>DeleteLabel 関数
ファイルから機密ラベルを削除します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。 Privileged および Auto メソッドを使用すると、API で既存のラベルを上書きすることができます。ラベルを設定する場合は、(labelingOptions パラメーターを使用して) 操作を正当化する必要があります。
  
### <a name="setprotection-function"></a>SetProtection 関数
カスタムまたはテンプレート ベースのアクセス許可 (protectionDescriptor->GetProtectionType に従う) のいずれかをファイルに設定します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。
  
### <a name="setprotection-function"></a>SetProtection 関数
既存の保護ハンドラーを使用して、ドキュメントの保護を設定します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。
  
### <a name="removeprotection-function"></a>RemoveProtection 関数
ファイルから保護を削除します。 ファイルにラベルが付いている場合、ラベルは失われます。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。
  
### <a name="commitasync-function"></a>CommitAsync 関数
|outputFilePath| パラメーターで指定されたファイルに変更を書き込みます。
FileHandler:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="commitasync-function"></a>CommitAsync 関数
|outputStream| パラメーターで指定されたストリームに変更を書き込みます。
FileHandler:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="ismodified-function"></a>IsModified 関数
ファイルにコミットする変更があるかどうかを確認します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。
  
### <a name="getdecryptedtemporaryfileasync-function"></a>GetDecryptedTemporaryFileAsync 関数
復号化されたコンテンツを表す一時ファイル (可能であれば削除される) へのパスを返します。
FileHandler:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="getdecryptedtemporarystreamasync-function"></a>GetDecryptedTemporaryStreamAsync 関数
復号化されたコンテンツを表すストリームを返します。
FileHandler:: オブザーバーは、成功または失敗時に呼び出されます。
  
### <a name="notifycommitsuccessful-function"></a>NotifyCommitSuccessful 関数
変更がディスクにコミットされたときに、呼び出されます。

パラメーター:  
* **Actualfilepath**: 出力ファイルの実際のファイルパス 


監査イベントを発生させます
  
### <a name="getoutputfilename-function"></a>GetOutputFileName 関数
元のファイル名および累積された変更に基づいて出力ファイル名と拡張子を計算します。

### <a name="isprotected-function"></a>IsProtected 関数
ファイルが保護されているかどうかを確認します。

### <a name="getserializedpublishinglicense-function"></a>GetSerializedPublishingLicense 関数
ファイルに公開ライセンスがある場合は、それを返します。