# <a name="class-mipprotectionengine"></a>class mip::ProtectionEngine 
特定の ID に関連した、保護に関連するアクションを実行します。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  エンジンの設定を取得します。
public void GetTemplatesAsync(const std::shared_ptr<ProtectionEngine::Observer>& observer, const std::shared_ptr<void>& context)  |  ユーザーが利用できるテンプレートのコレクションを取得します。
public void CreateProtectionHandlerFromDescriptorAsync(const std::shared_ptr<ProtectionDescriptor>& descriptor, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。
public void CreateProtectionHandlerFromPublishingLicenseAsync(const std::vector<uint8_t>& serializedPublishingLicense, const ProtectionHandlerCreationOptions& options, const std::shared_ptr<ProtectionHandler::Observer>& observer, const std::shared_ptr<void>& context)  |  シリアル化された形式から保護ハンドラーを作成します。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
エンジンの設定を取得します。

  
**戻り値**: エンジンの設定
  
### <a name="gettemplatesasync"></a>GetTemplatesAsync
ユーザーが利用できるテンプレートのコレクションを取得します。

パラメーター:  
* **observer**: [ProtectionEngine::Observer](class_mip_protectionengine_observer.md) インターフェイスを実装するクラス 


* **context**: 同じコンテキストが [ProtectionEngine::Observer::OnGetTemplatesSuccess](class_mip_protectionengine_observer.md#ongettemplatessuccess) または [ProtectionEngine::Observer::OnGetTemplatesFailure](class_mip_protectionengine_observer.md#ongettemplatesfailure) に転送されます


  
### <a name="createprotectionhandlerfromdescriptorasync"></a>CreateProtectionHandlerFromDescriptorAsync
権限/ロールが特定のユーザーに割り当てられる保護ハンドラーを作成します。

パラメーター:  
* **descriptor**: 保護構成を記述する [ProtectionDescriptor](class_mip_protectiondescriptor.md) 


* **options**: 作成オプション 


* **observer**: [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) インターフェイスを実装するクラス 


* **context**: 同じコンテキストが [ProtectionHandler::Observer::OnCreateProtectionHandlerSuccess](class_mip_protectionhandler_observer.md#oncreateprotectionhandlersuccess) または ProtectionHandler::Observer::OnCreateProtectionHandlerFailure に転送されます


  
### <a name="createprotectionhandlerfrompublishinglicenseasync"></a>CreateProtectionHandlerFromPublishingLicenseAsync
シリアル化された形式から保護ハンドラーを作成します。

パラメーター:  
* **serializedPublishingLicense**: シリアル化された発行ライセンス 


* **options**: 作成オプション 


* **observer**: [ProtectionHandler::Observer](class_mip_protectionhandler_observer.md) インターフェイスを実装するクラス 


* **context**: 同じコンテキストが [ProtectionHandler::Observer::OnCreateProtectionHandlerSuccess](class_mip_protectionhandler_observer.md#oncreateprotectionhandlersuccess) または ProtectionHandler::Observer::OnCreateProtectionHandlerFailure に転送されます

