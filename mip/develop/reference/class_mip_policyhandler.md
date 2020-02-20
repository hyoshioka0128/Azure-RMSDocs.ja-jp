---
title: class mip::PolicyHandler
description: Microsoft Information Protection (MIP) SDK の mip::p olicyhandler クラスについて説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 9f270a628a6320b005145aab8cd0611acc907d68
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489794"
---
# <a name="class-mippolicyhandler"></a>class mip::PolicyHandler 
このクラスは、ファイル上のすべてのポリシー ハンドラー関数にインターフェイスを提供します。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<ContentLabel\> GetSensitivityLabel (const ExecutionState & 状態)  |  既存のコンテンツから機密ラベルを取得します。
public std:: vector\<std:: shared_ptr\<アクション\>\> ComputeActions (const ExecutionState & state)  |  指定された状態に基づいてハンドラー内でルールを実行し、実行するアクションの一覧を返します。
public void NotifyCommittedActions(const ExecutionState& state)  |  計算されたアクションが適用され、データがディスクにコミットされると呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="getsensitivitylabel-function"></a>GetSensitivityLabel 関数
既存のコンテンツから機密ラベルを取得します。

パラメータ:  
* **state**: コンテンツの現在の状態。 



  
**戻り値**: 現在、コンテンツに適用されているラベル。 ラベルが付いていない場合は、空を返します。
  
### <a name="computeactions-function"></a>ComputeActions 関数
指定された状態に基づいてハンドラー内でルールを実行し、実行するアクションの一覧を返します。

パラメータ:  
* **state**: ルールが実行されているコンテンツの現在の実行状態。 



  
**戻り値**: コンテンツに適用する必要のあるアクションの一覧。
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions 関数
計算されたアクションが適用され、データがディスクにコミットされると呼び出されます。

パラメータ:  
* **状態**: アクションがコミットされた後のコンテンツの現在の実行状態。 


: この呼び出しは、監査イベントを送信します。