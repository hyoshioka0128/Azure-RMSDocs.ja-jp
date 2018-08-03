---
title: iOS/OS X のコード例 | Azure RMS
description: このトピックでは、iOS/OS X バージョンの RMS SDK の重要なコード要素について説明します。
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7E12EBF2-5A19-4A8D-AA99-531B09DA256A
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: c57b825146b209a688133ce79e421bbf78670200
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2018
ms.locfileid: "39375336"
---
# <a name="iosos-x-code-examples"></a>iOS/OS X のコード例

このトピックでは、iOS/OS X バージョンの RMS SDK の重要なコード要素について説明します。

**注**: 以下のコード例と説明では、クライアント プロセスを参照するために MSIPC (Microsoft Information Protection and Control) という用語を使用します。



## <a name="using-the-microsoft-rights-management-sdk-42---key-scenarios"></a>Microsoft Rights Management SDK 4.2 の使用 - 主要なシナリオ


この SDK を理解するうえで重要な開発シナリオを表す大規模なサンプル アプリケーションの **Objective C** コード例を次に示します。 これらのコード例では、保護ファイルと呼ばれる Microsoft Protected File 形式の使用例、カスタム保護ファイル形式の使用例、およびカスタムの UI コントロールの使用例を示します。

### <a name="scenario-consume-an-rms-protected-file"></a>シナリオ: RMS 保護ファイルを使用する


- **手順 1**. [MSProtectedData](https://msdn.microsoft.com/library/dn758348.aspx) オブジェクトを作成します。

 **説明**: [MSProtectedData](https://msdn.microsoft.com/library/dn758348.aspx) オブジェクトを、その作成メソッドによりインスタンス化し、サービス認証を実装します。これには、[MSAuthenticationCallback](https://msdn.microsoft.com/library/dn758312.aspx) を使用し、**MSAuthenticationCallback** のインスタンスを、パラメーター *authenticationCallback* として MSIPC API に渡し、トークンを取得します。 次のコード例セクションの [MSProtectedData protectedDataWithProtectedFile](https://msdn.microsoft.com/library/dn758351.aspx) の呼び出しを参照してください。

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

- **手順 2**. Active Directory 認証ライブラリ (ADAL) を使用して認証をセットアップします。

  **説明**: この手順では、例の認証パラメーターで [MSAuthenticationCallback](https://msdn.microsoft.com/library/dn758312.aspx) を実装するために ADAL が使用されています。 ADAL の使用の詳細については、「Azure AD Authentication Library (ADAL) (Azure AD 認証ライブラリ (ADAL))」を参照してください。

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
          NSString *appClientId = @”com.microsoft.sampleapp”;
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

-   **手順 3**. [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx) オブジェクトの [MSUserPolicy accessCheck](https://msdn.microsoft.com/library/dn790789.aspx) メソッドを呼び出して、このユーザーにこのコンテンツの編集権限があるかどうかを確認します。

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

### <a name="scenario-create-a-new-protected-file-using-a-template"></a>シナリオ: テンプレートを使用して新しい保護ファイルを作成する

このシナリオは、初めにテンプレートの一覧 [MSTemplateDescriptor](https://msdn.microsoft.com/library/dn790785.aspx) を取得し、最初の 1 つを選択してポリシーを作成してから、新しい保護ファイルを作成して書き込みます。

-   **手順 1**. テンプレートの一覧を取得します。

        + (void)templateListUsageWithAuthenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            [MSTemplateDescriptor templateListWithUserId:@"user@domain.com"
                            authenticationCallback:authenticationCallback
                                   completionBlock:^(NSArray/*MSTemplateDescriptor*/ *templates, NSError *error)
                                   {
                                     // use templates array of MSTemplateDescriptor (Note: will be nil on error)
                                   }];
        }

-   **手順 2**. 一覧の最初のテンプレートを使用して [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx) を作成します。

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

-   **手順 3**. [MSMutableProtectedData](https://msdn.microsoft.com/library/dn758325.aspx) を作成し、コンテンツを書き込みます。

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

### <a name="scenario-open-a-custom-protected-file"></a>シナリオ: カスタム保護ファイルを開く


-   **手順 1**. *serializedContentPolicy* から [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx) を作成します。

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

-   **手順 2**. **手順 1** の [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx) を使用して [MSCustomProtectedData](https://msdn.microsoft.com/library/dn758321.aspx) を作成し、読み取りを行います。

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

### <a name="scenario-create-a-custom-protected-file-using-a-custom-ad-hoc-policy"></a>シナリオ: カスタム (アドホック) ポリシーを使用してカスタム保護ファイルを作成する


-   **手順 1**: ユーザーが指定した電子メール アドレスでポリシー記述子を作成する

    **説明**: 実際には、次のオブジェクトは、デバイス インターフェイス [MSUserRights](https://msdn.microsoft.com/library/dn790811.aspx) と [MSPolicyDescriptor](https://msdn.microsoft.com/library/dn758339.aspx) からのユーザー入力を使用して作成されます。

        + (void)policyDescriptor
        {
            MSUserRights *userRights = [[MSUserRights alloc] initWithUsers:[NSArray arrayWithObjects: @"user1@domain.com", @"user2@domain.com", nil] rights:[MSEmailRights all]];

            MSPolicyDescriptor *policyDescriptor = [[MSPolicyDescriptor alloc] initWithUserRights:[NSArray arrayWithObjects:userRights, nil]];
            policyDescriptor.contentValidUntil = [[NSDate alloc] initWithTimeIntervalSinceNow:NSTimeIntervalSince1970 + 3600.0];
            policyDescriptor.offlineCacheLifetimeInDays = 10;
        }

-   **手順 2**. ポリシー記述子 *selectedDescriptor* からカスタムの [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx) を作成します。

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

-   **手順 3**. [MSMutableCustomProtectedData](https://msdn.microsoft.com/library/dn758321.aspx) を作成してコンテンツを書き込み、閉じます。

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
