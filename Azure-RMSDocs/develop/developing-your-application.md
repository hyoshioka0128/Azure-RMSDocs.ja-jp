---
title: アプリケーションの開発 - AIP
description: AIP によるドキュメントの保護を実装する基本的なコンソール アプリのガイダンスです。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 07/03/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.custom: dev, has-adal-ref
ms.openlocfilehash: 841669b3db3e86e2ea6f1860a9d8e9d915c4d28d
ms.sourcegitcommit: dc50f9a6c2f66544893278a7fd16dff38eef88c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/18/2020
ms.locfileid: "88564245"
---
# <a name="developing-your-application"></a>アプリケーションの開発

この例では、Azure Information Protection サービス (AIP) と連携する簡単なコンソール アプリケーションを作成します。  保護するドキュメントのパスを入力し、アドホック ポリシーまたは Azure テンプレートを使用してドキュメントを保護する手順を説明します。 アプリケーションは入力に従って正しいポリシーを適用し、情報が保護されたドキュメントを作成します。 使用するサンプル コードは、[Azure IP テスト アプリケーション](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/AzureIP_Test)および Github を参照してください。

## <a name="sample-app-prerequisites"></a>サンプル アプリの前提条件
- **オペレーティング システム**: Windows 10、Windows 8、Windows 7、Windows Server 2008、Windows Server 2008 R2、Windows Server 2012 のいずれか
- **プログラミング言語**: C# (.NET Framework 3.0 以降)
- **開発環境**: Visual Studio 2015 (およびそれ以降)

## <a name="setting-up-your-azure-configuration"></a>Azure 構成のセットアップ

このアプリ用に Azure をセットアップするには、テナント ID、対称キー、およびアプリケーションのプリンシパル ID を作成する必要があります。

### <a name="azure-ad-tenant-configuration"></a>Azure AD テナントの構成

