---
title: 'クラス mip:: FileExecutionState'
description: 'Microsoft Information Protection (MIP) SDK の mip:: fileexecutionstate クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 24750ea7c719545889cb833aa4c685fdcd1e9e3d
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885730"
---
# <a name="class-mipfileexecutionstate"></a>クラス mip:: FileExecutionState 
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック仮想 DataState GetDataState () const  |  アプリケーションで操作中のコンテンツの状態を取得します。
public 仮想 std:: shared_ptr\<ClassificationResults\> GetClassificationResults (const std:: shared_ptr\<filehandler\> &、const std:: vector\<std:: shared_ptr\<ClassificationRequest\> &)\> const  |  分類結果のマップを返します。
public virtual std::map\<std::string, std::string\> GetAuditMetadata() const  |  アプリケーション固有のキーと値のペアのマップを返します。
  
## <a name="members"></a>メンバー
  
### <a name="getdatastate-function"></a>GetDataState 関数
アプリケーションで操作中のコンテンツの状態を取得します。

  
次の**値を返し**ます。コンテンツデータの状態
  
### <a name="getclassificationresults-function"></a>GetClassificationResults 関数
分類結果のマップを返します。

パラメーター:  
* **Filehandler**:-使用されたファイルのファイルハンドラー 


* **classificationIds**: 分類 id の一覧。 



  
次の**値を返し**ます。分類結果の一覧。
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata 関数
アプリケーション固有のキーと値のペアのマップを返します。

  
次の**値を返し**ます。アプリケーション固有の監査メタデータの登録済みキー: 値のペア送信者:送信者受信者の電子メール Id:電子メールの受信者の JSON 配列を表します。コンテンツ LastModifiedDate を最後に変更したユーザーの電子メール Id:コンテンツが最後に変更された日付