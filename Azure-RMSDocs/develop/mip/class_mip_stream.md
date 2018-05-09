# <a name="class-mipstream"></a>class mip::Stream 
mip sdk とストリーム ベースのコンテンツの間のインターフェイスを定義するクラス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public int64_t Read(uint8_t* buffer, int64_t bufferLength)  |  ストリームからバッファーに読み取ります。
public int64_t Write(const uint8_t* buffer, int64_t bufferLength)  |  バッファーからストリームを書き出します。
public bool Flush()  |  ストリームをフラッシュします。
public void Seek(uint64_t position)  |  ストリーム内の特定の位置をシークします。
public bool CanRead() const  |  ストリームが読み取り可能かどうかを確認します。
public bool CanWrite() const  |  ストリームが書き出し可能かどうかを確認します。
public uint64_t Position()  |  ストリーム内の現在の位置を取得します。
public uint64_t Size()  |  ストリーム内のコンテンツのサイズを取得します。
public void Size(uint64_t value)  |  ストリームのサイズを設定します。
public std::shared_ptr<Stream> Clone()  |  ストリームを複製します。
  
## <a name="members"></a>メンバー
  
### <a name="read"></a>読み取り
ストリームからバッファーに読み取ります。
  
#### <a name="parameters"></a>パラメーター
* buffer: バッファーへのポインター 
* bufferLength: バッファー サイズ。 
  
#### <a name="returns"></a>戻り値
実際に読み取られたバイト数。
  
### <a name="write"></a>書き込み
バッファーからストリームを書き出します。
  
#### <a name="parameters"></a>パラメーター
* buffer: バッファーへのポインター 
* bufferLength: バッファー サイズ。 
  
#### <a name="returns"></a>戻り値
実際に読み取られたバイト数。
  
### <a name="flush"></a>フラッシュ
ストリームをフラッシュします。
  
#### <a name="returns"></a>戻り値
正常終了した場合は true、それ以外の場合は false。
  
### <a name="seek"></a>Seek
ストリーム内の特定の位置をシークします。
  
#### <a name="parameters"></a>パラメーター
* ストリームをシークする位置。
  
### <a name="canread"></a>CanRead
ストリームが読み取り可能かどうかを確認します。
  
#### <a name="returns"></a>戻り値
読み取り可能な場合は true、それ以外の場合は false。
  
### <a name="canwrite"></a>CanWrite
ストリームが書き出し可能かどうかを確認します。
  
#### <a name="returns"></a>戻り値
書き出し可能な場合は true、それ以外の場合は false。
  
### <a name="position"></a>位置
ストリーム内の現在の位置を取得します。
  
#### <a name="returns"></a>戻り値
ストリーム内の位置。
  
### <a name="size"></a>Size
ストリーム内のコンテンツのサイズを取得します。
  
#### <a name="returns"></a>戻り値
ストリームのサイズ。
  
### <a name="size"></a>Size
ストリームのサイズを設定します。
  
#### <a name="parameters"></a>パラメーター
* ストリームのサイズ。
  
### <a name="stream"></a>ストリーム
ストリームを複製します。
  
#### <a name="returns"></a>戻り値
新しいストリーム。