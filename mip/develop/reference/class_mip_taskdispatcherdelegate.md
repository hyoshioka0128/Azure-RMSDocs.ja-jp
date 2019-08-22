---
title: 'クラス mip:: TaskDispatcherDelegate'
description: 'Microsoft Information Protection (MIP) SDK の mip:: taskdispatcherdelegate クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 0455f446cddd7db1c05f0f7e7b76b33496810cf1
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69883029"
---
# <a name="class-miptaskdispatcherdelegate"></a>クラス mip:: TaskDispatcherDelegate 
MIP SDK タスクディスパッチャーへのインターフェイスを定義するクラス。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public void DispatchTask (const std:: string & taskId, std:: function\<void ()\>タスク)  |  バックグラウンドスレッドでタスクを実行します。
public void DispatchTask (const std:: string & taskId、std:: function\<void ()\>タスク、int64_t delay)  |  指定された遅延を使用して、バックグラウンドスレッドでタスクを実行します。
public void ExecuteTaskOnIndependentThread (const std:: string & taskId, std:: function\<void ()\>タスク)  |  独立したスレッドでタスクを直ちに実行します。
public bool CancelTask (const std:: string & taskId)  |  バックグラウンドタスクをキャンセルします。
public void CancelAllTasks ()  |  すべてのバックグラウンドタスクを取り消します。
  
## <a name="members"></a>メンバー
  
### <a name="dispatchtask-function"></a>DispatchTask 関数
バックグラウンドスレッドでタスクを実行します。

パラメーター:  
* **taskId**:タスクを一意に識別する ID 


* **タスク**:実行する関数


  
### <a name="dispatchtask-function"></a>DispatchTask 関数
指定された遅延を使用して、バックグラウンドスレッドでタスクを実行します。

パラメーター:  
* **taskId**:タスクを一意に識別する ID 


* **タスク**:実行する関数 


* **遅延**:タスクを実行するまでの待ち時間 (秒)


  
### <a name="executetaskonindependentthread-function"></a>ExecuteTaskOnIndependentThread 関数
独立したスレッドでタスクを直ちに実行します。

パラメーター:  
* **taskId**:タスクを一意に識別する ID 


* **タスク**:実行する関数


  
### <a name="canceltask-function"></a>CancelTask 関数
バックグラウンドタスクをキャンセルします。

パラメーター:  
* **taskId**:取り消すタスクの ID



  
次の**値を返し**ます。タスクが正常に取り消された場合は True、それ以外の場合は false
  
### <a name="cancelalltasks-function"></a>CancelAllTasks 関数
すべてのバックグラウンドタスクを取り消します。