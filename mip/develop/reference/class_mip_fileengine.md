---
title: class mip::FileEngine
description: 'Microsoft Information Protection (MIP) SDK の mip:: fileengine クラスについて説明します。'
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 10/29/2019
ms.openlocfilehash: 8f1ef9e1ca46037243e170a59717be74954d4cb1
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73560276"
---
# <a name="class-mipfileengine"></a>class mip::FileEngine 
このクラスは、すべてのエンジン関数のインターフェイスを提供します。
  
## <a name="summary"></a>要約
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  エンジンの設定を返します。
public const std:: vector\<std:: shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes () const  |  ポリシーエンジンに関連付けられている感度の種類を一覧表示します。
public const std:: shared_ptr\<Label\> GetDefaultSensitivityLabel () const  |  既定の機密ラベルを取得します。
public std:: shared_ptr\<Label\> GetLabelById (const std:: string & id) const  |  指定された id に従ってラベルを取得します。
public const std:: vector\<std:: shared_ptr\<Label\>\>& ListSensitivityLabels ()  |  機密ラベルの一覧を返します。
public const std::string& GetMoreInfoUrl() const  |  ポリシー/ラベルに関する詳細情報を検索するための URL を提供します。
public const std:: string & GetPolicyFileId () const  |  ポリシーファイル ID を取得します。
public const std:: string & GetSensitivityFileId () const  |  感度ファイル ID を取得します。
public bool IsLabelingRequired() const  |  ドキュメントにラベルを付ける必要があることを、ポリシーで指示するかどうかを確認します。
public std:: chrono:: time_point\<std:: chrono:: system_clock\> GetLastPolicyFetchTime () const  |  ポリシーが最後にフェッチされた時刻を取得します。
public void Createfilehandler Async (const std:: string & inputFilePath、const std:: string & actualFilePath、bool isAuditDiscoveryEnabled、const std:: shared_ptr\<FileHandler:: オブザーバー\>& Fileハンドラオブザーバー、const std:: shared_ptr\<void\>& context、const std:: shared_ptr\<FileExecutionState\>& fileExecutionState)  |  指定されたファイル パスのファイル ハンドラーの作成を開始します。
public void Createfilehandler Async (const std:: shared_ptr\<Stream\>& inputStream、const std:: string & actualFilePath、bool isAuditDiscoveryEnabled、const std:: shared_ptr\<FileHandler:: Observer\>&Fileハンドラオブザーバー、const std:: shared_ptr\<void\>& context、const std:: shared_ptr\<Filehandlerobserver\>& Filehandlerobserver)  |  指定されたファイル ストリームのファイル ハンドラーの作成を開始します。
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  アプリケーションに固有のイベントを監査パイプラインにログを記録します。
public const std:: vector\<std::p air\<std:: string、std:: string\>\>& GetCustomSettings () const  |  カスタム設定の一覧を取得します。
public bool HasClassificationRules () const  |  ポリシーに自動または推奨規則があるかどうかを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
エンジンの設定を返します。
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes 関数
ポリシーエンジンに関連付けられている感度の種類を一覧表示します。

  
**戻り値**: 機密ラベルの一覧。 LoadSensitivityTypesEnabled が false の場合は空 (
  
**参照**: fileengine:: Settings)
  
### <a name="getdefaultsensitivitylabel-function"></a>GetDefaultSensitivityLabel 関数
既定の機密ラベルを取得します。

  
**戻り値**: 存在する場合は既定の機密ラベル、既定のラベルが設定されていない場合は nullptr。
  
### <a name="getlabelbyid-function"></a>GetLabelById 関数
指定された id に従ってラベルを取得します。
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels 関数
機密ラベルの一覧を返します。
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl 関数
ポリシー/ラベルに関する詳細情報を検索するための URL を提供します。

  
**戻り値**: 文字列形式の URL。
  
### <a name="getpolicyfileid-function"></a>GetPolicyFileId 関数
ポリシーファイル ID を取得します。

  
**戻り値**: ポリシーファイル ID を表す文字列
  
### <a name="getsensitivityfileid-function"></a>GetSensitivityFileId 関数
感度ファイル ID を取得します。

  
**戻り値**: ポリシーファイル ID を表す文字列
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired 関数
ドキュメントにラベルを付ける必要があることを、ポリシーで指示するかどうかを確認します。

  
**戻り値**: ラベルが必須の場合は true、それ以外の場合は false。
  
### <a name="getlastpolicyfetchtime-function"></a>GetLastPolicyFetchTime 関数
ポリシーが最後にフェッチされた時刻を取得します。

  
**戻り値**: ポリシーが最後にフェッチされた時刻
  
### <a name="createfilehandlerasync-function"></a>Createfileハンドラ Async 関数
指定されたファイル パスのファイル ハンドラーの作成を開始します。

パラメーター:  
* **Inputfilepath**: 開くファイル。 パスにはファイル名を含める必要があり、ファイル名拡張子が存在する場合はそれも含めます。 


* **Actualfilepath**: 監査に使用される実際の (一時ではない) ファイルパス。 


* **Isauditdiscoveryenabled**: 監査検出が有効かどうかを表します。 


* **Fileハンドラオブザーバー**: filehandler:: Observer インターフェイスを実装するクラス。 


* **context**: オブザーバーに不透明に渡されるクライアント コンテキスト。


  
### <a name="createfilehandlerasync-function"></a>Createfileハンドラ Async 関数
指定されたファイル ストリームのファイル ハンドラーの作成を開始します。

パラメーター:  
* **inputStream**: ファイル データを含むストリーム。 


* **Actualfilepath**: ファイルへのパス。 パスにはファイル名を含める必要があり、ファイル名拡張子が存在する場合はそれも含めます。 は、監査でファイルを識別するためにも使用します。 


* **Isauditdiscoveryenabled**: 監査検出が有効かどうかを表します。 


* **Fileハンドラオブザーバー**: filehandler:: Observer インターフェイスを実装するクラス。 


* **context**: オブザーバーに不透明に渡されるクライアント コンテキスト。


  
### <a name="sendapplicationauditevent-function"></a>SendApplicationAuditEvent 関数
アプリケーションに固有のイベントを監査パイプラインにログを記録します。

パラメーター:  
* **level**: ログ レベルの説明: 情報/エラー/警告 


* **eventType**: イベントの種類の説明 


* **eventData**: イベントに関連付けられているデータ


  
### <a name="getcustomsettings-function"></a>GetCustomSettings 関数
カスタム設定の一覧を取得します。

  
**戻り**値: カスタム設定のベクター
  
### <a name="hasclassificationrules-function"></a>HasClassificationRules 関数
ポリシーに自動または推奨規則があるかどうかを取得します。

  
**戻り値**: ポリシーに自動または推奨規則があるかどうかを示すブール値