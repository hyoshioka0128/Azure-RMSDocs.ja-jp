# <a name="class-mipstream"></a>class mip::Stream 
mip sdk とストリーム ベースのコンテンツの間のインターフェイスを定義するクラス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public int64_t Read(uint8_t* buffer, int64_t bufferLength)  |  ストリームからバッファーに読み取ります。
 public int64_t Write(const uint8_t* buffer, int64_t bufferLength)  |  バッファーからストリームに書き込みます。
 public bool Flush()  |  ストリームをフラッシュします。
 public void Seek(uint64_t position)  |  ストリーム内の特定の位置をシークします。
 public bool CanRead() const  |  ストリームが読み取り可能かどうかを確認します。
 public bool CanWrite() const  |  ストリームが書き出し可能かどうかを確認します。
 public uint64_t Position()  |  ストリーム内の現在の位置を取得します。
 public uint64_t Size()  |  ストリーム内のコンテンツのサイズを取得します。
 public void Size(uint64_t value)  |  ストリームのサイズを設定します。
  
## <a name="members"></a>メンバー
  
### <a name="read"></a>読み取り
ストリームからバッファーに読み取ります。

パラメーター:  
* **buffer**: バッファーへのポインター 


* **bufferLength**: バッファー サイズ。 



  
**戻り値**: 実際に読み取られたバイト数。
  
### <a name="write"></a>書き込み
バッファーからストリームに書き込みます。

パラメーター:  
* **buffer**: バッファーへのポインター 


* **bufferLength**: バッファー サイズ。 



  
**戻り値**: 実際に書き込まれたバイト数。
  
### <a name="flush"></a>フラッシュ
ストリームをフラッシュします。

  
**戻り値**: 正常終了した場合は true、それ以外の場合は false。
  
### <a name="seek"></a>Seek
ストリーム内の特定の位置をシークします。

パラメーター:  
* **position**: ストリームをシークする位置。


  
### <a name="canread"></a>CanRead
ストリームが読み取り可能かどうかを確認します。

  
**戻り値**: 読み取り可能な場合は true、それ以外の場合は false。
  
### <a name="canwrite"></a>CanWrite
ストリームが書き出し可能かどうかを確認します。

  
**戻り値**: 書き出し可能な場合は true、それ以外の場合は false。
  
### <a name="position"></a>位置
ストリーム内の現在の位置を取得します。

  
**戻り値**: ストリーム内の位置。
  
### <a name="size"></a>Size
ストリーム内のコンテンツのサイズを取得します。

  
**戻り値**: ストリームのサイズ。
  
### <a name="size"></a>Size
ストリームのサイズを設定します。

パラメーター:  
* **stream**: ストリームのサイズ。

