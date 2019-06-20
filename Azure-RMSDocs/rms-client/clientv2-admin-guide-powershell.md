---
title: PowerShell を使用して、Azure Information Protection でラベル付けのクライアントの統合
description: 手順と、Azure Information Protection を管理する管理者向けの情報は、PowerShell を使用してラベル付けのクライアントを統合します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/20/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: f90697e1e4df90ab8876843b45957b93c8ba8b07
ms.sourcegitcommit: a26e4e50165107efd51280b5c621dfe74be51a7a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2019
ms.locfileid: "67236880"
---
# <a name="admin-guide-using-powershell-with-the-azure-information-protection-unified-client"></a>管理者ガイド: Azure Information Protection の統合されたクライアントで PowerShell の使用

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012, Windows Server 2008 R2*
>
> *手順:[Azure Information Protection unified Windows 用のラベル付けのクライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection の統合されたラベル付けクライアントをインストールするときに、PowerShell コマンドが自動的にインストールします。 自動化のためのスクリプトに追加できるコマンドを実行することでクライアントを管理できます。

PowerShell モジュールのコマンドレットがインストールされている**AzureInformationProtection**、ラベル付けのコマンドレットがあります。 以下に例を示します。

|ラベル付けコマンドレット|使用例|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)|共有フォルダーで、すべてのファイルを特定のラベルで識別します。|
|[Set-AIPFileClassification](/powershell/module/azureinformationprotection/set-aipfileclassification)|共有フォルダーで、ファイルの内容を検査したあと、指定した条件に基づいて、ラベル付けされていないファイルに自動的にラベルを付与します。|
|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)|共有フォルダーで、ラベルが付いていないすべてのファイルに指定したラベルを適用します。|
|[Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication)|独自の別のユーザー アカウントを使用して対話形式でファイルをラベルします。|

