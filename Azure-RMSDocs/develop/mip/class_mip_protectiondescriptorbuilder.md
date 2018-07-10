# <a name="class-mipprotectiondescriptorbuilder"></a>class mip::ProtectionDescriptorBuilder 
保護されたコンテンツに関連付けられているアドホック ポリシーを表します。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public MIP_API std::shared_ptr<ProtectionDescriptor> Build()  |  この [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md) インスタンスによってアクセス許可が定義される [ProtectionDescriptor](class_mip_protectiondescriptor.md) を作成します。
 public void SetName(const std::string& value)  |  保護ポリシー名を設定します。
 public void SetDescription(const std::string& value)  |  保護ポリシーの説明を設定します。
public void SetContentValidUntil(const std::chrono::time_point<std::chrono::system_clock>& value)  |  保護ポリシーの有効期限を設定します。
 public void SetAllowOfflineAccess(bool value)  |  保護ポリシーがオフライン コンテンツへのアクセスを許可するかどうかを設定します。
 public void SetReferrer(const std::string& uri)  |  保護ポリシーの参照元のアドレスを設定します。
public void SetEncryptedAppData(const std::map<std::string, std::string>& value)  |  暗号化する必要のあるアプリ固有のデータを設定します。
public void SetSignedAppData(const std::map<std::string, std::string>& value)  |  署名する必要があるアプリ固有のデータを設定します。
 public virtual ~ProtectionDescriptorBuilder()  | _まだ文書化されていません。_
  
## <a name="members"></a>メンバー
  
### <a name="protectiondescriptor"></a>ProtectionDescriptor
この [ProtectionDescriptorBuilder](class_mip_protectiondescriptorbuilder.md) インスタンスによってアクセス許可が定義される [ProtectionDescriptor](class_mip_protectiondescriptor.md) を作成します。

  
**戻り値**: 新しい [ProtectionDescriptor](class_mip_protectiondescriptor.md) インスタンス
  
### <a name="setname"></a>SetName
保護ポリシー名を設定します。

パラメーター:  
* **value**: 保護ポリシー名


  
### <a name="setdescription"></a>SetDescription
保護ポリシーの説明を設定します。

パラメーター:  
* **value**: ポリシーの説明


  
### <a name="setcontentvaliduntil"></a>SetContentValidUntil
保護ポリシーの有効期限を設定します。

パラメーター:  
* **value**: ポリシーの有効期限


  
### <a name="setallowofflineaccess"></a>SetAllowOfflineAccess
保護ポリシーがオフライン コンテンツへのアクセスを許可するかどうかを設定します。

パラメーター:  
* **value**: ポリシーがオフライン コンテンツへのアクセスを許可するかどうか


  
### <a name="setreferrer"></a>SetReferrer
保護ポリシーの参照元のアドレスを設定します。

パラメーター:  
* **uri**: ポリシーの参照元のアドレス


参照元は、保護ポリシーの取得に失敗したときにユーザーが表示できる URI であり、ユーザーがコンテンツへのアクセス許可を取得する方法に関する情報が含まれます。
  
### <a name="setencryptedappdata"></a>SetEncryptedAppData
暗号化する必要のあるアプリ固有のデータを設定します。

パラメーター:  
* **value**: アプリ固有のデータ


アプリケーションでは、保護サービスによって暗号化されるアプリ固有のデータのディクショナリを指定できます。 この暗号化データは、SetSignedAppData によって設定される署名済みデータに依存しません。
  
### <a name="setsignedappdata"></a>SetSignedAppData
署名する必要があるアプリ固有のデータを設定します。

パラメーター:  
* **value**: アプリ固有のデータ


アプリケーションでは、保護サービスによって署名されるアプリ固有のデータのディクショナリを指定できます。 この署名済みデータは、SetEncryptedAppData によって設定される暗号化データに依存しません。
  
### <a name="protectiondescriptorbuilder"></a>~ProtectionDescriptorBuilder
_まだ文書化されていません。_
