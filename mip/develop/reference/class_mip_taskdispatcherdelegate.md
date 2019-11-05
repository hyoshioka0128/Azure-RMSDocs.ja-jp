---
title: 'クラス mip:: TaskDispatcherDelegate'
description: 'Microsoft Information Protection (MIP) SDK の mip:: taskdispatcherdelegate クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: e73a03b842b1216bcc4ef71941ca4bc0b0233945
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559958"
---
# <a name="class-miptaskdispatcherdelegate"></a>クラス mip:: TaskDispatcherDelegate 
MIP SDK タスクディスパッチャーへのインターフェイスを定義するクラス。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public void DispatchTask (const std:: string & taskId, std:: function\<void ()\> タスク)  |  バックグラウンドスレッドでタスクを実行します。
public void DispatchTask (const std:: string & taskId、std:: function\<void ()\> タスク、int64_t delaySeconds)  |  指定された遅延を使用して、バックグラウンドスレッドでタスクを実行します。
public void ExecuteTaskOnIndependentThread (const std:: string & taskId, std:: function\<void ()\> タスク)  |  独立したスレッドでタスクを直ちに実行します。
public bool CancelTask (const std:: string & taskId)  |  バックグラウンドタスクをキャンセルします。
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



  
は、タスクが正常にキャンセルされた場合は True、それ以外の場合は false**を返し**ます。
  
### <a name="cancelalltasks-function"></a>CancelAllTasks 関数
すべてのバックグラウンドタスクを取り消します。