---
title: 'クラス FileHandler:: オブザーバー'
description: 'Microsoft Information Protection (MIP) SDK の filehandler:: observer クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 7cc73d0a81d6a620a411035bb0aae4258794e978
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98215291"
---
# <a name="class-filehandlerobserver"></a>クラス FileHandler:: オブザーバー 
クライアントがファイル ハンドラーに関連する通知イベントを取得するための Observer インターフェイス。
すべてのエラーは mip::Error から継承されます。 クライアントは、オブザーバーを呼び出すスレッド上でエンジンをコールバックしてはなりません。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual void OnCreateFileHandlerSuccess(const std::shared_ptr\<FileHandler\>& fileHandler, const std::shared_ptr\<void\>& context)  |  ハンドラーが正しく作成されると呼び出されます。
public virtual void OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  ハンドラー フィールドを作成するときに呼び出されます。
パブリック仮想 void Onclassid 年成功 (const std:: vector \<std::shared_ptr\<Action\> \>& actions, const std:: shared_ptr \<void\>& context)  |  分類が成功したときに呼び出されます。
パブリック仮想 void Onclassid の失敗 (const std:: exception_ptr& error、const std:: shared_ptr \<void\>& context)  |  分類に失敗したときに呼び出されます。
public virtual void OnGetDecryptedTemporaryFileSuccess (const std:: string& decryptedFilePath、const std:: shared_ptr \<void\>& context)  |  復号化された一時ファイルの成功を取得するときに呼び出されます。
public virtual void OnGetDecryptedTemporaryFileFailure (const std:: exception_ptr& error、const std:: shared_ptr \<void\>& context)  |  復号化された一時ファイルの取得に失敗したときに呼び出されます。
public virtual void OnGetDecryptedTemporaryStreamSuccess (const std:: shared_ptr \<Stream\>& decryptedStream、const std:: shared_ptr \<void\>& context)  |  復号化された一時ストリームの成功を取得するときに呼び出されます。
public virtual void OnGetDecryptedTemporaryStreamFailure (const std:: exception_ptr& error、const std:: shared_ptr \<void\>& context)  |  復号化された一時ストリームの取得に失敗したときに呼び出されます。
public virtual void OnCommitSuccess(bool committed, const std::shared_ptr\<void\>& context)  |  ファイルに対する変更のコミットが正常に実行された場合に呼び出されます。
public virtual void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  失敗したファイルへの変更をコミットするときに呼び出されます。
public virtual void OnInspectSuccess (const std:: shared_ptr \<FileInspector\>& fileinspector、const std:: shared_ptr \<void\>& context)  |  検査が成功したときに呼び出されます。
public virtual void OnInspectFailure (const std:: exception_ptr& error、const std:: shared_ptr \<void\>& context)  |  検査が失敗したときに呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="oncreatefilehandlersuccess-function"></a>Oncreatefileハンドラ Success 関数
ハンドラーが正しく作成されると呼び出されます。
  
### <a name="oncreatefilehandlerfailure-function"></a>Oncreatefileハンドラ Failure 関数
ハンドラー フィールドを作成するときに呼び出されます。
  
### <a name="onclassifysuccess-function"></a>Onclassid の成功関数
分類が成功したときに呼び出されます。
  
### <a name="onclassifyfailure-function"></a>Onclassid のエラー関数
分類に失敗したときに呼び出されます。
  
### <a name="ongetdecryptedtemporaryfilesuccess-function"></a>OnGetDecryptedTemporaryFileSuccess 関数
復号化された一時ファイルの成功を取得するときに呼び出されます。
  
### <a name="ongetdecryptedtemporaryfilefailure-function"></a>OnGetDecryptedTemporaryFileFailure 関数
復号化された一時ファイルの取得に失敗したときに呼び出されます。
  
### <a name="ongetdecryptedtemporarystreamsuccess-function"></a>OnGetDecryptedTemporaryStreamSuccess 関数
復号化された一時ストリームの成功を取得するときに呼び出されます。
  
### <a name="ongetdecryptedtemporarystreamfailure-function"></a>OnGetDecryptedTemporaryStreamFailure 関数
復号化された一時ストリームの取得に失敗したときに呼び出されます。
  
### <a name="oncommitsuccess-function"></a>OnCommitSuccess 関数
ファイルに対する変更のコミットが正常に実行された場合に呼び出されます。
  
### <a name="oncommitfailure-function"></a>OnCommitFailure 関数
失敗したファイルへの変更をコミットするときに呼び出されます。
  
### <a name="oninspectsuccess-function"></a>OnInspectSuccess 関数
検査が成功したときに呼び出されます。
  
### <a name="oninspectfailure-function"></a>OnInspectFailure 関数
検査が失敗したときに呼び出されます。