---
title: 'クラス mip:: NoPermissionsError'
description: 'Microsoft Information Protection (MIP) SDK の mip:: nopermissionserror クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: d5067dfcac8ad66464df061d6d043ae343d967cf
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77487652"
---
# <a name="class-mipnopermissionserror"></a>クラス mip:: NoPermissionsError 
ユーザーがコンテンツにアクセスできませんでした。 例: アクセス許可がない、コンテンツが取り消された。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
public std::string GetReferrer() const  |  ドキュメントに対する権限がない場合に、連絡先を取得します。
public std::string GetOwner() const  |  ドキュメントの所有者を取得します。
  
## <a name="members"></a>Members
  
### <a name="getreferrer-function"></a>GetReferrer 元関数
ドキュメントに対する権限がない場合に、連絡先を取得します。

  
は、ドキュメントに対する権限がない場合の連絡先を**返し**ます。
  
### <a name="getowner-function"></a>GetOwner 関数
ドキュメントの所有者を取得します。

  
**返さ**れる: ドキュメント所有者