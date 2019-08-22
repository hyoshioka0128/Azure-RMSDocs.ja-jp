---
title: class mip::ApplyLabelAction
description: 'Microsoft Information Protection (MIP) SDK の mip:: applylabelaction クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 7d2067ad030e909d53602fcdb3eefa9b88af56bf
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69884526"
---
# <a name="class-mipapplylabelaction"></a>class mip::ApplyLabelAction 
ラベルのアクションを適用するには、呼び出し元のアプリケーションで特定のラベルを適用する必要があります。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: shared_ptr\<ラベル\>& getlabel () const  |  ラベルを取得する必要があります。
public const std:: vector\<std:: string\>& GetClassificationIds () const  |  一致し、このラベルが表示される原因となった分類 Id を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getlabel-function"></a>GetLabel 関数
ラベルを取得する必要があります。

  
次の**値を返し**ます。ラベル。
  
### <a name="getclassificationids-function"></a>GetClassificationIds 関数
一致し、このラベルが表示される原因となった分類 Id を取得します。

  
次の**値を返し**ます。Const std:: vector < std:: string >、このラベルが表示される原因となった分類 Id の一覧を & します。