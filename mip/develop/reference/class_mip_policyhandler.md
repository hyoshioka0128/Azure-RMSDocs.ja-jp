---
title: class mip::PolicyHandler
description: Mip::policyhandler クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 7cc1eeeafa4a086631f5d3c376643b5758002679
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2019
ms.locfileid: "59572836"
---
# <a name="class-mippolicyhandler"></a>class mip::PolicyHandler 
このクラスは、ファイル上のすべてのポリシー ハンドラー関数にインターフェイスを提供します。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public std::shared_ptr\<ContentLabel\> GetSensitivityLabel (const ExecutionState & state)  |  既存のコンテンツから機密ラベルを取得します。
public std::vector\<std::shared_ptr\<アクション\>\> ComputeActions (const ExecutionState & state)  |  指定された状態に基づいてハンドラー内でルールを実行し、実行するアクションの一覧を返します。
public void NotifyCommittedActions(const ExecutionState& state)  |  計算されたアクションが適用され、データがディスクにコミットされると呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="getsensitivitylabel-function"></a>GetSensitivityLabel 関数
既存のコンテンツから機密ラベルを取得します。

パラメーター:  
* **state**:コンテンツの現在の状態。 



  
**返します**:現在、コンテンツに適用されているラベルです。 ラベルが付いていない場合は、空を返します。
  
### <a name="computeactions-function"></a>ComputeActions 関数
指定された状態に基づいてハンドラー内でルールを実行し、実行するアクションの一覧を返します。

パラメーター:  
* **state**: ルールが実行されているコンテンツの現在の実行状態。 



  
**返します**:コンテンツに適用されるアクションの一覧。
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions 関数
計算されたアクションが適用され、データがディスクにコミットされると呼び出されます。

パラメーター:  
* **状態**: アクションがコミットされた後に、コンテンツの現在の実行状態。 


:この呼び出しは、監査イベントを送信します。