# <a name="class-mipprotectionprofileobserver"></a>class mip::ProtectionProfile::Observer 
[ProtectionProfile](class_mip_protectionprofile.md) に関連する通知を受け取るインターフェイス。
このインターフェイスは、保護 SDK を使用してアプリケーションによって実装する必要があります
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual void OnLoadSuccess(const std::shared_ptr<ProtectionProfile>& profile, const std::shared_ptr<void>& context)  |  プロファイルが正常に読み込まれたときに呼び出されます。
public virtual void OnLoadFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  プロファイルの読み込みでエラーが発生したときに呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="onloadsuccess"></a>OnLoadSuccess
プロファイルが正常に読み込まれたときに呼び出されます。

パラメーター:  
* **profile**: 新たに作成された [ProtectionProfile](class_mip_protectionprofile.md) への参照


* **context**: [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#loadasync) に渡されたものと同じコンテキスト。


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function など) を [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#loadasync) に渡すことができ、その同じコンテキストがそのまま [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) または [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure) に転送されます
  
### <a name="onloadfailure"></a>OnLoadFailure
プロファイルの読み込みでエラーが発生したときに呼び出されます。

パラメーター:  
* **error**: 読み込み中に発生した [Error](class_mip_error.md) 


* **context**: [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#loadasync) に渡されたものと同じコンテキスト。


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function など) を [ProtectionProfile::LoadAsync](class_mip_protectionprofile.md#loadasync) に渡すことができ、その同じコンテキストがそのまま [ProtectionProfile::Observer::OnLoadSuccess](class_mip_protectionprofile_observer.md#onloadsuccess) または [ProtectionProfile::Observer::OnLoadFailure](class_mip_protectionprofile_observer.md#onloadfailure) に転送されます