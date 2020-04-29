---
title: クラス AsyncControl
description: 'Microsoft Information Protection (MIP) SDK の asynccontrol:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: d032abf9fe7192cfe6ccfd5890d6585aaa2ba645
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763659"
---
# <a name="class-asynccontrol"></a>クラス AsyncControl 
非同期操作を取り消すために使用されるクラスです。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public bool Cancel ()  |  Cancel を呼び出すと、タスクの取り消しが試行されます。成功した場合は、適切な onFailure コールバックが mip:: Operationcancel Error で呼び出されます。 この機能は、タスクディスパッチャーデリゲート (に依存します。
  
## <a name="members"></a>メンバー
  
### <a name="cancel-function"></a>Cancel 関数
Cancel を呼び出すと、タスクの取り消しが試行されます。成功した場合は、適切な onFailure コールバックが mip:: Operationcancel Error で呼び出されます。 この機能は、タスクディスパッチャーデリゲート (に依存します。
  
**関連**項目: mip:: TaskDispatcherDelegate)、

  
は、キャンセルシグナルをディスパッチできない場合は False を返します。それ以外の場合は true を**返し**ます。
タスク完了ブロックには、AsyncControl オブジェクトへの強い参照を保持しないでください。