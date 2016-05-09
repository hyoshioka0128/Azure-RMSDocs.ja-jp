---
# required metadata

title: Linux のコード例 | Azure RMS
description: このトピックでは、Linux バージョンの RMS SDK の重要なシナリオとコード要素について説明します。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 11acef4b-67f8-4e45-a0e7-d9310213b5f9

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿# Linux のコード例

このトピックでは、Linux バージョンの RMS SDK の重要なシナリオとコード要素について説明します。

次のコード スニペットは、サンプル アプリケーション、*rms\_sample* および *rmsauth\_sample* からのものです。 詳しくは、GitHub リポジトリの「[サンプル](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples)」をご覧ください。

-   [**シナリオ**: 保護されたファイルから保護ポリシー情報にアクセスする](#scenario__access_protection_policy_information_from_a___protected_file)
-   [**シナリオ**: テンプレートを使用して新しい保護ファイルを作成する](#scenario__create_a_new_protected_file_using_a_template)
-   [**シナリオ**: カスタム保護を使用してファイルを保護する](#scenario__protect_a_file_using_custom_protection)
-   [WorkerThread - サポート メソッド](#workerthread_-_a_supporting_method)
-   [**シナリオ**: RMS 認証](#scenario__rms_authentication)

## シナリオ: 保護されたファイルから保護ポリシー情報にアクセスする

**RMS 保護ファイルを開いて読み取ります。**
**ソース**: [rms\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**説明**: ユーザーからファイル名を取得したら、証明書を読み取り (*MainWindow::addCertificates* を参照)、クライアント ID とリダイレクト URL で承認コールバックを設定し、*ConvertFromPFile* を呼び出してから (次のコード例を参照)、保護ポリシー名、説明、およびコンテンツの有効期日を読み取ります。

**C++**:

    void MainWindow::ConvertFromPFILE(const string&amp; fileIn,
        const string&amp; clientId,
        const string&amp; redirectUrl,
        const string&amp; clientEmail) 
    {
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared&lt;ifstream&gt;(
    fileIn, ios_base::in | ios_base::binary);
    
    if (!inFile-&gt;is_open()) {
     AddLog(&quot;ERROR: Failed to open &quot;, fileIn.c_str());
    return;
    }
    
    string fileOut;
    
    // generate output filename
    auto pos = fileIn.find_last_of(&#39;.&#39;);
    
    if (pos != string::npos) {
     fileOut = fileIn.substr(0, pos);
    }
    
     // create streams
    auto outFile = make_shared&lt;fstream&gt;(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!outFile-&gt;is_open()) {
     AddLog(&quot;ERROR: Failed to open &quot;, fileOut.c_str());
     return;
      }
    
    try
    {
    // create authentication context
    AuthCallback auth(clientId, redirectUrl);
    
    // process convertion
    auto pfs = PFileConverter::ConvertFromPFile(
      clientEmail,
      inFile,
      outFile,
      auth,
      this-&gt;consent);
    
    AddLog(&quot;Successfully converted to &quot;, fileOut.c_str());
    }
    catch (const rmsauth::Exception&amp; e)
    {
    AddLog(&quot;ERROR: &quot;, e.error().c_str());
    }
    catch (const rmscore::exceptions::RMSException&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.what());
    }
    inFile-&gt;close();
    outFile-&gt;close();
    }

**保護されたファイル ストリームを作成します。**
**ソース**: [rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**説明**: この方法では、SDK メソッド、*ProtectedFileStream::Aquire* を通じて渡されたサポートするストリームから保護ファイル ストリームを作成します。これは、呼び出し元に返されます。

**C++**:

    shared_ptr&lt;GetProtectedFileStreamResult&gt;PFileConverter::ConvertFromPFile(
    const string           &amp; userId,
    shared_ptr&lt;istream&gt;      inStream,
    shared_ptr&lt;iostream&gt;     outStream,
    IAuthenticationCallback&amp; auth,
    IConsentCallback       &amp; consent)
    {
    auto inIStream = rmscrypto::api::CreateStreamFromStdStream(inStream);
    
    auto fsResult = ProtectedFileStream::Acquire(
    inIStream,
    userId,
    auth,
    consent,
    POL_None,
    static_cast&lt;ResponseCacheFlags&gt;(RESPONSE_CACHE_INMEMORY
                                    | RESPONSE_CACHE_ONDISK));
    
    if ((fsResult.get() != nullptr) &amp;&amp; (fsResult-&gt;m_status == Success) &amp;&amp;
      (fsResult-&gt;m_stream != nullptr)) {
    auto pfs = fsResult-&gt;m_stream;
    
    // preparing
    readPosition  = 0;
    writePosition = 0;
    totalSize     = pfs-&gt;Size();
    
    // start threads
    for (size_t i = 0; i &lt; THREADS_NUM; ++i) {
      threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast&lt;iostream&gt;(outStream), pfs,
                                  false));
    }
    
    for (thread&amp; t: threadPool) {
      if (t.joinable()) {
        t.join();
      }
    }
    }
      return fsResult;
    }

## シナリオ: テンプレートを使用して新しい保護ファイルを作成する

**ユーザーが選択したテンプレートを使用してファイルを保護します。**
**ソース**: [rms\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**説明**: ユーザーからファイル名を取得したら、証明書を読み取り (*MainWindow::addCertificates* を参照)、クライアント ID とリダイレクト URL で承認コールバックを設定し、選択したファイルを *ConvertToPFileTemplates* を呼び出して保護します (次のコード例を参照)。

**C++**:

    void MainWindow::ConvertToPFILEUsingTemplates(const string&amp; fileIn,
                                              const string&amp; clientId,
                                              const string&amp; redirectUrl,
                                              const string&amp; clientEmail) 
    {
    // generate output filename
    string fileOut = fileIn + &quot;.pfile&quot;;
    
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared&lt;ifstream&gt;(
    fileIn, ios_base::in | ios_base::binary);
    auto outFile = make_shared&lt;fstream&gt;(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!inFile-&gt;is_open()) {
    AddLog(&quot;ERROR: Failed to open &quot;, fileIn.c_str());
    return;
    }
    
    if (!outFile-&gt;is_open()) {
    AddLog(&quot;ERROR: Failed to open &quot;, fileOut.c_str());
    return;
    }
    
    // find file extension
    string fileExt;
    auto   pos = fileIn.find_last_of(&#39;.&#39;);
    
    if (pos != string::npos) {
    fileExt = fileIn.substr(pos);
    }
    
    try {
    // create authentication callback
    AuthCallback auth(clientId, redirectUrl);
    
    // process convertion
    PFileConverter::ConvertToPFileTemplates(
      clientEmail, inFile, fileExt, outFile, auth,
      this-&gt;consent, this-&gt;templates);
    
    AddLog(&quot;Successfully converted to &quot;, fileOut.c_str());
    }
   catch (const rmsauth::Exception&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.error().c_str());
    outFile-&gt;close();
    remove(fileOut.c_str());
    }
    catch (const rmscore::exceptions::RMSException&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.what());
    
    outFile-&gt;close();
    remove(fileOut.c_str());
    }
    inFile-&gt;close();
    outFile-&gt;close();
    }


**テンプレートから作成されたポリシーを使用してファイルを保護します。**
**ソース**: [rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**説明**: ユーザーに関連付けられたテンプレートの一覧がフェッチされ、選択したテンプレートがポリシーの作成に使用されます。このポリシーを使用してファイルを保護します。

**C++**:

    void PFileConverter::ConvertToPFileTemplates(const string           &amp; userId,
                                             shared_ptr&lt;istream&gt;      inStream,
                                             const string           &amp; fileExt,
                                             std::shared_ptr&lt;iostream&gt;outStream,
                                             IAuthenticationCallback&amp; auth,
                                             IConsentCallback&amp; /*consent*/,
                                             ITemplatesCallback     &amp; templ)
    {
    auto templates = TemplateDescriptor::GetTemplateList(userId, auth);
    
    rmscore::modernapi::AppDataHashMap signedData;
    
    size_t pos = templ.SelectTemplate(templates);
    
    if (pos &lt; templates.size()) {
    auto policy = UserPolicy::CreateFromTemplateDescriptor(
      templates[pos],
      userId,
      auth,
      USER_AllowAuditedExtraction,
      signedData);
   
    ConvertToPFileUsingPolicy(policy, inStream, fileExt, outStream);
    }
    }

**ポリシーを指定してファイルを保護します。**
**ソース**: [rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**説明**: 特定のポリシーを使用して保護されたファイル ストリームを作成し、そのファイルを保護します。

**C++**:

    void PFileConverter::ConvertToPFileUsingPolicy(shared_ptr&lt;UserPolicy&gt;   policy,
                                               shared_ptr&lt;istream&gt;      inStream,
                                               const string           &amp; fileExt,
                                               std::shared_ptr&lt;iostream&gt;outStream)
    {
    if (policy.get() != nullptr) {
    auto outIStream = rmscrypto::api::CreateStreamFromStdStream(outStream);
    auto pStream    = ProtectedFileStream::Create(policy, outIStream, fileExt);
    
    // preparing
    readPosition  = 0;
    writePosition = pStream-&gt;Size();
    
    inStream-&gt;seekg(0, ios::end);
    totalSize = inStream-&gt;tellg();
    
    // start threads
    for (size_t i = 0; i &lt; THREADS_NUM; ++i) {
      threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast&lt;iostream&gt;(inStream),
                                  pStream,
                                  true));
    }
    
    for (thread&amp; t: threadPool) {
      if (t.joinable()) {
        t.join();
      }
    }
    
    pStream-&gt;Flush();
    }
    


## シナリオ: カスタム保護を使用してファイルを保護する

**カスタム保護を使用してファイルを保護します。**
**ソース**: [rms\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**説明**: ユーザーからファイル名を取得したら、証明書を読み取り (*MainWindow::addCertificates* を参照)、ユーザーから権限情報を収集し、クライアント ID とリダイレクト URL で承認コールバックを設定し、選択したファイルを *ConvertToPFilePredefinedRights* を呼び出して保護します (次のコード例を参照)。

**C++**:

    void MainWindow::ConvertToPFILEUsingRights(const string            &amp; fileIn,
                                           const vector&lt;UserRights&gt;&amp; userRights,
                                           const string            &amp; clientId,
                                           const string            &amp; redirectUrl,
                                           const string            &amp; clientEmail)
    {
    // generate output filename
    string fileOut = fileIn + &quot;.pfile&quot;;
    
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared&lt;ifstream&gt;(
    fileIn, ios_base::in | ios_base::binary);
    auto outFile = make_shared&lt;fstream&gt;(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!inFile-&gt;is_open()) {
    AddLog(&quot;ERROR: Failed to open &quot;, fileIn.c_str());
    return;
    }
    
    if (!outFile-&gt;is_open()) {
    AddLog(&quot;ERROR: Failed to open &quot;, fileOut.c_str());
    return;
    }
    
    // find file extension
    string fileExt;
    auto   pos = fileIn.find_last_of(&#39;.&#39;);
    
    if (pos != string::npos) {
    fileExt = fileIn.substr(pos);
    }
    
    // is anything to add
    if (userRights.size() == 0) {
    AddLog(&quot;ERROR: &quot;, &quot;Please fill email and check rights&quot;);
    return;
    }
    
    
    try {
    // create authentication callback
    AuthCallback auth(clientId, redirectUrl);
    
    // process convertion
    PFileConverter::ConvertToPFilePredefinedRights(
      clientEmail,
      inFile,
      fileExt,
      outFile,
      auth,
      this-&gt;consent,
      userRights);
    
    AddLog(&quot;Successfully converted to &quot;, fileOut.c_str());
    }
    catch (const rmsauth::Exception&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.error().c_str());
    
    outFile-&gt;close();
    remove(fileOut.c_str());
    }
    catch (const rmscore::exceptions::RMSException&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.what());
    
    outFile-&gt;close();
    remove(fileOut.c_str());
    }
    inFile-&gt;close();
    outFile-&gt;close();
    }


**ユーザーが選択した権限を指定して保護ポリシーを作成します。**
**ソース**: [rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**説明**: ポリシー記述子を作成し、ユーザーの権限情報を使ってこれを入力し、このポリシー記述子を使用してユーザー ポリシーを作成します。 このポリシーを使用して *ConvertToPFileUsingPolicy* への呼び出しにより選択したファイルを保護します (このトピックの前のセクションの説明を参照)。

**C++**:

    void PFileConverter::ConvertToPFilePredefinedRights(
    const string            &amp; userId,
    shared_ptr&lt;istream&gt;       inStream,
    const string            &amp; fileExt,
    shared_ptr&lt;iostream&gt;      outStream,
    IAuthenticationCallback &amp; auth,
    IConsentCallback&amp; /*consent*/,
    const vector&lt;UserRights&gt;&amp; userRights)
    {
    auto endValidation = chrono::system_clock::now() + chrono::hours(48);
    
    
    PolicyDescriptor desc(userRights);
    
    desc.Referrer(make_shared&lt;string&gt;(&quot;https://client.test.app&quot;));
    desc.ContentValidUntil(endValidation);
    desc.AllowOfflineAccess(false);
    desc.Name(&quot;Test Name&quot;);
    desc.Description(&quot;Test Description&quot;);
    
    auto policy = UserPolicy::Create(desc, userId, auth,
                                   USER_AllowAuditedExtraction);
    ConvertToPFileUsingPolicy(policy, inStream, fileExt, outStream);
    

## WorkerThread - サポート メソッド


*WorkerThread()* メソッドは、上のシナリオ例の 2 つ (**保護されたファイル ストリームの作成**および**ポリシーを指定してファイルを保護**) によって、次の方法で呼び出されます。

**C++**:

    threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast&lt;iostream&gt;(outStream), pfs,
                                  false));


**サポート メソッド、WorkerThread()**

**C++**:

    static mutex   threadLocker;
    static int64_t totalSize     = 0;
    static int64_t readPosition  = 0;
    static int64_t writePosition = 0;
    static vector&lt;thread&gt; threadPool;
    
    static void WorkerThread(shared_ptr&lt;iostream&gt;           stdStream,
                         shared_ptr&lt;ProtectedFileStream&gt;pStream,
                         bool                           modeWrite) {
    vector&lt;uint8_t&gt; buffer(4096);
    int64_t bufferSize = static_cast&lt;int64_t&gt;(buffer.size());
    
    while (totalSize - readPosition &gt; 0) {
    // lock
    threadLocker.lock();
    
    // check remain
    if (totalSize - readPosition &lt;= 0) {
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
    
        stdStream-&gt;seekg(offsetRead);
        stdStream-&gt;read(reinterpret_cast&lt;char *&gt;(&amp;buffer[0]), toProcess);
        threadLocker.unlock();
        auto written =
          pStream-&gt;WriteAsync(
            buffer.data(), toProcess, offsetWrite, std::launch::deferred).get();
    
        if (written != toProcess) {
          throw rmscore::exceptions::RMSStreamException(&quot;Error while writing data&quot;);
        }
      }
      catch (exception&amp; e) {
        qDebug() &lt;&lt; &quot;Exception: &quot; &lt;&lt; e.what();
      }
    } else {
      auto read =
        pStream-&gt;ReadAsync(&amp;buffer[0],
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
        stdStream-&gt;seekp(offsetWrite);
        stdStream-&gt;write(reinterpret_cast&lt;const char *&gt;(buffer.data()), read);
        threadLocker.unlock();
      }
      catch (exception&amp; e) {
        qDebug() &lt;&lt; &quot;Exception: &quot; &lt;&lt; e.what();
      }
    }
    }
    }


## シナリオ: RMS 認証

次の例は、2 つの異なる認証方法 (UI を使用、または使用せずに Azure 認証 oAuth2 トークンを取得) を示しています。
**UI を使用した oAuth2 認証トークンの取得**
**ソース**: [rmsauth\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rmsauth_sample)

**手順 1**: **rmsauth::FileCache** オブジェクトの共有ポイントを作成します。
説明: キャッシュのパスを設定するか、既定値を使用できます。

**C++**:

    auto FileCachePtr = std::make_shared&lt; rmsauth::FileCache&gt;();


**手順 2**: **rmsauth::AuthenticationContext** オブジェクトを作成します。
説明: Azure *証明機関 URI* と *FileCache* オブジェクトを指定します。

**C++**:

    AuthenticationContext authContext(
                              std::string(“https://sts.aadrm.com/_sts/oauth/authorize”),
                              AuthorityValidationType::False,
                              FileCachePtr);


**手順 3**: **authContext** オブジェクトの **aquireToken** メソッドを呼び出し、次のパラメーターを指定します。
説明:

-   *要求されるリソース* - アクセスする必要のある保護されたリソース
-   *クライアントの一意な ID* - 通常は GUID
-   *リダイレクト URI* - 認証トークンがフェッチされた後に回送される URI
-   *認証プロンプトの動作* - **PromptBehavior::Auto** を設定した場合、必要に応じて、ライブラリによりキャッシュの使用トークンの更新が試行されます
-   *ユーザー ID* - プロンプト ウィンドウに表示されるユーザー名

**C++**:

    auto result = authContext.acquireToken(
                std::string(“api.aadrm.com”),
                std::string(“4a63455a-cfa1-4ac6-bd2e-0d046cf1c3f7”),
                std::string(“https://client.test.app”),
                PromptBehavior::Auto,
                std::string(“john.smith@msopentechtest01.onmicrosoft.com”));


**手順 4**: 結果からアクセス トークンを取得します。
説明: **result-&gt; accessToken()** メソッドを呼び出します

**注**  いずれかの認証ライブラリ メソッドにより **rmsauth::Exception** が発生する場合があります

 
**UI なしの oAuth2 認証トークンの取得**
**ソース**: [rmsauth\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rmsauth_sample)

**手順 1**: **rmsauth::FileCache** オブジェクトの共有ポイントを作成します。
説明: キャッシュのパスを設定するか、既定値を使用できます

**C++**:

    auto FileCachePtr = std::make_shared&lt; rmsauth::FileCache&gt;();


**手順 2**: **UserCredential** オブジェクトを作成します
説明: *ユーザー ログイン*と*パスワード*を指定します

**C++**:

    auto userCred = std::make_shared&lt;UserCredential&gt;(&quot;john.smith@msopentechtest01.onmicrosoft.com&quot;,
                                                 &quot;SomePass&quot;);


**手順 3**: **rmsauth::AuthenticationContext** オブジェクトを作成します
説明: Azure *証明機関 URI* と *FileCache* オブジェクトを指定します

**C++**:

    AuthenticationContext authContext(
                        std::string(“https://sts.aadrm.com/_sts/oauth/authorize”),
                        AuthorityValidationType::False,
                        FileCachePtr);


**手順 4**: **authContext** オブジェクトの **aquireToken** メソッドを呼び出し、次のパラメーターを指定します。
-   *要求されるリソース* - アクセスする必要のある保護されたリソース
-   *クライアントの一意な ID* - 通常は GUID
-   *ユーザーの資格情報* - 作成されたオブジェクトを渡します

**C++**:

    auto result = authContext.acquireToken(
                std::string(“api.aadrm.com”),
                std::string(“4a63455a-cfa1-4ac6-bd2e-0d046cf1c3f7”),
                userCred);


**手順 5**: 結果からアクセス トークンを取得します
説明: **result-&gt; accessToken()** メソッドを呼び出します

**注**  いずれかの認証ライブラリ メソッドにより **rmsauth::Exception** が発生する場合があります



<!--HONumber=Apr16_HO3-->


