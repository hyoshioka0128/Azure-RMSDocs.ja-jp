---
title: class mip PolicyEngine
description: class mip PolicyEngine のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 57dd325e9c00a3cb2a4056f7ef0b522efef5d0c4
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446041"
---
# <a name="class-mippolicyengine"></a>class mip::PolicyEngine 
このクラスは、すべてのエンジン関数のインターフェイスを提供します。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  ポリシー エンジン[設定](class_mip_policyengine_settings.md)を取得します。
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  ポリシー エンジンに関連付けられている機密ラベルの一覧を示します。
 public const std::string& GetMoreInfoUrl() const  |  ポリシー/ラベルに関する詳細情報を検索するための URL を提供します。
 public bool IsLabelingRequired() const  |  ドキュメントにラベルを付ける必要があるかどうかを、ポリシーで指示するかどうかを確認します。
public std::shared_ptr<Label> GetDefaultSensitivityLabel()  |  既定の機密ラベルを取得します。
public std::shared_ptr<PolicyHandler> CreatePolicyHandler(const std::string& contentIdentifier)  |  ポリシー ハンドラーを作成して、ファイルの事項状態でポリシー関連の関数を実行します。
 public void SendApplicationAuditEvent(const std::string& level, const std::string& eventType, const std::string& eventData)  |  アプリケーションに固有のイベントを監査パイプラインにログを記録します。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
ポリシー エンジン[設定](class_mip_policyengine_settings.md)を取得します。

  
**戻り値**: ポリシー エンジン設定。 
  
**関連項目**: [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md)
  
### <a name="label"></a>Label
ポリシー エンジンに関連付けられている機密ラベルの一覧を示します。

  
**戻り値**: 機密ラベルの一覧。
  
### <a name="getmoreinfourl"></a>GetMoreInfoUrl
ポリシー/ラベルに関する詳細情報を検索するための URL を提供します。

  
**戻り値**: 文字列形式の URL。
  
### <a name="islabelingrequired"></a>IsLabelingRequired
ドキュメントにラベルを付ける必要があるかどうかを、ポリシーで指示するかどうかを確認します。

  
**戻り値**: ラベルが必須の場合は true、それ以外の場合は false。
  
### <a name="label"></a>Label
既定の機密ラベルを取得します。

  
**戻り値**: 存在する場合は既定の機密ラベル、既定のラベルが設定されていない場合は nullptr。
  
### <a name="policyhandler"></a>PolicyHandler
ポリシー ハンドラーを作成して、ファイルの事項状態でポリシー関連の関数を実行します。

パラメーター:  
* **contentIdentifier**: コンテンツに対する人間が判読できる識別子。 ファイルの例: "C:\mip-sdk-for-cpp\files\audit.docx" [パス] 電子メールの例: "RE: 監査 design:user1@contoso.com" [件名:送信者]



  
**戻り値**: ポリシー ハンドラー。
  
### <a name="sendapplicationauditevent"></a>SendApplicationAuditEvent
アプリケーションに固有のイベントを監査パイプラインにログを記録します。

パラメーター:  
* **description**: ログ レベルの説明: 情報/エラー/警告 


* **eventType**: イベントの種類の説明 


* **eventData**: イベントに関連付けられているデータ

