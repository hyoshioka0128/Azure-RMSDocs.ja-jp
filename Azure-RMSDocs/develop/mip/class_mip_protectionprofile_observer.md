# <a name="class-mipprotectionprofileobserver"></a>class mip::ProtectionProfile::Observer 
[ProtectionProfile](#classmip_1_1_protection_profile) に関連する通知を受け取るインターフェイス。
このインターフェイスは、保護 SDK を使用してアプリケーションによって実装する必要があります
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public inline virtual void OnLoadSuccess(const std::shared_ptr<ProtectionProfile>& profile, const std::shared_ptr<void>& context)  |  プロファイルが正常に読み込まれたときに呼び出されます。
public inline virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  プロファイルの読み込みでエラーが発生したときに呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="onloadsuccess"></a>OnLoadSuccess
プロファイルが正常に読み込まれたときに呼び出されます。
  
#### <a name="parameters"></a>パラメーター
* profile: 新たに作成された [ProtectionProfile](#classmip_1_1_protection_profile) への参照
* context: [ProtectionProfile::LoadAsync](#classmip_1_1_protection_profile_1aeb141706dc10935931841fdb82d11031) に渡されたのと同じコンテキスト。アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function など) を [ProtectionProfile::LoadAsync](#classmip_1_1_protection_profile_1aeb141706dc10935931841fdb82d11031) に渡すことができ、その同じコンテキストがそのまま [ProtectionProfile::Observer::OnLoadSuccess](#classmip_1_1_protection_profile_1_1_observer_1a31e73965ffb0bd152b3954b013faa773) または [ProtectionProfile::Observer::OnLoadFailure](#classmip_1_1_protection_profile_1_1_observer_1acdad73bb6a2dcc93295e0e16e422f291) に転送されます
  
### <a name="onloadfailure"></a>OnLoadFailure
プロファイルの読み込みでエラーが発生したときに呼び出されます。
  
#### <a name="parameters"></a>パラメーター
* error: 読み込み中に発生した[エラー](#classmip_1_1_error) 
* context: [ProtectionProfile::LoadAsync](#classmip_1_1_protection_profile_1aeb141706dc10935931841fdb82d11031) に渡されたのと同じコンテキスト。アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function など) を [ProtectionProfile::LoadAsync](#classmip_1_1_protection_profile_1aeb141706dc10935931841fdb82d11031) に渡すことができ、その同じコンテキストがそのまま [ProtectionProfile::Observer::OnLoadSuccess](#classmip_1_1_protection_profile_1_1_observer_1a31e73965ffb0bd152b3954b013faa773) または [ProtectionProfile::Observer::OnLoadFailure](#classmip_1_1_protection_profile_1_1_observer_1acdad73bb6a2dcc93295e0e16e422f291) に転送されます