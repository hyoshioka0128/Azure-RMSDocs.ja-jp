---
title: class mip::FileProfile::Observer
description: Mip::fileprofile クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 7b9c3440d577e9ba2e08bdba6ed890d3a480c783
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60174104"
---
# <a name="class-mipfileprofileobserver"></a>class mip::FileProfile::Observer 
クライアントがプロファイル関連のイベントに関する通知を取得するための [Observer](class_mip_fileprofile_observer.md) インターフェイス。
すべてのエラーは [mip::Error](class_mip_error.md) から継承されます。 クライアントは、オブザーバーを呼び出すスレッド上でエンジンをコールバックしてはなりません。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public virtual ~Observer()  | _まだ文書化されていません。_
パブリック仮想 void OnLoadSuccess (const std::shared_ptr\<mip::FileProfile\>(& a) プロファイル、const std::shared_ptr\<void\>& コンテキスト)  |  プロファイルが正常に読み込まれたときに呼び出されます。
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  プロファイルの読み込みでエラーが発生したときに呼び出されます。
パブリック仮想 void OnListEnginesSuccess (const std::vector\<std::string\>& engineids:、const std::shared_ptr\<void\>& コンテキスト)  |  エンジンの一覧が正常に生成されたときに呼び出されます。
public virtual void OnListEnginesFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  エラーの原因となったエンジンを一覧表示するときに呼び出されます。
パブリック仮想 void OnUnloadEngineSuccess (const std::shared_ptr\<void\>& コンテキスト)  |  エンジンが正常にアンロードされたときに呼び出されます。
パブリック仮想 void OnUnloadEngineFailure (const std::exception_ptr & エラー、const std::shared_ptr\<void\>& コンテキスト)  |  エンジンのアンロードがエラーの原因となったときに呼び出されます。
public virtual void OnAddEngineSuccess(const std::shared_ptr\<mip::FileEngine\>& engine, const std::shared_ptr\<void\>& context)  |  新しいエンジンが正常に追加されたときに呼び出されます。
public virtual void OnAddEngineFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  新しいエンジンの追加がエラーの原因となったときに呼び出されます。
public virtual void OnDeleteEngineSuccess(const std::shared_ptr\<void\>& context)  |  エンジンが正常に削除されたときに呼び出されます。
public virtual void OnDeleteEngineFailure(const std::exception_ptr& error, const std::shared_ptr\<void\>& context)  |  エンジンの削除がエラーの原因となったときに呼び出されます。
public virtual void OnPolicyChanged(const std::string& engineId)  |  指定された ID のエンジンに対してポリシーが変更されたときに呼び出されます。
パブリック仮想 void OnAddPolicyEngineStarting (bool requiresPolicyFetch)  |  サーバーから、ポリシー エンジンのポリシーのデータをフェッチする必要があるかどうか、またはローカルにキャッシュされたデータから作成するかどうかを示すエンジンを作成する前に呼び出されます。
protected Observer()  | _まだ文書化されていません。_
  
## <a name="members"></a>メンバー
  
### <a name="observer-function"></a>~ オブザーバー関数
_まだ文書化されていません。_

  
### <a name="onloadsuccess-function"></a>OnLoadSuccess 関数
プロファイルが正常に読み込まれたときに呼び出されます。
  
### <a name="onloadfailure-function"></a>OnLoadFailure 関数
プロファイルの読み込みでエラーが発生したときに呼び出されます。
  
### <a name="onlistenginessuccess-function"></a>OnListEnginesSuccess 関数
エンジンの一覧が正常に生成されたときに呼び出されます。
  
### <a name="onlistenginesfailure-function"></a>OnListEnginesFailure 関数
エラーの原因となったエンジンを一覧表示するときに呼び出されます。
  
### <a name="onunloadenginesuccess-function"></a>OnUnloadEngineSuccess 関数
エンジンが正常にアンロードされたときに呼び出されます。
  
### <a name="onunloadenginefailure-function"></a>OnUnloadEngineFailure 関数
エンジンのアンロードがエラーの原因となったときに呼び出されます。
  
### <a name="onaddenginesuccess-function"></a>OnAddEngineSuccess 関数
新しいエンジンが正常に追加されたときに呼び出されます。
  
### <a name="onaddenginefailure-function"></a>OnAddEngineFailure 関数
新しいエンジンの追加がエラーの原因となったときに呼び出されます。
  
### <a name="ondeleteenginesuccess-function"></a>OnDeleteEngineSuccess 関数
エンジンが正常に削除されたときに呼び出されます。
  
### <a name="ondeleteenginefailure-function"></a>OnDeleteEngineFailure 関数
エンジンの削除がエラーの原因となったときに呼び出されます。
  
### <a name="onpolicychanged-function"></a>OnPolicyChanged 関数
指定された ID のエンジンに対してポリシーが変更されたときに呼び出されます。
  
### <a name="onaddpolicyenginestarting-function"></a>OnAddPolicyEngineStarting 関数
サーバーから、ポリシー エンジンのポリシーのデータをフェッチする必要があるかどうか、またはローカルにキャッシュされたデータから作成するかどうかを示すエンジンを作成する前に呼び出されます。

パラメーター:  
* **requiresPolicyFetch**:エンジンのデータを HTTP 経由でフェッチする必要があるかどうか、またはキャッシュから読み込まれるかどうかについて説明します


この省略可能なコールバックをアプリケーションにできない形式であるかどうか、AddEngineAsync 操作が必要になります (その関連付けられている遅延) で HTTP 操作を完了することができます。
  
### <a name="observer-function"></a>オブザーバー関数
_まだ文書化されていません。_
