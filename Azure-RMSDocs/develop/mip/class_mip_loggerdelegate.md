# <a name="class-miploggerdelegate"></a>class mip::LoggerDelegate 
MIP SDK のロガーに対してインターフェイスを定義するクラス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public void Init(const std::string& storagePath)  |  ロガーを初期化します。
 public void Flush()  |  ロガーをフラッシュします。
 public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const uint64_t line)  |  ログ ファイルにログ ステートメントを書き込みます。
  
## <a name="members"></a>メンバー
  
### <a name="init"></a>Init
ロガーを初期化します。

パラメーター:  
* **storagePath**: ログを含む継続状態が格納される可能性のある場所へのパス。


  
### <a name="flush"></a>フラッシュ
ロガーをフラッシュします。
  
### <a name="writetolog"></a>WriteToLog
ログ ファイルにログ ステートメントを書き込みます。

パラメーター:  
* **level**: ログ ステートメントの loglevel。 


* **message**: ログ ステートメントのメッセージ。 


* **function**: ログ ステートメントの関数の名前。 


* **file**: ログ ステートメントが生成されたファイル名。 


* **line**: ログ ステートメントが生成された行番号。

