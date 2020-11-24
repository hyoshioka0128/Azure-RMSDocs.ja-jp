---
title: クラス FileHandler
description: 'Microsoft Information Protection (MIP) SDK の filehandler:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: bf3866fb1ec06156ebf40b2efed8c44f8af4a4ce
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566961"
---
# <a name="class-filehandler"></a>クラス FileHandler 
すべてのファイル処理関数のインターフェイス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std:: shared_ptr \<ContentLabel\> getlabel ()  |  ファイルからの機密ラベルの取得を開始します。
public std:: vector \<std::pair\<std::string, std::string\> \> GetProperties (uint32_t version)  |  Retrievs は、バージョンに応じてファイルを適切に試行します。
public std:: shared_ptr \<ProtectionHandler\> getprotection ()  |  ファイルからの保護ポリシーの取得を開始します。
public std:: shared_ptr \<AsyncControl\> RegisterContentForTrackingAndRevocationAsync (Bool isOwnerNotificationEnabled, const std:: shared_ptr \<ProtectionEngine::Observer\>& オブザーバー, const std:: shared_ptr \<void\>& context)  |  # # # # パラメーター
public std:: shared_ptr \<AsyncControl\> RevokeContentAsync (const std:: shared_ptr \<ProtectionEngine::Observer\>& オブザーバー、const std:: shared_ptr \<void\>& context)  |  コンテンツの失効を実行します。
public void Classid (const std:: shared_ptr \<void\>& context)  |  ハンドラーで規則を実行し、実行するアクションの一覧を返します。
public void InspectAsync (const std:: shared_ptr \<void\>& context)  |  互換性のあるファイル形式からファイルの内容を取得するために使用するファイルインスペクタオブジェクトを作成します。
public void SetLabel (const std:: shared_ptr \<Label\>& label、Const labelingoptions& labelingoptions、Const protectionsettings& protectionsettings)  |  機密ラベルをファイルに設定します。
public void DeleteLabel(const LabelingOptions& labelingOptions)  |  ファイルから機密ラベルを削除します。
public void SetProtection (const std:: shared_ptr \<ProtectionDescriptor\>& protectiondescriptor、Const protectiondescriptor& protectiondescriptor)  |  カスタムまたはテンプレート ベースのアクセス許可 (protectionDescriptor->GetProtectionType に従う) のいずれかをファイルに設定します。
public void SetProtection (const std:: shared_ptr \<ProtectionHandler\>& protectionhandler)  |  既存の保護ハンドラーを使用して、ドキュメントの保護を設定します。
public void RemoveProtection()  |  ファイルから保護を削除します。 元のファイル形式でラベル付けがサポートされていない場合、保護が解除されるとラベルは失われます。 ネイティブ形式でラベル付けがサポートされている場合は、ラベルのメタデータが保持されます。
public void CommitAsync(const std::string& outputFilePath, const std::shared_ptr\<void\>& context) | \|outputFilePath\ で指定されたファイルに変更を書き込みます。 |  %2!d! です。
public void CommitAsync(const std::shared_ptr\<Stream\>& outputStream, const std::shared_ptr\<void\>& context) | \|outputStream\ で指定されたストリームに変更を書き込みます。 |  %2!d! です。
public bool IsModified ()  |  ファイルにコミットする変更があるかどうかを確認します。
public void GetDecryptedTemporaryFileAsync (const std:: shared_ptr \<void\>& context)  |  復号化されたコンテンツを表す一時ファイル (可能であれば削除される) へのパスを返します。
public void GetDecryptedTemporaryStreamAsync (const std:: shared_ptr \<void\>& context)  |  復号化されたコンテンツを表すストリームを返します。
public void NotifyCommitSuccessful (const std:: string& actualFilePath)  |  変更がディスクにコミットされたときに、呼び出されます。
public std::string GetOutputFileName()  |  元のファイル名および累積された変更に基づいて出力ファイル名と拡張子を計算します。
  
## <a name="members"></a>メンバー
  
### <a name="getlabel-function"></a>GetLabel 関数
ファイルからの機密ラベルの取得を開始します。
  
### <a name="getproperties-function"></a>GetProperties 関数
Retrievs は、バージョンに応じてファイルを適切に試行します。
  
### <a name="getprotection-function"></a>GetProtection 関数
ファイルからの保護ポリシーの取得を開始します。
  
