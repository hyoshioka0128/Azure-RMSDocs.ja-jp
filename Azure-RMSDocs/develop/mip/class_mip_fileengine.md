# <a name="class-mipfileengine"></a>class mip::FileEngine 
すべてのエンジン関数のインターフェイス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
public inline virtual ~FileEngine()  |  
public const Settings& GetSettings() const  |  エンジンの設定を返します。
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  機密ラベルの一覧を返します。
public std::shared_ptr<FileHandler> CreateFileHandler(const std::string& inputFilePath, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver)  |  指定されたファイル パスのファイル ハンドラーを返します。
public std::shared_ptr<FileHandler> CreateFileHandler(const std::shared_ptr<Stream>& inputStream, const std::string& inputFileName, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver)  |  指定されたファイル ストリームのファイル ハンドラーを返します。
protected inline FileEngine()  |  
  
## <a name="members"></a>メンバー
  
### <a name="fileengine"></a>~FileEngine
  
### <a name="settings"></a>Settings
エンジンの設定を返します。
  
### <a name="label"></a>Label
機密ラベルの一覧を返します。
  
### <a name="filehandler"></a>FileHandler
指定されたファイル パスのファイル ハンドラーを返します。
  
#### <a name="parameters"></a>パラメーター
* 開くファイル。 パスにはファイル名を含める必要があり、ファイル名拡張子が存在する場合はそれも含めます。 
* [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer) インターフェイスを実装するクラス。
  
### <a name="filehandler"></a>FileHandler
指定されたファイル ストリームのファイル ハンドラーを返します。
  
#### <a name="parameters"></a>パラメーター
* ファイルを表すストリーム。 
* ファイルへのパス。 パスにはファイル名を含める必要があり、ファイル名拡張子が存在する場合はそれも含めます。 
* [FileHandler::Observer](#classmip_1_1_file_handler_1_1_observer) インターフェイスを実装するクラス。
  
### <a name="fileengine"></a>FileEngine