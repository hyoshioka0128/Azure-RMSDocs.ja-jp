# <a name="class-mipprofile"></a>class mip::Profile 
[Profile](class_mip_profile.md) クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。 一般的なアプリケーションでは[プロファイル](class_mip_profile.md)は 1 つしか必要ありませんが、必要に応じて複数のプロファイルを作成できます。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  プロファイルに設定されている設定値を取得します。
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  エンジンの一覧操作を開始します。
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  指定した ID を持つポリシー エンジンのアンロードを開始します。
public void AddEngineAsync(const PolicyEngine::Settings& settings, const std::shared_ptr<void>& context)  |  プロファイルへの新しいポリシー エンジンの追加を開始します。
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  指定した ID を持つポリシー エンジンの削除を開始します。特定のプロファイルのすべてのデータが完全に削除されます。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
プロファイルに設定されている設定値を取得します。

  
**戻り値**: プロファイルに設定されている設定値。
  
### <a name="listenginesasync"></a>ListEnginesAsync
エンジンの一覧操作を開始します。

パラメーター:  
* **context**: オブザーバー関数に渡されるパラメーター。 


[Profile::Observer](class_mip_profile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="unloadengineasync"></a>UnloadEngineAsync
指定した ID を持つポリシー エンジンのアンロードを開始します。

パラメーター:  
* **id**: 一意のエンジン ID。 


* **context**: オブザーバー関数に渡されるパラメーター。 


[Profile::Observer](class_mip_profile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="addengineasync"></a>AddEngineAsync
プロファイルへの新しいポリシー エンジンの追加を開始します。

パラメーター:  
* **settings**: エンジン パラメーターを指定する [mip::PolicyEngine::Settings](class_mip_policyengine_settings.md) オブジェクト。 


* **context**: オブザーバー関数に渡されるパラメーター。 


[Profile::Observer](class_mip_profile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
指定した ID を持つポリシー エンジンの削除を開始します。特定のプロファイルのすべてのデータが完全に削除されます。

パラメーター:  
* **id**: 一意のエンジン ID。 


* **context**: オブザーバー関数に渡されるパラメーター。 


[Profile::Observer](class_mip_profile_observer.md) は成功または失敗時に呼び出されます。