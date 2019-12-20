---
title: class mip::FileHandler::Observer
description: 'Microsoft Information Protection (MIP) SDK の mip:: filehandler クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: d1c1a66ce3821bf3d552ee0daa0648940b645fcb
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "73560257"
---
# <a name="class-mipfilehandlerobserver"></a>class mip::FileHandler::Observer 
クライアントがファイルハンドラーに関連する通知イベントを取得するためのオブザーバーインターフェイス。
すべてのエラーは mip:: Error から継承します。 クライアントは、オブザーバーを呼び出すスレッド上でエンジンをコールバックしてはなりません。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual void Oncreatefileハンドラ Success (const std:: shared_ptr\<FileHandler\>& fileHandler、const std:: shared_ptr\<void\>& context)  |  ハンドラーが正しく作成されると呼び出されます。
public virtual void Oncreatefileハンドラ Failure (const std:: exception_ptr & error、const std:: shared_ptr\<void\>& context)  |  ハンドラー フィールドを作成するときに呼び出されます。
パブリック仮想 void Onclassid 年成功 (const std:: vector\<std:: shared_ptr\<アクション\>\>& アクション、const std:: shared_ptr\<void\>& context)  |  分類が成功したときに呼び出されます。
パブリック仮想 void Onclassid の失敗 (const std:: exception_ptr & error、const std:: shared_ptr\<void\>& context)  |  分類に失敗したときに呼び出されます。
public virtual void OnGetDecryptedTemporaryFileSuccess (const std:: string & decryptedFilePath、const std:: shared_ptr\<void\>& context)  |  復号化された一時ファイルの成功を取得するときに呼び出されます。
public virtual void OnGetDecryptedTemporaryFileFailure (const std:: exception_ptr & error、const std:: shared_ptr\<void\>& context)  |  復号化された一時ファイルの取得に失敗したときに呼び出されます。
public virtual void OnGetDecryptedTemporaryStreamSuccess (const std:: shared_ptr\<Stream\>& decryptedStream、const std:: shared_ptr\<void\>& context)  |  復号化された一時ストリームの成功を取得するときに呼び出されます。
public virtual void OnGetDecryptedTemporaryStreamFailure (const std:: exception_ptr & error、const std:: shared_ptr\<void\>& context)  |  復号化された一時ストリームの取得に失敗したときに呼び出されます。
パブリック仮想 void OnCommitSuccess (bool committed、const std:: shared_ptr\<void\>& context)  |  ファイルに対する変更のコミットが正常に実行された場合に呼び出されます。
パブリック仮想 void OnCommitFailure (const std:: exception_ptr & error、const std:: shared_ptr\<void\>& context)  |  失敗したファイルへの変更をコミットするときに呼び出されます。
public virtual void OnInspectSuccess (const std:: shared_ptr\<FileInspector\>& fileInspector、const std:: shared_ptr\<void\>& context)  |  検査が成功したときに呼び出されます。
public virtual void OnInspectFailure (const std:: exception_ptr & error、const std:: shared_ptr\<void\>& context)  |  検査が失敗したときに呼び出されます。
  
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