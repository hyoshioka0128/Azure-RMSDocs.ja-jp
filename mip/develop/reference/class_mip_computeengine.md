---
title: クラス ComputeEngine
description: 'Microsoft Information Protection (MIP) SDK の computeengine:: undefined クラスを文書にします。'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: bd3f287022b567ba2531108f9f24f614a3bb6b01
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98211908"
---
# <a name="class-computeengine"></a>クラス ComputeEngine 
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const std:: vector \<std::shared_ptr\<Label\> \> ListSensitivityLabels (const std:: Vector \<std::string\>& contentformats)  | _まだ文書化されていません。_
public std:: shared_ptr \<ContentLabel\> GetSensitivityLabel (ComputeEngineContext& context、Const DocumentState& 状態)  | _まだ文書化されていません。_
public std:: vector \<std::shared_ptr\<Action\> \> computeactions (ComputeEngineContext& context、Const documentstate& documentstate、Const ApplicationActionState& actionstate)  | _まだ文書化されていません。_
パブリック std::p air \<std::vector\<std::shared_ptr\<Action\> \> 、bool \> computeactions Withremotestate (ComputeEngineContext& Context、const Documentstate& localdocumentstate、const Documentstate& Remotedocumentstate、Const applicationactionstate& actionstate)  |  リモートとローカルの状態のどちらかを選択しているときに、アクションを計算します。
public void NotifyCommittedActions (ComputeEngineContext& context、const DocumentState& documentState、const ApplicationActionState& actionState)  | _まだ文書化されていません。_
public const std:: shared_ptr \<Label\> GetDefaultLabel (const std:: string& contentFormat) const  | _まだ文書化されていません。_
public const std::string& GetMoreInfoUrl() const  | _まだ文書化されていません。_
public const std:: string& GetUpn () const  | _まだ文書化されていません。_
public bool IsLabelingRequired (const std:: string& contentFormat) const  | _まだ文書化されていません。_
public const std:: string& GetFileId () const  | _まだ文書化されていません。_
public bool HasClassificationRules (const std:: vector \<std::string\>& contentformats) const  | _まだ文書化されていません。_
public bool IsEnhancedClassificationEnabled () const  | _まだ文書化されていません。_
public std:: shared_ptr \<Label\> GetLabelById (const std:: string& id) const  | _まだ文書化されていません。_
public const std:: string& GetTenantId () const  | _まだ文書化されていません。_
public void SetSensitivityTypesRulePackages (std:: vector \<std::shared_ptr\<SensitivityTypesRulePackage\> \> && カスタム)  | _まだ文書化されていません。_
public const std:: vector \<std::shared_ptr\<SensitivityTypesRulePackage\> \>& GetSensitivityTypesRulePackages () const  | _まだ文書化されていません。_
public const std:: vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings () const  | _まだ文書化されていません。_
パブリック uint32_t GetOpcMetadataVersion () const  | _まだ文書化されていません。_
public const std:: string& GetUserObjectId () const  | _まだ文書化されていません。_
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

パラメーター:  
* **コンテキスト**: comput エンジンコンテキスト。 


* **Localdocumentstate**: ローカルドキュメントの状態。 


* **Remotedocumentstate**: リモートドキュメントの状態。 


* **actionstate**: アプリケーションのアクションの状態。



  
戻り **値**: メソッドはペアを返します。 最初に、アクションのリストを格納します。これは、リモートドキュメントに対して false アクションを適用する必要があり、そのドキュメントの状態を使用する必要がある場合に、そのアクションがローカルに適用されるかどうかを示します。
  
### <a name="notifycommittedactions-function"></a>NotifyCommittedActions 関数
_まだ文書化されていません。_

  
### <a name="getdefaultlabel-function"></a>GetDefaultLabel 関数
_まだ文書化されていません。_

  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl 関数
_まだ文書化されていません。_

  
### <a name="getupn-function"></a>GetUpn 関数
_まだ文書化されていません。_

  
### <a name="islabelingrequired-function"></a>IsLabelingRequired 関数
_まだ文書化されていません。_

  
### <a name="getfileid-function"></a>GetFileId 関数
_まだ文書化されていません。_

  
### <a name="hasclassificationrules-function"></a>HasClassificationRules 関数
_まだ文書化されていません。_

  
### <a name="isenhancedclassificationenabled-function"></a>IsEnhancedClassificationEnabled 関数
_まだ文書化されていません。_

  
### <a name="getlabelbyid-function"></a>GetLabelById 関数
_まだ文書化されていません。_

  
### <a name="gettenantid-function"></a>GetTenantId 関数
_まだ文書化されていません。_

  
### <a name="setsensitivitytypesrulepackages-function"></a>SetSensitivityTypesRulePackages 関数
_まだ文書化されていません。_

  
### <a name="getsensitivitytypesrulepackages-function"></a>GetSensitivityTypesRulePackages 関数
_まだ文書化されていません。_

  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
_まだ文書化されていません。_

  
### <a name="getopcmetadataversion-function"></a>GetOpcMetadataVersion 関数
_まだ文書化されていません。_

  
### <a name="getuserobjectid-function"></a>GetUserObjectId 関数
_まだ文書化されていません。_

  
### <a name="computeengine-function"></a>~ ComputeEngine 関数
_まだ文書化されていません。_
