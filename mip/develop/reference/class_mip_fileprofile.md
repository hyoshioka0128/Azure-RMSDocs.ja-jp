# <a name="class-mipfileprofile"></a>class mip::FileProfile 
[FileProfile](class_mip_fileprofile.md) クラスは、Microsoft Information Protection 操作を使用するためのルート クラスです。
一般的なアプリケーションでは[プロファイル](class_mip_profile.md)は 1 つしか必要ありませんが、必要に応じて複数のプロファイルを作成できます。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  プロファイル設定を返します。
public void ListEnginesAsync(const std::shared_ptr<void>& context)  |  エンジンの一覧操作を開始します。
public void UnloadEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  指定した ID を持つファイル エンジンのアンロードを開始します。
public void AddEngineAsync(const FileEngine::Settings& settings, const std::shared_ptr<void>& context)  |  プロファイルへの新しいファイル エンジンの追加を開始します。
public void DeleteEngineAsync(const std::string& id, const std::shared_ptr<void>& context)  |  指定した ID を持つファイル エンジンの削除を開始します。特定のプロファイルのすべてのデータが完全に削除されます。
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
プロファイル設定を返します。
  
### <a name="listenginesasync"></a>ListEnginesAsync
エンジンの一覧操作を開始します。
[FileProfile::Observer](class_mip_fileprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="unloadengineasync"></a>UnloadEngineAsync
指定した ID を持つファイル エンジンのアンロードを開始します。[FileProfile::Observer](class_mip_fileprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="addengineasync"></a>AddEngineAsync
プロファイルへの新しいファイル エンジンの追加を開始します。
[FileProfile::Observer](class_mip_fileprofile_observer.md) は成功または失敗時に呼び出されます。
  
### <a name="deleteengineasync"></a>DeleteEngineAsync
指定した ID を持つファイル エンジンの削除を開始します。特定のプロファイルのすべてのデータが完全に削除されます。
[FileProfile::Observer](class_mip_fileprofile_observer.md) は成功または失敗時に呼び出されます。