---
title: iOS/OS X のコード例 | Azure RMS
description: このトピックでは、iOS/OS X バージョンの RMS SDK の重要なコード要素について説明します。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7E12EBF2-5A19-4A8D-AA99-531B09DA256A
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev, has-adal-ref
ms.openlocfilehash: 3c50c4579d32add393b680616106b37e92d2364c
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "95570654"
---
# <a name="iosos-x-code-examples"></a>iOS/OS X のコード例

[!INCLUDE [deprecation notice](../includes/deprecation-warning.md)]

このトピックでは、iOS/OS X バージョンの RMS SDK の重要なコード要素について説明します。

**注**: 以下のコード例と説明では、クライアント プロセスを参照するために MSIPC (Microsoft Information Protection and Control) という用語を使用します。



## <a name="using-the-microsoft-rights-management-sdk-42---key-scenarios"></a>Microsoft Rights Management SDK 4.2 の使用 - 主要なシナリオ


この SDK を理解するうえで重要な開発シナリオを表す大規模なサンプル アプリケーションの **Objective C** コード例を次に示します。 これらのコード例では、保護ファイルと呼ばれる Microsoft Protected File 形式の使用例、カスタム保護ファイル形式の使用例、およびカスタムの UI コントロールの使用例を示します。

### <a name="scenario-consume-an-rms-protected-file"></a>シナリオ: RMS 保護ファイルを使用する


- **手順 1**. [MSProtectedData](/previous-versions/windows/desktop/msipcthin2/msprotecteddata-interface-objc) オブジェクトを作成します。

  **説明**: [MSProtectedData](/previous-versions/windows/desktop/msipcthin2/msprotecteddata-interface-objc) オブジェクトを、その作成メソッドによりインスタンス化し、サービス認証を実装します。これには、[MSAuthenticationCallback](/previous-versions/windows/desktop/msipcthin2/msauthenticationcallback-protocol-objc) を使用し、**MSAuthenticationCallback** のインスタンスを、パラメーター *authenticationCallback* として MSIPC API に渡し、トークンを取得します。 次のコード例セクションの [MSProtectedData protectedDataWithProtectedFile](/previous-versions/windows/desktop/msipcthin2/msprotecteddata-protecteddatawithprotectedfile-completionblock-method-objc) の呼び出しを参照してください。

    ```objectivec
        + (void)consumePtxtFile:(NSString *)path authenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            // userId can be provided as a hint for authentication
            [MSProtectedData protectedDataWithProtectedFile:path
                                                 userId:nil
                                 authenticationCallback:authenticationCallback
                                                options:Default
                                        completionBlock:^(MSProtectedData *data, NSError *error)
            {
                //Read the content from the ProtectedData, this will decrypt the data
                NSData *content = [data retrieveData];
            }];
        }
    ```

- **手順 2**: Active Directory 認証ライブラリ (ADAL) を使用する認証をセットアップする

  **説明**: この手順では、例の認証パラメーターで [MSAuthenticationCallback](/previous-versions/windows/desktop/msipcthin2/msauthenticationcallback-protocol-objc) を実装するために ADAL が使用されています。 ADAL の使用の詳細については、「Azure AD Authentication Library (ADAL) (Azure AD 認証ライブラリ (ADAL))」を参照してください。

    ```objectivec
      // AuthenticationCallback holds the necessary information to retrieve an access token.
      @interface MsipcAuthenticationCallback : NSObject<MSAuthenticationCallback>

      @end

      @implementation MsipcAuthenticationCallback

      - (void)accessTokenWithAuthenticationParameters:
             (MSAuthenticationParameters *)authenticationParameters
                                    completionBlock:
             (void(^)(NSString *accessToken, NSError *error))completionBlock
      {
          ADAuthenticationError *error;
          ADAuthenticationContext* context = [
              ADAuthenticationContext authenticationContextWithAuthority:authenticationParameters.authority
                                                                error:&error
          ];
          NSString *appClientId = @"com.microsoft.sampleapp";
          NSURL *redirectURI = [NSURL URLWithString:@"local://authorize"];
          // Retrieve token using ADAL
          [context acquireTokenWithResource:authenticationParameters.resource
                                 clientId:appClientId
                              redirectUri:redirectURI
                                   userId:authenticationParameters.userId
                          completionBlock:^(ADAuthenticationResult *result) {
                              if (result.status != AD_SUCCEEDED)
                              {
                                  NSLog(@"Auth Failed");
                                  completionBlock(nil, result.error);
                              }
                              else
                              {
                                  completionBlock(result.accessToken, result.error);
                              }
                          }];
       }
    ```

