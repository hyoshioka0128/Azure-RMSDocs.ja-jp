---
title: クラス ComputeEngine
description: 'Microsoft Information Protection (MIP) SDK の computeengine:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: 3b33c9a91f40422c29282ddee9292f6bbbad90c9
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763506"
---
# <a name="class-computeengine"></a>クラス ComputeEngine 
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: vector\<std:: shared_ptr\<Label\> \>& ListSensitivityLabels ()  | _まだ文書化されていません。_
public std:: shared_ptr\<contentlabel\> GetSensitivityLabel (ComputeEngineContext& Context、const documentstate& 状態)  | _まだ文書化されていません。_
public std:: vector\<std:: shared_ptr\<Action\> \> computeactions (ComputeEngineContext& context、const documentstate& documentstate、const applicationactionstate& actionstate)  | _まだ文書化されていません。_
public std::p air\<std:: vector\<std:: shared_ptr\<Action\>\>、bool\> computeactions withremotestate (ComputeEngineContext& context、const documentstate& localdocumentstate、const documentstate& remotedocumentstate、const applicationactionstate& actionstate)  |  リモートとローカルの状態のどちらかを選択しているときに、アクションを計算します。
public void NotifyCommittedActions (ComputeEngineContext& context、const DocumentState& documentState、const ApplicationActionState& actionState)  | _まだ文書化されていません。_
public const std:: shared_ptr\<Label\>& GetDefaultLabel () const  | _まだ文書化されていません。_
public const std::string& GetMoreInfoUrl() const  | _まだ文書化されていません。_
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
状態は、この優先順位を使用して選択されます。 不明な保護の種類、(テンプレートまたはアドホックでないポリシー)。 保護状態は、保護されていない状態に常に適しています。 ラベル付きのドキュメントの状態は、を使用しない場合より上の方が優先されます。 ラベルの順序の方が優先されます。 ラベルのタイムスタンプ。最も新しいラベルの付いたドキュメントを優先します。 [Documentstate](class_mip_documentstate.md)。 Lastmodifiedtime オプションで実装され、新しく変更されたファイルを優先します。

パラメーター:  
* **コンテキスト**: comput エンジンコンテキスト。 


* **Localdocumentstate**: ローカルドキュメントの状態。 


* **Remotedocumentstate**: リモートドキュメントの状態。 


* **actionstate**: アプリケーションのアクションの状態。



  
戻り**値**: メソッドはペアを返します。 最初に、アクションのリストを格納します。これは、リモートドキュメントに対して false アクションを適用する必要があり、そのドキュメントの状態を使用する必要がある場合に、そのアクションがローカルに適用されるかどうかを示します。
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions 関数
_まだ文書化されていません。_

  
### <a name="getdefaultlabel-function"></a>GetDefaultLabel 関数
_まだ文書化されていません。_

  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl 関数
_まだ文書化されていません。_

  
### <a name="computeengine-function"></a>~ ComputeEngine 関数
_まだ文書化されていません。_
