---
title: TaskDispatcherDelegate クラス
description: 'Microsoft Information Protection (MIP) SDK の taskdispatcherdelegate:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: f8f84b51200ff630b6158f7b02ca88e2a3d21e25
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212877"
---
# <a name="class-taskdispatcherdelegate"></a>TaskDispatcherDelegate クラス 
MIP SDK タスクディスパッチャーへのインターフェイスを定義するクラス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public void DispatchTask (const std:: string& taskId, std:: function \<void()\> タスク)  |  バックグラウンドスレッドでタスクを実行します。
public void DispatchTask (const std:: string& taskId、std:: function \<void()\> タスク、Int64_t delaySeconds)  |  指定された遅延を使用して、バックグラウンドスレッドでタスクを実行します。
public void ExecuteTaskOnIndependentThread (const std:: string& taskId, std:: function \<void()\> タスク)  |  独立したスレッドでタスクを直ちに実行します。
public bool CancelTask (const std:: string& taskId)  |  バックグラウンドタスクをキャンセルします。
public void CancelAllTasks ()  |  すべてのバックグラウンドタスクを取り消します。
  
## <a name="members"></a>メンバー
  
### <a name="dispatchtask-function"></a>DispatchTask 関数
バックグラウンドスレッドでタスクを実行します。

パラメーター:  
* **taskId**: タスクを一意に識別する ID 


* **タスク**: 実行する関数


  
### <a name="dispatchtask-function"></a>DispatchTask 関数
指定された遅延を使用して、バックグラウンドスレッドでタスクを実行します。

パラメーター:  
* **taskId**: タスクを一意に識別する ID 


* **タスク**: 実行する関数 


* **Delayseconds**: タスクを実行するまでの待ち時間 (秒)


  
### <a name="executetaskonindependentthread-function"></a>ExecuteTaskOnIndependentThread 関数
独立したスレッドでタスクを直ちに実行します。

パラメーター:  
* **taskId**: タスクを一意に識別する ID 


* **タスク**: 実行する関数


  
### <a name="canceltask-function"></a>CancelTask 関数
バックグラウンドタスクをキャンセルします。

パラメーター:  
* **taskId**: 取り消すタスクの ID



  
は、タスクが正常にキャンセルされた場合は True、それ以外の場合は false **を返し** ます。
  
### <a name="cancelalltasks-function"></a>CancelAllTasks 関数
すべてのバックグラウンドタスクを取り消します。