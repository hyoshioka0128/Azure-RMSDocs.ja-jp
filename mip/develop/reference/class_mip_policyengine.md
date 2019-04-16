---
title: class mip::PolicyEngine
description: Mip::policyengine クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: ce8ef7df12cdc9823a62234b5dadaaacdb7fed37
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2019
ms.locfileid: "59573787"
---
# <a name="class-mippolicyengine"></a>class mip::PolicyEngine 
このクラスは、すべてのエンジン関数のインターフェイスを提供します。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  ポリシー エンジン[設定](class_mip_policyengine_settings.md)を取得します。
public const std::vector\<std::shared_ptr\<Label\>\>& ListSensitivityLabels()  |  ポリシー エンジンに関連付けられている機密ラベルの一覧を示します。
public const std::vector\<std::shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes() const  |  ポリシー エンジンに関連付けられている機密の種類を一覧表示します。
public const std::string& GetMoreInfoUrl() const  |  ポリシー/ラベルに関する詳細情報を検索するための URL を提供します。
public bool IsLabelingRequired() const  |  ドキュメントにラベルを付ける必要があるかどうかを、ポリシーで指示するかどうかを確認します。
public std::shared_ptr\<ラベル\>GetDefaultSensitivityLabel()  |  既定の機密ラベルを取得します。
public std::shared_ptr\<PolicyHandler\> CreatePolicyHandler (bool isAuditDiscoveryEnabled)  |  ポリシー ハンドラーを作成して、ファイルの事項状態でポリシー関連の関数を実行します。
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  アプリケーションに固有のイベントを監査パイプラインにログを記録します。
public const std::string& GetPolicyDataXml() const  |  ポリシー データの設定、ラベル、およびこのポリシーに関連付けられているルールを記述する XML を取得します。
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  カスタム設定の一覧を取得します。
public const std::string& GetPolicyId() const  |  ポリシー ID を取得します
public bool HasClassificationRules() const  |  場合は、ポリシーは自動または推奨事項ルールを取得します。
public std::chrono::time_point\<std::chrono::system_clock\> GetLastPolicyFetchTime() const  |  ポリシーが最後にフェッチした時刻を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
ポリシー エンジン[設定](class_mip_policyengine_settings.md)を取得します。

  
**返します**:ポリシー エンジン設定。 
  
**関連項目**: [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md)
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels 関数
ポリシー エンジンに関連付けられている機密ラベルの一覧を示します。

  
**返します**:機密ラベルの一覧。
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes 関数
ポリシー エンジンに関連付けられている機密の種類を一覧表示します。

  
**返します**:機密ラベルの一覧。 LoadSensitivityTypesEnabled されました (false の場合は、空
  
**参照してください**:[PolicyEngine::Settings](class_mip_policyengine_settings.md))。
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl 関数
ポリシー/ラベルに関する詳細情報を検索するための URL を提供します。

  
**返します**:文字列の形式で url です。
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired 関数
ドキュメントにラベルを付ける必要があるかどうかを、ポリシーで指示するかどうかを確認します。

  
**返します**:必須、それ以外の場合は false にはラベルを付ける場合は true。
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel 関数
既定の機密ラベルを取得します。

  
**返します**:既定の機密ラベルの場合は存在の場合は、既定のラベルが設定されていない場合は nullptr。
  
### <a name="createpolicyhandler-function"></a>CreatePolicyHandler 関数
ポリシー ハンドラーを作成して、ファイルの事項状態でポリシー関連の関数を実行します。

パラメーター:  
* **A**: 監査検出が有効か無効かどうかを表すブール値。



  
**返します**:ポリシーのハンドラー。
アプリケーションは、ドキュメントの有効期間ポリシーのハンドラー オブジェクトを保持する必要があります。
  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent 関数
アプリケーションに固有のイベントを監査パイプラインにログを記録します。

パラメーター:  
* **レベル**: のログ レベル。情報/エラー/警告します。 


* **eventType**: イベントの種類の説明。 


* **eventData**: イベントに関連付けられたデータ。


  
### <a name="getpolicydataxml-function"></a>GetPolicyDataXml 関数
ポリシー データの設定、ラベル、およびこのポリシーに関連付けられているルールを記述する XML を取得します。

  
**返します**:ポリシー データは XML です。
  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
カスタム設定の一覧を取得します。

  
**返します**:カスタム設定のベクター。
  
### <a name="getpolicyid-function"></a>GetPolicyId 関数
ポリシー ID を取得します

  
**返します**:ポリシー ID を表す文字列です。
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules 関数
場合は、ポリシーは自動または推奨事項ルールを取得します。

  
**返します**:かどうかがあります、自動または recommandation 規則、ポリシーでのかを示すブール値
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime 関数
ポリシーが最後にフェッチした時刻を取得します。

  
**返します**:ポリシーが最後にフェッチした時間