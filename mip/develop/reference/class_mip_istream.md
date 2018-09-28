# <a name="class-mipistream"></a>class mip::IStream 
保護されたストリーム用の基底インターフェイス。
Windows::Storage::Streams::IRandomAccessStream::IRandomAccessStream および Windows::Storage::Streams::FileRandomAccessStream::FileRandomAccessStream から移植されました。 [https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.irandomaccessstream.aspx](https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.irandomaccessstream.aspx)[https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.filerandomaccessstream.aspx](https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.filerandomaccessstream.aspx)
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public std::shared_future<int64_t> ReadAsync(uint8_t* pbBuffer, int64_t cbBuffer, int64_t cbOffset, std::launch launchType)  |  ストリームからデータのブロックを非同期的に読み取ります。
public std::shared_future<int64_t> WriteAsync(const uint8_t* cpbBuffer, int64_t cbBuffer, int64_t cbOffset, std::launch launchType)  |  ストリームにデータのブロックを非同期的に書き込みます。
public std::future<bool> FlushAsync(std::launch launchType)  |  出力ストリーム バッファーを非同期的にフラッシュします。
 public int64_t Read(uint8_t* pbBuffer, int64_t cbBuffer)  |  ストリームからデータのブロックを同期的に読み取ります。
 public int64_t Write(const uint8_t* cpbBuffer, int64_t cbBuffer)  |  ストリームにデータのブロックを同期的に書き込みます。
 public bool Flush()  |  出力ストリーム バッファーを同期的にフラッシュします。
 public SharedStream Clone()  |  ストリームを複製します。
 public void Seek(uint64_t u64Position)  |  ストリーム内の位置をシークします。
 public bool CanRead() const  |  ストリームを読み取ることができるかどうかを取得します。
 public bool CanWrite() const  |  ストリームを書き出すことができるかどうかを取得します。
 public uint64_t Position()  |  先頭からのストリームの現在位置を取得します (バイト単位)
 public uint64_t Size()  |  ストリームのサイズを取得します (バイト単位)
 public void Size(uint64_t u64Value)  |  ストリームのサイズを設定します (バイト単位)
public virtual std::vector<uint8_t> Read(uint64_t u64size)  |  ストリームからデータのブロックを同期的に読み取ります。
  
## <a name="members"></a>メンバー
  
### <a name="readasync"></a>ReadAsync
ストリームからデータのブロックを非同期的に読み取ります。

パラメーター:  
* **pbBuffer**: ストリームの読み取り先バッファー 


* **cbBuffer**: バッファーのサイズ 


* **cbOffset**: 入力ストリームの先頭からの読み取り開始位置のオフセット 


* **launchType**: 非同期起動の種類



  
**戻り値**: 読み取る実際のバイト数を含む非同期の未来。結果が std::future から取得されるまでバッファーが存在することを確認します
  
### <a name="writeasync"></a>WriteAsync
ストリームにデータのブロックを非同期的に書き込みます。

パラメーター:  
* **cpbBuffer**: 書き込むデータのバッファー 


* **cbBuffer**: バッファーのサイズ 


* **cbOffset**: 出力ストリームの先頭からの書き込み開始位置のオフセット 


* **launchType**: 非同期起動の種類



  
**戻り値**: 書き込む実際のバイト数を含む非同期の未来。結果が std::future から取得されるまでバッファーが存在することを確認します
  
### <a name="flushasync"></a>FlushAsync
出力ストリーム バッファーを非同期的にフラッシュします。

パラメーター:  
* **launchType**: 非同期起動の種類



  
**戻り値**: フラッシュが成功したかどうかを含む非同期の未来
  
### <a name="read"></a>読み取り
ストリームからデータのブロックを同期的に読み取ります。

パラメーター:  
* **pbBuffer**: ストリームの読み取り先バッファー 


* **cbBuffer**: バッファーのサイズ



  
**戻り値**: 読み取った実際のバイト数
  
### <a name="write"></a>書き込み
ストリームにデータのブロックを同期的に書き込みます。

パラメーター:  
* **cpbBuffer**: 書き込むデータのバッファー 


* **cbBuffer**: バッファーのサイズ



  
**戻り値**: 書き込んだ実際のバイト数
  
### <a name="flush"></a>フラッシュ
出力ストリーム バッファーを同期的にフラッシュします。

  
**戻り値**: フラッシュが成功したかどうか
  
### <a name="sharedstream"></a>SharedStream
ストリームを複製します。

  
**戻り値**: 複製されたストリーム
  
### <a name="seek"></a>Seek
ストリーム内の位置をシークします。

パラメーター:  
* **u64Position**: ストリームの先頭からのバイト オフセット


  
### <a name="canread"></a>CanRead
ストリームを読み取ることができるかどうかを取得します。

  
**戻り値**: ストリームを読み取ることができるかどうか
  
### <a name="canwrite"></a>CanWrite
ストリームを書き出すことができるかどうかを取得します。

  
**戻り値**: ストリームを書き出すことができるかどうか
  
### <a name="position"></a>位置
先頭からのストリームの現在位置を取得します (バイト単位)

  
**戻り値**: 先頭からのストリームの現在位置 (バイト単位)
  
### <a name="size"></a>Size
ストリームのサイズを取得します (バイト単位)

  
**戻り値**: ストリームのサイズ (バイト単位)
  
### <a name="size"></a>Size
ストリームのサイズを設定します (バイト単位)

パラメーター:  
* **u64Value**: ストリームのサイズ (バイト単位)


  
### <a name="read"></a>読み取り
ストリームからデータのブロックを同期的に読み取ります。

パラメーター:  
* **u64size**: 読み取るデータのサイズ (バイト単位)



  
**戻り値**: 実際の読み取りデータのベクター