---
title: class mip PolicyHandler
description: class mip PolicyHandler のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 23de5616558a298189cb885727d69a20373a3609
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445939"
---
# <a name="class-mippolicyhandler"></a>class mip::PolicyHandler 
このクラスは、ファイル上のすべてのポリシー ハンドラー関数にインターフェイスを提供します。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::shared_ptr<ContentLabel> GetSensitivityLabel(const ExecutionState& state)  |  既存のコンテンツから機密ラベルを取得します。
public std::vector<std::shared_ptr<Action>> ComputeActions(const ExecutionState& state)  |  指定された状態に基づいてハンドラー内でルールを実行し、実行するアクションの一覧を返します。
 public void NotifyCommittedActions(const ExecutionState& state)  |  計算されたアクションが適用され、データがディスクにコミットされると呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="contentlabel"></a>ContentLabel
既存のコンテンツから機密ラベルを取得します。

パラメーター:  
* **state**: コンテンツの現在の状態。 



  
**戻り値**: 現在、コンテンツに適用されているラベル。 ラベルが付いていない場合は、空を返します。
  
### <a name="action"></a>操作
指定された状態に基づいてハンドラー内でルールを実行し、実行するアクションの一覧を返します。

パラメーター:  
* **state**: ルールが実行されているコンテンツの現在の実行状態。 



  
**戻り値**: コンテンツに適用する必要のあるアクションの一覧。
  
### <a name="notifycommittedactions"></a>NotifyCommittedActions
計算されたアクションが適用され、データがディスクにコミットされると呼び出されます。

パラメーター:  
* **state**: アクションがコミットされた後のコンテンツの現在の実行状態。 


: この呼び出しで監査イベントが送信されます