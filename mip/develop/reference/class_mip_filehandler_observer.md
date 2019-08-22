---
title: class mip::FileHandler::Observer
description: 'Microsoft Information Protection (MIP) SDK の mip:: filehandler クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 9c550f2d678995a4438f22246d00b383574533fd
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885638"
---
# <a name="class-mipfilehandlerobserver"></a>class mip::FileHandler::Observer 
クライアントがファイル ハンドラーに関連する通知イベントを取得するための [Observer](class_mip_filehandler_observer.md) インターフェイス。
すべてのエラーは [mip::Error](class_mip_error.md) から継承されます。 クライアントは、オブザーバーを呼び出すスレッド上でエンジンをコールバックしてはなりません。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual void oncreatefileハンドラ success (const std:: shared_ptr\<filehandler\>& filehandler、const std:: shared_ptr\<void\>& context)  |  ハンドラーが正しく作成されると呼び出されます。
public virtual void oncreatefileハンドラ failure (const std:: exception_ptr & error, const std:: shared_ptr\<void\>& context)  |  ハンドラー フィールドを作成するときに呼び出されます。
パブリック仮想 void onclassid 年成功 (const std:: vector\<std:: shared_ptr\<アクション\>\>& アクション、const std:: shared_ptr\<void\>& コンテキスト)  |  分類が成功したときに呼び出されます。
パブリック仮想 void onclassid の失敗 (const std:: exception_ptr & error、const std:: shared_ptr\<void\>& context)  |  分類に失敗したときに呼び出されます。
public virtual void OnGetDecryptedTemporaryFileSuccess (const std:: string & decryptedFilePath、const std:: shared_ptr\<void\>& context)  |  復号化された一時ファイルの成功を取得するときに呼び出されます。
public virtual void OnGetDecryptedTemporaryFileFailure (const std:: exception_ptr & error, const std:: shared_ptr\<void\>& context)  |  復号化された一時ファイルの取得に失敗したときに呼び出されます。
public virtual void OnGetDecryptedTemporaryStreamSuccess (const std:: shared_ptr\<Stream\>& decryptedStream、const std:: shared_ptr\<void\>& context)  |  復号化された一時ストリームの成功を取得するときに呼び出されます。
public virtual void OnGetDecryptedTemporaryStreamFailure (const std:: exception_ptr & error, const std:: shared_ptr\<void\>& context)  |  復号化された一時ストリームの取得に失敗したときに呼び出されます。
パブリック仮想 void oncommitsuccess (bool committed、const std:: shared_ptr\<void\>& context)  |  ファイルに対する変更のコミットが正常に実行された場合に呼び出されます。
パブリック仮想 void oncommitfailure (const std:: exception_ptr & error, const std:: shared_ptr\<void\>& context)  |  失敗したファイルへの変更をコミットするときに呼び出されます。
public virtual void OnInspectSuccess (const std:: shared_ptr\<fileinspector\>& fileinspector、const std:: shared_ptr\<void\>& context)  |  検査が成功したときに呼び出されます。
public virtual void OnInspectFailure (const std:: exception_ptr & error, const std:: shared_ptr\<void\>& context)  |  検査が失敗したときに呼び出されます。
  
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