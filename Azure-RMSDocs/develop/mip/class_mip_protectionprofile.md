# <a name="class-mipprotectionprofile"></a>class mip::ProtectionProfile 
[ProtectionProfile](#classmip_1_1_protection_profile) は、保護操作を実行するためのルート クラスです。
アプリケーションでは、保護操作を実行する前に [ProtectionProfile](#classmip_1_1_protection_profile) を作成する必要があります
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public const Settings& GetSettings() const  |  初期化時および有効期間全体にわたって [ProtectionProfile](#classmip_1_1_protection_profile) によって使用される設定を取得します。
public void ClearCaches()  |  キャッシュを削除します (例: 同意データベースなど)
  
## <a name="members"></a>メンバー
  
### <a name="settings"></a>Settings
初期化時および有効期間全体にわたって [ProtectionProfile](#classmip_1_1_protection_profile) によって使用される設定を取得します。
  
#### <a name="returns"></a>戻り値
初期化時および有効期間全体にわたって [ProtectionProfile](#classmip_1_1_protection_profile) によって使用される[設定](#classmip_1_1_protection_profile_1_1_settings)
  
### <a name="clearcaches"></a>ClearCaches
キャッシュを削除します (例: 同意データベースなど)デバッグまたはテストに役立ちます