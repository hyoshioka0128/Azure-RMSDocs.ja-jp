---
title: Azure Information Protection 統合されたラベル付けクライアントで PowerShell を使用する
description: 管理者が PowerShell を使用して Azure Information Protection 統合されたラベル付けクライアントを管理するための手順と情報です。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/03/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 38e2156b0102c857d13b99233a5bad2331662606
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97385490"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>管理者ガイド: Azure Information Protection 統合クライアントでの PowerShell の使用

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、Windows 8、Windows Server 2019、Windows Server 2016、windows Server 2012 R2、windows server 2012 *
>
>*Windows 7 または Office 2010 を使用している場合は、「 [AIP For windows And office versions in extended support](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)」を参照してください。*
>
>***関連**: [Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)ます。 従来のクライアントについては、「 [従来のクライアント管理者ガイド](client-admin-guide-powershell.md)」を参照してください。

Azure Information Protection 統合ラベル付けクライアントをインストールすると、PowerShell コマンドが自動的にインストールされます。 自動化のためのスクリプトに追加できるコマンドを実行することでクライアントを管理できます。

コマンドレットは、ラベル付け用のコマンドレットを持つ PowerShell モジュール **Azureinformationprotection** と共にインストールされます。 次に例を示します。

|ラベル付けコマンドレット|使用例|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|共有フォルダーで、すべてのファイルを特定のラベルで識別します。|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|共有フォルダーで、ファイルの内容を検査したあと、指定した条件に基づいて、ラベル付けされていないファイルに自動的にラベルを付与します。|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|共有フォルダーで、ラベルが付いていないすべてのファイルに指定したラベルを適用します。|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|スケジュールに基づいて実行されるスクリプトを利用するなど、非対話式にファイルにラベルを付けます。|
| | |

このモジュールは、**\ProgramFiles (x86)\Microsoft Azure Information Protection** にインストールされ、このフォルダーを **PSModulePath** システム変数に追加します。 このモジュールの .dll の名前は **AIP.dll** です。

