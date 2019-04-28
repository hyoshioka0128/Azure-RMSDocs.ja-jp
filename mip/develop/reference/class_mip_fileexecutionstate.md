---
title: mip::FileExecutionState をクラスします。
description: Mip::fileexecutionstate クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: bdf0814e56d64bd16918a6f4d269a057620f92f5
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184673"
---
# <a name="class-mipfileexecutionstate"></a>mip::FileExecutionState をクラスします。 
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public virtual DataState GetDataState() const  |  アプリケーションで操作中のコンテンツの状態を取得します。
パブリック仮想 std::shared_ptr\<ClassificationResults\> GetClassificationResults (const std::shared_ptr\<FileHandler\> &, const std::vector\<std::shared_ptr\<ClassificationRequest\> \> (& a)) 定数  |  分類結果のマップを返します。
public virtual std::vector\<uint8_t\> GetSerializedProtectionInfo() const  |  シリアル化されたプランを使用して、バッファーを返す
public virtual std::map\<std::string, std::string\> GetAuditMetadata() const  |  アプリケーションの特定の監査のキー/値ペアのマップを返します。
  
## <a name="members"></a>メンバー
  
### <a name="getdatastate-function"></a>GetDataState 関数
アプリケーションで操作中のコンテンツの状態を取得します。

  
**返します**:コンテンツ データの状態
  
### <a name="getclassificationresults-function"></a>GetClassificationResults 関数
分類結果のマップを返します。

パラメーター:  
* **fileHandler**:-使用されるファイルのファイル ハンドラー 


* **classificationIds**: 分類 Id の一覧。 



  
**返します**:分類の結果の一覧。
  
### <a name="getserializedprotectioninfo-function"></a>GetSerializedProtectionInfo 関数
シリアル化されたプランを使用して、バッファーを返す

  
**返します**:シリアル化されたプランを使用して、バッファー
  
### <a name="getauditmetadata-function"></a>GetAuditMetadata 関数
アプリケーションの特定の監査のキー/値ペアのマップを返します。

  
**返します**:アプリケーションの特定の監査メタデータの登録キーと値ペア送信者の一覧:送信者が受信者の電子メール Id:LastModifiedBy、電子メールの受信者の JSON 配列を表します。コンテンツの LastModifiedDate を前回変更したユーザーの電子メール Id:コンテンツの最終変更日