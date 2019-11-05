---
title: 'クラス mip:: FileExecutionState'
description: 'Microsoft Information Protection (MIP) SDK の mip:: fileexecutionstate クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 063f1b0227415dc413e0c56d26f60fc39274a817
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560241"
---
# <a name="class-mipfileexecutionstate"></a>クラス mip:: FileExecutionState 
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック仮想 DataState GetDataState () const  |  アプリケーションで操作中のコンテンツの状態を取得します。
パブリック仮想 std:: shared_ptr\<ClassificationResults\> GetClassificationResults (const std:: shared_ptr\<FileHandler\> &、const std:: vector\<std:: shared_ptr\<ClassificationRequest\>\> &) const  |  分類結果のマップを返します。
パブリック仮想 std:: map\<std:: string、std:: string\> GetAuditMetadata () const  |  アプリケーション固有のキーと値のペアのマップを返します。
  
## <a name="members"></a>メンバー
  
### <a name="getdatastate-function"></a>GetDataState 関数
アプリケーションで操作中のコンテンツの状態を取得します。

  
**戻り値**: コンテンツ データの状態
  
### <a name="getclassificationresults-function"></a>GetClassificationResults 関数
分類結果のマップを返します。

パラメーター:  
* **Filehandler**:-使用されたファイルのファイルハンドラー 


* **classificationIds**: 分類 id の一覧。 



  
**戻り値**: 分類結果の一覧。
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata 関数
アプリケーション固有のキーと値のペアのマップを返します。

  
**戻り**値: アプリケーション固有の監査メタデータの登録済みキー: 値のペア送信者: 送信者受信者の電子メール id: 電子メールの受信者の JSON 配列を表します。最後にコンテンツを変更したユーザーの電子メール id。LastModifiedDate: コンテンツが最後に変更された日付