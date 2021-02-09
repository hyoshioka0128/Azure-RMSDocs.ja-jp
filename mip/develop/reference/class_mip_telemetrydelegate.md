---
title: TelemetryDelegate クラス
description: 'Microsoft Information Protection (MIP) SDK の telemetrydelegate:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 40e9c3a695f70af8051ef2a6e89ad232a7c09f54
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98225051"
---
# <a name="class-telemetrydelegate"></a>TelemetryDelegate クラス 
MIP SDK 監査/テレメトリ通知へのインターフェイスを定義するクラス。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public void WriteEvent (const std:: shared_ptr \<TelemetryEvent\>& イベント)  |  診断イベントをログに記録します。
public void Flush()  |  キューに登録されたイベントをフラッシュする (例: シャットダウンによる)
  
## <a name="members"></a>メンバー
  
### <a name="writeevent-function"></a>WriteEvent 関数
診断イベントをログに記録します。

パラメーター:  
* **イベント**: ログに記録されるイベント


  
### <a name="flush-function"></a>Flush 関数
キューに登録されたイベントをフラッシュする (例: シャットダウンによる)