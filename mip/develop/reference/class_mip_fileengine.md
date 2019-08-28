---
title: class mip::FileEngine
description: 'Microsoft Information Protection (MIP) SDK の mip:: fileengine クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 08/27/2019
ms.openlocfilehash: d19751e9da113be2cea94d7b169be29026813da8
ms.sourcegitcommit: 1499790746145d40d667d138baa6e18598421f0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2019
ms.locfileid: "70056116"
---
# <a name="class-mipfileengine"></a>class mip::FileEngine 
このクラスは、すべてのエンジン関数のインターフェイスを提供します。
  
## <a name="summary"></a>Summary
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  エンジンの設定を返します。
public const std:: vector\<std:: shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes () const  |  ポリシーエンジンに関連付けられている感度の種類を一覧表示します。
public const std:: shared_ptr\<Label\> GetDefaultSensitivityLabel () const  |  既定の機密ラベルを取得します。
public std:: shared_ptr\<Label\> GetLabelById (const std:: string & id) const  |  指定された id に従ってラベルを取得します。
public const std:: vector\<std:: shared_ptr\<Label\>\>& ListSensitivityLabels ()  |  機密ラベルの一覧を返します。
public const std::string& GetMoreInfoUrl() const  |  ポリシー/ラベルに関する詳細情報を検索するための URL を提供します。
public const std:: string & GetPolicyFileId () const  |  ポリシーファイル ID を取得します。
public bool IsLabelingRequired() const  |  ドキュメントにラベルを付ける必要があることを、ポリシーで指示するかどうかを確認します。
public std::chrono::time_point\<std::chrono::system_clock\> GetLastPolicyFetchTime() const  |  ポリシーが最後にフェッチされた時刻を取得します。
public void createfilehandler async (const std:: string & inputfilepath、const std:: string & actualfilepath、bool isauditdiscoveryenabled、const std:: shared_ptr\<filehandler:: Observer\>& fileハンドラオブザーバー、const std:: shared_ptr\<void\>& context、const std:: shared_ptr\<fileexecutionstate\>& fileexecutionstate)  |  指定されたファイル パスのファイル ハンドラーの作成を開始します。
public void createfilehandler async (const std:: shared_ptr\<ストリーム\>& inputStream、const std:: string & actualfilepath、bool isauditdiscoveryenabled、const std:: shared_ptr\<filehandler:: オブザーバー\>\<\>\<& fileハンドラオブザーバー、const std:: shared_ptr void & context、const std:: shared_ptr filehandlerobserver & filehandlerobserver) \>  |  指定されたファイル ストリームのファイル ハンドラーの作成を開始します。
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  アプリケーションに固有のイベントを監査パイプラインにログを記録します。
public const std:: vector\<std::p air\<std:: string、std:: string\>\>& GetCustomSettings () const  |  カスタム設定の一覧を取得します。
public bool HasClassificationRules () const  |  ポリシーに自動または推奨規則があるかどうかを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
エンジンの設定を返します。
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes 関数
ポリシーエンジンに関連付けられている感度の種類を一覧表示します。

  
次の**値を返し**ます。機密ラベルの一覧。 LoadSensitivityTypesEnabled が false の場合は空 (
  
**関連**項目:[Fileengine:: Settings](class_mip_fileengine_settings.md))。
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel 関数
既定の機密ラベルを取得します。

  
次の**値を返し**ます。既定の感度ラベル (存在する場合)、既定のラベルが設定されていない場合は nullptr。
  
### <a name="getlabelbyid-function"></a>GetLabelById 関数
指定された id に従ってラベルを取得します。
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels 関数
機密ラベルの一覧を返します。
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl 関数
ポリシー/ラベルに関する詳細情報を検索するための URL を提供します。

  
次の**値を返し**ます。文字列形式の url。
  
### <a name="getpolicyfileid-function"></a>GetPolicyFileId 関数
ポリシーファイル ID を取得します。

  
次の**値を返し**ます。ポリシーファイル ID を表す文字列
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired 関数
ドキュメントにラベルを付ける必要があることを、ポリシーで指示するかどうかを確認します。

  
次の**値を返し**ます。ラベル付けが必須の場合は True、それ以外の場合は false。
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime 関数
ポリシーが最後にフェッチされた時刻を取得します。

  
次の**値を返し**ます。ポリシーが最後にフェッチされた時刻
  
### <a name="createfilehandlerasync-function"></a>Createfileハンドラ Async 関数
指定されたファイル パスのファイル ハンドラーの作成を開始します。

パラメーター:  
* **Inputfilepath**:開くファイル。 パスにはファイル名を含める必要があり、ファイル名拡張子が存在する場合はそれも含めます。 


* **Actualfilepath**:監査には、(一時ではなく) 実際のファイルパスが使用されます。 


* **Isauditdiscoveryenabled**: 監査検出が有効かどうかを表します。 


* **Fileハンドラオブザーバー**:[FileHandler::Observer](class_mip_filehandler_observer.md) インターフェイスを実装するクラス。 


* **コンテキスト**:オブザーバーに戻される不透明クライアントコンテキスト。


  
### <a name="createfilehandlerasync-function"></a>Createfileハンドラ Async 関数
指定されたファイル ストリームのファイル ハンドラーの作成を開始します。

パラメーター:  
* **inputStream**:ファイルデータを格納しているストリーム。 


* **Actualfilepath**:ファイルへのパス。 パスにはファイル名を含める必要があり、ファイル名拡張子が存在する場合はそれも含めます。 は、監査でファイルを識別するためにも使用します。 


* **Isauditdiscoveryenabled**: 監査検出が有効かどうかを表します。 


* **Fileハンドラオブザーバー**:[FileHandler::Observer](class_mip_filehandler_observer.md) インターフェイスを実装するクラス。 


* **コンテキスト**:オブザーバーに戻される不透明クライアントコンテキスト。


  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent 関数
アプリケーションに固有のイベントを監査パイプラインにログを記録します。

パラメーター:  
* **level**: ログレベルの説明。情報/エラー/警告 


* **eventType**: イベントの種類の説明 


* **eventData**: イベントに関連付けられているデータ


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
カスタム設定の一覧を取得します。

  
次の**値を返し**ます。カスタム設定のベクター
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules 関数
ポリシーに自動または推奨規則があるかどうかを取得します。

  
次の**値を返し**ます。ポリシーに自動または推奨設定の規則があるかどうかを示すブール値