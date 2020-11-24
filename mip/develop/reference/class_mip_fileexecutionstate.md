---
title: クラス FileExecutionState
description: 'Microsoft Information Protection (MIP) SDK の fileexecutionstate:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: c84f7aa81fd628a8af9598653f0895dc0dd934d2
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566970"
---
# <a name="class-fileexecutionstate"></a>クラス FileExecutionState 
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック仮想 DataState GetDataState () const  |  アプリケーションで操作中のコンテンツの状態を取得します。
public virtual std:: shared_ptr \<ClassificationResults\> GetClassificationResults (const std:: shared_ptr \<FileHandler\> &、const std:: vector \<std::shared_ptr\<ClassificationRequest\> \> &) const  |  分類結果のマップを返します。
public virtual std:: map \<std::string, std::string\> getauditmetadata () const  |  アプリケーション固有のキーと値のペアのマップを返します。
  
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

  
**戻り** 値: アプリケーション固有の監査メタデータの登録済みキー: 値のペア送信者: 送信者受信者の電子メール id: 電子メールの受信者の JSON 配列: コンテンツを最後に変更したユーザーの電子メール id LastModifiedDate: コンテンツが最後に変更された日付