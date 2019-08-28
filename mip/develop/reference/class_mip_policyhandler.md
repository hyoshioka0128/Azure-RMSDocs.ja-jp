---
title: class mip::PolicyHandler
description: Microsoft Information Protection (MIP) SDK の mip::p olicyhandler クラスについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: 58186e1b445bdfc6d1d3d1ebfa2680697ab67404
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70055767"
---
# <a name="class-mippolicyhandler"></a>class mip::PolicyHandler 
このクラスは、ファイル上のすべてのポリシー ハンドラー関数にインターフェイスを提供します。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std:: shared_ptr\<contentlabel\> GetSensitivityLabel (const executionstate & state)  |  既存のコンテンツから機密ラベルを取得します。
public std:: vector\<std:: shared_ptr\<アクション\> \> computeactions (const executionstate & state)  |  指定された状態に基づいてハンドラー内でルールを実行し、実行するアクションの一覧を返します。
public void NotifyCommittedActions(const ExecutionState& state)  |  計算されたアクションが適用され、データがディスクにコミットされると呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="getsensitivitylabel-function"></a>GetSensitivityLabel 関数
既存のコンテンツから機密ラベルを取得します。

パラメーター:  
* **state**:コンテンツの現在の状態。 



  
次の**値を返し**ます。コンテンツに現在適用されているラベル。 ラベルが付いていない場合は、空を返します。
  
### <a name="computeactions-function"></a>ComputeActions 関数
指定された状態に基づいてハンドラー内でルールを実行し、実行するアクションの一覧を返します。

パラメーター:  
* **state**: ルールが実行されているコンテンツの現在の実行状態。 



  
次の**値を返し**ます。コンテンツに適用する必要があるアクションの一覧。
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions 関数
計算されたアクションが適用され、データがディスクにコミットされると呼び出されます。

パラメーター:  
* **状態**: アクションがコミットされた後のコンテンツの現在の実行状態。 


:この呼び出しは、監査イベントを送信します。