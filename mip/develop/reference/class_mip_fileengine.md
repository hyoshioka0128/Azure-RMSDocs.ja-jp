---
title: class mip FileEngine
description: class mip FileEngine のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a7342edf27b19f43881b2e8d378fa243d26f7056
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446075"
---
# <a name="class-mipfileengine"></a>class mip::FileEngine 
このクラスは、すべてのエンジン関数のインターフェイスを提供します。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  エンジンの設定を返します。
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  機密ラベルの一覧を返します。
 public const std::string& GetMoreInfoUrl() const  |  ポリシー/ラベルに関する詳細情報を検索するための URL を提供します。
 public bool IsLabelingRequired() const  |  ドキュメントにラベルを付ける必要があることを、ポリシーで指示するかどうかを確認します。
public void CreateFileHandlerAsync(const std::string& inputFilePath, const ContentState contentState, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver, const std::shared_ptr<void>& context)  |  指定されたファイル パスのファイル ハンドラーの作成を開始します。
public void CreateFileHandlerAsync(const std::shared_ptr<Stream>& inputStream, const std::string& inputFilePath, const mip::ContentState contentState, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver, const std::shared_ptr<void>& context)  |  指定されたファイル ストリームのファイル ハンドラーの作成を開始します。
 public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  アプリケーションに固有のイベントを監査パイプラインにログを記録します。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
エンジンの設定を返します。
  
### <a name="label"></a>Label
機密ラベルの一覧を返します。
  
### <a name="getmoreinfourl"></a>GetMoreInfoUrl
ポリシー/ラベルに関する詳細情報を検索するための URL を提供します。

  
**戻り値**: 文字列形式の URL。
  
### <a name="islabelingrequired"></a>IsLabelingRequired
ドキュメントにラベルを付ける必要があることを、ポリシーで指示するかどうかを確認します。

  
**戻り値**: ラベルが必須の場合は true、それ以外の場合は false。
  
### <a name="createfilehandlerasync"></a>CreateFileHandlerAsync
指定されたファイル パスのファイル ハンドラーの作成を開始します。

パラメーター:  
* 開くファイル。**** パスにはファイル名を含める必要があり、ファイル名拡張子が存在する場合はそれも含めます。 


* **contentState**: アプリケーションで操作中のコンテンツの状態。 


* [FileHandler::Observer](class_mip_filehandler_observer.md) インターフェイスを実装するクラス。**** 


* **context**: オブザーバーに不透明に渡されるクライアント コンテキスト。


  
### <a name="createfilehandlerasync"></a>CreateFileHandlerAsync
指定されたファイル ストリームのファイル ハンドラーの作成を開始します。

パラメーター:  
* **inputStream**: ファイル データを含むストリーム。 


* **inputFilePath**: ファイルへのパス。 パスにはファイル名を含める必要があり、ファイル名拡張子が存在する場合はそれも含めます。 


* **contentState**: アプリケーションで操作中のコンテンツの状態。 


* **fileHandlerObserver**: [FileHandler::Observer](class_mip_filehandler_observer.md) インターフェイスを実装するクラス。 


* **context**: オブザーバーに不透明に渡されるクライアント コンテキスト。


  
### <a name="sendapplicationauditevent"></a>SendApplicationAuditEvent
アプリケーションに固有のイベントを監査パイプラインにログを記録します。

パラメーター:  
* **level**: ログ レベルの説明: 情報/エラー/警告 


* **eventType**: イベントの種類の説明 


* **eventData**: イベントに関連付けられているデータ

