---
title: class mip::FileEngine
description: Mip::fileengine クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 15ce90a80430f50854580f6c7a2993d92db0a744
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184792"
---
# <a name="class-mipfileengine"></a>class mip::FileEngine 
このクラスは、すべてのエンジン関数のインターフェイスを提供します。
  
## <a name="summary"></a>まとめ
 メンバー                        | [説明]                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  エンジンの設定を返します。
public const std::vector\<std::shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes() const  |  ポリシー エンジンに関連付けられている機密の種類を一覧表示します。
public const std::shared_ptr\<ラベル\>GetDefaultSensitivityLabel() 定数  |  既定の機密ラベルを取得します。
public const std::vector\<std::shared_ptr\<Label\>\>& ListSensitivityLabels()  |  機密ラベルの一覧を返します。
public const std::string& GetMoreInfoUrl() const  |  ポリシー/ラベルに関する詳細情報を検索するための URL を提供します。
public const std::string& GetPolicyId() const  |  ポリシー ID を取得します
public bool IsLabelingRequired() const  |  ドキュメントにラベルを付ける必要があることを、ポリシーで指示するかどうかを確認します。
public std::chrono::time_point\<std::chrono::system_clock\> GetLastPolicyFetchTime() const  |  ポリシーが最後にフェッチした時刻を取得します。
public void CreateFileHandlerAsync (const std::string & inputFilePath、const std::string & actualFilePath、bool isAuditDiscoveryEnabled、const std::shared_ptr\<filehandler::observer\>& fileHandlerObserver、const std::shared_ptr\<void\>& コンテキストには、const std::shared_ptr\<FileExecutionState\>& fileExecutionState)  |  指定されたファイル パスのファイル ハンドラーの作成を開始します。
public void CreateFileHandlerAsync (const std::shared_ptr\<Stream\>& inputStream、const std::string & actualFilePath、bool isAuditDiscoveryEnabled、const std::shared_ptr\<filehandler::observer\>& fileHandlerObserver、const std::shared_ptr\<void\>& コンテキストには、const std::shared_ptr\<FileExecutionState\>& fileExecutionState)  |  指定されたファイル ストリームのファイル ハンドラーの作成を開始します。
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  アプリケーションに固有のイベントを監査パイプラインにログを記録します。
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  カスタム設定の一覧を取得します。
public bool HasClassificationRules() const  |  場合は、ポリシーは自動または推奨事項ルールを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
エンジンの設定を返します。
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes 関数
ポリシー エンジンに関連付けられている機密の種類を一覧表示します。

  
**返します**:機密ラベルの一覧。 LoadSensitivityTypesEnabled されました (false の場合は、空
  
**参照してください**:[FileEngine::Settings](class_mip_fileengine_settings.md))。
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel 関数
既定の機密ラベルを取得します。

  
**返します**:既定の機密ラベルの場合は存在の場合は、既定のラベルが設定されていない場合は nullptr。
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels 関数
機密ラベルの一覧を返します。
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl 関数
ポリシー/ラベルに関する詳細情報を検索するための URL を提供します。

  
**返します**:文字列の形式で url です。
  
### <a name="getpolicyid-function"></a>GetPolicyId 関数
ポリシー ID を取得します

  
**返します**:ポリシー ID を表す文字列です。
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired 関数
ドキュメントにラベルを付ける必要があることを、ポリシーで指示するかどうかを確認します。

  
**返します**:必須、それ以外の場合は false にはラベルを付ける場合は true。
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime 関数
ポリシーが最後にフェッチした時刻を取得します。

  
**返します**:ポリシーが最後にフェッチした時間
  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync 関数
指定されたファイル パスのファイル ハンドラーの作成を開始します。

パラメーター:  
* **inputFilePath**:開くファイル。 パスにはファイル名を含める必要があり、ファイル名拡張子が存在する場合はそれも含めます。 


* **actualFilePath**:実際の (一時的ではない) ファイルのパスは、監査に使用されます。 


* **isAuditDiscoveryEnabled**: 監査検出が有効かどうかを表します。 


* **fileHandlerObserver**:[FileHandler::Observer](class_mip_filehandler_observer.md) インターフェイスを実装するクラス。 


* **コンテキスト**:オブザーバーに不透明渡されるクライアント コンテキスト。


  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync 関数
指定されたファイル ストリームのファイル ハンドラーの作成を開始します。

パラメーター:  
* **inputStream**:ファイル データを含むストリーム。 


* **actualFilePath**:ファイルへのパス。 パスにはファイル名を含める必要があり、ファイル名拡張子が存在する場合はそれも含めます。 監査ファイルを識別するためにも使用されます。 


* **isAuditDiscoveryEnabled**: 監査検出が有効かどうかを表します。 


* **fileHandlerObserver**:[FileHandler::Observer](class_mip_filehandler_observer.md) インターフェイスを実装するクラス。 


* **コンテキスト**:オブザーバーに不透明渡されるクライアント コンテキスト。


  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent 関数
アプリケーションに固有のイベントを監査パイプラインにログを記録します。

パラメーター:  
* **レベル**: ログ レベルの説明。警告/情報/エラー 


* **eventType**: イベントの種類の説明 


* **eventData**: イベントに関連付けられているデータ


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
カスタム設定の一覧を取得します。

  
**返します**:カスタム設定のベクター
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules 関数
場合は、ポリシーは自動または推奨事項ルールを取得します。

  
**返します**:かどうかがあります、自動または recommandation 規則、ポリシーでのかを示すブール値