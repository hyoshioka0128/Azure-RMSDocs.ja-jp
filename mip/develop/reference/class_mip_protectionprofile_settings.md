---
title: class mip::ProtectionProfile::Settings
description: Mip::protectionprofile クラスの Microsoft Information Protection (MIP) SDK について説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: mbaldwin
ms.date: 01/28/2019
ms.openlocfilehash: 5e609cfbc7cbb705dafbee239726c0cfd15cc38a
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57331870"
---
# <a name="class-mipprotectionprofilesettings"></a>class mip::ProtectionProfile::Settings 
作成時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される[設定](class_mip_protectionprofile_settings.md)。
  
## <a name="summary"></a>まとめ
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
パブリック設定 (const std::string & パス、bool useinmemorystorage: const std::shared_ptr\<authdelegate:\>& authdelegate:、const std::shared_ptr\<ConsentDelegate\>& consentDelegate、const std::shared_ptr\<protectionprofile::observer\>& observer, const ApplicationInfo & applicationInfo)  |  非同期操作に使用されるオブザーバーを指定する [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) コンストラクター。
パブリック設定 (const std::string & パス、bool useinmemorystorage: const std::shared_ptr\<authdelegate:\>& authdelegate:、const std::shared_ptr\<ConsentDelegate\>& consentDelegate、const ApplicationInfo & applicationInfo)  |  同期操作に使用される、[ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) コンストラクター。
public const std::string& GetPath() const  |  ログ、テレメトリ、その他の保護関連資料が格納されるファイル パスを取得します。
public bool GetUseInMemoryStorage() const  |  キャッシュが (ディスク上ではなく) メモリにのみ格納されているかどうかを取得します
public std::shared_ptr\<AuthDelegate\> GetAuthDelegate() const  |  認証トークンを取得するために使用する認証委任を取得します。
public std::shared_ptr\<ConsentDelegate\> GetConsentDelegate() const  |  サービスに接続するために使用する同意委任を取得します。
public std::shared_ptr\<ProtectionProfile::Observer\> GetObserver() const  |  [ProtectionProfile](class_mip_protectionprofile.md) に関連するイベントの通知を受信するオブザーバーを取得します。
public const ApplicationInfo& GetApplicationInfo() const  |  保護 SDK を利用しているアプリケーションに関する情報を取得します。
public void OptOutTelemetry()  |  テレメトリの収集をすべて無効にします。
public bool IsTelemetryOptedOut() const  |  テレメトリの収集を無効にする必要があるかどうかを取得します。
public std::shared_ptr\<LoggerDelegate\> GetLoggerDelegate() const  |  アプリケーションによって提供されるロガー委任を取得します (提供される場合)。
public void SetLoggerDelegate(const std::shared_ptr\<LoggerDelegate\>& loggerDelegate)  |  既定のロガーをオーバーライドします。
public std::shared_ptr\<HttpDelegate\> GetHttpDelegate() const  |  アプリケーションによって提供される HTTP 委任が取得されます (提供される場合)。
public void SetHttpDelegate (const std::shared_ptr\<HttpDelegate\>& httpDelegate)  |  クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。
public bool GetSkipTelemetryInit() const  |  テレメトリ初期化をスキップする必要があるかどうかを取得します。
public void SetSkipTelemetryInit()  |  テレメトリ初期化を無効にします。
public void SetNewFeaturesDisabled()  |  新機能を無効にします。
public bool AreNewFeaturesDisabled() const  |  新機能が無効になっているかどうかを取得します。
public void SetSessionId(const std::string& sessionId)  |  セッション ID を設定します。
public const std::string& GetSessionId() const  |  セッション ID を取得します。
public void SetMinimumLogLevel(LogLevel logLevel)  |  ログ イベントをトリガーする最小のログ レベルを設定します。
public LogLevel GetMinimumLogLevel() const  |  最小のログ レベル オブジェクトを取得します。
  
## <a name="members"></a>メンバー
  
### <a name="settings-function"></a>ポリシーの設定
非同期操作に使用されるオブザーバーを指定する [ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) コンストラクター。

パラメーター:  
* **パス**:ログ、テレメトリ、およびその他のファイル パス保護関連資料が格納されています。 


* **useInMemoryStorage**:ディスクではなくメモリにキャッシュされた状態を保存します。 


* **authDelegate**:クライアント アプリケーションによって実装される認証に使用するコールバック オブジェクト 


* **オブザーバー**:[オブザーバー](class_mip_protectionprofile_observer.md)イベントの通知を受信するインスタンスに関連する[ProtectionProfile](class_mip_protectionprofile.md)


* **applicationInfo**:保護 SDK を利用するアプリケーションに関する情報


  
### <a name="settings-function"></a>ポリシーの設定
同期操作に使用される、[ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) コンストラクター。

パラメーター:  
* **パス**:ログ、テレメトリ、およびその他のファイル パス保護関連資料が格納されています。 


* **useInMemoryStorage**:ディスクではなくメモリにキャッシュされた状態を保存します。 


