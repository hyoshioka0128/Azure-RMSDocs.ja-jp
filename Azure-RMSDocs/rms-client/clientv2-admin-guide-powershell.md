---
title: Azure Information Protection 統合されたラベル付けクライアントで PowerShell を使用する
description: 管理者が PowerShell を使用して Azure Information Protection 統合されたラベル付けクライアントを管理するための手順と情報です。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 07/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: 495a88ee3296fc8d3e075abbd992298b7bae55ea
ms.sourcegitcommit: fdc1f3d76b48f4e865a538087d66ee69f0f9888d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68141614"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>管理者ガイド: Azure Information Protection 統合クライアントでの PowerShell の使用

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012, Windows Server 2008 R2*
>
> *手順:[Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection 統合ラベル付けクライアントをインストールすると、PowerShell コマンドが自動的にインストールされます。 自動化のためのスクリプトに追加できるコマンドを実行することでクライアントを管理できます。

コマンドレットは、ラベル付け用のコマンドレットを持つ PowerShell モジュール**Azureinformationprotection**と共にインストールされます。 例えば:

|ラベル付けコマンドレット|使用例|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|共有フォルダーで、すべてのファイルを特定のラベルで識別します。|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|共有フォルダーで、ファイルの内容を検査したあと、指定した条件に基づいて、ラベル付けされていないファイルに自動的にラベルを付与します。|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|共有フォルダーで、ラベルが付いていないすべてのファイルに指定したラベルを適用します。|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|別のユーザーアカウントを使用して、対話形式でファイルにラベルを付けます。|

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

Azure Information Protection テナントが保護を適用するためにアクティブ化されていない場合は、 [Azure Rights Management をアクティブ化](../activate-service.md)するための手順を参照してください。

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>前提条件 2: 自分のアカウントを使って他のユーザーのファイルから保護を削除するには

他のユーザーのファイルから保護を削除する一般的なシナリオには、データの探索またはデータの回復が含まれます。 ラベルを使って保護を適用している場合は、保護を適用しない新しいラベルを設定することによって、またはラベルを削除することによって保護を削除できます。

ファイルから保護を削除するには、Rights Management の使用権限を持っているか、スーパー ユーザーである必要があります。 データの探索またはデータの回復には、スーパー ユーザー機能が通常使われます。 この機能を有効にし、アカウントをスーパー ユーザーとして構成するには、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../configure-super-users.md)」をご覧ください。

## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>非対話形式でファイルに Azure Information Protection のラベル付けをする方法

**Set-AIPAuthentication** コマンドレットを利用し、ラベル付けコマンドレットを非対話式に実行できます。

既定では、ラベル付けのコマンドレットを実行するとき、対話型 PowerShell セッション内のユーザー コンテキストでコマンドは動作します。 自動実行するには、そのための新しい Azure AD ユーザー アカウントを作成します。 次に、ユーザーのコンテキストで Set-AIPAuthentication コマンドレットを実行し、Azure AD のアクセス トークンを使用して資格情報を設定し、格納します。 その後、このユーザーアカウントが認証され、保護サービスに対して Azure Information Protection からブートストラップされます。 このアカウントは、Azure Information Protection ポリシーと、ラベルが使用するすべての保護テンプレートをダウンロードします。

> [!NOTE]
> [スコープ付きポリシー](../configure-policy-scope.md)を使用する場合は、このアカウントをスコープ付きポリシーに追加しなければならない場合があります。

このコマンドレットを初めて実行する際は、Azure Information Protection へのサインインを求められます。 自動アカウント用に作成したユーザーアカウント名とパスワードを指定します。 その後、このアカウントは、Azure AD の認証トークンの有効期限が切れるまで、ラベル付けコマンドレットを非対話形式で実行できます。 

初めてユーザーアカウントがサインインできるようにするには、アカウントに "**ローカルログオン**" ユーザー権利が割り当てられている必要があります。 この権限はユーザー アカウントの標準ですが、会社のポリシーによっては、サービス アカウントに対してこの構成を禁止することがあります。 その場合は、サインインプロンプトを表示せずに認証が完了するように、 *OnBehalfOf*パラメーターを指定して Set-AIPAuthentication を実行できます。

Azure AD のトークンの有効期限が切れた場合は、もう一度コマンドレットを実行して新しいトークンを取得します。

パラメーターを指定せずにこのコマンドレットを実行すると、アカウントは 90 日間またはパスワードの有効期限が切れるまで有効なアクセス トークンを取得します。  

