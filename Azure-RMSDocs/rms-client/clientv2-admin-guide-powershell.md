---
title: Azure Information Protection 統合されたラベル付けクライアントで PowerShell を使用する
description: 管理者が PowerShell を使用して Azure Information Protection 統合されたラベル付けクライアントを管理するための手順と情報です。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: v2client
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b1db49d2a6033301b5922e66bc76be190b6162af
ms.sourcegitcommit: 437143e1f7f33aba46ffcc3900c31a763a2105c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71227792"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>管理者ガイド: Azure Information Protection 統合クライアントでの PowerShell の使用

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012, Windows Server 2008 R2*
>
> *手順:[Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection 統合ラベル付けクライアントをインストールすると、PowerShell コマンドが自動的にインストールされます。 自動化のためのスクリプトに追加できるコマンドを実行することでクライアントを管理できます。

コマンドレットは、ラベル付け用のコマンドレットを持つ PowerShell モジュール**Azureinformationprotection**と共にインストールされます。 以下に例を示します。

|ラベル付けコマンドレット|使用例|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|共有フォルダーで、すべてのファイルを特定のラベルで識別します。|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|共有フォルダーで、ファイルの内容を検査したあと、指定した条件に基づいて、ラベル付けされていないファイルに自動的にラベルを付与します。|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|共有フォルダーで、ラベルが付いていないすべてのファイルに指定したラベルを適用します。|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|スケジュールに基づいて実行されるスクリプトを利用するなど、非対話式にファイルにラベルを付けます。|

> [!TIP]
> 260 文字よりも長いパスとともにコマンドレットを使用するには、Windows 10 バージョン 1607 以降で利用できる次の[グループ ポリシー設定](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)を使用します。<br /> **ローカルコンピューターポリシー** > **コンピューターの構成** > **管理用テンプレート** > **すべての設定** > で**Win32 の長いパスを有効にする** 
> 
> Windows Server 2016 の場合、Windows 10 用の最新の管理用テンプレート (.admx) をインストールすれば、同じグループ ポリシー設定を使用できます。
>
> 詳しくは、Windows 10 開発者向けドキュメントの「[Maximum Path Length Limitation (パスの最大長の制限)](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation)」をご覧ください。

このモジュールは、 **\ProgramFiles (x86)\Microsoft Azure Information Protection** にインストールされ、このフォルダーを **PSModulePath** システム変数に追加します。 このモジュールの .dll の名前は **AIP.dll** です。

> [!IMPORTANT]
> AzureInformationProtection モジュールは、ラベルまたはラベルポリシーの詳細設定の構成をサポートしていません。 これらの設定には、Office 365 セキュリティ/コンプライアンスセンター PowerShell が必要です。 詳細については、「 [Azure Information Protection の統合ラベル付けクライアントのカスタム構成](clientv2-admin-guide-customizations.md)」を参照してください。

### <a name="prerequisites-for-using-the-azureinformationprotection-module"></a>AzureInformationProtection モジュールを使用するための前提条件

AzureInformationProtection モジュールをインストールするための前提条件に加えて、Azure Information Protection のラベル付けコマンドレットを使用する場合は、次のような追加の前提条件があります。

1. Azure Rights Management サービスをアクティブ化する必要があります。

2. 自分のアカウントを使って他のユーザーのファイルから保護を削除するには: 

    - 組織のスーパー ユーザー機能を有効にし、自分のアカウントを Azure Rights Management のスーパー ユーザーとして構成する必要があります。

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>前提条件 1: Azure Rights Management サービスをアクティブ化する必要があります

Azure Information Protection テナントがアクティブ化されていない場合は、「[Azure Information Protection からの保護サービスのアクティブ化](../activate-service.md)」の手順を参照してください。

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>前提条件 2: 自分のアカウントを使って他のユーザーのファイルから保護を削除するには

他のユーザーのファイルから保護を削除する一般的なシナリオには、データの探索またはデータの回復が含まれます。 ラベルを使って保護を適用している場合は、保護を適用しない新しいラベルを設定することによって、またはラベルを削除することによって保護を削除できます。

ファイルから保護を削除するには、Rights Management の使用権限を持っているか、スーパー ユーザーである必要があります。 データの探索またはデータの回復には、スーパー ユーザー機能が通常使われます。 この機能を有効にし、アカウントをスーパー ユーザーとして構成するには、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../configure-super-users.md)」をご覧ください。

## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>非対話形式でファイルに Azure Information Protection のラベル付けをする方法

**Set-AIPAuthentication** コマンドレットを利用し、ラベル付けコマンドレットを非対話式に実行できます。

既定では、ラベル付けのコマンドレットを実行するとき、対話型 PowerShell セッション内のユーザー コンテキストでコマンドは動作します。 自動実行するには、そのための新しい Azure AD ユーザー アカウントを作成します。 次に、ユーザーのコンテキストで Set-AIPAuthentication コマンドレットを実行し、Azure AD のアクセス トークンを使用して資格情報を設定し、格納します。 その後、このユーザーアカウントが認証され、保護サービスに対して Azure Information Protection からブートストラップされます。 このアカウントは、Azure Information Protection ポリシーと、ラベルが使用するすべての保護テンプレートをダウンロードします。

> [!NOTE]
> 異なるユーザーにラベルポリシーを使用する場合は、特定のラベルポリシーにこのアカウントを追加することが必要になる場合があることに注意してください。

このコマンドレットを初めて実行する際は、Azure Information Protection へのサインインを求められます。 自動アカウント用に作成したユーザーアカウント名とパスワードを指定します。 その後、このアカウントは、Azure AD の認証トークンの有効期限が切れるまで、ラベル付けコマンドレットを非対話形式で実行できます。 

初めてユーザーアカウントがサインインできるようにするには、アカウントに "**ローカルログオン**" ユーザー権利が割り当てられている必要があります。 この権限はユーザー アカウントの標準ですが、会社のポリシーによっては、サービス アカウントに対してこの構成を禁止することがあります。 その場合は、サインインプロンプトを表示せずに認証が完了するように、 *OnBehalfOf*パラメーターを指定して Set-AIPAuthentication を実行できます。

Azure AD のトークンの有効期限が切れた場合は、もう一度コマンドレットを実行して新しいトークンを取得します。

パラメーターを指定せずにこのコマンドレットを実行すると、アカウントは 90 日間またはパスワードの有効期限が切れるまで有効なアクセス トークンを取得します。  

アクセス トークンの有効期限を制御するには、パラメーターを指定してこのコマンドレットを実行します。 この構成では、1年間、2年間、または期限切れにならないように Azure AD にアクセストークンを構成できます。 Set-AIPAuthentication のパラメーターは、Azure AD のアプリ登録プロセスの値を使用します。

このコマンドレットを実行すると、作成したサービスアカウントのコンテキストでラベル付けコマンドレットを実行できます。

### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication"></a>Set-AIPAuthentication 用の Azure AD アプリケーションを作成し、構成するには