* **authDelegate**:クライアント アプリケーションによって実装される認証に使用するコールバック オブジェクト 


* **applicationInfo**:保護 SDK を利用しているアプリケーションに関する情報


  
### <a name="getpath-function"></a>GetPath 関数
ログ、テレメトリ、その他の保護関連資料が格納されるファイル パスを取得します。

  
**返します**:ログ、テレメトリ、その他の保護関連資料が格納されるパス
  
### <a name="getuseinmemorystorage-function"></a>GetUseInMemoryStorage 関数
キャッシュが (ディスク上ではなく) メモリにのみ格納されているかどうかを取得します

  
**返します**:キャッシュがメモリにのみ格納されている場合は true。
  
### <a name="getauthdelegate-function"></a>GetAuthDelegate 関数
認証トークンを取得するために使用する認証委任を取得します。

  
**返します**:認証トークンを取得するために使用される認証委任
  
### <a name="getconsentdelegate-function"></a>GetConsentDelegate 関数
サービスに接続するために使用する同意委任を取得します。

  
**返します**:サービスに接続するために使用されるデリゲートを同意します。
  
### <a name="getobserver-function"></a>GetObserver 関数
[ProtectionProfile](class_mip_protectionprofile.md) に関連するイベントの通知を受信するオブザーバーを取得します。

  
**返します**:[オブザーバー](class_mip_protectionprofile_observer.md)に関連するイベントの通知を受け取る[ProtectionProfile](class_mip_protectionprofile.md)
  
### <a name="getapplicationinfo-function"></a>GetApplicationInfo 関数
保護 SDK を利用しているアプリケーションに関する情報を取得します。

  
**返します**:保護 SDK を利用するアプリケーションに関する情報
  
### <a name="optouttelemetry-function"></a>OptOutTelemetry 関数
テレメトリの収集をすべて無効にします。
  
### <a name="istelemetryoptedout-function"></a>IsTelemetryOptedOut 関数
テレメトリの収集を無効にする必要があるかどうかを取得します。

  
**返します**:かどうか、テレメトリの収集を無効にする場合
  
### <a name="getloggerdelegate-function"></a>GetLoggerDelegate 関数
アプリケーションによって提供されるロガー委任を取得します (提供される場合)。

  
**返します**:ロガー
  
### <a name="setloggerdelegate-function"></a>SetLoggerDelegate 関数
既定のロガーをオーバーライドします。

パラメーター:  
* **loggerDelegate**:クライアント アプリケーションによって実装されるコールバック インターフェイスをログ記録


このメソッドは、独自のロガー実装を使用するクライアント アプリケーションによって呼び出される必要があります
  
### <a name="gethttpdelegate-function"></a>GetHttpDelegate 関数
アプリケーションによって提供される HTTP 委任が取得されます (提供される場合)。

  
**返します**:HTTP 操作に使用する HTTP デリゲート
  
### <a name="sethttpdelegate-function"></a>SetHttpDelegate 関数
クライアント自体のスタックで既定の HTTP スタックをオーバーライドします。

パラメーター:  
* **httpDelegate**:クライアント アプリケーションによって実装される HTTP コールバック インターフェイス


  
### <a name="getskiptelemetryinit-function"></a>GetSkipTelemetryInit 関数
テレメトリ初期化をスキップする必要があるかどうかを取得します。

  
**返します**:場合か、テレメトリ初期化をスキップする必要があります。
  
### <a name="setskiptelemetryinit-function"></a>SetSkipTelemetryInit 関数
テレメトリ初期化を無効にします。
このメソッドは、通常、クライアント アプリケーションによっては呼び出されず、初期化の重複を防ぐためにファイル SDK によって使用されます
  
### <a name="setnewfeaturesdisabled-function"></a>SetNewFeaturesDisabled 関数
新機能を無効にします。
新機能を試さないアプリケーションの場合
  
### <a name="arenewfeaturesdisabled-function"></a>AreNewFeaturesDisabled 関数
新機能が無効になっているかどうかを取得します。

  
**返します**:かどうかの新機能が無効な場合
  
### <a name="setsessionid-function"></a>SetSessionId 関数
セッション ID を設定します。

パラメーター:  
* **sessionId**:ログ/テレメトリを関連付けるために使用されるセッション ID


  
### <a name="getsessionid-function"></a>GetSessionId 関数
セッション ID を取得します。

  
**返します**:ログ/テレメトリを関連付けるために使用されるセッション ID
  
### <a name="setminimumloglevel-function"></a>SetMinimumLogLevel 関数
ログ イベントをトリガーする最小のログ レベルを設定します。

パラメーター:  
* **logLevel**: ログ イベントをトリガーする最小のログ レベル。 



  
**返します**:True
  
### <a name="getminimumloglevel-function"></a>GetMinimumLogLevel 関数
最小のログ レベル オブジェクトを取得します。

  
**返します**:ログ イベントをトリガーするための最小ログ レベル。