- **手順 3**. [MSUserPolicy](/previous-versions/windows/desktop/msipcthin2/msuserpolicy-interface-objc) オブジェクトの [MSUserPolicy accessCheck](/previous-versions/windows/desktop/msipcthin2/msuserpolicy-accesscheck-method-objc) メソッドを呼び出して、このユーザーにこのコンテンツの編集権限があるかどうかを確認します。

    ```objectivec
      - (void)accessCheckWithProtectedData:(MSProtectedData *)protectedData
      {
          //check if user has edit rights and apply enforcements
          if (!protectedData.userPolicy.accessCheck(EditableDocumentRights.Edit))
          {
              // enforce on the UI
              textEditor.focusableInTouchMode = NO;
              textEditor.focusable = NO;
              textEditor.enabled = NO;
          }
      }
    ```

### <a name="scenario-create-a-new-protected-file-using-a-template"></a>シナリオ: テンプレートを使用して新しい保護ファイルを作成する

このシナリオは、初めにテンプレートの一覧 [MSTemplateDescriptor](/previous-versions/windows/desktop/msipcthin2/mstemplatedescriptor-interface-objc) を取得し、最初の 1 つを選択してポリシーを作成してから、新しい保護ファイルを作成して書き込みます。

-   **手順 1**. テンプレートの一覧を取得します。

    ```objectivec
        + (void)templateListUsageWithAuthenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            [MSTemplateDescriptor templateListWithUserId:@"user@domain.com"
                            authenticationCallback:authenticationCallback
                                   completionBlock:^(NSArray/*MSTemplateDescriptor*/ *templates, NSError *error)
                                   {
                                     // use templates array of MSTemplateDescriptor (Note: will be nil on error)
                                   }];
        }
    ```

-   **手順 2**. 一覧の最初のテンプレートを使用して [MSUserPolicy](/previous-versions/windows/desktop/msipcthin2/msuserpolicy-interface-objc) を作成します。

    ```objectivec
        + (void)userPolicyCreationFromTemplateWithAuthenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            [MSUserPolicy userPolicyWithTemplateDescriptor:[templates objectAtIndex:0]
                                            userId:@"user@domain.com"
                                     signedAppData:nil
                            authenticationCallback:authenticationCallback
                                           options:None
                                   completionBlock:^(MSUserPolicy *userPolicy, NSError *error)
            {
            // use userPolicy (Note: will be nil on error)
            }];
        }
    ```

-   **手順 3**. [MSMutableProtectedData](/previous-versions/windows/desktop/msipcthin2/msmutableprotecteddata-interface-objc) を作成し、コンテンツを書き込みます。

    ```objectivec
        + (void)createPtxtWithUserPolicy:(MSUserPolicy *)userPolicy contentToProtect:(NSData *)contentToProtect
        {
            // create an MSMutableProtectedData to write content
            [contentToProtect protectedDataInFile:filePath
                        originalFileExtension:kDefaultTextFileExtension
                               withUserPolicy:userPolicy
                              completionBlock:^(MSMutableProtectedData *data, NSError *error)
            {
             // use data (Note: will be nil on error)
            }];
        }
    ```

### <a name="scenario-open-a-custom-protected-file"></a>シナリオ: カスタム保護ファイルを開く


-   **手順 1**. *serializedContentPolicy* から [MSUserPolicy](/previous-versions/windows/desktop/msipcthin2/msuserpolicy-interface-objc) を作成します。

    ```objectivec
        + (void)userPolicyWith:(NSData *)protectedData
        authenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            // Read header information from protectedData and extract the  PL
            /*-------------------------------------------
            | PL length | PL | ContetSizeLength |
            -------------------------------------------*/
            NSUInteger serializedPolicySize;
            NSMutableData *serializedPolicy;
            [protectedData getBytes:&serializedPolicySize length:sizeof(serializedPolicySize)];
            [protectedData getBytes:[serializedPolicy mutableBytes] length:serializedPolicySize];

            // Get the user policy , this is an async method as it hits the REST service
            // for content key and usage restrictions
            // userId provided as a hint for authentication
            [MSUserPolicy userPolicyWithSerializedPolicy:serializedPolicy
                                              userId:@"user@domain.com"
                              authenticationCallback:authenticationCallback
                                             options:Default
                                     completionBlock:^(MSUserPolicy *userPolicy,
                                                       NSError *error)
            {

            }];
         }
    ```

