---
title: TaskDispatcherDelegate クラス
description: 'Microsoft Information Protection (MIP) SDK の taskdispatcherdelegate:: undefined クラスを文書にします。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 057ba0d4de58ab4dedf8d3e2f8b2a42b0e5f969a
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95567033"
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