---
title: クラス ApplyLabelAction
description: 'Microsoft Information Protection (MIP) SDK の applylabelaction:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 1de755d141cd86441ef3eb756d1f46dbdd73f2c4
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95569302"
---
# <a name="class-applylabelaction"></a>クラス ApplyLabelAction 
ラベルのアクションを適用するには、呼び出し元のアプリケーションで特定のラベルを適用する必要があります。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: shared_ptr \<Label\>& getlabel () const  |  ラベルを取得する必要があります。
public const std:: vector \<std::string\>& GetClassificationIds () const  |  一致し、このラベルが表示される原因となった分類 Id を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getlabel-function"></a>GetLabel 関数
ラベルを取得する必要があります。

  
は、ラベルを **返し** ます。
  
### <a name="getclassificationids-function"></a>GetClassificationIds 関数
一致し、このラベルが表示される原因となった分類 Id を取得します。

  
は、Const std:: vector<std:: string>& 、このラベルが表示される原因となった分類 Id の一覧を **返し** ます。