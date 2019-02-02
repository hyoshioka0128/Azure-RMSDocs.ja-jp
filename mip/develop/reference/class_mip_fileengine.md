---
title: class mip::FileEngine
description: Mip::fileengine クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 4bcdd08cb7ced9e2eea8fa09d9364064a8d198df
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651464"
---
# <a name="class-mipfileengine"></a>class mip::FileEngine 
このクラスは、すべてのエンジン関数のインターフェイスを提供します。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  エンジンの設定を返します。
public const std::vector\<std::shared_ptr\<SensitivityTypesRulePackage\>\>& ListSensitivityTypes() const  |  ポリシー エンジンに関連付けられている機密の種類を一覧表示します。
public const std::vector\<std::shared_ptr\<Label\>\>& ListSensitivityLabels()  |  機密ラベルの一覧を返します。
public const std::string& GetMoreInfoUrl() const  |  ポリシー/ラベルに関する詳細情報を検索するための URL を提供します。
public bool IsLabelingRequired() const  |  ドキュメントにラベルを付ける必要があることを、ポリシーで指示するかどうかを確認します。
public void CreateFileHandlerAsync (const std::string & inputFilePath、const std::string & contentIdentifier、const の ContentState contentState bool isAuditDiscoveryEnabled、const std::shared_ptr\<filehandler::observer\>& fileHandlerObserver、const std::shared_ptr\<void\>& コンテキストには、const std::shared_ptr\<FileExecutionState\>& fileExecutionState)  |  指定されたファイル パスのファイル ハンドラーの作成を開始します。
public void CreateFileHandlerAsync (const std::shared_ptr\<Stream\>& inputStream、const std::string & inputFilePath、const std::string & contentIdentifier、const mip::ContentState contentState、boolisAuditDiscoveryEnabled、const std::shared_ptr\<filehandler::observer\>& fileHandlerObserver、const std::shared_ptr\<void\>& コンテキストには、const std::shared_ptr\<FileExecutionState\>& fileExecutionState)  |  指定されたファイル ストリームのファイル ハンドラーの作成を開始します。
public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  アプリケーションに固有のイベントを監査パイプラインにログを記録します。
public const std::vector\<std::pair\<std::string, std::string\>\>& GetCustomSettings() const  |  カスタム設定の一覧を取得します。
  
## <a name="members"></a>メンバー
  
### <a name="getsettings-function"></a>GetSettings 関数
エンジンの設定を返します。
  
### <a name="listsensitivitytypes-function"></a>ListSensitivityTypes 関数
ポリシー エンジンに関連付けられている機密の種類を一覧表示します。

  
**返します**:機密ラベルの一覧。 LoadSensitivityTypesEnabled されました (false の場合は、空
  
**参照してください**:[FileEngine::Settings](class_mip_fileengine_settings.md))。
  
### <a name="listsensitivitylabels-function"></a>ListSensitivityLabels 関数
機密ラベルの一覧を返します。
  
### <a name="getmoreinfourl-function"></a>GetMoreInfoUrl 関数
ポリシー/ラベルに関する詳細情報を検索するための URL を提供します。

  
**返します**:文字列の形式で url です。
  
### <a name="islabelingrequired-function"></a>IsLabelingRequired 関数
ドキュメントにラベルを付ける必要があることを、ポリシーで指示するかどうかを確認します。

  
**返します**:必須、それ以外の場合は false にはラベルを付ける場合は true。
  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync 関数
指定されたファイル パスのファイル ハンドラーの作成を開始します。

パラメーター:  
* **inputFilePath**:開くファイル。 パスにはファイル名を含める必要があり、ファイル名拡張子が存在する場合はそれも含めます。 


* **contentIdentifier**: コンテンツを人間が判読できる識別子。 ファイルの例:電子メールの"C:\mip-sdk-for-cpp\files\audit.docx"[&] 例:"RE:監査design:user1@contoso.com"[サブジェクト: 送信者] 


* **contentState**:アプリケーションが操作中に、コンテンツの状態。 


* **isAuditDiscoveryEnabled**: 監査検出が有効かどうかを表します。 


* **fileHandlerObserver**:[FileHandler::Observer](class_mip_filehandler_observer.md) インターフェイスを実装するクラス。 


* **コンテキスト**:オブザーバーに不透明渡されるクライアント コンテキスト。


  
### <a name="createfilehandlerasync-function"></a>CreateFileHandlerAsync 関数
指定されたファイル ストリームのファイル ハンドラーの作成を開始します。

パラメーター:  
* **inputStream**:ファイル データを含むストリーム。 


* **inputFilePath**:ファイルへのパス。 パスにはファイル名を含める必要があり、ファイル名拡張子が存在する場合はそれも含めます。 


* **contentIdentifier**: コンテンツを人間が判読できる識別子。 ファイルの例:電子メールの"C:\mip-sdk-for-cpp\files\audit.docx"[&] 例:"RE:監査design:user1@contoso.com"[サブジェクト: 送信者] 


* **contentState**:アプリケーションが操作中に、コンテンツの状態。 


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