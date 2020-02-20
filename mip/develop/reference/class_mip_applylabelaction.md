---
title: class mip::ApplyLabelAction
description: 'Microsoft Information Protection (MIP) SDK の mip:: applylabelaction クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: e1551adddec611c6f9a0982c5a267fad39c436c4
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490678"
---
# <a name="class-mipapplylabelaction"></a>class mip::ApplyLabelAction 
ラベルのアクションを適用するには、呼び出し元のアプリケーションで特定のラベルを適用する必要があります。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
public const std:: shared_ptr\<Label\>& GetLabel () const  |  ラベルを取得する必要があります。
public const std:: vector\<std:: string\>& GetClassificationIds () const  |  一致し、このラベルが表示される原因となった分類 Id を取得します。
  
## <a name="members"></a>Members
  
### <a name="getlabel-function"></a>GetLabel 関数
ラベルを取得する必要があります。

  
は、ラベルを**返し**ます。
  
### <a name="getclassificationids-function"></a>GetClassificationIds 関数
一致し、このラベルが表示される原因となった分類 Id を取得します。

  
は、Const std:: vector < std:: string > &、このラベルが表示される原因となった分類 Id の一覧を**返し**ます。