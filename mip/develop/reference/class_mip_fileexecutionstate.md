---
title: mip::FileExecutionState をクラスします。
description: Mip::fileexecutionstate クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 380e5f6732a2662d83b9bb37af5763ef30ffa3bf
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2019
ms.locfileid: "56259220"
---
# <a name="class-mipfileexecutionstate"></a>mip::FileExecutionState をクラスします。 
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック仮想 std::map\<std::string, std::shared_ptr\<ClassificationResult\> \> GetClassificationResults (const std::shared_ptr\<FileHandler\> &, const std: ベクター\<std::shared_ptr\<ClassificationRequest\> \> (& a)) 定数  |  分類結果のマップを返します。
public virtual std::vector\<uint8_t\> GetSerializedProtectionInfo() const  |  シリアル化されたプランを使用して、バッファーを返す
  
## <a name="members"></a>メンバー
  
### <a name="getclassificationresults-function"></a>GetClassificationResults 関数
分類結果のマップを返します。

パラメーター:  
* **fileHandler**:-使用されるファイルのファイル ハンドラー 


* **classificationIds**: 分類 Id の一覧。 



  
**返します**:分類結果の一覧。
  
### <a name="getserializedprotectioninfo-function"></a>GetSerializedProtectionInfo 関数
シリアル化されたプランを使用して、バッファーを返す

  
**返します**:シリアル化されたプランを使用して、バッファー
