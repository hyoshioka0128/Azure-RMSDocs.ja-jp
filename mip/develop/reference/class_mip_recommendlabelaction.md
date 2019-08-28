---
title: class mip::RecommendLabelAction
description: 'Microsoft Information Protection (MIP) SDK の mip:: recommendlabelaction クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: a36158153216a0e8fe2324580256cb61ec708dbc
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70057353"
---
# <a name="class-miprecommendlabelaction"></a>class mip::RecommendLabelAction 
このアクションの目的は、ユーザーにラベルを提案することです。 ユーザーが推奨ラベルを無視した後にこの呼び出しを抑制する場合、実行状態のサポートされるアクションを使用して行う必要があります。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: shared_ptr\<ラベル\>& getlabel () const  |  推奨されるラベルを取得します。
public const std:: vector\<std:: string\>& GetClassificationIds () const  |  一致し、このラベルが表示される原因となった分類 Id を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getlabel-function"></a>GetLabel 関数
推奨されるラベルを取得します。

  
次の**値を返し**ます。ラベル。
  
### <a name="getclassificationids-function"></a>GetClassificationIds 関数
一致し、このラベルが表示される原因となった分類 Id を取得します。

  
次の**値を返し**ます。Const std:: vector < std:: string >、このラベルが表示される原因となった分類 Id の一覧を & します。