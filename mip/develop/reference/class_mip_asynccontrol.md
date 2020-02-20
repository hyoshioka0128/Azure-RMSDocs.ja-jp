---
title: 'クラス mip:: AsyncControl'
description: 'Microsoft Information Protection (MIP) SDK の mip:: asynccontrol クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: afef25cef1363d5275581a774279c97d61239f4b
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77492768"
---
# <a name="class-mipasynccontrol"></a>クラス mip:: AsyncControl 
非同期操作を取り消すために使用されるクラスです。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
public bool Cancel ()  |  Cancel を呼び出すと、タスクの取り消しが試行されます。成功した場合は、適切な onFailure コールバックが mip:: Operationcancel Error で呼び出されます。 この機能は、タスクディスパッチャーデリゲート (に依存します。
  
## <a name="members"></a>Members
  
### <a name="cancel-function"></a>Cancel 関数
Cancel を呼び出すと、タスクの取り消しが試行されます。成功した場合は、適切な onFailure コールバックが mip:: Operationcancel Error で呼び出されます。 この機能は、タスクディスパッチャーデリゲート (に依存します。
  
**関連**項目: mip:: TaskDispatcherDelegate)、

  
は、キャンセルシグナルをディスパッチできない場合は False を返します。それ以外の場合は true を**返し**ます。
タスク完了ブロックには、AsyncControl オブジェクトへの強い参照を保持しないでください。