Azure Information Protection の Azure AD 環境を構成するには、 [Azure Information Protection からの保護サービスのアクティブ化](https://docs.microsoft.com/information-protection/deploy-use/activate-service)に関するガイダンスに従ってください。

サービスをアクティブにすると、次の手順で PowerShell コンポーネントが必要になります。 [PowerShell を使用した Azure Information Protection からの保護の管理](https://docs.microsoft.com/information-protection/deploy-use/administer-powershell)については、こちらを参照してください。

### <a name="getting-your-tenant-id"></a>テナント ID を取得する

- 管理者として PowerShell を実行します。
- RMS モジュールをインポートします: `Import-Module AIPService`
- 割り当てられたユーザーの資格情報でサービスに接続します: `Connect-AipService –Verbose`
- RMS が有効になっていることを確認します: `enable-aipservice`
- `Get-AipServiceConfiguration` を実行してテナント ID を取得します。

>BPOS ID (テナント ID) 値を記録します。 後の手順で必要になります。

*出力例* 
 ![コマンドレットの出力](../media/develop/output-of-Get-AadrmConfiguration.png)

- サービスから切断します: `Disconnect-AipServiceService`

### <a name="create-a-service-principal"></a>サービス プリンシパルの作成
サービス プリンシパルを作成するには、次の手順に従います。
> サービス プリンシパルは、アクセス制御のためにグローバルに構成された資格情報です。サービス プリンシパルを使用するサービスでは、Microsoft Azure AD による認証および Microsoft Azure AD Rights Management を使用した情報の保護が可能になります。

- 管理者として PowerShell を実行します。
- `Import-Module MSOnline` を使用して Microsoft Azure AD モジュールをインポートします。
- 割り当てられたユーザーの資格情報でオンライン サービスに接続します: `Connect-MsolService`
- `New-MsolServicePrincipal` を実行して、新しいサービス プリンシパルを作成します。
- サービス プリンシパルの名前を入力します。
  > 後で使用するために、対称キーとアプリケーションのプリンシパル ID を記録します。

*出力例* 
 ![コマンドレットの出力](../media/develop/output-of-NewMsolServicePrincipal.png)

- アプリケーションのプリンシパル ID、対称キー、およびテナント ID をアプリケーションの App.config ファイルに追加します。

*App.config ファイル* 
 ![ の例コマンドレットの出力](../media/develop/example-App.config-file.png)

- *ClientID* と *RedirectUri* は、Azure にアプリケーションを登録したときに入手できます。 Azure にアプリケーションを登録する方法、および *ClientID* と *RedirectUri* の取得方法の詳細については、「[Azure RMS の ADAL 認証を構成する](adal-auth.md)」を参照してください。


## <a name="design-summary"></a>設計の概要
次の図は、作成するアプリのアーキテクチャとプロセス フローを示しています。図の下には手順を示しています。
![設計の概要](../media/develop/design-summary.png)

1. ユーザーは次を入力します。
   - 保護されるファイルのパス。
   - テンプレートを選択するか、またはアドホック ポリシーを作成します。
2. アプリケーションが AIP による認証を要求します。
3. AIP が認証を確認します。
4. アプリケーションが AIP のテンプレートを要求します。
5. AIP が事前に定義されたテンプレートを返します。
6. アプリケーションは、指定された場所の指定されたファイルを検索します。
7. アプリケーションは、そのファイルに AIP 保護ポリシーを適用します。

## <a name="how-the-code-works"></a>コードの動作

サンプルでは、Iprotect.cs ファイルを使用してソリューションの Azure IP テストを開始します。 Azure IP テストは C# コンソール アプリケーションであり、他の AIP 対応アプリケーションと同様に、`main()` メソッドで示されるように *MSIPC.dll* の読み込みで開始します。

```csharp
//Loads MSIPC.dll
SafeNativeMethods.IpcInitialize();
SafeNativeMethods.IpcSetAPIMode(APIMode.Server);
```

Azure への接続に必要なパラメーターを読み込みます。

```csharp
//Loads credentials for the service principal from App.Config
SymmetricKeyCredential symmetricKeyCred = new SymmetricKeyCredential();
symmetricKeyCred.AppPrincipalId = ConfigurationManager.AppSettings["AppPrincipalId"];
symmetricKeyCred.Base64Key = ConfigurationManager.AppSettings["Base64Key"];
symmetricKeyCred.BposTenantId = ConfigurationManager.AppSettings["BposTenantId"];
```

コンソール アプリケーションにファイルのパスを入力すると、アプリケーションはドキュメントが既に暗号化されているかどうかを確認します。 このメソッドは **SafeFileApiNativeMethods** クラスです。

```csharp
var checkEncryptionStatus = SafeFileApiNativeMethods.IpcfIsFileEncrypted(filePath);
```

ドキュメントが暗号化されていない場合は、プロンプトで入力された選択に従ってドキュメントの暗号化処理が行われます。

```csharp
if (!checkEncryptionStatus.ToString().ToLower().Contains(alreadyEncrypted))
{
  if (method == EncryptionMethod1)
  {
    //Encrypt a file via AIP template
    ProtectWithTemplate(symmetricKeyCred, filePath);

  }
  else if (method == EncryptionMethod2)
  {
    //Encrypt a file using ad-hoc policy
    ProtectWithAdHocPolicy(symmetricKeyCred, filePath);
  }
}
```

テンプレート オプションによる保護では、サーバーからテンプレートの一覧が取得され、選択するオプションがユーザーに提供されます。
>テンプレートを変更していない場合は、AIP から既定のテンプレートを取得します。

```csharp
public static void ProtectWithTemplate(SymmetricKeyCredential symmetricKeyCredential, string filePath)
{
  // Gets the available templates for this tenant
  Collection<TemplateInfo> templates = SafeNativeMethods.IpcGetTemplateList(null, false, true,
      false, true, null, null, symmetricKeyCredential);

  //Requests tenant template to use for encryption
  Console.WriteLine("Please select the template you would like to use to encrypt the file.");

  //Outputs templates available for selection
  int counter = 0;
  for (int i = 0; i < templates.Count; i++)
  {
    counter++;
    Console.WriteLine(counter + ". " + templates.ElementAt(i).Name + "\n" +
        templates.ElementAt(i).Description);
  }

  //Parses template selection
  string input = Console.ReadLine();
  int templateSelection;
  bool parseResult = Int32.TryParse(input, out templateSelection);

  //Returns error if no template selection is entered
  if (parseResult)
  {
    //Ensures template value entered is valid
    if (0 < templateSelection && templateSelection <= counter)
    {
      templateSelection -= templateSelection;

      // Encrypts the file using the selected template
      TemplateInfo selectedTemplateInfo = templates.ElementAt(templateSelection);

      string encryptedFilePath = SafeFileApiNativeMethods.IpcfEncryptFile(filePath,
          selectedTemplateInfo.TemplateId,
          SafeFileApiNativeMethods.EncryptFlags.IPCF_EF_FLAG_KEY_NO_PERSIST, true, false, true, null,
          symmetricKeyCredential);
    }
  }
}
```

アドホック ポリシーを選択した場合、アプリケーションのユーザーは権限を持つユーザーのメール アドレスを入力する必要があります。 このセクションでは、**IpcCreateLicenseFromScratch()** メソッドを使用し、テンプレートに新しいポリシーを適用してライセンスが作成されます。

```csharp
if (issuerDisplayName.Trim() != "")
{
  // Gets the available issuers of rights policy templates.
  // The available issuers is a list of RMS servers that this user has already contacted.
  try
  {
    Collection<TemplateIssuer> templateIssuers = SafeNativeMethods.IpcGetTemplateIssuerList(
                                                    null,
                                                    true,
                                                    false,
                                                    false, true, null, symmetricKeyCredential);

    // Creates the policy and associates the chosen user rights with it
    SafeInformationProtectionLicenseHandle handle = SafeNativeMethods.IpcCreateLicenseFromScratch(
                                                        templateIssuers.ElementAt(0));
    SafeNativeMethods.IpcSetLicenseOwner(handle, owner);
    SafeNativeMethods.IpcSetLicenseUserRightsList(handle, userRights);
    SafeNativeMethods.IpcSetLicenseDescriptor(handle, new TemplateInfo(null, CultureInfo.CurrentCulture,
                                                            policyName,
                                                            policyDescription,
                                                            issuerDisplayName,
                                                            false));

    //Encrypts the file using the ad hoc policy
    string encryptedFilePath = SafeFileApiNativeMethods.IpcfEncryptFile(
                                    filePath,
                                    handle,
                                    SafeFileApiNativeMethods.EncryptFlags.IPCF_EF_FLAG_KEY_NO_PERSIST,
                                    true,
                                    false,
                                    true,
                                    null,
                                    symmetricKeyCredential);
    }
}
```

## <a name="user-interaction-example"></a>ユーザー操作の例

すべて作成して実行すると、アプリケーションの出力は次のようになります。

1. 暗号化方法を選択するように求められます。
   ![アプリの出力 - 手順 1](../media/develop/app-output-1.png)

2. 保護されるファイルのパスを入力するよう求められます。
   ![アプリの出力 - 手順 2](../media/develop/app-output-2.png)

3. ライセンス所有者のメール アドレスを入力するよう求められます (この所有者は、Azure AD テナントでグローバル管理者の権限を持つ必要があります)。
   ![アプリの出力 - 手順 3](../media/develop/app-output-3.png)

4. ファイルへのアクセス権を持つユーザーのメール アドレスを入力します (メール アドレスはスペースで区切る必要があります)。
   ![アプリの出力 - 手順 4](../media/develop/app-output-4.png)

5. 承認されたユーザーに与えられる権限の一覧から選択します。
   ![アプリの出力 - 手順 5](../media/develop/app-output-5.png)

6. 最後に、ポリシーのメタデータの一部 (ポリシー名、説明、発行者 (Azure AD テナント) の表示名) を入力します。![アプリの出力 - 手順 6](../media/develop/app-output-6.png)