> [!TIP]
> 260 文字よりも長いパスとともにコマンドレットを使用するには、Windows 10 バージョン 1607 以降で利用できる次の[グループ ポリシー設定](https://blogs.msdn.microsoft.com/jeremykuhne/2016/07/30/net-4-6-2-and-long-paths-on-windows-10/)を使用します。<br /> **ローカル コンピューター ポリシー** > **コンピューターの構成** > **管理用テンプレート** > **すべて設定**  > **長いパスを有効にする Win32** 
> 
> Windows Server 2016 の場合、Windows 10 用の最新の管理用テンプレート (.admx) をインストールすれば、同じグループ ポリシー設定を使用できます。
>
> 詳しくは、Windows 10 開発者向けドキュメントの「[Maximum Path Length Limitation (パスの最大長の制限)](https://docs.microsoft.com/windows/desktop/FileIO/naming-a-file#maximum-path-length-limitation)」をご覧ください。

このモジュールは、 **\ProgramFiles (x86)\Microsoft Azure Information Protection** にインストールされ、このフォルダーを **PSModulePath** システム変数に追加します。 このモジュールの .dll の名前は **AIP.dll** です。

> [!IMPORTANT]
> AzureInformationProtection モジュールには、ラベルやポリシーのラベルの高度な設定の構成をサポートしていません。 これらの設定では、Office 365 セキュリティ/コンプライアンス センターの PowerShell が必要です。 詳細については、次を参照してください。 [、Azure Information Protection のカスタム構成の統合のラベル付けクライアント](clientv2-admin-guide-customizations.md)します。

### <a name="prerequisites-for-using-the-azureinformationprotection-module"></a>AzureInformationProtection モジュールを使用するための前提条件

に加えて、AzureInformationProtection モジュールのインストールの前提条件、追加の前提条件の場合は Azure Information Protection のラベル付けコマンドレットを使用します。

1. Azure Rights Management サービスをアクティブ化する必要があります。

2. 自分のアカウントを使って他のユーザーのファイルから保護を削除するには: 

    - 組織のスーパー ユーザー機能を有効にし、自分のアカウントを Azure Rights Management のスーパー ユーザーとして構成する必要があります。

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>前提条件 1: Azure Rights Management サービスをアクティブ化する必要があります

保護を適用する、Azure Information Protection テナントがアクティブでない場合の手順を参照してください。 [Azure Rights Management のアクティブ化](../activate-service.md)します。

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>前提条件 2: 自分のアカウントを使って他のユーザーのファイルから保護を削除するには

他のユーザーのファイルから保護を削除する一般的なシナリオには、データの探索またはデータの回復が含まれます。 ラベルを使って保護を適用している場合は、保護を適用しない新しいラベルを設定することによって、またはラベルを削除することによって保護を削除できます。

ファイルから保護を削除するには、Rights Management の使用権限を持っているか、スーパー ユーザーである必要があります。 データの探索またはデータの回復には、スーパー ユーザー機能が通常使われます。 この機能を有効にし、アカウントをスーパー ユーザーとして構成するには、「[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](../configure-super-users.md)」をご覧ください。

## <a name="how-to-label-files-non-interactively-for-azure-information-protection"></a>非対話形式でファイルに Azure Information Protection のラベル付けをする方法

注:このセクションの情報は、Azure Information Protection の統合されたラベル付けクライアントのみのプレビュー バージョンです。

**Set-AIPAuthentication** コマンドレットを利用し、ラベル付けコマンドレットを非対話式に実行できます。

既定では、ラベル付けのコマンドレットを実行するとき、対話型 PowerShell セッション内のユーザー コンテキストでコマンドは動作します。 自動実行するには、そのための新しい Azure AD ユーザー アカウントを作成します。 次に、ユーザーのコンテキストで Set-AIPAuthentication コマンドレットを実行し、Azure AD のアクセス トークンを使用して資格情報を設定し、格納します。 このユーザー アカウントを認証し、Azure Information Protection からの保護サービスのブートス トラップはします。 アカウントは、Azure Information Protection ポリシーとラベルを使用するすべての保護テンプレートをダウンロードします。

> [!NOTE]
> [スコープ付きポリシー](../configure-policy-scope.md)を使用する場合は、このアカウントをスコープ付きポリシーに追加しなければならない場合があります。

このコマンドレットを初めて実行する際は、Azure Information Protection へのサインインを求められます。 ユーザー アカウント名と、自動アカウント用に作成したパスワードを指定します。 その後、このアカウントを実行できます、ラベル付けコマンドレット非対話形式で Azure AD で認証トークンの有効期限が切れるまで。 

この初回対話形式でサインインできるユーザー アカウントのアカウントが必要、**ローカル ログオン**ユーザー権利が割り当てられています。 この権限はユーザー アカウントの標準ですが、会社のポリシーによっては、サービス アカウントに対してこの構成を禁止することがあります。 場合は、して Set-aipauthentication を実行することができます、 *OnBehalfOf*サインイン プロンプトなしで認証を完了するためのパラメーター。

Azure AD のトークンの期限が切れると、新しいトークンを取得するには、もう一度コマンドレットを実行します。

パラメーターを指定せずにこのコマンドレットを実行すると、アカウントは 90 日間またはパスワードの有効期限が切れるまで有効なアクセス トークンを取得します。  

アクセス トークンの有効期限を制御するには、パラメーターを指定してこのコマンドレットを実行します。 この構成では、1 年間、2 年間、Azure ad アクセス トークンを構成したりしないようにするには、次の有効期限が切れる: できます。 Azure Active Directory に登録されている 2 つのアプリケーションが必要です。**Web アプリ/API** アプリケーションと**ネイティブ アプリケーション**を登録する必要があります。 Set-aipauthentication のパラメーターは、これらのアプリケーションからの値を使用します。

このコマンドレットを実行した後は、作成したサービス アカウントのコンテキストでラベル付けコマンドレットを実行できます。

### <a name="to-create-and-configure-the-azure-ad-applications-for-set-aipauthentication"></a>Set-AIPAuthentication 用の Azure AD アプリケーションを作成し、構成するには

1. 新しいブラウザー ウィンドウで、[Azure Portal](https://portal.azure.com/) にサインインします。

2. Azure Information Protection で使用する Azure AD テナントに移動します**Azure Active Directory** > **管理** > **アプリの登録。** . 

3. 選択 **+ 新しい登録**、Web アプリ/API アプリケーションを作成します。 **アプリケーションを登録する**ブレードは、次の値を指定して、クリックして**登録**:

   - **名前**: `AIPOnBehalfOf`
        
        必要に応じて、別の名前を指定することもできます。 名前は、テナントごとに一意である必要があります。
    
    - **勘定科目の種類がサポートされている**:**この組織のディレクトリのみでのアカウント**
    
    - **リダイレクト URI (省略可能)** :**Web**と `http://localhost`

4. **AIPOnBehalfOf**ブレードの値をコピー、**アプリケーション (クライアント) ID**します。 値は次の例のようになります:`57c3c1c3-abf9-404e-8b2b-4652836c8c66`します。 この値は、使用、 *WebAppId* Set-aipauthentication コマンドレットを実行するときにパラメーター。 貼り付けし、後で参照値を保存します。

5. **AIPOnBehalfOf**ブレードから、**管理**メニューの **認証**します。

6. **AIPOnBehalfOf - 認証**ブレードで、**詳細設定**セクションで、 **ID トークン**チェック ボックスをオンし、 **の保存**.

7. **AIPOnBehalfOf - 認証**ブレードから、**管理**メニューの **証明書およびシークレット**します。

8. **AIPOnBehalfOf - 証明書およびシークレット**ブレードで、**クライアント シークレット**セクションで、 **+ 新しいクライアント シークレット**します。 

9. **クライアント シークレットを追加**、次を指定し、**追加**:
    
    - **説明**: `Azure Information Protection client`
    - **有効期限が切れる**:任意の期間 (1 年、2 年、または期限なし)

9. 戻り、 **AIPOnBehalfOf - 証明書およびシークレット**ブレードで、**クライアント シークレット**セクションで、文字列をコピーします、**値**します。 この文字列は次の例に似ています。`+LBkMvddz?WrlNCK5v0e6_=meM59sSAn`します。 すべての文字をコピーするようにするには、アイコンを選択する**クリップボードにコピー**します。 
    
    この文字列は再び表示されることがなく、取得することもできないため、保存しておくことが重要です。 使用する機密情報と同様に安全に保存されている値を格納し、アクセスを制限します。

10. **AIPOnBehalfOf - 証明書およびシークレット**ブレードから、**管理**メニューの  **API を公開**します。

11. **AIPOnBehalfOf - 公開 API**ブレードで、**設定**の**アプリケーション ID URI**オプション、および、**アプリケーション ID URI**値、変更**api**に**http**します。 この文字列は次の例に似ています。`http://d244e75e-870b-4491-b70d-65534953099e`します。 
    
    **[保存]** を選択します。

12. 戻り、 **AIPOnBehalfOf - 公開 API**ブレードで、 **+ スコープの追加**します。

13. **スコープを追加**ブレードで、以下を指定しと例については、推奨される文字列を使用して、**スコープの追加**:
    - **スコープ名**: `user-impersonation`
    - **ユーザーが同意できるでしょうか。** :**管理者とユーザー**
    - **管理者の同意の表示名**: `Access Azure Information Protection scanner`
    - **管理者の同意の説明**: `Allow the application to access the scanner for the signed-in user`
    - **ユーザーの同意の表示名**: `Access Azure Information Protection scanner`
    - **ユーザーの同意の説明**: `Allow the application to access the scanner for the signed-in user`
    - **状態**:**有効になっている**(既定値)

14. 戻り、 **AIPOnBehalfOf - 公開 API**ブレードで、このブレードを閉じます。

15. **アプリの登録**ブレードで、 **+ 新しいアプリケーションの登録**をネイティブ アプリケーションを作成するようになりました。

16. **アプリケーションを登録する**ブレードで、次の設定を指定し、**登録**:
    - **名前**: `AIPClient`
    - **勘定科目の種類がサポートされている**:**この組織のディレクトリのみでのアカウント**
    - **リダイレクト URI (省略可能)** :**パブリック クライアント (モバイルとデスクトップ)** と `http://localhost`

17. **AIPClient**ブレードの値をコピー、**アプリケーション (クライアント) ID**します。 値は次の例のようになります:`8ef1c873-9869-4bb1-9c11-8313f9d7f76f`します。 
    
    この値は、Set-aipauthentication コマンドレットを実行するときに、NativeAppId パラメーターに使用されます。 貼り付けし、後で参照値を保存します。

18. **AIPClient**ブレードから、**管理**メニューの **認証**します。

19. **AIPClient - 認証**ブレードで、次を指定し、**保存**:
    - **詳細設定**セクションで、 **ID トークン**します。
    - **既定のクライアントの種類**セクションで、**はい**します。

20. **AIPClient - 認証**ブレードから、**管理**メニューの  **API のアクセス許可**。

21. **AIPClient - アクセス許可**ブレードで、**アクセス許可を追加 +** します。

22. **API の要求のアクセス許可**ブレードで、**マイ Api**します。

23. **API を選択します**セクションで、選択**APIOnBehalfOf**、し、チェック ボックスをオン**ユーザー偽装**、アクセス許可とします。 選択**アクセス許可の追加**します。 

24. 戻り、 **API のアクセス許可**ブレードで、**同意が付与される**セクションで、**の管理者の同意を与える\<*テナント名*>** 選択と**はい**確認プロンプトをします。

2 つのアプリの構成を完了し、パラメーターとして *WebAppId*、*WebAppKey*、*NativeAppId* を指定して [Set-AIPAuthentication](/powershell/module/azureinformationprotection/set-aipauthentication) を実行するために必要な値を取得しました。 例: から

`Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f"`

アカウントで非対話式で文書にラベルを付け、保護するという状況でこのコマンドを実行します。 たとえば、PowerShell スクリプトのユーザー アカウントやサービス アカウントで Azure Information Protection スキャナーを実行します。

このコマンドを初めて実行するとき、サインインが求められます。それにより、アカウントのアクセス トークンが作成され、%localappdata%\Microsoft\MSIP に安全に保管されます。 この初回サインイン後、コンピューターで非対話式でファイルにラベルを付け、保護できます。 ただし、ラベルにサービス アカウントを使用して、ファイルを保護するこのサービス アカウントが対話形式でサインインできない場合は、使用、 *OnBehalfOf* Set-aipauthentication パラメーター。

1. 対話形式でサインインするユーザーの権限の割り当てが許可されている Active Directory アカウントの資格情報を格納する変数を作成します。 以下に例を示します。
    
        $pscreds = Get-Credential "scv_scanner@contoso.com"

2. Set-aipauthentication コマンドレットを実行、 *OnBeHalfOf*パラメーター、先ほど作成した変数の値として指定します。 以下に例を示します。
    
        Set-AIPAuthentication -WebAppId "57c3c1c3-abf9-404e-8b2b-4652836c8c66" -WebAppKey "+LBkMvddz?WrlNCK5v0e6_=meM59sSAn" -NativeAppId "8ef1c873-9869-4bb1-9c11-8313f9d7f76f" -OnBehalfOf $pscreds

## <a name="next-steps"></a>次の手順
PowerShell セッションでは、コマンドレットのヘルプの種類`Get-Help <cmdlet name> -online`します。 以下に例を示します。 

    Get-Help Set-AIPFileLabel -online

Azure Information Protection クライアントのサポートに必要な詳細については、以下をご覧ください。

- [カスタマイズ](clientv2-admin-guide-customizations.md)

- [クライアント ファイルおよび使用状況ログの記録](clientv2-admin-guide-files-and-logging.md)

- [サポートされるファイルの種類](clientv2-admin-guide-file-types.md)