### <a name="registercontentfortrackingandrevocationasync-function"></a>RegisterContentForTrackingAndRevocationAsync 関数

パラメーター:  
* **isOwnerNotificationEnabled**: ドキュメントの暗号化が解除されるたびに電子メールで所有者に通知する場合は true に設定し、通知を送信しない場合は false に設定します。 


* **observer**: ProtectionHandler::Observer インターフェイスを実装するクラス 


* **コンテキスト**: オブザーバーおよびオプションの httpdelegate に不透明に転送されるクライアントコンテキスト



  
**戻り値**: Async control オブジェクト。
  
### <a name="revokecontentasync-function"></a>RevokeContentAsync 関数
コンテンツの失効を実行します。

パラメーター:  
* **observer**: ProtectionHandler::Observer インターフェイスを実装するクラス 


* **コンテキスト**: オブザーバーおよびオプションの httpdelegate に不透明に転送されるクライアントコンテキスト



  
**戻り値**: Async control オブジェクト。
  
### <a name="classifyasync-function"></a>Classid 関数の非同期関数
ハンドラーで規則を実行し、実行するアクションの一覧を返します。

  
**戻り値**: コンテンツに適用する必要のあるアクションの一覧。
  
### <a name="inspectasync-function"></a>InspectAsync 関数
互換性のあるファイル形式からファイルの内容を取得するために使用するファイルインスペクタオブジェクトを作成します。

  
は、ファイルインスペクターを **返し** ます。
  
### <a name="setlabel-function"></a>SetLabel 関数
機密ラベルをファイルに設定します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。 Privileged および Auto メソッドでは、既存のラベルを API でオーバーライドできます。ラベルの設定に labelingOptions パラメーターを介して正当性を示す操作が必要な場合は、JustificationRequiredError をスローします。
  
### <a name="deletelabel-function"></a>DeleteLabel 関数
ファイルから機密ラベルを削除します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。 Privileged および Auto メソッドでは、既存のラベルを API でオーバーライドできます。ラベルの設定に labelingOptions パラメーターを介して正当性を示す操作が必要な場合は、JustificationRequiredError をスローします。
  
### <a name="setprotection-function"></a>SetProtection 関数
カスタムまたはテンプレート ベースのアクセス許可 (protectionDescriptor->GetProtectionType に従う) のいずれかをファイルに設定します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。
  
### <a name="setprotection-function"></a>SetProtection 関数
既存の保護ハンドラーを使用して、ドキュメントの保護を設定します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。
  
### <a name="removeprotection-function"></a>RemoveProtection 関数
ファイルから保護を削除します。 元のファイル形式でラベル付けがサポートされていない場合、保護が解除されるとラベルは失われます。 ネイティブ形式でラベル付けがサポートされている場合は、ラベルのメタデータが保持されます。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。
  
### <a name="commitasync-function"></a>CommitAsync 関数
|outputFilePath| パラメーターで指定されたファイルに変更を書き込みます。
FileHandler::Observer は成功または失敗時に呼び出されます。
  
### <a name="commitasync-function"></a>CommitAsync 関数
|outputStream| パラメーターで指定されたストリームに変更を書き込みます。
FileHandler::Observer は成功または失敗時に呼び出されます。
  
### <a name="ismodified-function"></a>IsModified 関数
ファイルにコミットする変更があるかどうかを確認します。
CommitAsync が呼び出されるまで、変更はファイルに書き込まれません。
  
### <a name="getdecryptedtemporaryfileasync-function"></a>GetDecryptedTemporaryFileAsync 関数
復号化されたコンテンツを表す一時ファイル (可能であれば削除される) へのパスを返します。
FileHandler::Observer は成功または失敗時に呼び出されます。
  
### <a name="getdecryptedtemporarystreamasync-function"></a>GetDecryptedTemporaryStreamAsync 関数
復号化されたコンテンツを表すストリームを返します。
FileHandler::Observer は成功または失敗時に呼び出されます。
  
### <a name="notifycommitsuccessful-function"></a>NotifyCommitSuccessful 関数
変更がディスクにコミットされたときに、呼び出されます。

パラメーター:  
* **Actualfilepath**: 出力ファイルの実際のファイルパス 


監査イベントを発生させます
  
### <a name="getoutputfilename-function"></a>GetOutputFileName 関数
元のファイル名および累積された変更に基づいて出力ファイル名と拡張子を計算します。