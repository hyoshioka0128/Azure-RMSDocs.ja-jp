---
title: Linux のコード例 | Azure RMS
description: このトピックでは、Linux バージョンの RMS SDK の重要なシナリオとコード要素について説明します。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0F7714CA-1D3E-4846-B187-739825B7DE26
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: a1246cb929eaf5e7632825dc240ab26c478ab7fe
ms.sourcegitcommit: b763a7204421a4c5f946abb7c5cbc06e2883199c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2020
ms.locfileid: "95569710"
---
# <a name="linux-code-examples"></a>Linux のコード例

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

このトピックでは、Linux バージョンの RMS SDK の重要なシナリオとコード要素について説明します。

次のコード スニペットは、サンプル アプリケーション、*rms\_sample* および *rmsauth\_sample* からのものです。 詳しくは、GitHub リポジトリの「[サンプル](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples)」をご覧ください。

## <a name="scenario-access-protection-policy-information-from-a-protected-file"></a>シナリオ: 保護されたファイルから保護ポリシー情報にアクセスする

**RMS で保護されたファイル** 
 を開いて読み取ります。**ソース**: [rms \_ sample/mainwindow.xaml](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**説明**: ユーザーからファイル名を取得したら、証明書を読み取り (*MainWindow::addCertificates* を参照)、クライアント ID とリダイレクト URL で承認コールバックを設定し、*ConvertFromPFile* を呼び出してから (次のコード例を参照)、保護ポリシー名、説明、およびコンテンツの有効期日を読み取ります。

**C++**:

  ```cpp
    void MainWindow::ConvertFromPFILE(const string& fileIn,
        const string& clientId,
        const string& redirectUrl,
        const string& clientEmail) 
    {
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared<ifstream>(
    fileIn, ios_base::in | ios_base::binary);
    
    if (!inFile->is_open()) {
     AddLog("ERROR: Failed to open ", fileIn.c_str());
    return;
    }
    
    string fileOut;
    
    // generate output filename
    auto pos = fileIn.find_last_of('.');
    
    if (pos != string::npos) {
     fileOut = fileIn.substr(0, pos);
    }
    
     // create streams
    auto outFile = make_shared<fstream>(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!outFile->is_open()) {
     AddLog("ERROR: Failed to open ", fileOut.c_str());
     return;
      }
    
    try
    {
    // create authentication context
    AuthCallback auth(clientId, redirectUrl);
    
    // process conversion
    auto pfs = PFileConverter::ConvertFromPFile(
      clientEmail,
      inFile,
      outFile,
      auth,
      this->consent);
    
    AddLog("Successfully converted to ", fileOut.c_str());
    }
    catch (const rmsauth::Exception& e)
    {
    AddLog("ERROR: ", e.error().c_str());
    }
    catch (const rmscore::exceptions::RMSException& e) {
    AddLog("ERROR: ", e.what());
    }
    inFile->close();
    outFile->close();
    }
  ```

**保護されたファイルストリーム** 
 を作成する **ソース**: [rms \_ sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**説明**: このメソッドは、SDK メソッド *ProtectedFileStream:: 獲得* を通じて渡されたバッキングストリームから、保護されたファイルストリームを作成します。このメソッドは、呼び出し元に返されます。

**C++**:

  ```cpp
    shared_ptr<GetProtectedFileStreamResult>PFileConverter::ConvertFromPFile(
    const string           & userId,
    shared_ptr<istream>      inStream,
    shared_ptr<iostream>     outStream,
    IAuthenticationCallback& auth,
    IConsentCallback       & consent)
    {
    auto inIStream = rmscrypto::api::CreateStreamFromStdStream(inStream);
    
    auto fsResult = ProtectedFileStream::Acquire(
    inIStream,
    userId,
    auth,
    consent,
    POL_None,
    static_cast<ResponseCacheFlags>(RESPONSE_CACHE_INMEMORY
                                    | RESPONSE_CACHE_ONDISK));
    
    if ((fsResult.get() != nullptr) && (fsResult->m_status == Success) &&
      (fsResult->m_stream != nullptr)) {
    auto pfs = fsResult->m_stream;
    
    // preparing
    readPosition  = 0;
    writePosition = 0;
    totalSize     = pfs->Size();
    
    // start threads
    for (size_t i = 0; i < THREADS_NUM; ++i) {
      threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast<iostream>(outStream), pfs,
                                  false));
    }
    
    for (thread& t: threadPool) {
      if (t.joinable()) {
        t.join();
      }
    }
    }
      return fsResult;
    }
  ```

## <a name="scenario-create-a-new-protected-file-using-a-template"></a>シナリオ: テンプレートを使用して新しい保護ファイルを作成する

**ユーザーが選択したテンプレート** 
 を使用してファイルを保護します **ソース**: [rms \_ sample/mainwindow.xaml](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**説明**: ユーザーからファイル名を取得したら、証明書を読み取り (*MainWindow::addCertificates* を参照)、クライアント ID とリダイレクト URL で承認コールバックを設定し、選択したファイルを *ConvertToPFileTemplates* を呼び出して保護します (次のコード例を参照)。

**C++**:

  ```cpp
    void MainWindow::ConvertToPFILEUsingTemplates(const string& fileIn,
                                              const string& clientId,
                                              const string& redirectUrl,
                                              const string& clientEmail) 
    {
    // generate output filename
    string fileOut = fileIn + ".pfile";
    
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared<ifstream>(
    fileIn, ios_base::in | ios_base::binary);
    auto outFile = make_shared<fstream>(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!inFile->is_open()) {
    AddLog("ERROR: Failed to open ", fileIn.c_str());
    return;
    }
    
    if (!outFile->is_open()) {
    AddLog("ERROR: Failed to open ", fileOut.c_str());
    return;
    }
    
    // find file extension
    string fileExt;
    auto   pos = fileIn.find_last_of('.');
    
    if (pos != string::npos) {
    fileExt = fileIn.substr(pos);
    }
    
    try {
    // create authentication callback
    AuthCallback auth(clientId, redirectUrl);
    
    // process conversion
    PFileConverter::ConvertToPFileTemplates(
      clientEmail, inFile, fileExt, outFile, auth,
      this->consent, this->templates);
    
    AddLog("Successfully converted to ", fileOut.c_str());
    }
   catch (const rmsauth::Exception& e) {
    AddLog("ERROR: ", e.error().c_str());
    outFile->close();
    remove(fileOut.c_str());
    }
    catch (const rmscore::exceptions::RMSException& e) {
    AddLog("ERROR: ", e.what());
    
    outFile->close();
    remove(fileOut.c_str());
    }
    inFile->close();
    outFile->close();
    }
  ```


**テンプレートから作成されたポリシーを使用してファイルを保護し** 
 ます **ソース**: [rms \_ sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**説明**: ユーザーに関連付けられたテンプレートの一覧がフェッチされ、選択したテンプレートがポリシーの作成に使用されます。このポリシーを使用してファイルを保護します。

**C++**:

  ```cpp
    void PFileConverter::ConvertToPFileTemplates(const string           & userId,
                                             shared_ptr<istream>      inStream,
                                             const string           & fileExt,
                                             std::shared_ptr<iostream>outStream,
                                             IAuthenticationCallback& auth,
                                             IConsentCallback& /*consent*/,
                                             ITemplatesCallback     & templ)
    {
    auto templates = TemplateDescriptor::GetTemplateList(userId, auth);
    
    rmscore::modernapi::AppDataHashMap signedData;
    
    size_t pos = templ.SelectTemplate(templates);
    
    if (pos < templates.size()) {
    auto policy = UserPolicy::CreateFromTemplateDescriptor(
      templates[pos],
      userId,
      auth,
      USER_AllowAuditedExtraction,
      signedData);
   
    ConvertToPFileUsingPolicy(policy, inStream, fileExt, outStream);
    }
    }
  ```

ポリシーを指定 **してファイルを保護し** 
 ます。**ソース**: [rms \_ sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**説明**: 特定のポリシーを使用して保護されたファイル ストリームを作成し、そのファイルを保護します。

**C++**:

  ```cpp
    void PFileConverter::ConvertToPFileUsingPolicy(shared_ptr<UserPolicy>   policy,
                                               shared_ptr<istream>      inStream,
                                               const string           & fileExt,
                                               std::shared_ptr<iostream>outStream)
    {
    if (policy.get() != nullptr) {
    auto outIStream = rmscrypto::api::CreateStreamFromStdStream(outStream);
    auto pStream    = ProtectedFileStream::Create(policy, outIStream, fileExt);
    
    // preparing
    readPosition  = 0;
    writePosition = pStream->Size();
    
    inStream->seekg(0, ios::end);
    totalSize = inStream->tellg();
    
    // start threads
    for (size_t i = 0; i < THREADS_NUM; ++i) {
      threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast<iostream>(inStream),
                                  pStream,
                                  true));
    }
    
    for (thread& t: threadPool) {
      if (t.joinable()) {
        t.join();
      }
    }
    
    pStream->Flush();
    }
  ```


## <a name="scenario-protect-a-file-using-custom-protection"></a>シナリオ: カスタム保護を使用してファイルを保護する

**カスタム保護を使用してファイルを保護し** 
 ます。**ソース**: [rms \_ sample/mainwindow.xaml](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**説明**: ユーザーからファイル名を取得したら、証明書を読み取り (*MainWindow::addCertificates* を参照)、ユーザーから権限情報を収集し、クライアント ID とリダイレクト URL で承認コールバックを設定し、選択したファイルを *ConvertToPFilePredefinedRights* を呼び出して保護します (次のコード例を参照)。

**C++**:

  ```cpp
    void MainWindow::ConvertToPFILEUsingRights(const string            & fileIn,
                                           const vector<UserRights>& userRights,
                                           const string            & clientId,
                                           const string            & redirectUrl,
                                           const string            & clientEmail)
    {
    // generate output filename
    string fileOut = fileIn + ".pfile";
    
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared<ifstream>(
    fileIn, ios_base::in | ios_base::binary);
    auto outFile = make_shared<fstream>(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!inFile->is_open()) {
    AddLog("ERROR: Failed to open ", fileIn.c_str());
    return;
    }
    
    if (!outFile->is_open()) {
    AddLog("ERROR: Failed to open ", fileOut.c_str());
    return;
    }
    
    // find file extension
    string fileExt;
    auto   pos = fileIn.find_last_of('.');
    
    if (pos != string::npos) {
    fileExt = fileIn.substr(pos);
    }
    
    // is anything to add
    if (userRights.size() == 0) {
    AddLog("ERROR: ", "Please fill email and check rights");
    return;
    }
    
    
    try {
    // create authentication callback
    AuthCallback auth(clientId, redirectUrl);
    
    // process conversion
    PFileConverter::ConvertToPFilePredefinedRights(
      clientEmail,
      inFile,
      fileExt,
      outFile,
      auth,
      this->consent,
      userRights);
    
    AddLog("Successfully converted to ", fileOut.c_str());
    }
    catch (const rmsauth::Exception& e) {
    AddLog("ERROR: ", e.error().c_str());
    
    outFile->close();
    remove(fileOut.c_str());
    }
    catch (const rmscore::exceptions::RMSException& e) {
    AddLog("ERROR: ", e.what());
    
    outFile->close();
    remove(fileOut.c_str());
    }
    inFile->close();
    outFile->close();
    }
  ```


**保護ポリシーを作成し、ユーザーが選択した権限** 
 を付与します **ソース**: [rms \_ sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**説明**: ポリシー記述子を作成し、ユーザーの権限情報を使ってこれを入力し、このポリシー記述子を使用してユーザー ポリシーを作成します。 このポリシーを使用して *ConvertToPFileUsingPolicy* への呼び出しにより選択したファイルを保護します (このトピックの前のセクションの説明を参照)。

**C++**:

  ```cpp
    void PFileConverter::ConvertToPFilePredefinedRights(
    const string            & userId,
    shared_ptr<istream>       inStream,
    const string            & fileExt,
    shared_ptr<iostream>      outStream,
    IAuthenticationCallback & auth,
    IConsentCallback& /*consent*/,
    const vector<UserRights>& userRights)
    {
    auto endValidation = chrono::system_clock::now() + chrono::hours(48);
    
    
    PolicyDescriptor desc(userRights);
    
    desc.Referrer(make_shared<string>("https://client.test.app"));
    desc.ContentValidUntil(endValidation);
    desc.AllowOfflineAccess(false);
    desc.Name("Test Name");
    desc.Description("Test Description");
    
    auto policy = UserPolicy::Create(desc, userId, auth,
                                   USER_AllowAuditedExtraction);
    ConvertToPFileUsingPolicy(policy, inStream, fileExt, outStream);
  ```
    

## <a name="workerthread---a-supporting-method"></a>WorkerThread - サポート メソッド


*WorkerThread()* メソッドは、上のシナリオ例の 2 つ (**保護されたファイル ストリームの作成** および **ポリシーを指定してファイルを保護**) によって、次の方法で呼び出されます。

**C++**:

  ```cpp
    threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast<iostream>(outStream), pfs,
                                  false));
  ```


**サポート メソッド、WorkerThread()**

**C++**:

  ```cpp
    static mutex   threadLocker;
    static int64_t totalSize     = 0;
    static int64_t readPosition  = 0;
    static int64_t writePosition = 0;
    static vector<thread> threadPool;
    
    static void WorkerThread(shared_ptr<iostream>           stdStream,
                         shared_ptr<ProtectedFileStream>pStream,
                         bool                           modeWrite) {
    vector<uint8_t> buffer(4096);
    int64_t bufferSize = static_cast<int64_t>(buffer.size());
    
    while (totalSize - readPosition > 0) {
    // lock
    threadLocker.lock();
    
    // check remain
    if (totalSize - readPosition <= 0) {
      threadLocker.unlock();
      return;
    }
    
    // get read/write offset
    int64_t offsetRead  = readPosition;
    int64_t offsetWrite = writePosition;
    int64_t toProcess   = min(bufferSize, totalSize - readPosition);
    readPosition  += toProcess;
    writePosition += toProcess;
    
    // no need to lock more
    threadLocker.unlock();
    
    if (modeWrite) {
      // stdStream is not thread safe!!!
      try {
        threadLocker.lock();
    
        stdStream->seekg(offsetRead);
        stdStream->read(reinterpret_cast<char *>(&buffer[0]), toProcess);
        threadLocker.unlock();
        auto written =
          pStream->WriteAsync(
            buffer.data(), toProcess, offsetWrite, std::launch::deferred).get();
    
        if (written != toProcess) {
          throw rmscore::exceptions::RMSStreamException("Error while writing data");
        }
      }
      catch (exception& e) {
        qDebug() << "Exception: " << e.what();
      }
    } else {
      auto read =
        pStream->ReadAsync(&buffer[0],
                           toProcess,
                           offsetRead,
                           std::launch::deferred).get();
    
      if (read == 0) {
        break;
      }
    
      try {
        // stdStream is not thread safe!!!
        threadLocker.lock();
    
        // seek to write
        stdStream->seekp(offsetWrite);
        stdStream->write(reinterpret_cast<const char *>(buffer.data()), read);
        threadLocker.unlock();
      }
      catch (exception& e) {
        qDebug() << "Exception: " << e.what();
      }
    }
    }
    }
  ```


## <a name="scenario-rms-authentication"></a>シナリオ: RMS 認証

次の例は、2 つの異なる認証方法 (UI を使用、または使用せずに Azure 認証 oAuth2 トークンを取得) を示しています。
UI を使用し **た OAuth2 認証トークンの取得** 
**ソース**: [rmsauth \_ sample/mainwindow.xaml](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rmsauth_sample)

**手順 1**: **Rmsauth:: FileCache** オブジェクトの共有ポイントを作成します。
説明: キャッシュのパスを設定するか、既定値を使用できます。

**C++**:

  ```cpp
    auto FileCachePtr = std::make_shared< rmsauth::FileCache>();
  ```


**手順 2**: **rmsauth::AuthenticationContext** オブジェクトを作成します。説明: Azure *証明機関 URI* と *FileCache* オブジェクトを指定します。

**C++**:

  ```cpp
    AuthenticationContext authContext(
                              std::string("https://sts.aadrm.com/_sts/oauth/authorize"),
                              AuthorityValidationType::False,
                              FileCachePtr);
  ```


**手順 3**: **Authcontext** オブジェクトの **acquireToken** メソッドを呼び出し、次のパラメーターを指定します。説明:

-   *要求されるリソース* - アクセスする必要のある保護されたリソース
-   *クライアントの一意な ID* - 通常は GUID
-   *リダイレクト URI* - 認証トークンがフェッチされた後に回送される URI
-   *認証プロンプトの動作* - **PromptBehavior::Auto** を設定した場合、必要に応じて、ライブラリによりキャッシュの使用トークンの更新が試行されます
-   *ユーザー ID* - プロンプト ウィンドウに表示されるユーザー名

**C++**:

  ```cpp
    auto result = authContext.acquireToken(
                std::string("api.aadrm.com"),
                std::string("4a63455a-cfa1-4ac6-bd2e-0d046cf1c3f7"),
                std::string("https://client.test.app"),
                PromptBehavior::Auto,
                std::string("john.smith@msopentechtest01.onmicrosoft.com"));
  ```

**手順 4**: 結果からアクセストークンを取得する説明: Call **Result-> accessToken ()** メソッド

**注**  いずれかの認証ライブラリ メソッドにより **rmsauth::Exception** が発生する場合があります

 
UI を使用 **せずに OAuth2 認証トークンを取得** 
 する **ソース**: [rmsauth \_ sample/mainwindow.xaml](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rmsauth_sample)

**手順 1**: **rmsauth::FileCache** オブジェクトの共有ポイントを作成します。説明: キャッシュのパスを設定するか、既定値を使用できます。

**C++**:

  ```cpp
    auto FileCachePtr = std::make_shared< rmsauth::FileCache>();
  ```


**手順 2**: **UserCredential** オブジェクトを作成します。説明: *ユーザー ログイン* と *パスワード* を指定します。

**C++**:

  ```cpp
    auto userCred = std::make_shared<UserCredential>("john.smith@msopentechtest01.onmicrosoft.com",
                                                 "SomePass");
  ```

**手順 3**: **rmsauth::AuthenticationContext** オブジェクトを作成します。説明: Azure *証明機関 URI* と *FileCache* オブジェクトを指定します。

**C++**:

  ```cpp
    AuthenticationContext authContext(
                        std::string("https://sts.aadrm.com/_sts/oauth/authorize"),
                        AuthorityValidationType::False,
                        FileCachePtr);
  ```


**手順 4**: **Authcontext** の **acquireToken** メソッドを呼び出し、パラメーターを指定します。
-   *要求されるリソース* - アクセスする必要のある保護されたリソース
-   *クライアントの一意な ID* - 通常は GUID
-   *ユーザーの資格情報* - 作成されたオブジェクトを渡します

**C++**:

  ```cpp
    auto result = authContext.acquireToken(
                std::string("api.aadrm.com"),
                std::string("4a63455a-cfa1-4ac6-bd2e-0d046cf1c3f7"),
                userCred);
  ```


**手順 5**: 結果からアクセストークンを取得する説明: Call **Result-> accessToken ()** メソッド

**注**  いずれかの認証ライブラリ メソッドにより **rmsauth::Exception** が発生する場合があります
