---
title: "Android のコード例 |Azure RMS"
description: "このトピックでは、Android バージョンの RMS SDK の重要なコード要素について説明します。"
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 58CC2E50-1E4D-4621-A947-25312C3FF519
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 7fe417d8c2e0758fcb6c9dfc88be86208cb8e294
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
ms.translationtype: HT
ms.contentlocale: ja-JP
---
# <a name="android-code-examples"></a>Android のコード例

このトピックでは、Android バージョンの RMS SDK の重要なコード要素について説明します。

**注** 以下のコード例と説明では、クライアント プロセスを参照するために MSIPC (Microsoft Information Protection and Control) という用語を使用します。


## <a name="using-the-microsoft-rights-management-sdk-42---key-scenarios"></a>Microsoft Rights Management SDK 4.2 の使用 - 主要なシナリオ

この SDK を理解する上で重要な開発シナリオを表す大規模なサンプル アプリケーションのコード例を次に示します。 これらのコード例では、保護ファイルと呼ばれる Microsoft Protected File 形式の使用例、カスタム保護ファイル形式の使用例、およびカスタムの UI コントロールの使用例を示します。



サンプル アプリケーション *MSIPCSampleApp* は、この Android オペレーティング システム用の SDK で使用可能です。 このサンプル アプリケーションにアクセスするには、GitHub の [rms-sdk-ui-for-android](https://github.com/AzureAD/rms-sdk-ui-for-android) を参照してください。

### <a name="scenario-consume-an-rms-protected-file"></a>シナリオ: RMS 保護ファイルを使用する

-   **手順 1**. [ProtectedFileInputStream](https://msdn.microsoft.com/library/dn790851.aspx) を作成します。

    **ソース**: *MsipcAuthenticationCallback.java*

    **説明**: [ProtectedFileInputStream](https://msdn.microsoft.com/library/dn790851.aspx) オブジェクトをインスタンス化し、[AuthenticationRequestCallback](https://msdn.microsoft.com/library/dn758250.aspx) を使用してサービス認証を実装するその作成メソッドを呼び出してトークンを取得します。それには、パラメーター *mRmsAuthCallback* として **AuthenticationRequestCallback** インスタンスを MSIPC API に渡します。 以下のコード例セクションの末尾近くの [ProtectedFileInputStream.create](https://msdn.microsoft.com/library/dn790851.aspx) の呼び出しを参照してください。

        public void startContentConsumptionFromPtxtFileFormat(InputStream inputStream)
        {
            CreationCallback<ProtectedFileInputStream> protectedFileInputStreamCreationCallback =
              new CreationCallback<ProtectedFileInputStream>()
            {
                @Override
                public Context getContext()
                {
                   …
               }

                @Override
                public void onCancel()
                {
                   …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                   …
                }

                @Override
                public void onSuccess(ProtectedFileInputStream protectedFileInputStream)
                {
                   …
                   …
                    byte[] dataChunk = new byte[16384];
                    try
                    {
                        while ((nRead = protectedFileInputStream.read(dataChunk, 0,
                                dataChunk.length)) != -1)
                        {
                            …
                        }
                         …
                        protectedFileInputStream.close();
                    }
                    catch (IOException e)
                    {
                      …
                    }  
              }
            };
            try
            {
               …
                ProtectedFileInputStream.create(inputStream, null, mRmsAuthCallback,
                                                PolicyAcquisitionFlags.NONE,
                                                protectedFileInputStreamCreationCallback);
            }
            catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e)
            {
                …
            }
        }


-   **手順 2**. Active Directory 認証ライブラリ (ADAL) を使用して認証をセットアップします。

    **ソース**: *MsipcAuthenticationCallback.java*

    **説明**: この手順では、例の認証パラメーターで [AuthenticationRequestCallback](https://msdn.microsoft.com/library/dn758255.aspx) を実装するために ADAL を使用します。 ADAL の使用の詳細については、「[Azure AD Authentication Library (ADAL)](https://msdn.microsoft.com/library/jj573266.aspx)」 (Azure AD 認証ライブラリ (ADAL)) を参照してください。


        class MsipcAuthenticationCallback implements AuthenticationRequestCallback
        {

        …

        @Override
        public void getToken(Map<String, String> authenticationParametersMap,
                             final AuthenticationCompletionCallback authenticationCompletionCallbackToMsipc)
        {
            String authority = authenticationParametersMap.get("oauth2.authority");
            String resource = authenticationParametersMap.get("oauth2.resource");
            String userId = authenticationParametersMap.get("userId");
            final String userHint = (userId == null)? "" : userId;
            AuthenticationContext authenticationContext = App.getInstance().getAuthenticationContext();
            if (authenticationContext == null || !authenticationContext.getAuthority().equalsIgnoreCase(authority))
            {
                try
                {
                    authenticationContext = new AuthenticationContext(App.getInstance().getApplicationContext(), authority, …);
                    App.getInstance().setAuthenticationContext(authenticationContext);
                }
                catch (NoSuchAlgorithmException e)
                {
                    …
                    authenticationCompletionCallbackToMsipc.onFailure();
                }
                catch (NoSuchPaddingException e)
                {
                    …
                    authenticationCompletionCallbackToMsipc.onFailure();
                }
           }
            App.getInstance().getAuthenticationContext().acquireToken(mParentActivity, resource, mClientId, mRedirectURI, userId, mPromptBehavior,
                           "&USERNAME=" + userHint, new AuthenticationCallback<AuthenticationResult>()
                            {
                                @Override
                                public void onError(Exception exc)
                                {
                                    …
                                    if (exc instanceof AuthenticationCancelError)
                                    {
                                         …
                                        authenticationCompletionCallbackToMsipc.onCancel();
                                    }
                                    else
                                    {
                                         …
                                        authenticationCompletionCallbackToMsipc.onFailure();
                                    }
                                }

                                @Override
                                public void onSuccess(AuthenticationResult result)
                                {
                                    …
                                    if (result == null || result.getAccessToken() == null
                                            || result.getAccessToken().isEmpty())
                                    {
                                         …
                                    }
                                    else
                                    {
                                        // request is successful
                                        …
                                        authenticationCompletionCallbackToMsipc.onSuccess(result.getAccessToken());
                                    }
                                }
                            }

                            );
                      }


-   **手順 3**. [UserPolicy.accessCheck](https://msdn.microsoft.comlibrary/dn790885.aspx) メソッドを呼び出して、このユーザーにこのコンテンツの**編集**権限があるかを確認します。

    **ソース**: *TextEditorFragment.java*


         //check if user has edit rights and apply enforcements
                if (!mUserPolicy.accessCheck(EditableDocumentRights.Edit))
                {
                    mTextEditor.setFocusableInTouchMode(false);
                    mTextEditor.setFocusable(false);
                    mTextEditor.setEnabled(false);
                    …
                }


### <a name="scenario-create-a-new-protected-file-using-a-template"></a>シナリオ: テンプレートを使用して新しい保護ファイルを作成する

このシナリオは、はじめにテンプレートの一覧を取得し、最初の&1; つを選択してポリシーを作成してから、新しい保護ファイルを作成して書き込みます。

-   **手順 1**. [TemplateDescriptor](https://msdn.microsoft.com/library/dn790871.aspx) オブジェクトを使用してテンプレートの一覧を取得します。

    **ソース**: *MsipcTaskFragment.java*



    CreationCallback<List<TemplateDescriptor>> getTemplatesCreationCallback = new CreationCallback<List<TemplateDescriptor>>() { @Override public Context getContext() { …
          }

          @Override
          public void onCancel()
          {
              …
          }

          @Override
          public void onFailure(ProtectionException e)
          {
              …
          }

          @Override
          public void onSuccess(List<TemplateDescriptor> templateDescriptors)
          {
             …
          }
      }; try { …
          mIAsyncControl = TemplateDescriptor.getTemplates(emailId, mRmsAuthCallback, getTemplatesCreationCallback); } catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e) { …
      }


-    **手順 2**. 一覧の最初のテンプレートを使用して [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) を作成します。

    **ソース**: *MsipcTaskFragment.java*



      CreationCallback<UserPolicy> userPolicyCreationCallback = new CreationCallback<UserPolicy>() { @Override public Context getContext() { …
          }

          @Override
          public void onCancel()
          {
              …
          }

          @Override
          public void onFailure(ProtectionException e)
          {
              …
          }

          @Override
          public void onSuccess(final UserPolicy item)
          {
              …
          }
      }; try { …
          mIAsyncControl = UserPolicy.create((TemplateDescriptor)selectedDescriptor, mEmailId, mRmsAuthCallback, UserPolicyCreationFlags.NONE, userPolicyCreationCallback); …
      } catch (InvalidParameterException e) { …
      }


-    **手順 3**. [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx) を作成して、コンテンツを書き込みます。

    **ソース**: *MsipcTaskFragment.java*


    private void createPTxt(final byte[] contentToProtect) { …
            CreationCallback<ProtectedFileOutputStream> protectedFileOutputStreamCreationCallback = new CreationCallback<ProtectedFileOutputStream>() { @Override public Context getContext() { …
                }

                @Override
                public void onCancel()
                {
                 …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                 …
                }

                @Override
                public void onSuccess(ProtectedFileOutputStream protectedFileOutputStream)
                {
                    try
                    {
                        // write to this stream
                        protectedFileOutputStream.write(contentToProtect);
                        protectedFileOutputStream.flush();
                        protectedFileOutputStream.close();
                        …
                    }
                    catch (IOException e)
                    {
                        …
                    }
                }
            };
            try
            {
                File file = new File(filePath);
                outputStream = new FileOutputStream(file);
                mIAsyncControl = ProtectedFileOutputStream.create(outputStream, mUserPolicy, originalFileExtension,
                        protectedFileOutputStreamCreationCallback);
            }
            catch (FileNotFoundException e)
            {
                 …
            }
            catch (InvalidParameterException e)
            {
                 …
            }
        }



### <a name="scenario-open-a-custom-protected-file"></a>シナリオ: カスタム保護ファイルを開く

-   **手順 1**. *serializedContentPolicy* から [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) を作成します。

    **ソース**: *MsipcTaskFragment.java*


    CreationCallback<UserPolicy> userPolicyCreationCallbackFromSerializedContentPolicy = new CreationCallback<UserPolicy>() { @Override public void onSuccess(UserPolicy userPolicy) { …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                  …
                }

                @Override
                public void onCancel()
                {
                  …
                }

                @Override
                public Context getContext()
                {
                  …
                }
            };


    try {   ...

      // Read the serializedContentPolicyLength from the inputStream.
      long serializedContentPolicyLength = readUnsignedInt(inputStream);

      // Read the PL bytes from the input stream using the PL size.
      byte[] serializedContentPolicy = new byte[(int)serializedContentPolicyLength]; inputStream.read(serializedContentPolicy);

      ...

      UserPolicy.acquire(serializedContentPolicy, null, mRmsAuthCallback, PolicyAcquisitionFlags.NONE,           userPolicyCreationCallbackFromSerializedContentPolicy); } catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e) {   ... } catch (IOException e) {   ... }



-    **手順 2**. **手順 1** の [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) を使用して、[CustomProtectedInputStream](https://msdn.microsoft.com/library/dn758271.aspx) を作成します。

    **ソース**: *MsipcTaskFragment.java*



      CreationCallback<CustomProtectedInputStream> customProtectedInputStreamCreationCallback = new CreationCallback<CustomProtectedInputStream>() { @Override public Context getContext() { …
         }

         @Override
         public void onCancel()
         {
             …
         }

         @Override
         public void onFailure(ProtectionException e)
         {
             …
         }

         @Override
         public void onSuccess(CustomProtectedInputStream customProtectedInputStream)
         {
            …

             byte[] dataChunk = new byte[16384];
             try
             {
                 while ((nRead = customProtectedInputStream.read(dataChunk, 0, dataChunk.length)) != -1)
                 {
                      …
                 }
                  …
                 customProtectedInputStream.close();
             }
             catch (IOException e)
             {
                …
             }
             …
         }
     };

    try {  ...

      // Retrieve the encrypted content size.
      long encryptedContentLength = readUnsignedInt(inputStream);

      updateTaskStatus(new TaskStatus(TaskState.Starting, "Consuming content", true));

      CustomProtectedInputStream.create(userPolicy, inputStream,                                 encryptedContentLength,                                 customProtectedInputStreamCreationCallback); } catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e) {  ... } catch (IOException e) {  ... }


-    **手順 3**. [CustomProtectedInputStream](https://msdn.microsoft.com/library/dn758271.aspx) から *mDecryptedContent* にコンテンツを読み取り、閉じます。

    **ソース**: *MsipcTaskFragment.java*


    @Override public void onSuccess(CustomProtectedInputStream customProtectedInputStream) {  mUserPolicy = customProtectedInputStream.getUserPolicy();  ByteArrayOutputStream buffer = new ByteArrayOutputStream();

      int nRead;                      
      byte[] dataChunk = new byte[16384];

      try  {    while ((nRead = customProtectedInputStream.read(dataChunk, 0,                                                        dataChunk.length)) != -1)    {       buffer.write(dataChunk, 0, nRead);    }

        buffer.flush();    mDecryptedContent = new String(buffer.toByteArray(), Charset.forName("UTF-8"));

        buffer.close();    customProtectedInputStream.close();  }  catch (IOException e)  {    ...  } }


### <a name="scenario-create-a-custom-protected-file-using-a-custom-ad-hoc-policy"></a>シナリオ: カスタム (アドホック) ポリシーを使用してカスタム保護ファイルを作成する

-   **手順 1**: ユーザーが指定した電子メール アドレスでポリシー記述子を作成する

    **ソース**: *MsipcTaskFragment.java*

    **説明**: 実際には、次のオブジェクトは、デバイス インターフェイス [UserRights](https://msdn.microsoft.com/library/dn790911.aspx) と [PolicyDescriptor](https://msdn.microsoft.com/library/dn790843.aspx) からのユーザー入力を使用して作成されます。



      // create userRights list   UserRights userRights = new UserRights(Arrays.asList("consumer@domain.com"),     Arrays.asList( CommonRights.View, EditableDocumentRights.Print));   ArrayList<UserRights> usersRigthsList = new ArrayList<UserRights>();   usersRigthsList.add(userRights);

      // Create PolicyDescriptor using userRights list   PolicyDescriptor policyDescriptor = PolicyDescriptor.createPolicyDescriptorFromUserRights(                                                          usersRigthsList);   policyDescriptor.setOfflineCacheLifetimeInDays(10);   policyDescriptor.setContentValidUntil(new Date());



-    **手順 2**. ポリシー記述子 *selectedDescriptor* からカスタムの [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) を作成します。

    **ソース**: *MsipcTaskFragment.java*


       mIAsyncControl = UserPolicy.create((PolicyDescriptor)selectedDescriptor,                                          mEmailId, mRmsAuthCallback,                                          UserPolicyCreationFlags.NONE,                                          userPolicyCreationCallback);



-   **手順 3**. [CustomProtectedOutputStream](https://msdn.microsoft.com/library/dn758274.aspx) を作成してコンテンツを書き込み、閉じます。

    **ソース**: *MsipcTaskFragment.java*


    File file = new File(filePath); final OutputStream outputStream = new FileOutputStream(file); CreationCallback<CustomProtectedOutputStream> customProtectedOutputStreamCreationCallback = new CreationCallback<CustomProtectedOutputStream>() { @Override public Context getContext() { …
            }

            @Override
            public void onCancel()
            {
              …
            }

            @Override
            public void onFailure(ProtectionException e)
            {
              …
            }

            @Override
            public void onSuccess(CustomProtectedOutputStream protectedOutputStream)
            {
                try
                {
                    // write serializedContentPolicy
                    byte[] serializedContentPolicy = mUserPolicy.getSerializedContentPolicy();
                    writeLongAsUnsignedIntToStream(outputStream, serializedContentPolicy.length);
                    outputStream.write(serializedContentPolicy);
                    // write encrypted content
                    if (contentToProtect != null)
                    {
                        writeLongAsUnsignedIntToStream(outputStream,
                                CustomProtectedOutputStream.getEncryptedContentLength(contentToProtect.length,
                                        protectedOutputStream.getUserPolicy()));
                        protectedOutputStream.write(contentToProtect);
                        protectedOutputStream.flush();
                        protectedOutputStream.close();
                    }
                    else
                    {
                        outputStream.flush();
                        outputStream.close();
                    }
                    …
                }
                catch (IOException e)
                {
                  …
                }
            }
        };
        try
        {
            mIAsyncControl = CustomProtectedOutputStream.create(outputStream, mUserPolicy,
                    customProtectedOutputStreamCreationCallback);
        }
        catch (InvalidParameterException e)
        {
          …
        }

[!INCLUDE[Commenting house rules](../includes/houserules.md)]