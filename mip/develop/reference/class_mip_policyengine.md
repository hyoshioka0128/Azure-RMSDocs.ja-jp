---
title: class mip::PolicyEngine
description: Microsoft Information Protection (MIP) SDK の mip::p olicyengine クラスについて説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 07/16/2019
ms.openlocfilehash: 7ef57d0864ff4899476dc22639942afdbfe6bffe
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69885243"
---
# <a name="class-mippolicyengine"></a>class mip::PolicyEngine 
このクラスは、すべてのエンジン関数のインターフェイスを提供します。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  ポリシー エンジン[設定](class_mip_policyengine_settings.md)を取得します。
public const std:: vector\<std:: shared_ptr\<Label\>\>& ListSensitivityLabels ()  |  ポリシー エンジンに関連付けられている機密ラベルの一覧を示します。
public const std:: vector\<std:: shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes () const  |  ポリシーエンジンに関連付けられている感度の種類を一覧表示します。
public const std::string& GetMoreInfoUrl() const  |  ポリシー/ラベルに関する詳細情報を検索するための URL を提供します。
public bool IsLabelingRequired() const  |  ドキュメントにラベルを付ける必要があるかどうかを、ポリシーで指示するかどうかを確認します。
public std:: shared_ptr\<Label\> GetDefaultSensitivityLabel ()  |  既定の機密ラベルを取得します。
public std:: shared_ptr\<Label\> GetLabelById (const std:: string & id) const  |  指定された id に従ってラベルを取得します。
public std:: shared_ptr\<policyhandler\> createpolicyhandler (bool isauditdiscoveryenabled)  |  ポリシー ハンドラーを作成して、ファイルの事項状態でポリシー関連の関数を実行します。
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  アプリケーションに固有のイベントを監査パイプラインにログを記録します。
public const std::string& GetPolicyDataXml() const  |  このポリシーに関連付けられている設定、ラベル、および規則を記述するポリシーデータ XML を取得します。
public const std:: vector\<std::p air\<std:: string、std:: string\>\>& GetCustomSettings () const  |  カスタム設定の一覧を取得します。
public const std:: string & GetPolicyFileId () const  |  ポリシーファイル ID を取得します。
public bool HasClassificationRules () const  |  ポリシーに自動または推奨規則があるかどうかを取得します。
public std::chrono::time_point\<std::chrono::system_clock\> GetLastPolicyFetchTime() const  |  ポリシーが最後にフェッチされた時刻を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
ポリシー エンジン[設定](class_mip_policyengine_settings.md)を取得します。

  
次の**値を返し**ます。ポリシーエンジンの設定。 
  
**関連項目**: [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md)
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels 関数
ポリシー エンジンに関連付けられている機密ラベルの一覧を示します。

  
次の**値を返し**ます。機密ラベルの一覧。
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes 関数
ポリシーエンジンに関連付けられている感度の種類を一覧表示します。

  
次の**値を返し**ます。機密ラベルの一覧。 LoadSensitivityTypesEnabled が false の場合は空 (
  
**関連**項目:[Policyengine:: Settings](class_mip_policyengine_settings.md))。
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl 関数
ポリシー/ラベルに関する詳細情報を検索するための URL を提供します。

  
次の**値を返し**ます。文字列形式の url。
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired 関数
ドキュメントにラベルを付ける必要があるかどうかを、ポリシーで指示するかどうかを確認します。

  
次の**値を返し**ます。ラベル付けが必須の場合は True、それ以外の場合は false。
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel 関数
既定の機密ラベルを取得します。

  
次の**値を返し**ます。既定の感度ラベル (存在する場合)、既定のラベルが設定されていない場合は nullptr。
  
### <a name="getlabelbyid-function"></a>GetLabelById 関数
指定された id に従ってラベルを取得します。
  
### <a name="createpolicyhandler-function"></a>CreatePolicyHandler 関数
ポリシー ハンドラーを作成して、ファイルの事項状態でポリシー関連の関数を実行します。

パラメーター:  
* **A**: 監査検出が有効かどうかを表すブール値。



  
次の**値を返し**ます。ポリシーハンドラー。
アプリケーションでは、ドキュメントの有効期間にわたってポリシーハンドラーオブジェクトを保持する必要があります。
  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent 関数
アプリケーションに固有のイベントを監査パイプラインにログを記録します。

パラメーター:  
* **レベル**: ログレベルの:Info/Error/Warning。 


* **eventType**: イベントの種類の説明。 


* **eventData**: イベントに関連付けられているデータ。


  
### <a name="getpolicydataxml-function"></a>GetPolicyDataXml 関数
このポリシーに関連付けられている設定、ラベル、および規則を記述するポリシーデータ XML を取得します。

  
次の**値を返し**ます。ポリシーデータ XML。
  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
カスタム設定の一覧を取得します。

  
次の**値を返し**ます。カスタム設定のベクター。
  
### <a name="getpolicyfileid-function"></a>GetPolicyFileId 関数
ポリシーファイル ID を取得します。

  
次の**値を返し**ます。ポリシーファイル ID を表す文字列
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules 関数
ポリシーに自動または推奨規則があるかどうかを取得します。

  
次の**値を返し**ます。ポリシーに自動または推奨設定の規則があるかどうかを示すブール値
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime 関数
ポリシーが最後にフェッチされた時刻を取得します。

  
次の**値を返し**ます。ポリシーが最後にフェッチされた時刻