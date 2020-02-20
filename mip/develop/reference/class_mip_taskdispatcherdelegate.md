---
title: 'クラス mip:: TaskDispatcherDelegate'
description: 'Microsoft Information Protection (MIP) SDK の mip:: taskdispatcherdelegate クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: dca6a5fa04b62abf23f0116f63fd4a91c6081da0
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489335"
---
# <a name="class-miptaskdispatcherdelegate"></a>クラス mip:: TaskDispatcherDelegate 
MIP SDK タスクディスパッチャーへのインターフェイスを定義するクラス。
  
## <a name="summary"></a>要約
 Members                        | [説明]                                
--------------------------------|---------------------------------------------
public void DispatchTask (const std:: string & taskId, std:: function\<void ()\> タスク)  |  バックグラウンドスレッドでタスクを実行します。
public void DispatchTask (const std:: string & taskId、std:: function\<void ()\> タスク、int64_t delaySeconds)  |  指定された遅延を使用して、バックグラウンドスレッドでタスクを実行します。
public void ExecuteTaskOnIndependentThread (const std:: string & taskId, std:: function\<void ()\> タスク)  |  独立したスレッドでタスクを直ちに実行します。
public bool CancelTask (const std:: string & taskId)  |  バックグラウンドタスクをキャンセルします。
public void CancelAllTasks ()  |  すべてのバックグラウンドタスクを取り消します。
  
## <a name="members"></a>Members
  
### <a name="dispatchtask-function"></a>DispatchTask 関数
バックグラウンドスレッドでタスクを実行します。

パラメータ:  
* **taskId**: タスクを一意に識別する ID 


* **タスク**: 実行する関数


  
### <a name="dispatchtask-function"></a>DispatchTask 関数
指定された遅延を使用して、バックグラウンドスレッドでタスクを実行します。

パラメータ:  
* **taskId**: タスクを一意に識別する ID 


* **タスク**: 実行する関数 


* **Delayseconds**: タスクを実行するまでの待ち時間 (秒)


  
### <a name="executetaskonindependentthread-function"></a>ExecuteTaskOnIndependentThread 関数
独立したスレッドでタスクを直ちに実行します。

パラメータ:  
* **taskId**: タスクを一意に識別する ID 


* **タスク**: 実行する関数


  
### <a name="canceltask-function"></a>CancelTask 関数
バックグラウンドタスクをキャンセルします。

パラメータ:  
* **taskId**: 取り消すタスクの ID



  
は、タスクが正常にキャンセルされた場合は True、それ以外の場合は false**を返し**ます。
  
### <a name="cancelalltasks-function"></a>CancelAllTasks 関数
すべてのバックグラウンドタスクを取り消します。