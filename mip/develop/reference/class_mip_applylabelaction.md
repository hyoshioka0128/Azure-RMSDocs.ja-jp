---
title: class mip::ApplyLabelAction
description: 'Microsoft Information Protection (MIP) SDK の mip:: applylabelaction クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: cb3ff8c247ad4dbcf4d85ba31608b07f3aaceddf
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559034"
---
# <a name="class-mipapplylabelaction"></a>class mip::ApplyLabelAction 
ラベルのアクションを適用するには、呼び出し元のアプリケーションで特定のラベルを適用する必要があります。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: shared_ptr\<Label\>& GetLabel () const  |  ラベルを取得する必要があります。
public const std:: vector\<std:: string\>& GetClassificationIds () const  |  一致し、このラベルが表示される原因となった分類 Id を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getlabel-function"></a>GetLabel 関数
ラベルを取得する必要があります。

  
は、ラベルを**返し**ます。
  
### <a name="getclassificationids-function"></a>GetClassificationIds 関数
一致し、このラベルが表示される原因となった分類 Id を取得します。

  
は、Const std:: vector < std:: string > &、このラベルが表示される原因となった分類 Id の一覧を**返し**ます。