アクセス トークンの有効期限を制御するには、パラメーターを指定してこのコマンドレットを実行します。 この構成では、1年間、2年間、または期限切れにならないように Azure AD にアクセストークンを構成できます。 Azure Active Directory に登録されている2つのアプリケーションが必要です。**Web アプリ/API** アプリケーションと**ネイティブ アプリケーション**を登録する必要があります。 これらのアプリケーションの値は、Set-AIPAuthentication のパラメーターで使用されます。

このコマンドレットを実行すると、作成したサービスアカウントのコンテキストでラベル付けコマンドレットを実行できます。

### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication"></a>Set-AIPAuthentication 用の Azure AD アプリケーションを作成し、構成するには

1. 新しいブラウザー ウィンドウで、[Azure Portal](https://portal.azure.com/) にサインインします。

2. Azure Information Protection で使用する Azure AD テナントについては、 **Azure Active Directory** > **Manage** > **アプリの登録** を参照してください。 

3. [ **+ 新規登録**] を選択して、Web アプリ/API アプリケーションを作成します。 [**アプリケーションの登録**] ブレードで、次の値を指定し、[**登録**] をクリックします。

   - **名前**:`AIPOnBehalfOf`
        
        必要に応じて、別の名前を指定することもできます。 名前は、テナントごとに一意である必要があります。
    
    - **サポートされているアカウントの種類**:**この組織ディレクトリ内のアカウントのみ**
    
    - **リダイレクト URI (省略可能)** :**Web**および`http://localhost`

4. [ **Aiponbehalfof** ] ブレードで、**アプリケーション (クライアント) ID**の値をコピーします。 値は次の例`57c3c1c3-abf9-404e-8b2b-4652836c8c66`のようになります。 この値は、Set AIPAuthentication コマンドレットを実行するときに*Webappid*パラメーターに使用されます。 後で参照するために値を貼り付けて保存します。

5. [ **Aiponbehalfof** ] ブレードで、[**管理**] メニューから [**認証**] を選択します。

6. [ **Aiponbehalfof-Authentication** ] ブレードの [**詳細設定**] セクションで、[ **ID トークン**] チェックボックスをオンにして、[**保存**] を選択します。

7. [ **Aiponbehalfof-Authentication** ] ブレードで、[**管理**] メニューから [**証明書 & シークレット**] を選択します。

8. [ **Aiponbehalfof-証明書 & シークレット**] ブレードの [**クライアントシークレット**] セクションで、[ **+ 新しいクライアントシークレット**] を選択します。 

9. [**クライアントシークレットの追加**] で、次のように指定し、[**追加**] を選択します。
    
    - **説明**:`Azure Information Protection client`
    - **有効期限**:選択した期間 (1 年、2年間、または無期限) を指定します

9. [ **Aiponbehalfof-Certificates & シークレット**] ブレードに戻り、[**クライアントシークレット**] セクションで、**値**の文字列をコピーします。 この文字列は次の例`+LBkMvddz?WrlNCK5v0e6_=meM59sSAn`のようになります。 すべての文字がコピーされるようにするには、**クリップボードにコピー**するアイコンを選択します。 
    
    この文字列は再び表示されることがなく、取得することもできないため、保存しておくことが重要です。 使用する機密情報と同様に、保存した値を安全に保存し、アクセスを制限します。

10. [ **Aiponbehalfof-Certificates & シークレット**] ブレードで、[**管理**] メニューの [ **API の公開**] を選択します。

11. [ **Aiponbehalfof-api を公開**する] ブレードで、[**アプリケーション id uri** ] オプションに [**設定**] を選択し、[**アプリケーション id uri** ] の値で [ **api** ] を [ **http**] に変更します。 この文字列は次の例`http://d244e75e-870b-4491-b70d-65534953099e`のようになります。 
    
    **[保存]** を選択します。

12. **Aiponbehalfof-API を公開する**ブレードに戻り、[ **+ スコープの追加**] を選択します。

13. [**スコープの追加**] ブレードで、推奨される文字列を例として使用して、次のように指定し、[**スコープの追加**] を選択します。
    - **スコープ名**:`user-impersonation`
    - **同意できるユーザー**:**管理者とユーザー**
    - **管理者の同意表示名**:`Access Azure Information Protection scanner`
    - **管理者の同意の説明**:`Allow the application to access the scanner for the signed-in user`
    - **ユーザーの同意の表示名**:`Access Azure Information Protection scanner`
    - **ユーザーの同意の説明**:`Allow the application to access the scanner for the signed-in user`
    - **状態**:**有効**(既定値)

14. **Aiponbehalfof-API を公開する**ブレードに戻り、このブレードを閉じます。

15. [**アプリの登録**] ブレードで、[ **+ 新しいアプリケーションの登録**] を選択し、ネイティブアプリケーションを作成します。

16. [**アプリケーションの登録**] ブレードで、次の設定を指定し、[**登録**] を選択します。
    - **名前**:`AIPClient`
    - **サポートされているアカウントの種類**:**この組織ディレクトリ内のアカウントのみ**
    - **リダイレクト URI (省略可能)** :**パブリッククライアント (モバイル & デスクトップ)** と`http://localhost`

17. [ **Aipclient** ] ブレードで、**アプリケーション (クライアント) ID**の値をコピーします。 値は次の例`8ef1c873-9869-4bb1-9c11-8313f9d7f76f`のようになります。 
    
    この値は、Set-AIPAuthentication コマンドレットを実行するときに、パラメーターに使用されます。 後で参照するために値を貼り付けて保存します。

18. [ **Aipclient** ] ブレードで、[**管理**] メニューから [**認証**] を選択します。

19. [ **Aipclient-Authentication** ] ブレードで、次のように指定し、[**保存**] を選択します。
    - [**詳細設定**] セクションで、[ **ID トークン**] を選択します。
    - [**既定のクライアントの種類**] セクションで、[**はい]** を選択します。

20. [ **Aipclient-Authentication** ] ブレードで、[**管理**] メニューの [ **API アクセス許可**] を選択します。

21. [ **Aipclient-アクセス許可**] ブレードで、[ **+ アクセス許可の追加**] を選択します。

22. [ **Api のアクセス許可の要求**] ブレードで、[**マイ api**] を選択します。

23. [ **API の選択**] セクションで [ **apionbehalfof**] を選択し、アクセス許可として [**ユーザー偽装**] のチェックボックスをオンにします。 [**アクセス許可の追加**] を選択します。 

24. [API の**アクセス許可**] ブレードに戻り、[**許可の同意**] セクションで、[  **\<*テナント名*>に管理者の同意を付与**する] を選択し、確認プロンプトで [**はい]** を選択します。

2 つのアプリの構成を完了し、パラメーターとして *WebAppId*、*WebAppKey*、*NativeAppId* を指定して [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) を実行するために必要な値を取得しました。 例を次に示します。

`Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f"`

アカウントで非対話式で文書にラベルを付け、保護するという状況でこのコマンドを実行します。 たとえば、PowerShell スクリプトのユーザー アカウントやサービス アカウントで Azure Information Protection スキャナーを実行します。

このコマンドを初めて実行するとき、サインインが求められます。それにより、アカウントのアクセス トークンが作成され、%localappdata%\Microsoft\MSIP に安全に保管されます。 この初回サインイン後、コンピューターで非対話式でファイルにラベルを付け、保護できます。 ただし、サービスアカウントを使用してファイルのラベル付けと保護を行っていて、このサービスアカウントが対話形式でサインインできない場合は、次のように、 *OnBehalfOf*パラメーターを Set-AIPAuthentication と共に使用します。

1. 対話形式でサインインするためのユーザー権利の割り当てが付与されている Active Directory アカウントの資格情報を格納する変数を作成します。 例えば:
    
        $pscreds = Get-Credential "scv_scanner@contoso.com"

2. *OnBeHalfOf*パラメーターを指定して、Set-AIPAuthentication コマンドレットを実行します。これには、作成した変数の値を指定します。 例えば:
    
        Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f" -OnBehalfOf $pscreds

## <a name="next-steps"></a>次の手順
PowerShell セッションでコマンドレットのヘルプを表示するには`Get-Help <cmdlet name> -online`、「」と入力します。 例えば: 

    Get-Help Set-AIPFileLabel -online

Azure Information Protection クライアントのサポートに必要な詳細については、以下をご覧ください。

- [カスタマイズ](clientv2-admin-guide-customizations.md)

- [クライアント ファイルおよび使用状況ログの記録](clientv2-admin-guide-files-and-logging.md)

- [サポートされるファイルの種類](clientv2-admin-guide-file-types.md)
