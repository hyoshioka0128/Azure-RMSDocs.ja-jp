---
title: クラス PolicyEngine
description: 'Microsoft Information Protection (MIP) SDK の policyengine:: undefined クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 733e1ced7a1f5ca1ec8d47709ef4c364c04e37a5
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "95566673"
---
# <a name="class-policyengine"></a>クラス PolicyEngine 
このクラスは、すべてのエンジン関数のインターフェイスを提供します。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  ポリシー エンジン設定を取得します。
public const std:: vector \<std::shared_ptr\<Label\> \>& ListSensitivityLabels ()  |  ポリシー エンジンに関連付けられている機密ラベルの一覧を示します。
public const std:: vector \<std::shared_ptr\<SensitivityTypesRulePackage\> \>& ListSensitivityTypes () const  |  ポリシーエンジンに関連付けられている感度の種類を一覧表示します。
public const std::string& GetMoreInfoUrl() const  |  ポリシー/ラベルに関する詳細情報を検索するための URL を提供します。
public bool IsLabelingRequired() const  |  ドキュメントにラベルを付ける必要があるかどうかを、ポリシーで指示するかどうかを確認します。
public std::shared_ptr\<Label\> GetDefaultSensitivityLabel()  |  既定の機密ラベルを取得します。
public std:: shared_ptr \<Label\> GetLabelById (const std:: string& id) const  |  指定された id に従ってラベルを取得します。
public std:: shared_ptr \<PolicyHandler\> createpolicyhandler (Bool isAuditDiscoveryEnabled)  |  ポリシー ハンドラーを作成して、ファイルの事項状態でポリシー関連の関数を実行します。
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  アプリケーションに固有のイベントを監査パイプラインにログを記録します。
public const std:: string& GetTenantId () const  |  エンジンに関連付けられているテナント ID を取得します。
public const std:: string& GetPolicyDataXml () const  |  このポリシーに関連付けられている設定、ラベル、および規則を記述するポリシーデータ XML を取得します。
public const std:: string& GetSensitivityTypesDataXml () const  |  このポリシーに関連付けられている感度の種類を記述する、秘密度の種類のデータ XML を取得します。
public const std:: vector \<std::pair\<std::string, std::string\> \>& GetCustomSettings () const  |  カスタム設定の一覧を取得します。
public const std:: string& GetPolicyFileId () const  |  ポリシーファイル ID を取得します。
public const std:: string& GetSensitivityFileId () const  |  感度ファイル ID を取得します。
public bool HasClassificationRules () const  |  ポリシーに自動または推奨規則があるかどうかを取得します。
public ClassificationScheme GetClassificationScheme () const  |  ポリシーが最新のに基づいて分類される必要があるかどうかを取得します。
public std:: chrono:: time_point \<std::chrono::system_clock\> getlastpolicyfetchtime () const  |  ポリシーが最後にフェッチされた時刻を取得します。
public uint32_t GetWxpMetadataVersion () const  |  推奨される WXP (Windows、Excel、Powerpoint) メタデータバージョンを取得します。現在、共同作成が有効になっているバージョンでは、古いバージョン1では0です。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
ポリシー エンジン設定を取得します。

  
**戻り値**: ポリシー エンジン設定。 
  
**関連** 項目: mip::P olicyEngine:: Settings
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels 関数
ポリシー エンジンに関連付けられている機密ラベルの一覧を示します。

  
**戻り値**: 機密ラベルの一覧。
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes 関数
ポリシーエンジンに関連付けられている感度の種類を一覧表示します。

  
**戻り値**: 機密ラベルの一覧。 LoadSensitivityTypesEnabled が false の場合は空 (
  
**関連** 項目: policyengine:: Settings)
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl 関数
ポリシー/ラベルに関する詳細情報を検索するための URL を提供します。

  
**戻り値**: 文字列形式の URL。
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired 関数
ドキュメントにラベルを付ける必要があるかどうかを、ポリシーで指示するかどうかを確認します。

  
**戻り値**: ラベルが必須の場合は true、それ以外の場合は false。
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel 関数
既定の機密ラベルを取得します。

  
**戻り値**: 存在する場合は既定の機密ラベル、既定のラベルが設定されていない場合は nullptr。
  
### <a name="getlabelbyid-function"></a>GetLabelById 関数
指定された id に従ってラベルを取得します。
  
### <a name="createpolicyhandler-function"></a>CreatePolicyHandler 関数
ポリシー ハンドラーを作成して、ファイルの事項状態でポリシー関連の関数を実行します。

パラメーター:  
* **A**: 監査検出が有効かどうかを表すブール値。



  
**戻り値**: ポリシー ハンドラー。
アプリケーションでは、ドキュメントの有効期間にわたってポリシーハンドラーオブジェクトを保持する必要があります。
  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent 関数
アプリケーションに固有のイベントを監査パイプラインにログを記録します。

パラメーター:  
* **レベル**: ログレベル: Info/Error/Warning。 


* **eventType**: イベントの種類の説明。 


* **eventData**: イベントに関連付けられているデータ。


  
### <a name="gettenantid-function"></a>GetTenantId 関数
エンジンに関連付けられているテナント ID を取得します。

  
**返される値**: テナント ID
  
### <a name="getpolicydataxml-function"></a>GetPolicyDataXml 関数
このポリシーに関連付けられている設定、ラベル、および規則を記述するポリシーデータ XML を取得します。

  
は、ポリシーデータ XML **を返し** ます。
  
### <a name="getsensitivitytypesdataxml-function"></a>GetSensitivityTypesDataXml 関数
このポリシーに関連付けられている感度の種類を記述する、秘密度の種類のデータ XML を取得します。

  
**を返し** ます。秘密度の種類のデータ XML です。
  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
カスタム設定の一覧を取得します。

  
**戻り** 値: カスタム設定のベクター。
  
### <a name="getpolicyfileid-function"></a>GetPolicyFileId 関数
ポリシーファイル ID を取得します。

  
**戻り値**: ポリシーファイル ID を表す文字列
  
### <a name="getsensitivityfileid-function"></a>GetSensitivityFileId 関数
感度ファイル ID を取得します。

  
**戻り値**: ポリシーファイル ID を表す文字列
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules 関数
ポリシーに自動または推奨規則があるかどうかを取得します。

  
**戻り値**: ポリシーに自動または推奨規則があるかどうかを示すブール値
  
### <a name="getclassificationscheme-function"></a>GetClassificationScheme 関数
ポリシーが最新のに基づいて分類される必要があるかどうかを取得します。

  
**戻り値**: 使用するエンジンを顧客に通知するエンジンの種類
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime 関数
ポリシーが最後にフェッチされた時刻を取得します。

  
**戻り値**: ポリシーが最後にフェッチされた時刻
  
### <a name="getwxpmetadataversion-function"></a>GetWxpMetadataVersion 関数
推奨される WXP (Windows、Excel、Powerpoint) メタデータバージョンを取得します。現在、共同作成が有効になっているバージョンでは、古いバージョン1では0です。

  
**を返し** ます。 Uint32_t int は、テナントが wxp ファイルに対してサポートするメタデータのバージョンを確認します。