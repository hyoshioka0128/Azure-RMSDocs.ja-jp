---
title: NoPermissionsError クラス
description: 'Microsoft Information Protection (MIP) SDK の nopermissionserror:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 18c3c66fe10ce9291a936a3e754923d36f3d1df0
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81761417"
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

  
は、ドキュメントに対する権限がない場合の連絡先を**返し**ます。
  
### <a name="getowner-function"></a>GetOwner 関数
ドキュメントの所有者を取得します。

  
**返さ**れる: ドキュメント所有者