# <a name="class-mipprotectionhandler"></a>class mip::ProtectionHandler 
特定の保護構成 (つまりユーザー、権限、ロールなど) に向けた、保護に関連するアクションを実行します。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::shared_ptr<Stream> CreateProtectedStream(const std::shared_ptr<Stream>& backingStream, uint64_t contentStartPosition, uint64_t contentSize)  |  コンテンツの暗号化/解読を可能にする、保護されたストリームを作成します。
 public int64_t EncryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  バッファーを暗号化します。
 public int64_t DecryptBuffer(int64_t offsetFromStart, const uint8_t* inputBuffer, int64_t inputBufferSize, uint8_t* outputBuffer, int64_t outputBufferSize, bool isFinal)  |  バッファーを暗号化解除します。
 public uint64_t GetProtectedContentLength(uint64_t size)  |  この [ProtectionHandler](class_mip_protectionhandler.md) を使用して暗号化される場合は、コンテンツのサイズ (バイト) を計算します。
 public uint64_t GetBlockSize()  |  この [ProtectionHandler](class_mip_protectionhandler.md) で使用される暗号モードのブロック サイズ (バイト) を取得します。
 public bool AccessCheck(const std::string& right) const  |  保護ハンドラーが指定された権限へのアクセス権をユーザーに付与するかどうかを確認します。
 public const std::string GetIssuedTo()  |  保護ハンドラーに関連付けられているユーザーを取得します。
 public const std::string GetOwner()  |  コンテンツ所有者のメール アドレスを取得します。
 public bool IsIssuedToOwner()  |  現在のユーザーがコンテンツの所有者かどうかを取得します。
public std::shared_ptr<ProtectionDescriptor> GetProtectionDescriptor()  |  保護の詳細を取得します。
 public const std::string GetContentId()  |  ドキュメント/コンテンツの一意識別子を取得します。
 public bool DoesUseDeprecatedAlgorithms()  |  保護ハンドラーで、下位互換性を実現するために非推奨の暗号アルゴリズム (ECB) を使用するかどうかを取得します。
 public bool IsAuditedExtractAllowed()  |  保護ハンドラーがユーザーに '監査済み抽出' 権限を付与するかどうかを取得します。
public const std::vector<uint8_t> GetSerializedPublishingLicense()  |  [ProtectionHandler](class_mip_protectionhandler.md) を発行ライセンス (PL) にシリアル化します
  
## <a name="members"></a>メンバー
  
### <a name="stream"></a>ストリーム
コンテンツの暗号化/解読を可能にする、保護されたストリームを作成します。

パラメーター:  
* **backingStream**: 読み取り/書き込みを行うバッキング ストリーム 


* **contentStartPosition**: 保護されたコンテンツが始まる、バッキング ストリーム内の開始位置 (バイト) 


* **contentSize**: バッキング ストリーム内の保護されたコンテンツのサイズ (バイト)



  
**戻り値**: 保護されたストリーム
  
### <a name="encryptbuffer"></a>EncryptBuffer
バッファーを暗号化します。

パラメーター:  
* **offsetFromStart**: クリア テキスト コンテンツの先頭からの、inputBuffer の相対位置 


* **inputBuffer**: 暗号化されるクリア テキスト コンテンツのバッファー 


* **inputBufferSize**: 入力バッファーのサイズ (バイト) 


* **outputBuffer**: 暗号化されたコンテンツがコピーされるバッファー 


* **outputBufferSize**: 出力バッファーのサイズ (バイト) 


* **isFinal**: 入力バッファーがクリア テキストの最終バイトを含んでいるかどうか



  
**戻り値**: 暗号化されたコンテンツの実際のサイズ (バイト)
  
### <a name="decryptbuffer"></a>DecryptBuffer
バッファーを暗号化解除します。

パラメーター:  
* **offsetFromStart**: 暗号化されたコンテンツの先頭からの、inputBuffer の相対位置 


* **inputBuffer**: 暗号化解除する、暗号化されたコンテンツのバッファー 


* **inputBufferSize**: 入力バッファーのサイズ (バイト) 


* **outputBuffer**: 暗号化解除されたコンテンツがコピーされるバッファー 


* **outputBufferSize**: 出力バッファーのサイズ (バイト) 


* **isFinal**: 入力バッファーが暗号化された最終バイトを含んでいるかどうか



  
**戻り値**: 暗号化解除されたコンテンツの実際のサイズ (バイト)
  
### <a name="getprotectedcontentlength"></a>GetProtectedContentLength
この [ProtectionHandler](class_mip_protectionhandler.md) を使用して暗号化される場合は、コンテンツのサイズ (バイト) を計算します。

パラメーター:  
* **contentLength**: 保護されないコンテンツのサイズ (バイト)



  
**戻り値**: 保護されたコンテンツのサイズ (バイト)
  
### <a name="getblocksize"></a>GetBlockSize
この [ProtectionHandler](class_mip_protectionhandler.md) で使用される暗号モードのブロック サイズ (バイト) を取得します。

  
**戻り値**: ブロック サイズ (バイト)
  
### <a name="accesscheck"></a>AccessCheck
保護ハンドラーが指定された権限へのアクセス権をユーザーに付与するかどうかを確認します。

パラメーター:  
* **right**: 確認する権限



  
**戻り値**: 保護ハンドラーが指定された権限へのアクセス権をユーザーに付与するかどうか
  
### <a name="getissuedto"></a>GetIssuedTo
保護ハンドラーに関連付けられているユーザーを取得します。

  
**戻り値**: 保護ハンドラーに関連付けられているユーザー
  
### <a name="getowner"></a>GetOwner
コンテンツ所有者のメール アドレスを取得します。

  
**戻り値**: コンテンツ所有者のメール アドレス
  
### <a name="isissuedtoowner"></a>IsIssuedToOwner
現在のユーザーがコンテンツの所有者かどうかを取得します。

  
**戻り値**: 現在のユーザーがコンテンツの所有者かどうか
  
### <a name="protectiondescriptor"></a>ProtectionDescriptor
保護の詳細を取得します。

  
**戻り値**: 保護の詳細
  
### <a name="getcontentid"></a>GetContentId
ドキュメント/コンテンツの一意識別子を取得します。

  
**戻り値**: 一意のコンテンツ識別子
  
### <a name="doesusedeprecatedalgorithms"></a>DoesUseDeprecatedAlgorithms
保護ハンドラーで、下位互換性を実現するために非推奨の暗号アルゴリズム (ECB) を使用するかどうかを取得します。

  
**戻り値**: 保護ハンドラーで非推奨の暗号アルゴリズムを使用するかどうか
  
### <a name="isauditedextractallowed"></a>IsAuditedExtractAllowed
保護ハンドラーがユーザーに '監査済み抽出' 権限を付与するかどうかを取得します。

  
**戻り値**: 保護ハンドラーがユーザーに '監査済み抽出' 権限を付与するかどうか
  
### <a name="getserializedpublishinglicense"></a>GetSerializedPublishingLicense
[ProtectionHandler](class_mip_protectionhandler.md) を発行ライセンス (PL) にシリアル化します

  
**戻り値**: シリアル化された発行ライセンス