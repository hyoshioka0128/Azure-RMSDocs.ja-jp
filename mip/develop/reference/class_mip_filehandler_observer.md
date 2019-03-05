---
title: class mip::FileHandler::Observer
description: Mip::filehandler クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 02ed14c315cfc15e39b030e42db0dd9a1e785249
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57329575"
---
# <a name="class-mipfilehandlerobserver"></a>class mip::FileHandler::Observer 
クライアントがファイル ハンドラーに関連する通知イベントを取得するための [Observer](class_mip_filehandler_observer.md) インターフェイス。
すべてのエラーは [mip::Error](class_mip_error.md) から継承されます。 クライアントは、オブザーバーを呼び出すスレッド上でエンジンをコールバックしてはなりません。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック仮想 void OnCreateFileHandlerSuccess (const std::shared_ptr\<FileHandler\>& fileHandler、const std::shared_ptr\<void\>& コンテキスト)  |  ハンドラーが正しく作成されると呼び出されます。
パブリック仮想 void OnCreateFileHandlerFailure (const std::exception_ptr & エラー、const std::shared_ptr\<void\>& コンテキスト)  |  ハンドラー フィールドを作成するときに呼び出されます。
パブリック仮想 void OnClassifySuccess (const std::vector\<std::shared_ptr\<アクション\>\>& アクション、const std::shared_ptr\<void\>& コンテキスト)  |  ときに呼び出されます成功を分類します。
パブリック仮想 void OnClassifyFailure (const std::exception_ptr & エラー、const std::shared_ptr\<void\>& コンテキスト)  |  ときに呼び出されます分類できませんでした。
パブリック仮想 void OnGetDecryptedTemporaryFileSuccess (const std::string & decryptedFilePath、const std::shared_ptr\<void\>& コンテキスト)  |  取得する復号化された一時ファイルが成功したときに呼び出されます。
public virtual void OnGetDecryptedTemporaryFileFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  失敗、復号化された一時ファイルを取得するときに呼び出されます。
パブリック仮想 void OnCommitSuccess (bool コミットされ、const std::shared_ptr\<void\>& コンテキスト)  |  ファイルに対する変更のコミットが正常に実行された場合に呼び出されます。
public virtual void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  失敗したファイルへの変更をコミットするときに呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="oncreatefilehandlersuccess-function"></a>OnCreateFileHandlerSuccess 関数
ハンドラーが正しく作成されると呼び出されます。
  
### <a name="oncreatefilehandlerfailure-function"></a>OnCreateFileHandlerFailure 関数
ハンドラー フィールドを作成するときに呼び出されます。
  
### <a name="onclassifysuccess-function"></a>OnClassifySuccess 関数
ときに呼び出されます成功を分類します。
  
### <a name="onclassifyfailure-function"></a>OnClassifyFailure 関数
ときに呼び出されます分類できませんでした。
  
### <a name="ongetdecryptedtemporaryfilesuccess-function"></a>OnGetDecryptedTemporaryFileSuccess 関数
取得する復号化された一時ファイルが成功したときに呼び出されます。
  
### <a name="ongetdecryptedtemporaryfilefailure-function"></a>OnGetDecryptedTemporaryFileFailure 関数
失敗、復号化された一時ファイルを取得するときに呼び出されます。
  
### <a name="oncommitsuccess-function"></a>OnCommitSuccess 関数
ファイルに対する変更のコミットが正常に実行された場合に呼び出されます。
  
### <a name="oncommitfailure-function"></a>OnCommitFailure 関数
失敗したファイルへの変更をコミットするときに呼び出されます。
