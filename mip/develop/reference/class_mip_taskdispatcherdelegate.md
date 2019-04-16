---
title: mip::TaskDispatcherDelegate をクラスします。
description: Mip::taskdispatcherdelegate クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 568a6df614370769556cd3634070e199beb4da5b
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574433"
---
# <a name="class-miptaskdispatcherdelegate"></a>mip::TaskDispatcherDelegate をクラスします。 
MIP SDK タスク ディスパッチャーにインターフェイスを定義するクラス。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public void DispatchTask (const std::string & taskId、std::function\<void()\>タスク)  |  バック グラウンド スレッドでタスクを実行します。
public void DispatchTask (const std::string & taskId、std::function\<void()\>タスク、int64_t 遅延)  |  指定遅延時間でバック グラウンド スレッドでタスクを実行します。
public void ExecuteTaskOnIndependentThread (const std::string & taskId、std::function\<void()\>タスク)  |  すぐに、独立したスレッドでタスクを実行します。
public bool CancelTask (const std::string & taskId)  |  バック グラウンド タスクをキャンセルします。
public void CancelAllTasks()  |  すべてのバック グラウンド タスクをキャンセルします。
  
## <a name="members"></a>メンバー
  
### <a name="dispatchtask-function"></a>DispatchTask 関数
バック グラウンド スレッドでタスクを実行します。

パラメーター:  
* **taskId**:タスクを一意に識別する ID 


* **タスク**:実行される関数


  
### <a name="dispatchtask-function"></a>DispatchTask 関数
指定遅延時間でバック グラウンド スレッドでタスクを実行します。

パラメーター:  
* **taskId**:タスクを一意に識別する ID 


* **タスク**:実行される関数 


* **遅延**:遅延 (秒単位) タスクを実行する前に


  
### <a name="executetaskonindependentthread-function"></a>ExecuteTaskOnIndependentThread 関数
すぐに、独立したスレッドでタスクを実行します。

パラメーター:  
* **taskId**:タスクを一意に識別する ID 


* **タスク**:実行される関数


  
### <a name="canceltask-function"></a>CancelTask 関数
バック グラウンド タスクをキャンセルします。

パラメーター:  
* **taskId**:キャンセルするタスクの ID



  
**返します**:タスクが正常に取り消された、それ以外の場合は false の場合は true。
  
### <a name="cancelalltasks-function"></a>CancelAllTasks 関数
すべてのバック グラウンド タスクをキャンセルします。