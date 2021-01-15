---
title: クラス AsyncControl
description: 'Microsoft Information Protection (MIP) SDK の asynccontrol:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 7d21002c9bf90014a57eeb9b666f706e2b41f68d
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212214"
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
  
**関連** 項目: mip:: TaskDispatcherDelegate)、

  
は、キャンセルシグナルをディスパッチできない場合は False を返します。それ以外の場合は true を **返し** ます。
タスク完了ブロックには、AsyncControl オブジェクトへの強い参照を保持しないでください。