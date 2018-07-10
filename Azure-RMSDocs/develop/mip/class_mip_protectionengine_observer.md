# <a name="class-mipprotectionengineobserver"></a>class mip::ProtectionEngine::Observer 
[ProtectionEngine](class_mip_protectionengine.md) に関連する通知を受け取るインターフェイス。
このインターフェイスは、保護 SDK を使用してアプリケーションによって実装する必要があります
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public virtual void OnGetTemplatesSuccess(const std::shared_ptr<std::vector<std::string>>& templateIds, const std::shared_ptr<void>& context)  |  テンプレートが正しく取得されると呼び出されます。
public virtual void OnGetTemplatesFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  テンプレートの取得でエラーが発生すると呼び出されます。
  
## <a name="members"></a>メンバー
  
### <a name="ongettemplatessuccess"></a>OnGetTemplatesSuccess
テンプレートが正しく取得されると呼び出されます。

パラメーター:  
* **templateIds**: 取得したテンプレートのリストへの参照 


* **context**: [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync) に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function など) を [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync) に渡すことができ、その同じコンテキストがそのまま [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) または [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure) に転送されます
  
### <a name="ongettemplatesfailure"></a>OnGetTemplatesFailure
テンプレートの取得でエラーが発生すると呼び出されます。

パラメーター:  
* **error**: テンプレートの取得中に発生した[エラー](class_mip_error.md) 


* **context**: [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync) に渡されたものと同じコンテキスト


アプリケーションは、任意の種類のコンテキスト (例: std::promise、std::function など) を [ProtectionEngine::GetTemplatesAsync](class_mip_protectionengine.md#gettemplatesasync) に渡すことができ、その同じコンテキストがそのまま [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) または [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure) に転送されます