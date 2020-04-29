---
title: クラス ApplyLabelAction
description: 'Microsoft Information Protection (MIP) SDK の applylabelaction:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: df208a53f6cd6ec3806e91c28901a3005b801742
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763702"
---
# <a name="class-applylabelaction"></a>クラス ApplyLabelAction 
ラベルのアクションを適用するには、呼び出し元のアプリケーションで特定のラベルを適用する必要があります。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: shared_ptr\<Label\>& getlabel () const  |  ラベルを取得する必要があります。
public const std:: vector\<std:: String\>& GetClassificationIds () const  |  一致し、このラベルが表示される原因となった分類 Id を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getlabel-function"></a>GetLabel 関数
ラベルを取得する必要があります。

  
は、ラベルを**返し**ます。
  
### <a name="getclassificationids-function"></a>GetClassificationIds 関数
一致し、このラベルが表示される原因となった分類 Id を取得します。

  
は、Const std:: vector<std:: string>& 、このラベルが表示される原因となった分類 Id の一覧を**返し**ます。