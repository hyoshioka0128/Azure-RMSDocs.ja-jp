---
title: class mip FileHandler Observer
description: class mip FileHandler Observer のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a587107afc2b8963d64c31ad47af81761bf2b9f8
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446180"
---
# <a name="class-mipfilehandlerobserver"></a>class mip::FileHandler::Observer 
クライアントがファイル ハンドラーに関連する通知イベントを取得するための [Observer](class_mip_filehandler_observer.md) インターフェイス。
すべてのエラーは [mip::Error](class_mip_error.md) から継承されます。 クライアントは、オブザーバーを呼び出すスレッド上でエンジンをコールバックしてはなりません。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual void OnCreateFileHandlerSuccess(const std::shared_ptr<FileHandler>& fileHandler, const std::shared_ptr<void>& context)  |  ハンドラーが正しく作成されると呼び出されます。
public virtual void OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  ハンドラー フィールドを作成するときに呼び出されます。
public virtual void OnGetLabelSuccess(const std::shared_ptr<ContentLabel>& label, const std::shared_ptr<void>& context)  |  ラベルが正常に取得されたときに呼び出されます。
public virtual void OnGetLabelFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  失敗したラベルを取得するときに呼び出されます。
public virtual void OnGetProtectionSuccess(const std::shared_ptr<ProtectionHandler>& protectionHandler, const std::shared_ptr<void>& context)  |  保護ポリシーが正常に取得されたときに呼び出されます。
public virtual void OnGetProtectionFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  失敗した保護ポリシーを取得するときに呼び出されます。
public virtual void OnCommitSuccess(bool committed, const std::shared_ptr<void>& context)  |  ファイルに対する変更のコミットが正常に実行された場合に呼び出されます。
public virtual void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  失敗したファイルへの変更をコミットするときに呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="oncreatefilehandlersuccess"></a>OnCreateFileHandlerSuccess
ハンドラーが正しく作成されると呼び出されます。
  
### <a name="oncreatefilehandlerfailure"></a>OnCreateFileHandlerFailure
ハンドラー フィールドを作成するときに呼び出されます。
  
### <a name="ongetlabelsuccess"></a>OnGetLabelSuccess
ラベルが正常に取得されたときに呼び出されます。
  
### <a name="ongetlabelfailure"></a>OnGetLabelFailure
失敗したラベルを取得するときに呼び出されます。
  
### <a name="ongetprotectionsuccess"></a>OnGetProtectionSuccess
保護ポリシーが正常に取得されたときに呼び出されます。
  
### <a name="ongetprotectionfailure"></a>OnGetProtectionFailure
失敗した保護ポリシーを取得するときに呼び出されます。
  
### <a name="oncommitsuccess"></a>OnCommitSuccess
ファイルに対する変更のコミットが正常に実行された場合に呼び出されます。
  
### <a name="oncommitfailure"></a>OnCommitFailure
失敗したファイルへの変更をコミットするときに呼び出されます。