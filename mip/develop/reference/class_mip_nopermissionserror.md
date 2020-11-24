---
title: NoPermissionsError クラス
description: 'Microsoft Information Protection (MIP) SDK の nopermissionserror:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: aaa26e640c59ffaf80bec182042b86a7b8e90d3f
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566709"
---
# <a name="class-nopermissionserror"></a>NoPermissionsError クラス 
ユーザーがコンテンツにアクセスできませんでした。 例: アクセス許可がない、コンテンツが取り消された。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::string GetReferrer() const  |  ドキュメントに対する権限がない場合に、連絡先を取得します。
public std::string GetOwner() const  |  ドキュメントの所有者を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getreferrer-function"></a>GetReferrer 元関数
ドキュメントに対する権限がない場合に、連絡先を取得します。

  
は、ドキュメントに対する権限がない場合の連絡先を **返し** ます。
  
### <a name="getowner-function"></a>GetOwner 関数
ドキュメントの所有者を取得します。

  
**返さ** れる: ドキュメント所有者