-   **手順 2**. **手順 1** の [MSUserPolicy](/previous-versions/windows/desktop/msipcthin2/msuserpolicy-interface-objc) を使用して [MSCustomProtectedData](/previous-versions/windows/desktop/msipcthin2/msmutablecustomprotecteddata-interface-objc) を作成し、読み取りを行います。

    ```objectivec
        + (void)customProtectedDataWith:(NSData *)protectedData
        {
            // Read header information from protectedData and extract the  protectedContentSize
            /*-------------------------------------------
            | PL length | PL | ContetSizeLength |
            -------------------------------------------*/
            NSUInteger protectedContentSize;
            [protectedData getBytes:&protectedContentSize
                         length:sizeof(protectedContentSize)];

            // Create the MSCustomProtector used for decrypting the content
            // The content start position is the header length
            [MSCustomProtectedData customProtectedDataWithPolicy:userPolicy
                                               protectedData:protectedData
                                        contentStartPosition:sizeof(NSUInteger) + serializedPolicySize
                                                 contentSize:protectedContentSize
                                             completionBlock:^(MSCustomProtectedData *customProtector,
                                                               NSError *error)
            {
             //Read the content from the custom protector, this will decrypt the data
             NSData *content = [customProtector retrieveData];
             NSLog(@"%@", content);
            }];
         }
    ```

### <a name="scenario-create-a-custom-protected-file-using-a-custom-ad-hoc-policy"></a>シナリオ: カスタム (アドホック) ポリシーを使用してカスタム保護ファイルを作成する


-   **手順 1**. ユーザーが指定した電子メール アドレスでポリシー記述子を作成します。

    **説明**: 実際には、次のオブジェクトは、デバイス インターフェイス [MSUserRights](/previous-versions/windows/desktop/msipcthin2/msuserrights-interface-objc) と [MSPolicyDescriptor](/previous-versions/windows/desktop/msipcthin2/mspolicydescriptor-interface-objc) からのユーザー入力を使用して作成されます。

    ```objectivec
        + (void)policyDescriptor
        {
            MSUserRights *userRights = [[MSUserRights alloc] initWithUsers:[NSArray arrayWithObjects: @"user1@domain.com", @"user2@domain.com", nil] rights:[MSEmailRights all]];

            MSPolicyDescriptor *policyDescriptor = [[MSPolicyDescriptor alloc] initWithUserRights:[NSArray arrayWithObjects:userRights, nil]];
            policyDescriptor.contentValidUntil = [[NSDate alloc] initWithTimeIntervalSinceNow:NSTimeIntervalSince1970 + 3600.0];
            policyDescriptor.offlineCacheLifetimeInDays = 10;
        }
    ```

-   **手順 2**. ポリシー記述子 *selectedDescriptor* からカスタムの [MSUserPolicy](/previous-versions/windows/desktop/msipcthin2/msuserpolicy-interface-objc) を作成します。

    ```objectivec
        + (void)userPolicyWithPolicyDescriptor:(MSPolicyDescriptor *)policyDescriptor
        {
            [MSUserPolicy userPolicyWithPolicyDescriptor:policyDescriptor
                                          userId:@"user@domain.com"
                          authenticationCallback:authenticationCallback
                                         options:None
                                 completionBlock:^(MSUserPolicy *userPolicy, NSError *error)
            {
              // use userPolicy (Note: will be nil on error)
            }];
        }
    ```

-   **手順 3**. [MSMutableCustomProtectedData](/previous-versions/windows/desktop/msipcthin2/msmutablecustomprotecteddata-interface-objc) を作成してコンテンツを書き込み、閉じます。

    ```objectivec
        + (void)mutableCustomProtectedData:(NSMutableData *)backingData policy:(MSUserPolicy *)policy contentToProtect:(NSString *)contentToProtect
        {
            //Get the serializedPolicy from a given policy
            NSData *serializedPolicy = [policy serializedPolicy];

            // Write header information to backing data including the PL
            // ------------------------------------
            // | PL length | PL | ContetSizeLength |
            // -------------------------------------
            NSUInteger serializedPolicyLength = [serializedPolicy length];
            [backingData appendData:[NSData dataWithBytes:&serializedPolicyLength length:sizeof(serializedPolicyLength)]];
            [backingData appendData:serializedPolicy];
            NSUInteger protectedContentLength = [MSCustomProtectedData getEncryptedContentLengthWithPolicy:policy contentLength:unprotectedData.length];
            [backingData appendData:[NSData dataWithBytes:&protectedContentLength length:sizeof(protectedContentLength)]];

            NSUInteger headerLength = sizeof(serializedPolicyLength) + serializedPolicyLength + sizeof(protectedContentLength);

            // Create the MSMutableCustomProtector used for encrypting content
            // The content start position is the current length of the backing data
            // The encryptedContentSize content size is 0 since there is no content yet
            [MSMutableCustomProtectedData customProtectorWithUserPolicy:policy
                                                        backingData:backingData
                                             protectedContentOffset:headerLength
                                                    completionBlock:^(MSMutableCustomProtectedData *customProtector,
                                                                      NSError *error)
            {
                //Append data to the custom protector, this will encrypt the data and write it to the backing data
                [customProtector appendData:[contentToProtect dataUsingEncoding:NSUTF8StringEncoding] error:&error];

                //close the custom protector so it will flush and finalise encryption
                [customProtector close:&error];

            }];
          }
    ```