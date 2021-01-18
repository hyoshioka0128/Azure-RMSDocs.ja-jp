---
title: Azure Information Protection 統合されたラベル付けクライアントで PowerShell を使用する
description: 管理者が PowerShell を使用して Azure Information Protection 統合されたラベル付けクライアントを管理するための手順と情報です。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 01/14/2021
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 60f9493601d40b17c42354dae2d3978b8cb5972b
ms.sourcegitcommit: af7ac2eeb8f103402c0036dd461c77911fbc9877
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/18/2021
ms.locfileid: "98560069"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>管理者ガイド: Azure Information Protection 統合クライアントでの PowerShell の使用

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8、Windows Server 2019、Windows Server 2016、windows Server 2012 R2、windows server 2012 *
>
>*Windows 7 または Office 2010 を使用している場合は、「 [AIP and Legacy Windows And office versions](../known-issues.md#aip-and-legacy-windows-and-office-versions)」を参照してください。*
>
>***関連**: [Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)ます。 従来のクライアントについては、「 [従来のクライアント管理者ガイド](client-admin-guide-powershell.md)」を参照してください。

Azure Information Protection 統合ラベル付けクライアントをインストールすると、PowerShell コマンドが [Azureinformationprotection](/powershell/module/azureinformationprotection) モジュールの一部として自動的にインストールされ、ラベル付け用のコマンドレットが使用されます。 

**Azureinformationprotection** モジュールを使用すると、オートメーションスクリプトのコマンドを実行してクライアントを管理できます。

次に例を示します。

- [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus): 指定したファイルまたはファイルの Azure Information Protection ラベルと保護情報を取得します。
- [Set-aipfileclassification](/powershell/module/azureinformationprotection/set-aipfileclassification): ポリシーで構成されている条件に従って、ファイルをスキャンして、ファイルの Azure Information Protection ラベルを自動的に設定します。
- [Set-aipfilelabel](/powershell/module/azureinformationprotection/set-aipfilelabel): ファイルの Azure Information Protection ラベルを設定または削除し、ラベル構成またはカスタムアクセス許可に従って保護を設定または削除します。
- [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication): Azure Information Protection クライアントの認証資格情報を設定します。

**Azureinformationprotection** モジュールは、 **\ProgramFiles (x86) \Microsoft Azure Information Protection** フォルダーにインストールされた後、このフォルダーを **PSModulePath** システム変数に追加します。 このモジュールの .dll の名前は **AIP.dll** です。

> [!IMPORTANT]
> **Azureinformationprotection** モジュールは、ラベルまたはラベルポリシーの詳細設定の構成をサポートしていません。 
>
>これらの設定には、Office 365 セキュリティ & コンプライアンスセンターの PowerShell が必要です。 詳細については、「 [Azure Information Protection の統合ラベル付けクライアントのカスタム構成](clientv2-admin-guide-customizations.md)」を参照してください。

> [!TIP]
> 260 文字よりも長いパスとともにコマンドレットを使用するには、Windows 10 バージョン 1607 以降で利用できる次の[グループ ポリシー設定](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)を使用します。<br /> **ローカルコンピューターポリシー**  > **コンピューターの構成**  > **管理用テンプレート**  > **すべての設定**  > **Win32 長いパスを有効にする** 
> 
> Windows Server 2016 の場合、Windows 10 用の最新の管理用テンプレート (.admx) をインストールすれば、同じグループ ポリシー設定を使用できます。
>
> 詳しくは、Windows 10 開発者向けドキュメントの「[Maximum Path Length Limitation (パスの最大長の制限)](/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation)」をご覧ください。

## <a name="prerequisites-for-using-the-azureinformationprotection-module"></a>AzureInformationProtection モジュールを使用するための前提条件

**Azureinformationprotection** モジュールをインストールするための前提条件に加えて、Azure Information Protection のラベル付けコマンドレットを使用する場合は、次のような追加の前提条件があります。

- **Azure Rights Management サービスをアクティブ化する必要があり** ます。

    Azure Information Protection テナントがアクティブ化されていない場合は、 [Azure Information Protection から保護サービスをアクティブ化](../activate-service.md)するための手順を参照してください。

- **自分のアカウントを使用して他のユーザーのファイルから保護を削除するに** は:

    - [スーパーユーザー](../configure-super-users.md)機能が組織で有効になっている必要があります。
    - アカウントは、Azure Rights Management のスーパーユーザーとして構成されている必要があります。

    たとえば、データの検出または回復のために、他のユーザーの保護を削除することができます。 ラベルを使用して保護を適用している場合は、保護を適用しない新しいラベルを設定することによって保護を削除できます。または、ラベルを削除することもできます。

    保護を削除するには、 [set-aipfilelabel](/powershell/module/azureinformationprotection/set-aipfilelabel) コマンドレットと *removeprotection* パラメーターを使用します。 保護の削除機能は既定で無効になっているため、まず、 [LabelPolicy](/powershell/module/azureinformationprotection/set-labelpolicy) コマンドレットを使用して有効にする必要があります。

## <a name="rms-to-unified-labeling-cmdlet-mapping"></a>RMS と統合されたラベル付けコマンドレットのマッピング

Azure RMS から移行した場合、RMS 関連のコマンドレットは、統合されたラベル付けで使用するために非推奨とされます。 

従来のコマンドレットの一部は、ラベル付けのための新しいコマンドレットに置き換えられました。 たとえば、 **RMSProtectionLicense** を RMS 保護と共に使用し、統合されたラベルに移行した場合は、代わりに **新しい-AIPCustomPermissions** を使用します。

次の表は、RMS 関連のコマンドレットと、統合されたラベル付けに使用される更新されたコマンドレットを示しています。

|RMS コマンドレット  |統一されたラベル付けコマンドレット  |
|---------|---------|
|[も get-rmsfilestatus](/powershell/module/azureinformationprotection/get-rmsfilestatus)     |  [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)        |
|[RMSServer](/powershell/module/azureinformationprotection/get-rmsserver)     |  統一されたラベル付けには関係ありません。      |
|[Set-rmsserverauthentication](/powershell/module/azureinformationprotection/get-rmsserverauthentication)      |   [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)       |
|[RMSAuthentication](/powershell/module/azureinformationprotection/clear-rmsauthentication)     | [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)       |
|[Set-RMSServerAuthentication](/powershell/module/azureinformationprotection/set-rmsserverauthentication)     |  [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)      |
|[Get-rmstemplate](/powershell/module/azureinformationprotection/get-rmstemplate)     |       ラベルの統合には関係ありません  |
|[RMSProtectionLicense](/powershell/module/azureinformationprotection/new-rmsprotectionlicense)     |  **Custompermissions** パラメーターを指定した [新しい-AIPCustomPermissions](/powershell/module/azureinformationprotection/new-aipcustompermissions)および [set-aipfilelabel](/powershell/module/azureinformationprotection/set-aipfilelabel)      |
|[保護-Protect-rmsfile](/powershell/module/azureinformationprotection/protect-rmsfile) |**Removeprotection** パラメーターを指定して [set-aipfilelabel を設定](/powershell/module/azureinformationprotection/set-aipfilelabel)する |
| | |


## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>非対話形式でファイルに Azure Information Protection のラベル付けをする方法

既定では、ラベル付けのコマンドレットを実行するとき、対話型 PowerShell セッション内のユーザー コンテキストでコマンドは動作します。

詳細については次を参照してください:

- [AIP ラベル付けコマンドレットを無人で実行するための前提条件](#prerequisites-for-running-aip-labeling-cmdlets-unattended)
- [Azure AD アプリケーションを作成して設定する-AIPAuthentication](#create-and-configure-azure-ad-applications-for-set-aipauthentication)
- [Set-AIPAuthentication コマンドレットの実行](#running-the-set-aipauthentication-cmdlet)

> [!NOTE]
> コンピューターがインターネットにアクセスできない場合は、Azure AD でアプリを作成し、 **Set AIPAuthentication** コマンドレットを実行する必要はありません。 代わりに、切断された [コンピューター](clientv2-admin-guide-customizations.md#support-for-disconnected-computers)の指示に従います。  

### <a name="prerequisites-for-running-aip-labeling-cmdlets-unattended"></a>AIP ラベル付けコマンドレットを無人で実行するための前提条件

コマンドレットの Azure Information Protection を無人で実行するには、次のアクセスの詳細を使用します。

- 対話形式でサインインできる **Windows アカウント**。

- 委任されたアクセスのための **Azure AD アカウント**。 管理を容易にするために、Active Directory から Azure AD に同期される1つのアカウントを使用します。

    委任されたユーザーアカウントの場合:

    |要件  |詳細  |
    |---------|---------|
    |**ラベルポリシー**     |  このアカウントにラベルポリシーが割り当てられていること、および使用する公開されたラベルがポリシーに含まれていることを確認してください。   <br><br>異なるユーザーにラベルポリシーを使用する場合は、すべてのラベルを発行する新しいラベルポリシーを作成し、この委任されたユーザーアカウントのみにポリシーを発行する必要がある場合があります。    |
    |**コンテンツの復号化**     |    このアカウントでコンテンツの暗号化を解除する必要がある場合 (たとえば、ファイルを再保護し、他のユーザーが保護しているファイルを検査する場合) は、Azure Information Protection の [スーパーユーザー](../configure-super-users.md) にして、スーパーユーザー機能が有効になっていることを確認してください。     |
    |**オンボードコントロール**     |    段階的展開の [オンボードコントロール](../activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) を実装している場合は、構成したオンボードコントロールにこのアカウントが含まれていることを確認してください。     |
    |     |         |

- **Azure AD アクセストークン**。 Azure Information Protection に対して認証するために、委任されたユーザーの資格情報を設定して格納します。 Azure AD のトークンの有効期限が切れた場合、新しいトークンを取得するには、もう一度コマンドレットを実行する必要があります。 

    **Set-AIPAuthentication** のパラメーターは、Azure AD のアプリ登録プロセスの値を使用します。 詳細については、「 [Set-AIPAuthentication の Azure AD アプリケーションの作成と構成](#create-and-configure-azure-ad-applications-for-set-aipauthentication)」を参照してください。

最初に [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) コマンドレットを実行して、ラベル付けのコマンドレットを非対話形式で実行します。

**Aipauthentication** コマンドレットを実行しているコンピューターは、ラベル付け管理センター内の委任されたユーザーアカウントに割り当てられているラベル付けポリシーをダウンロードします (Microsoft 365 セキュリティ & コンプライアンスセンターなど)。

### <a name="create-and-configure-azure-ad-applications-for-set-aipauthentication"></a>Set-AIPAuthentication 用の Azure AD アプリケーションの作成と構成

**Set AIPAuthentication** コマンドレットを使用するには、 *AppId* と *appsecret* パラメーターのアプリ登録が必要です。 

クラシッククライアントから最近移行したユーザーに対して、以前の *webappid* パラメーターとのアプリケーション登録を作成 *した* ユーザーについては、統一されたラベル付けクライアント用の新しいアプリ登録を作成する必要があります。

**統一されたラベル付けクライアント Set-AIPAuthentication コマンドレットの新しいアプリ登録を作成するには、次のように** します。

1. 新しいブラウザーウィンドウで、Azure Information Protection で使用する Azure AD テナントに [Azure portal](https://portal.azure.com/) をサインインします。

1. [   >    >  **アプリの登録** の管理] Azure Active Directory 移動し、[**新しい登録**] を選択します。 

1. [ **アプリケーションの登録** ] ウィンドウで、次の値を指定し、[ **登録**] をクリックします。

    |オプション  |値  |
    |---------|---------|
    |**名前**     |  `AIP-DelegatedUser` <br>必要に応じて別の名前を指定してください。 名前はテナントごとに一意である必要があります。       |
    |**サポートされているアカウントの種類**     |   **[この組織のディレクトリ内のアカウントのみ]** を選択します。      |
    |**リダイレクト URI (省略可能)**     |     [ **Web**] を選択し、「」と入力し `https://localhost` ます。    |
    |     |         |

1. [ **AIP-DelegatedUser** ] ウィンドウで、 **アプリケーション (クライアント) ID** の値をコピーします。 

    値は次の例のように `77c3c1c3-abf9-404e-8b2b-4652836c8c66` なります。 

    この値は、 **Set-AIPAuthentication コマンドレット** を実行するときに *AppId* パラメーターに使用されます。 後で参照するために値を貼り付けて保存します。

1. サイドバーで、[   >  **証明書 & シークレット** を管理する] を選択します。

    次に、[ **AIP-証明書 & シークレット** ] ウィンドウの [ **クライアントシークレット** ] セクションで、[ **新しいクライアントシークレット**] を選択します。

1. [ **クライアントシークレットの追加**] で、次のように指定し、[ **追加**] を選択します。

    |フィールド  |値  |
    |---------|---------|
    |**説明**     |  `Azure Information Protection unified labeling client`       |
    |**経過**     |   選択した期間 (1 年、2年間、または無期限) を指定します     |
    |     |         |

1. [ **AIP-DelegatedUser & シークレット** ] ウィンドウに戻り、[ **クライアントシークレット** ] セクションで、 **値** の文字列をコピーします。 

    この文字列は次の例のように `OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4` なります。 

    すべての文字がコピーされるようにするには、 **クリップボードにコピー** するアイコンを選択します。 
    
    > [!IMPORTANT]
    > この文字列は再び表示されることがなく、取得することもできないため、保存しておくことが重要です。 使用する機密情報と同様に、保存した値を安全に保存し、アクセスを制限します。
    > 

1. サイドバーで、[   >  **API のアクセス許可** の管理] を選択します。

    [ **AIP-DelegatedUser のアクセス許可** ] ウィンドウで、[ **アクセス許可の追加**] を選択します。

1. [ **Api のアクセス許可の要求** ] ウィンドウで、[ **Microsoft api** ] タブが表示されていることを確認し、[ **Azure Rights Management Services**] を選択します。 

    アプリケーションで必要なアクセス許可の種類を確認するメッセージが表示されたら、[ **アプリケーションのアクセス許可**] を選択します。

1. **[アクセス許可の選択**] で、[**コンテンツ**] を展開し、次のものを選択して、[**アクセス許可の追加**] を選択します。
    
    -  **DelegatedReader** 
    -  **DelegatedWriter**

1. [ **AIP-DelegatedUser のアクセス許可** ] ウィンドウに戻り、[ **アクセス許可の追加** ] をもう一度選択します。

    [ **AIP のアクセス許可の要求** ] ウィンドウで、[組織が使用する **api**] を選択し、[ **Microsoft Information Protection Sync Service**] を検索します。

1. [ **API のアクセス許可の要求** ] ウィンドウで、[アプリケーションの **アクセス許可**] を選択します。
    
    **[アクセス許可]** で、[ **UnifiedPolicy**] を展開し、[ **UnifiedPolicy**] を選択して、[**アクセス許可の追加**] を選択します。

1. [ **AIP-DelegatedUser のアクセス許可**] ウィンドウに戻り、[**管理者の \<*your tenant name*> 同意を付与する**] を選択し、確認プロンプトで [**はい]** を選択します。
    
    API のアクセス許可は次の図のようになります。

    :::image type="content" source="../media/api-permissions-app.png" alt-text="Azure AD で登録されているアプリの API アクセス許可":::

これで、シークレットを使用したこのアプリの登録が完了しました。次に、パラメーター *AppId* と *appsecret* を使用して、 [Set-aipauthentication](/powershell/module/azureinformationprotection/set-aipauthentication)を実行する準備ができました。 また、テナント ID も必要になります。 

> [!TIP]
>Azure portal: **Azure Active Directory**  >  **Manage**  >  **Properties**  >  **Directory id** を使用して、テナント id を簡単にコピーできます。

### <a name="running-the-set-aipauthentication-cmdlet"></a>Set-AIPAuthentication コマンドレットの実行

1. [ **管理者として実行] オプション** を使用して Windows PowerShell を開きます。 

1. PowerShell セッションで、非対話形式で実行される Windows ユーザーアカウントの資格情報を格納する変数を作成します。 たとえば、スキャナー用のサービスアカウントを作成した場合は、次のようになります。

    ```PowerShell
    $pscreds = Get-Credential "CONTOSO\srv-scanner"
    ```

    このアカウントのパスワードを入力するように求められます。

1. *OnBeHalfOf* パラメーターを指定して、 **Set-aipauthentication** コマンドレットを実行します。これには、作成した変数の値を指定します。 

    また、アプリの登録値、テナント ID、および Azure AD で委任されたユーザーアカウントの名前を指定します。 次に例を示します。
    
    ```PowerShell
    Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -DelegatedUser scanner@contoso.com -OnBehalfOf $pscreds
    ```
## <a name="next-steps"></a>次のステップ

PowerShell セッションでコマンドレットのヘルプを表示するには、「」と入力 `Get-Help <cmdlet name> -online` します。 次に例を示します。 

```PowerShell
Get-Help Set-AIPFileLabel -online
```

詳細については、次を参照してください。

- [クライアントカスタマイズの統一されたラベル付け](clientv2-admin-guide-customizations.md)

- [クライアントのファイルと使用状況ログ](clientv2-admin-guide-files-and-logging.md)

- [サポートされるファイルの種類](clientv2-admin-guide-file-types.md)