> [!NOTE]
> 現在のプレビューバージョンの統一されたラベル付けクライアントを使用していない場合は、「 [Set-AIPAuthentication-preview client の Azure AD アプリケーションを作成および構成するに](#to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication---preview-client)は」を参照してください。

1. 新しいブラウザー ウィンドウで、[Azure Portal](https://portal.azure.com/) にサインインします。

2. Azure Information Protection で使用する Azure AD テナントについては、 **Azure Active Directory** > **Manage** > **アプリの登録** を参照してください。 

3. **[+ 新規登録]** を選択して、Web アプリ/API アプリケーションを作成します。 **[アプリケーションの登録]** ブレードで、次の値を指定し、 **[登録]** をクリックします。

   - **名前**:`AIPOnBehalfOf`
        
        必要に応じて、別の名前を指定することもできます。 名前は、テナントごとに一意である必要があります。
    
    - **サポートされているアカウントの種類**:**この組織ディレクトリ内のアカウントのみ**
    
    - **リダイレクト URI (省略可能)** :**Web**および`http://localhost`

4. **[Aiponbehalfof]** ブレードで、**アプリケーション (クライアント) ID**の値をコピーします。 値は次の例`57c3c1c3-abf9-404e-8b2b-4652836c8c66`のようになります。 この値は、Set AIPAuthentication コマンドレットを実行するときに*Webappid*パラメーターに使用されます。 後で参照するために値を貼り付けて保存します。

5. **[Aiponbehalfof]** ブレードで、 **[管理]** サイドバーの **[認証]** を選択します。

6. **[Aiponbehalfof-Authentication]** ブレードの **[詳細設定]** セクションで、 **[ID トークン]** チェックボックスをオンにして、 **[保存]** を選択します。

7. **[Aiponbehalfof-Authentication]** ブレードの **[管理]** サイドバーで、 **[証明書 & シークレット]** を選択します。

8. **[Aiponbehalfof-証明書 & シークレット]** ブレードの **[クライアントシークレット]** セクションで、 **[+ 新しいクライアントシークレット]** を選択します。 

9. **[クライアントシークレットの追加]** で、次のように指定し、 **[追加]** を選択します。
    
    - **説明**:`Azure Information Protection client`
    - **有効期限**:選択した期間 (1 年、2年間、または無期限) を指定します

9. **[Aiponbehalfof-Certificates & シークレット]** ブレードに戻り、 **[クライアントシークレット]** セクションで、**値**の文字列をコピーします。 この文字列は次の例`+LBkMvddz?WrlNCK5v0e6_=meM59sSAn`のようになります。 すべての文字がコピーされるようにするには、**クリップボードにコピー**するアイコンを選択します。 
    
    この文字列は再び表示されることがなく、取得することもできないため、保存しておくことが重要です。 使用する機密情報と同様に、保存した値を安全に保存し、アクセスを制限します。

10. **[Aiponbehalfof-Certificates & シークレット]** ブレードで、 **[管理]** サイドバーの **[API の公開]** を選択します。

11. **[Aiponbehalfof-api を公開]** する ブレードで、 **[アプリケーション id uri]** オプションに **[設定]** を選択し、 **[アプリケーション id uri]** の値で **[api]** を **[http]** に変更します。 この文字列は次の例`http://d244e75e-870b-4491-b70d-65534953099e`のようになります。 
    
    **[保存]** を選択します。

12. **Aiponbehalfof-API を公開する**ブレードに戻り、 **[+ スコープの追加]** を選択します。

13. **[スコープの追加]** ブレードで、推奨される文字列を例として使用して、次のように指定し、 **[スコープの追加]** を選択します。
    - **スコープ名**:`user-impersonation`
    - **同意できるユーザー**:**管理者とユーザー**
    - **管理者の同意表示名**:`Access Azure Information Protection scanner`
    - **管理者の同意の説明**:`Allow the application to access the scanner for the signed-in user`
    - **ユーザーの同意の表示名**:`Access Azure Information Protection scanner`
    - **ユーザーの同意の説明**:`Allow the application to access the scanner for the signed-in user`
    - **状態**:**有効**(既定値)

14. **Aiponbehalfof-API を公開する**ブレードに戻り、このブレードを閉じます。

15. **[アプリの登録]** ブレードで、 **[+ 新しいアプリケーションの登録]** を選択し、ネイティブアプリケーションを作成します。

16. **[アプリケーションの登録]** ブレードで、次の設定を指定し、 **[登録]** を選択します。
    - **名前**:`AIPClient`
    - **サポートされているアカウントの種類**:**この組織ディレクトリ内のアカウントのみ**
    - **リダイレクト URI (省略可能)** :**パブリッククライアント (モバイル & デスクトップ)** と`http://localhost`

17. **[Aipclient]** ブレードで、**アプリケーション (クライアント) ID**の値をコピーします。 値は次の例`8ef1c873-9869-4bb1-9c11-8313f9d7f76f`のようになります。 
    
    この値は、Set-AIPAuthentication コマンドレットを実行するときに、パラメーターに使用されます。 後で参照するために値を貼り付けて保存します。

18. **[Aipclient]** ブレードで、 **[管理]** サイドバーの **[認証]** を選択します。

19. **[Aipclient-Authentication]** ブレードで、次のように指定し、 **[保存]** を選択します。
    - **[詳細設定]** セクションで、 **[ID トークン]** を選択します。
    - **[既定のクライアントの種類]** セクションで、[**はい]** を選択します。

20. **[Aipclient-Authentication]** ブレードで、 **[管理]** サイドバーの **[API アクセス許可]** を選択します。

21. **[Aipclient-アクセス許可]** ブレードで、 **[+ アクセス許可の追加]** を選択します。

22. **[Api のアクセス許可の要求]** ブレードで、 **[マイ api]** を選択します。

23. **[API の選択]** セクションで **[apionbehalfof]** を選択し、アクセス許可として **[ユーザー偽装]** のチェックボックスをオンにします。 **[アクセス許可の追加]** を選択します。 

24. API の **[アクセス許可]** ブレードに戻り、 **[許可の同意]** セクションで、[  **\<*テナント名*>に管理者の同意を付与**する] を選択し、確認プロンプトで [**はい]** を選択します。

2 つのアプリの構成を完了し、パラメーターとして *WebAppId*、*WebAppKey*、*NativeAppId* を指定して [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) を実行するために必要な値を取得しました。 例を次に示します。

`Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f"`

アカウントで非対話式で文書にラベルを付け、保護するという状況でこのコマンドを実行します。 たとえば、PowerShell スクリプトのユーザー アカウントやサービス アカウントで Azure Information Protection スキャナーを実行します。

このコマンドを初めて実行するとき、サインインが求められます。それにより、アカウントのアクセス トークンが作成され、%localappdata%\Microsoft\MSIP に安全に保管されます。 この初回サインイン後、コンピューターで非対話式でファイルにラベルを付け、保護できます。 ただし、サービスアカウントを使用してファイルのラベル付けと保護を行っていて、このサービスアカウントが対話形式でサインインできない場合は、次のように、 *OnBehalfOf*パラメーターを Set-AIPAuthentication と共に使用します。

1. 対話形式でサインインするためのユーザー権利の割り当てが付与されている Active Directory アカウントの資格情報を格納する変数を作成します。 以下に例を示します。
    
        $pscreds = Get-Credential "scv_scanner@contoso.com"

2. *OnBeHalfOf*パラメーターを指定して、Set-AIPAuthentication コマンドレットを実行します。これには、作成した変数の値を指定します。 以下に例を示します。
    
        Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f" -OnBehalfOf $pscreds


#### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication---preview-client"></a>Azure AD アプリケーションを作成して設定するには-AIPAuthentication-プレビュークライアント

次の手順は、統合ラベル付けクライアントのプレビューバージョンがインストールされている場合にのみ、別の手順として使用してください。 

このバージョンのクライアントでは、Set-AIPAuthentication の*AppId*と*appsecret*パラメーターの新しいアプリ登録を作成する必要があります。 以前のバージョンのクライアントからアップグレードし、以前の*webappid*パラメーターとのアプリケーション登録を作成した場合は、このバージョンのクライアントでは*動作しませ*ん。

1. 新しいブラウザー ウィンドウで、[Azure Portal](https://portal.azure.com/) にサインインします。

2. Azure Information Protection で使用する Azure AD テナントについては、 **Azure Active Directory** > **Manage** > **アプリの登録** を参照してください。 

3. **[+ 新規登録]** を選択します。 **[アプリケーションの登録]** ブレードで、次の値を指定し、 **[登録]** をクリックします。

   - **名前**:`AIPv2OnBehalfOf`
        
        必要に応じて、別の名前を指定することもできます。 名前は、テナントごとに一意である必要があります。
    
    - **サポートされているアカウントの種類**:**この組織ディレクトリ内のアカウントのみ**
    
    - **リダイレクト URI (省略可能)** :**Web**および`https://localhost`

4. **[AIPv2OnBehalfOf]** ブレードで、**アプリケーション (クライアント) ID**の値をコピーします。 値は次の例`77c3c1c3-abf9-404e-8b2b-4652836c8c66`のようになります。 この値は、Set-AIPAuthentication コマンドレットを実行するときに*AppId*パラメーターに使用されます。 後で参照するために値を貼り付けて保存します。

5. **AIPv2OnBehalfOf**ブレードの **[管理]** サイドバーで、 **[証明書 & シークレット]** を選択します。

6. **[AIPv2OnBehalfOf & シークレット]** ブレードの **[クライアントシークレット]** セクションで、 **[+ 新しいクライアントシークレット]** を選択します。

7. **[クライアントシークレットの追加]** で、次のように指定し、 **[追加]** を選択します。
    
    - **説明**:`Azure Information Protection unified labeling client`
    - **有効期限**:選択した期間 (1 年、2年間、または無期限) を指定します

8. **[AIPv2OnBehalfOf & シークレット]** ブレードに戻り、 **[クライアントシークレット]** セクションで、**値**の文字列をコピーします。 この文字列は次の例`OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4`のようになります。 すべての文字がコピーされるようにするには、**クリップボードにコピー**するアイコンを選択します。 
    
    この文字列は再び表示されることがなく、取得することもできないため、保存しておくことが重要です。 使用する機密情報と同様に、保存した値を安全に保存し、アクセスを制限します。

9. サイドバーの **[管理]** で、 **[API のアクセス許可]** を選択します。

10. **[AIPv2OnBehalfOf のアクセス許可]** ブレードで、 **[+ アクセス許可の追加]** を選択します。

11. **[Api のアクセス許可の要求]** ブレードで、 **[Microsoft api]** タブが表示されていることを確認し、 **[Azure Rights Management Services]** を選択します。 アプリケーションで必要なアクセス許可の種類を確認するメッセージが表示されたら、 **[アプリケーションのアクセス許可]** を選択します。

12. **[アクセス許可]** で、[コンテンツ] を展開し、次の**内容**を選択します。
    
    -  **DelegatedWriter** (常に必須)
    -  **Content. スーパー** [ユーザー (スーパーユーザー機能](../configure-super-users.md)が必要な場合は必須)
    -  **Content-type** (常に必須)
    
    スーパーユーザー機能を使用すると、アカウントは常にコンテンツの暗号化を解除できます。 たとえば、ファイルを再保護し、他のユーザーが保護しているファイルを検査します。

13. **[アクセス許可の追加]** を選択します。

14. AIPv2OnBehalfOf の **[アクセス許可]** ブレードに戻り、 **[+ アクセス許可をもう一度追加する]** を選択します。

15. **[AIP のアクセス許可の要求]** ブレードで、組織が使用する **[api]** を選択し、 **[Microsoft Information Protection Sync Service]** を検索します。

16. **[API のアクセス許可の要求]** ブレードで、アプリケーションの **[アクセス許可]** を選択します。

17. **[アクセス許可]** で、 **[UnifiedPolicy]** を展開し、次のように選択します。
    
    -  **UnifiedPolicy**

18. **[アクセス許可の追加]** を選択します。

19. [API のアクセス許可] ブレードに戻り、[  **\<*テナント名*>に管理者の同意を付与**する] を選択し、確認プロンプトで [**はい]** を選択します。

これで、シークレットを使用したこのアプリの登録が完了しました。パラメーター *AppId*と*appsecret*を使用して、 [Set-aipauthentication](/powershell/module/azureinformationprotection/set-aipauthentication)を実行する準備ができました。 また、テナント ID も必要になります。 

> [!TIP]
>Azure portal を使用して、テナント ID を簡単にコピーできます。 > **Manage**PropertiesDirectory > IDAzureActiveDirectoryします。 > 

この例では、テナント ID 9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a を使用しています。

`Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a"`

このコマンドを初めて実行するとき、サインインが求められます。それにより、アカウントのアクセス トークンが作成され、%localappdata%\Microsoft\MSIP に安全に保管されます。 この初回サインイン後、コンピューターで非対話式でファイルにラベルを付け、保護できます。 ただし、サービスアカウントを使用してファイルのラベル付けと保護を行っていて、このサービスアカウントが対話形式でサインインできない場合は、次のように、 *OnBehalfOf*パラメーターを Set-AIPAuthentication と共に使用します。

1. 対話形式でサインインするためのユーザー権利の割り当てが付与されている Active Directory アカウントの資格情報を格納する変数を作成します。 以下に例を示します。
    
        $pscreds = Get-Credential "scv_scanner@contoso.com"

2. *OnBeHalfOf*パラメーターを指定して、Set-AIPAuthentication コマンドレットを実行します。これには、作成した変数の値を指定します。 以下に例を示します。
    
        Set-AIPAuthentication -AppId "77c3c1c3-abf9-404e-8b2b-4652836c8c66" -AppSecret "OAkk+rnuYc/u+]ah2kNxVbtrDGbS47L4" -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -OnBehalfOf $pscreds


## <a name="next-steps"></a>次の手順
PowerShell セッションでコマンドレットのヘルプを表示するには`Get-Help <cmdlet name> -online`、「」と入力します。 以下に例を示します。 

    Get-Help Set-AIPFileLabel -online

Azure Information Protection クライアントのサポートに必要な詳細については、以下をご覧ください。

- [カスタマイズ](clientv2-admin-guide-customizations.md)

- [クライアント ファイルおよび使用状況ログの記録](clientv2-admin-guide-files-and-logging.md)

- [サポートされるファイルの種類](clientv2-admin-guide-file-types.md)
