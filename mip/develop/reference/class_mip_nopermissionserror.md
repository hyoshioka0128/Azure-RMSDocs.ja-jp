---
title: NoPermissionsError クラス
description: 'Microsoft Information Protection (MIP) SDK の nopermissionserror:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 0e9c13e1609b6ea5fa2033d5d27c47d76a1acb43
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98213574"
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