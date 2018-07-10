# <a name="class-mipfileengine"></a>class mip::FileEngine 
すべてのエンジン関数のインターフェイス。
  
## <a name="summary"></a>[概要]
 メンバー                        | 説明                                
--------------------------------|---------------------------------------------
 public virtual ~FileEngine()  | _まだ文書化されていません。_
 public const Settings& GetSettings() const  |  エンジンの設定を返します。
public const std::vector<std::shared_ptr<Label>>& ListSensitivityLabels()  |  機密ラベルの一覧を返します。
public void CreateFileHandlerAsync(const std::string& inputFilePath, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver, const std::shared_ptr<void>& context)  |  指定されたファイル パスのファイル ハンドラーの作成を開始します。
public void CreateFileHandlerAsync(const std::shared_ptr<Stream>& inputStream, const std::string& inputFileName, const std::shared_ptr<FileHandler::Observer>& fileHandlerObserver, const std::shared_ptr<void>& context)  |  指定されたファイル ストリームのファイル ハンドラーの作成を開始します。
 protected FileEngine()  | _まだ文書化されていません。_
  
## <a name="members"></a>メンバー
  
### <a name="fileengine"></a>~FileEngine
_まだ文書化されていません。_

  
### <a name="settings"></a>Settings
エンジンの設定を返します。
  
### <a name="label"></a>Label
機密ラベルの一覧を返します。
  
### <a name="createfilehandlerasync"></a>CreateFileHandlerAsync
指定されたファイル パスのファイル ハンドラーの作成を開始します。

パラメーター:  
* 開くファイル。**** パスにはファイル名を含める必要があり、ファイル名拡張子が存在する場合はそれも含めます。 


* [FileHandler::Observer](class_mip_filehandler_observer.md) インターフェイスを実装するクラス。**** 


* **context**: オブザーバーに不透明に渡されるクライアント コンテキスト。


  
### <a name="createfilehandlerasync"></a>CreateFileHandlerAsync
指定されたファイル ストリームのファイル ハンドラーの作成を開始します。

パラメーター:  
* ファイルを表すストリーム。**** 


* ファイルへのパス。**** パスにはファイル名を含める必要があり、ファイル名拡張子が存在する場合はそれも含めます。 


* [FileHandler::Observer](class_mip_filehandler_observer.md) インターフェイスを実装するクラス。**** 


* **context**: オブザーバーに不透明に渡されるクライアント コンテキスト。


  
### <a name="fileengine"></a>FileEngine
_まだ文書化されていません。_
