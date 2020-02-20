---
title: 'クラス mip:: ComputeEngine'
description: 'Microsoft Information Protection (MIP) SDK の mip:: computeengine クラスについて説明します。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 1faae8e64bbc2e2f2de54f8152b1227148c7d3de
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77490389"
---
# <a name="class-mipcomputeengine"></a>クラス mip:: ComputeEngine 
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: vector\<std:: shared_ptr\<Label\>\>& ListSensitivityLabels ()  | _まだ文書化されていません。_
public std:: shared_ptr\<ContentLabel\> GetSensitivityLabel (ComputeEngineContext & context、const DocumentState & state)  | _まだ文書化されていません。_
public std:: vector\<std:: shared_ptr\<Action\>\> ComputeActions (ComputeEngineContext & context、const DocumentState & documentState、const ApplicationActionState & actionState)  | _まだ文書化されていません。_
パブリック std::p air\<std:: vector\<std:: shared_ptr\<Action\>\>、bool\> Computeactions Withremotestate (ComputeEngineContext & context、const DocumentState & localDocumentState、const DocumentState & remoteDocumentState、const ApplicationActionState & actionState)  |  リモートとローカルの状態のどちらかを選択しているときに、アクションを計算します。
public void NotifyCommittedActions (ComputeEngineContext & context、const DocumentState & documentState、const ApplicationActionState & actionState)  | _まだ文書化されていません。_
パブリック仮想 ~ ComputeEngine ()  | _まだ文書化されていません。_
  
## <a name="members"></a>メンバー
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels 関数
_まだ文書化されていません。_

  
### <a name="getsensitivitylabel-function"></a>GetSensitivityLabel 関数
_まだ文書化されていません。_

  
### <a name="computeactions-function"></a>ComputeActions 関数
_まだ文書化されていません。_

  
### <a name="computeactionswithremotestate-function"></a>Computeactions Withremotestate 関数
リモートとローカルの状態のどちらかを選択しているときに、アクションを計算します。
状態は、この優先順位を使用して選択されます。 不明な保護の種類、(テンプレートまたはアドホックでないポリシー)。 保護状態は、保護されていない状態に常に適しています。 ラベル付きのドキュメントの状態は、を使用しない場合より上の方が優先されます。 ラベルの順序の方が優先されます。 ラベルのタイムスタンプ。最も新しいラベルの付いたドキュメントを優先します。 必要に応じて、DocumentState。 Lastmodifiedtime を実装し、新しく変更されたファイルを優先します。

パラメータ:  
* **コンテキスト**: comput エンジンコンテキスト。 


* **Localdocumentstate**: ローカルドキュメントの状態。 


* **Remotedocumentstate**: リモートドキュメントの状態。 


* **actionstate**: アプリケーションのアクションの状態。



  
戻り**値**: メソッドはペアを返します。 最初に、アクションのリストを格納します。これは、リモートドキュメントに対して false アクションを適用する必要があり、そのドキュメントの状態を使用する必要がある場合に、そのアクションがローカルに適用されるかどうかを示します。
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions 関数
_まだ文書化されていません。_

  
### <a name="computeengine-function"></a>~ ComputeEngine 関数
_まだ文書化されていません。_
