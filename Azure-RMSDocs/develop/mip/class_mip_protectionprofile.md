# <a name="class-mipprotectionprofile"></a>class mip::ProtectionProfile 
[ProtectionProfile](class_mip_protectionprofile.md) は、保護操作を実行するためのルート クラスです。
アプリケーションでは、保護操作を実行する前に [ProtectionProfile](class_mip_protectionprofile.md) を作成する必要があります
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public const Settings& GetSettings() const  |  初期化時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される設定を取得します。
 public void ClearCaches()  |  キャッシュを削除します (例: 同意データベースなど)
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
初期化時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される設定を取得します。

  
**戻り値**: 初期化時および有効期間全体にわたって [ProtectionProfile](class_mip_protectionprofile.md) によって使用される [Settings](class_mip_protectionprofile_settings.md)
  
### <a name="clearcaches"></a>ClearCaches
キャッシュを削除します (例: 同意データベースなど)デバッグまたはテストに役立ちます