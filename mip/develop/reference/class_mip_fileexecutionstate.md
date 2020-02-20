---
title: 'クラス mip:: FileExecutionState'
description: 'Microsoft Information Protection (MIP) SDK の mip:: fileexecutionstate クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: a55ad7b5d28a3115ea4f17f36a846011e82d7827
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490049"
---
# <a name="class-mipfileexecutionstate"></a>クラス mip:: FileExecutionState 
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック仮想 DataState GetDataState () const  |  アプリケーションで操作中のコンテンツの状態を取得します。
public virtual std:: shared_ptr\<ClassificationResults\> GetClassificationResults (const std:: shared_ptr\<FileHandler\> &、const std:: vector\<std:: shared_ptr\<ClassificationRequest\>\> &) const  |  分類結果のマップを返します。
パブリック仮想 std:: map\<std:: string、std:: string\> GetAuditMetadata () const  |  アプリケーション固有のキーと値のペアのマップを返します。
  
## <a name="members"></a>メンバー
  
### <a name="getdatastate-function"></a>GetDataState 関数
アプリケーションで操作中のコンテンツの状態を取得します。

  
**戻り値**: コンテンツ データの状態
  
### <a name="getclassificationresults-function"></a>GetClassificationResults 関数
分類結果のマップを返します。

パラメータ:  
* **Filehandler**:-使用されたファイルのファイルハンドラー 


* **classificationIds**: 分類 id の一覧。 



  
**戻り値**: 分類結果の一覧。
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata 関数
アプリケーション固有のキーと値のペアのマップを返します。

  
**戻り**値: アプリケーション固有の監査メタデータの登録済みキー: 値のペア送信者: 送信者受信者の電子メール id: 電子メールの受信者の JSON 配列: コンテンツを最後に変更したユーザーの電子メール id LastModifiedDate: コンテンツが最後に変更された日付