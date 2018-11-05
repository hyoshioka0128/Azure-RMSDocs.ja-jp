---
title: class mip PolicyProfile Settings
description: class mip PolicyProfile Settings のリファレンス
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 07cbcbc022c02a43f751e1cf55b5b0efdfb816d1
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "47446912"
---
# <a name="class-mippolicyprofilesettings"></a>class mip::PolicyProfile::Settings 
作成時および有効期間全体にわたって [PolicyProfile](class_mip_policyprofile.md) に使用される[設定](class_mip_policyprofile_settings.md)。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public Settings(const std::string& path, bool useInMemoryStorage, const std::shared_ptr<AuthDelegate>& authDelegate, const std::shared_ptr<PolicyProfile::Observer>& observer, const ApplicationInfo& applicationInfo)  |  プロファイルを構成するためのインターフェイス。
 public const std::string& GetPath() const  |  保存された状態へのパスを取得します。
 public bool GetUseInMemoryStorage() const  |  Use In Memory Storage フラグを取得します。
public const std::shared_ptr<AuthDelegate>& GetAuthDelegate() const  |  認証委任を取得します。
public const std::shared_ptr<PolicyProfile::Observer>& GetObserver() const  |  イベント オブザーバーを取得します。
 public const ApplicationInfo GetApplicationInfo() const  |  アプリケーション情報を取得します。
public std::shared_ptr<LoggerDelegate> GetLoggerDelegate() const  |  アプリケーションによって提供されるロガー委任を取得します (提供される場合)。
public void SetLoggerDelegate(const std::shared_ptr<LoggerDelegate>& loggerDelegate)  |  既定のロガーをオーバーライドします。
public std::shared_ptr<HttpDelegate> GetHttpDelegate() const  |  アプリケーションによって提供される HTTP 委任が取得されます (提供される場合)。
public void SetHttpDelegate(const std::shared_ptr<HttpDelegate>& httpDelegate)  |  クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。
 public void OptOutTelemetry()  |  テレメトリの収集をすべて無効にします。
 public bool IsTelemetryOptedOut() const  |  テレメトリの収集を無効にする必要があるかどうかを取得します。
 public void SetMinimumLogLevel(LogLevel logLevel)  |  ログ イベントをトリガーする最小のログ レベルを設定します。
 public LogLevel GetMinimumLogLevel() const  |  最小のログ レベル オブジェクトを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
プロファイルを構成するためのインターフェイス。

パラメーター:  
* **path**: SDK でプロファイル状態が格納されるディレクトリへのパス。 


* **useInMemoryStorage**: キャッシュされた状態をディスクではなくメモリに格納します。 


* **authDelegate**: 認証トークンを取得するために SDK によって使用される認証委任。 


* **observer**: [PolicyProfile::Observer](class_mip_policyprofile_observer.md) インターフェイスを実装するクラス。 nullptr にすることができます。 


* **applicationInfo**: サービスへのアクセスに使用されるアプリケーション識別子。


  
### <a name="getpath"></a>GetPath
保存された状態へのパスを取得します。

  
**戻り値**: 保存された状態へのパス。
  
### <a name="getuseinmemorystorage"></a>GetUseInMemoryStorage
Use In Memory Storage フラグを取得します。

  
**戻り値**: メモリでの使用が設定されている場合は true、それ以外の場合は false。
  
### <a name="getauthdelegate"></a>GetAuthDelegate
認証委任を取得します。

  
**戻り値**: 認証委任。
  
### <a name="policyprofileobserver"></a>PolicyProfile::Observer
イベント オブザーバーを取得します。

  
**戻り値**: イベント オブザーバー。
  
### <a name="applicationinfo"></a>ApplicationInfo
アプリケーション情報を取得します。

  
**戻り値**: アプリケーション情報。
  
### <a name="loggerdelegate"></a>LoggerDelegate
アプリケーションによって提供されるロガー委任を取得します (提供される場合)。

  
**戻り値**: ロガー
  
### <a name="setloggerdelegate"></a>SetLoggerDelegate
既定のロガーをオーバーライドします。

パラメーター:  
* **loggerDelegate**: クライアント アプリケーションによって実装されるログ コールバック インターフェイス


このメソッドは、独自のロガー実装を使用するクライアント アプリケーションによって呼び出される必要があります
  
### <a name="httpdelegate"></a>HttpDelegate
アプリケーションによって提供される HTTP 委任が取得されます (提供される場合)。

  
**戻り値**: HTTP 操作に使用される HTTP 委任
  
### <a name="sethttpdelegate"></a>SetHttpDelegate
クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。

パラメーター:  
* **httpDelegate**: クライアント アプリケーションによって実装される HTTP コールバック インターフェイス


  
### <a name="optouttelemetry"></a>OptOutTelemetry
テレメトリの収集をすべて無効にします。
  
### <a name="istelemetryoptedout"></a>IsTelemetryOptedOut
テレメトリの収集を無効にする必要があるかどうかを取得します。

  
**戻り値**: テレメトリの収集を無効にする必要があるかどうか
  
### <a name="setminimumloglevel"></a>SetMinimumLogLevel
ログ イベントをトリガーする最小のログ レベルを設定します。

パラメーター:  
* **logLevel**: ログ イベントをトリガーする最小のログ レベル。 



  
**戻り値**: True
  
### <a name="loglevel"></a>ログ レベル
最小のログ レベル オブジェクトを取得します。

  
**戻り値**: ログ イベントをトリガーする最小のログ レベル。