> [!IMPORTANT]
> AzureInformationProtection モジュールは、ラベルまたはラベルポリシーの詳細設定の構成をサポートしていません。 これらの設定には、Office 365 セキュリティ & コンプライアンスセンターの PowerShell が必要です。 詳細については、「 [Azure Information Protection の統合ラベル付けクライアントのカスタム構成](clientv2-admin-guide-customizations.md)」を参照してください。
> [!NOTE]
> Azure RMS から移行した場合、RMS 関連のコマンドレットは、統合されたラベル付けで使用するために非推奨とされます。 これらの一部は、ラベル付けのための新しいコマンドレットに置き換えられました。 詳細については、「 [RMS から統合されたラベル付けコマンドレットのマッピング](#rms-to-unified-labeling-cmdlet-mapping)」を参照してください。
>

> [!TIP]
> 260 文字よりも長いパスとともにコマンドレットを使用するには、Windows 10 バージョン 1607 以降で利用できる次の[グループ ポリシー設定](/archive/blogs/jeremykuhne/net-4-6-2-and-long-paths-on-windows-10)を使用します。<br /> **ローカルコンピューターポリシー**  > **コンピューターの構成**  > **管理用テンプレート**  > **すべての設定**  > **Win32 長いパスを有効にする** 
> 
> Windows Server 2016 の場合、Windows 10 用の最新の管理用テンプレート (.admx) をインストールすれば、同じグループ ポリシー設定を使用できます。
>
> 詳しくは、Windows 10 開発者向けドキュメントの「[Maximum Path Length Limitation (パスの最大長の制限)](/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation)」をご覧ください。

### <a name="prerequisites-for-using-the-azureinformationprotection-module"></a>AzureInformationProtection モジュールを使用するための前提条件

**Azureinformationprotection** モジュールをインストールするための前提条件に加えて、Azure Information Protection のラベル付けコマンドレットを使用する場合は、次のような追加の前提条件があります。

1. Azure Rights Management サービスをアクティブ化する必要があります。

2. 自分のアカウントを使用して他のユーザーのファイルから保護を削除するには、スーパーユーザー機能が組織で有効になっている必要があります。また、アカウントは Azure Rights Management のスーパーユーザーとして構成されている必要があります。

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>前提条件 1: Azure Rights Management サービスをアクティブ化する必要がある

Azure Information Protection テナントがアクティブ化されていない場合は、「[Azure Information Protection からの保護サービスのアクティブ化](../activate-service.md)」の手順を参照してください。

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>前提条件 2: 自分のアカウントを使って他のユーザーのファイルから保護を削除するには

他のユーザーのファイルから保護を削除する一般的なシナリオには、データの探索またはデータの回復が含まれます。 ラベルを使って保護を適用している場合は、保護を適用しない新しいラベルを設定することによって、またはラベルを削除することによって保護を削除できます。

ファイルから保護を削除するには、Rights Management の使用権限を持っているか、スーパー ユーザーである必要があります。 データの探索またはデータの回復には、スーパー ユーザー機能が通常使われます。 この機能を有効にし、アカウントをスーパーユーザーに構成するには、「 [Azure Information Protection および探索サービスまたはデータ回復用のスーパーユーザーの構成](../configure-super-users.md)」を参照してください。

## <a name="rms-to-unified-labeling-cmdlet-mapping"></a>RMS と統合されたラベル付けコマンドレットのマッピング

次の表は、RMS 関連のコマンドレットと、統合されたラベル付けに使用される更新されたコマンドレットをマップしたものです。

たとえば、 **RMSProtectionLicense** を RMS 保護と共に使用し、統合されたラベルに移行した場合は、代わりに **新しい-AIPCustomPermissions** を使用します。

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

[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) コマンドレットを利用し、ラベル付けコマンドレットを非対話式に実行できます。

既定では、ラベル付けのコマンドレットを実行するとき、対話型 PowerShell セッション内のユーザー コンテキストでコマンドは動作します。 これらを無人で実行するには、対話形式でサインインできる Windows アカウントを使用し、委任されたアクセスに使用される Azure AD のアカウントを使用します。 管理を容易にするために、Active Directory から Azure AD に同期される1つのアカウントを使用します。

また、Azure AD からアクセストークンを要求する必要もあります。これにより、委任されたユーザーが Azure Information Protection に対して認証するための資格情報を設定して格納します。

AIPAuthentication コマンドレットを実行しているコンピューターは、Office 365 セキュリティ & コンプライアンスセンターなどのラベル付け管理センターを使用して、委任されたユーザーアカウントに割り当てられているラベルを持つラベルポリシーをダウンロードします。

> [!NOTE]
> 異なるユーザーにラベルポリシーを使用する場合は、すべてのラベルを発行する新しいラベルポリシーを作成し、この委任されたユーザーアカウントのみにポリシーを発行する必要がある場合があります。

Azure AD のトークンの有効期限が切れた場合、新しいトークンを取得するには、もう一度コマンドレットを実行する必要があります。 アクセストークンは、1年間、2年間、または期限切れにならないように Azure AD で構成できます。 Set-AIPAuthentication のパラメーターは、次のセクションで説明するように、Azure AD のアプリ登録プロセスの値を使用します。

委任されたユーザーアカウントの場合:

- このアカウントにラベルポリシーが割り当てられていること、および使用する公開されたラベルがポリシーに含まれていることを確認してください。

- このアカウントでコンテンツの暗号化を解除する必要がある場合 (たとえば、ファイルを再保護し、他のユーザーが保護しているファイルを検査する場合) は、Azure Information Protection の [スーパーユーザー](../configure-super-users.md) にして、スーパーユーザー機能が有効になっていることを確認してください。

- 段階的展開の [オンボードコントロール](../activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) を実装している場合は、構成したオンボードコントロールにこのアカウントが含まれていることを確認してください。

### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication"></a>Set-AIPAuthentication 用の Azure AD アプリケーションを作成し、構成するには

> [!IMPORTANT]
> これらの手順は、統一されたラベル付けクライアントの現在の一般公開バージョンを対象としており、このクライアントのスキャナーの一般公開バージョンにも適用されます。

Set-AIPAuthentication には、 *AppId* と *appsecret* パラメーターのアプリ登録が必要です。 以前のバージョンのクライアントからアップグレードし、以前の *webappid* パラメーターとのアプリケーション登録を *作成した* 場合は、統合されたラベル付けクライアントでは動作しません。 次のように、新しいアプリの登録を作成する必要があります。

1. 新しいブラウザー ウィンドウで、[Azure Portal](https://portal.azure.com/) にサインインします。

2. Azure Information Protection で使用する Azure AD テナントについては、 **Azure Active Directory**  >  **Manage** アプリの登録] を参照して  >  ください。 

3. [ **+ 新規登録**] を選択します。 [ **アプリケーションの登録** ] ウィンドウで、次の値を指定し、[ **登録**] をクリックします。

   - **名前**: `AIP-DelegatedUser`
        
        必要に応じて、別の名前を指定することもできます。 名前は、テナントごとに一意である必要があります。
    
    - **サポートされているアカウントの種類**: **この組織ディレクトリ内のアカウントのみ**
    
    - **リダイレクト URI (省略可能)**: **Web** および `https://localhost`

4. [ **AIP-DelegatedUser** ] ウィンドウで、 **アプリケーション (クライアント) ID** の値をコピーします。 値は次の例のように `77c3c1c3-abf9-404e-8b2b-4652836c8c66` なります。 この値は、Set-AIPAuthentication コマンドレットを実行するときに *AppId* パラメーターに使用されます。 後で参照するために値を貼り付けて保存します。

5. サイドバーで、[   >  **証明書 & シークレット** を管理する] を選択します。

6. [ **AIP-DelegatedUser & シークレット** ] ウィンドウの [ **クライアントシークレット** ] セクションで、[ **+ 新しいクライアントシークレット**] を選択します。

7. [ **クライアントシークレットの追加**] で、次のように指定し、[ **追加**] を選択します。
    
    - **説明**: `Azure Information Protection unified labeling client`
    - **有効期限**: 選択した期間 (1 年、2年間、または無期限) を指定します

8. [ **AIP-DelegatedUser & シークレット** ] ウィンドウに戻り、[ **クライアントシークレット** ] セクションで、 **値** の文字列をコピーします。 この文字列は次の例のように `OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4` なります。 すべての文字がコピーされるようにするには、 **クリップボードにコピー** するアイコンを選択します。 
    
    この文字列は再び表示されることがなく、取得することもできないため、保存しておくことが重要です。 使用する機密情報と同様に、保存した値を安全に保存し、アクセスを制限します。

9. サイドバーで、[   >  **API のアクセス許可** の管理] を選択します。

10. [ **AIP-DelegatedUser のアクセス許可** ] ウィンドウで、[ **+ アクセス許可の追加**] を選択します。

11. [ **Api のアクセス許可の要求** ] ウィンドウで、[ **Microsoft api** ] タブが表示されていることを確認し、[ **Azure Rights Management Services**] を選択します。 アプリケーションで必要なアクセス許可の種類を確認するメッセージが表示されたら、[ **アプリケーションのアクセス許可**] を選択します。

12. **[アクセス許可]** で、[コンテンツ] を展開し、次の **内容** を選択します。
    
    -  **DelegatedReader** 
    -  **DelegatedWriter**

13. **[アクセス許可の追加]** を選択します.

14. [ **AIP-DelegatedUser のアクセス許可** ] ウィンドウに戻り、[ **+ アクセス許可をもう一度追加する** ] を選択します。

15. [ **AIP のアクセス許可の要求** ] ウィンドウで、[組織が使用する **api**] を選択し、[ **Microsoft Information Protection Sync Service**] を検索します。

16. [ **API のアクセス許可の要求** ] ウィンドウで、[アプリケーションの **アクセス許可**] を選択します。

17. **[アクセス許可]** で、[ **UnifiedPolicy** ] を展開し、次のように選択します。
    
    -  **UnifiedPolicy**

18. **[アクセス許可の追加]** を選択します.

19. [ **AIP-DelegatedUser のアクセス許可**] ウィンドウに戻り、[**管理者の \<*your tenant name*> 同意を付与する**] を選択し、確認プロンプトで [**はい]** を選択します。
    
    API のアクセス許可は次のようになります。
    
    ![Azure AD で登録されているアプリの API アクセス許可](../media/api-permissions-app.png)

これで、シークレットを使用したこのアプリの登録が完了しました。次に、パラメーター *AppId* と *appsecret* を使用して、 [Set-aipauthentication](/powershell/module/azureinformationprotection/set-aipauthentication)を実行する準備ができました。 また、テナント ID も必要になります。 

> [!TIP]
>Azure portal: **Azure Active Directory**  >  **Manage**  >  **Properties**  >  **Directory id** を使用して、テナント id を簡単にコピーできます。

1. [ **管理者として実行] オプション** を使用して Windows PowerShell を開きます。 

2. PowerShell セッションで、非対話形式で実行される Windows ユーザーアカウントの資格情報を格納する変数を作成します。 たとえば、スキャナー用のサービスアカウントを作成した場合は、次のようになります。

    ```PowerShell
    $pscreds = Get-Credential "CONTOSO\srv-scanner"
    ```

    このアカウントのパスワードを入力するように求められます。

2. *OnBeHalfOf* パラメーターを指定して Set-AIPAuthentication コマンドレットを実行します。これは、作成した変数の値として指定します。 また、アプリの登録値、テナント ID、および Azure AD で委任されたユーザーアカウントの名前を指定します。 次に例を示します。
    
    ```PowerShell
    Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -DelegatedUser scanner@contoso.com -OnBehalfOf $pscreds
    ```

> [!NOTE]
> コンピューターがインターネットにアクセスできない場合は、Azure AD でアプリを作成し、Set-AIPAuthentication を実行する必要はありません。 代わりに、切断された [コンピューター](clientv2-admin-guide-customizations.md#support-for-disconnected-computers)の指示に従います。  

## <a name="next-steps"></a>次のステップ
PowerShell セッションでコマンドレットのヘルプを表示するには、「」と入力 `Get-Help <cmdlet name> -online` します。 次に例を示します。 

```PowerShell
Get-Help Set-AIPFileLabel -online
```

Azure Information Protection クライアントのサポートに必要な詳細については、以下をご覧ください。

- [カスタマイズ](clientv2-admin-guide-customizations.md)

- [クライアントのファイルと使用状況ログ](clientv2-admin-guide-files-and-logging.md)

- [サポートされるファイルの種類](clientv2-admin-guide-file-types.md)