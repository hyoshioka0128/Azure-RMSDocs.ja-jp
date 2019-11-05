---
title: Windows Server FCI での Azure RMS 保護 - AIP
description: Rights Management (RMS) クライアントと Azure Information Protection クライアントを使用して、ファイル サーバー リソース マネージャーおよびファイル分類インフラストラクチャ (FCI) を構成するための手順です。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 09/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 9aa693db-9727-4284-9f64-867681e114c9
ms.subservice: fci
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 18b8e1525fa396c6b3e6e0e040e0f0d8b21144ae
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73561161"
---
# <a name="rms-protection-with-windows-server-file-classification-infrastructure-fci"></a>Windows Server ファイル分類インフラストラクチャ (FCI) での RMS の保護

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows Server 2016、Windows Server 2012、Windows Server 2012 R2*
>
> *手順: [Windows 用の Azure Information Protection クライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

この記事では、Azure Information Protection クライアントと PowerShell を使用して、ファイル サーバー リソース マネージャーおよびファイル分類インフラストラクチャ (FCI) を構成する方法とスクリプトを示します。

このソリューションを使用すると、Windows Server を搭載するファイル サーバー上のフォルダー内のすべてのファイルを自動的に保護したり、特定の条件に一致するファイルを自動的に保護したりすることができます。 たとえば、機密性の高い情報が含まれるものとして分類されたファイルなどです。 このソリューションは Azure Information Protection から Azure Rights Management サービスに直接接続してファイルを保護するため、このサービスを組織にデプロイしておく必要があります。

> [!NOTE]
> Azure Information Protection にはファイル分類インフラストラクチャをサポートする[コネクタ](../deploy-rms-connector.md)が含まれますが、そのソリューションはネイティブな保護 (たとえば Office ファイル) のみをサポートします。
> 
> Windows Server のファイル分類インフラストラクチャで複数のファイルの種類をサポートするには、この記事で説明するように、PowerShell の **AzureInformationProtection** モジュールを使用する必要があります。 Azure Information Protection クライアントと同様に、Azure Information Protection コマンドレットは汎用的な保護とネイティブ保護をサポートしています。つまり、Office ドキュメント以外のファイルの種類も保護できます。 詳細については、「Azure Information Protection クライアント管理者ガイド」の「[File types supported by the Azure Information Protection client](client-admin-guide-file-types.md)」(Azure Information Protection クライアントでサポートされるファイルの種類) を参照してください。

以下の手順は、Windows Server 2012 R2 または Windows Server 2012 に対するものです。 サポートされている他のバージョンの Windows を使用する場合は、バージョンの違いに合わせてこの記事で説明されている手順の調整が必要な場合があります。

## <a name="prerequisites-for-azure-rights-management-protection-with-windows-server-fci"></a>Windows Server FCI での Azure Rights Management 保護の前提条件
次のような前提条件があります。

- ファイル分類インフラストラクチャでファイル リソース マネージャーを実行する各ファイル サーバーでの前提条件:
    
  - ファイル サービス ロールのロール サービスの 1 つとして、ファイル サーバー リソース マネージャーをインストールしておきます。
    
  - Rights Management で保護するファイルを含むローカル フォルダーを特定しておきます。 C:\FileShare など。
    
  - AzureInformationProtection PowerShell モジュールをインストールし、このモジュールを Azure Rights Management サービスに接続するための前提条件を構成しておきます。
    
    AzureInformationProtection PowerShell モジュールは、Azure Information Protection クライアントに含まれています。 インストール手順については、Azure Information Protection 管理者ガイドの「[Install the Azure Information Protection client for users](client-admin-guide-install.md)」(ユーザー向けに Azure Information Protection クライアントをインストールする) をご覧ください。 必要であれば、`PowerShellOnly=true` パラメーターを使用して PowerShell モジュールのみをインストールできます。
    
    [この PowerShell モジュールを使用するための前提条件](client-admin-guide-powershell.md#azure-information-protection-and-azure-rights-management-service)には、Azure Rights Management サービスをアクティブ化すること、サービス プリンシパルを作成すること、テナントが北米以外にある場合にレジストリを編集することが含まれます。 この記事の手順を開始する前に、これらの前提条件の説明で使われる **BposTenantId**、**AppPrincipalId**、**対称キー**の値を確認してください。 
    
  - 特定のファイル名拡張子に対する既定の保護レベル (ネイティブまたは汎用) を変更する場合は、管理者ガイドの「[Changing the default protection level of files](client-admin-guide-file-types.md#changing-the-default-protection-level-of-files)」(ファイルの既定の保護レベルを変更する) セクションの説明に従ってレジストリを編集します。
    
  - インターネットに接続していて、プロキシサーバーに必要な場合はコンピューターの設定を構成している。 たとえば次のようになります。`netsh winhttp import proxy source=ie`
    
- オンプレミスの Active Directory ユーザー アカウントと Azure Active Directory または Office 365 を同期しました (電子メール アドレスを含みます)。 これは、FCI および Azure Rights Management サービスによって保護された後でファイルにアクセスする必要がある可能性のあるすべてのユーザーに必要です。 この手順を実行しないと (たとえばテスト環境で)、ユーザーはこれらのファイルにアクセスできない可能性があります。 この要件に関する詳細が必要な場合は、「[Azure Information Protection 向けのユーザーとグループの準備](../prepare.md)」をご覧ください。
    
- このシナリオでは部門別テンプレートがサポートされていないため、スコープ用に構成されていないテンプレートを使用するか、 *EnableInLegacyApps*パラメーターを使用して[設定](/powershell/module/aipservice/set-aipservicetemplateproperty)する必要があります。

## <a name="instructions-to-configure-file-server-resource-manager-fci-for-azure-rights-management-protection"></a>Azure Rights Management 保護のためのファイル サーバー リソース マネージャー FCI の構成手順
PowerShell スクリプトをカスタム タスクとして使用してフォルダー内のすべてのファイルを自動的に保護するには、以下の手順に従います。 以下の手順をこの順序で実行します。

1. PowerShell スクリプトを保存する

2. Rights Management (RMS) の分類プロパティを作成する

3. 分類規則を作成する (Classify for RMS)

4. 分類スケジュールを構成する

5. カスタム ファイル管理タスクを作成する (Protect files with RMS)

6. 規則とタスクを手動で実行して構成をテストする

この手順が終了すると、選択したフォルダー内のすべてのファイルは RMS のカスタム プロパティで分類され、Rights Management によって保護されるようになります。 一部のファイルだけを選択的に保護するさらに複雑な構成の場合は、異なる分類プロパティと規則、そしてそれらのファイルだけを保護するファイル管理タスクを、作成または使用できます。

FCI で使用する Rights Management テンプレートに変更を加える場合、ファイルを保護するスクリプトを実行するコンピューター アカウントは、更新されたテンプレートを自動的に取得しません。 そのためには、スクリプトでコメント アウトされた `Get-RMSTemplate -Force` コマンドを見つけて、`#` コメント文字を削除します。 更新されたテンプレートがダウンロードされる (スクリプトが少なくとも 1 回実行される) 際に、テンプレートが不必要に毎回ダウンロードされないように、この追加のコマンドをコメント アウトできます。 テンプレートへの変更が重要であり、ファイル サーバー上のファイルを再び保護する必要がある場合、そのファイルについてエクスポートやフル コントロールの使用権限を持つアカウントで Protect-RMSFile コマンドレットを対話的に実行することにより、これを行うことができます。 FCI で使用する新しいテンプレートを発行した場合は、`Get-RMSTemplate -Force` も実行する必要があります。

### <a name="save-the-windows-powershell-script"></a>Windows PowerShell スクリプトを保存する

1.  ファイル サーバー リソース マネージャーを使用して、Azure RMS 保護のための [Windows PowerShell スクリプト](fci-script.md)の内容をコピーします。 自分のコンピューターで、スクリプトの内容を **RMS-Protect-FCI.ps1** という名前のファイルに貼り付けます。

2.  スクリプトを確認し、次のように変更します。
    
    - 次の文字列を探し、Azure Rights Management サービスに接続するために [Set-RMSServerAuthentication](/powershell/azureinformationprotection/vlatest/set-rmsserverauthentication) コマンドレットで実際に使用する AppPrincipalId に置き換えます。

        ```
        <enter your AppPrincipalId here>
        ```
        たとえば、次のようなスクリプトになります。

        `[Parameter(Mandatory = $false)]`

        `[Parameter(Mandatory = $false)]             [string]$AppPrincipalId = "b5e3f76a-b5c2-4c96-a594-a0807f65bba4",`

    -   次の文字列を探し、Azure Rights Management サービスに接続するために [Set-RMSServerAuthentication](/powershell/azureinformationprotection/vlatest/set-rmsserverauthentication) コマンドレットで実際に使用する対称キーに置き換えます。

        ```
        <enter your key here>
        ```
        たとえば、次のようなスクリプトになります。

        `[Parameter(Mandatory = $false)]`

        `[string]$SymmetricKey = "zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA="`

    -   次の文字列を探し、Azure Rights Management サービスに接続するために [Set-RMSServerAuthentication](/powershell/azureinformationprotection/vlatest/set-rmsserverauthentication) コマンドレットで実際に使用する BposTenantId (テナント ID) に置き換えます。

        ```
        <enter your BposTenantId here>
        ```
        たとえば、次のようなスクリプトになります。

        `[Parameter(Mandatory = $false)]`

        `[string]$BposTenantId = "23976bc6-dcd4-4173-9d96-dad1f48efd42",`

3.  スクリプトに署名します。 スクリプトに署名 (セキュリティを強化) しない場合は、スクリプトを実行するサーバーで Windows PowerShell を構成する必要があります。 たとえば、 **[管理者として実行]** オプションを使用して Windows PowerShell セッションを実行し、「**Set-ExecutionPolicy RemoteSigned**」と入力します。 ただし、この構成を使用すると、署名されていないすべてのスクリプトは、このサーバーに保存されている場合に実行できます (セキュリティは低下)。

    Windows PowerShell スクリプトへの署名の詳細については、PowerShell のドキュメント ライブラリの「 [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) 」を参照してください。

4.  ファイル リソース マネージャーとファイル分類インフラストラクチャを実行する各ファイル サーバーにローカルにファイルを保存します。 たとえば、ファイルを **C:\RMS-Protection** に保存します。 別のパスまたはフォルダーの名前を使用する場合は、スペースを含まないパスとフォルダーを選択してください。 承認されていないユーザーが変更できないように、NTFS アクセス許可を使用してこのファイルをセキュリティ保護します。

これで、ファイル サーバー リソース マネージャーの構成を開始する準備ができました。

### <a name="create-a-classification-property-for-rights-management-rms"></a>Rights Management (RMS) の分類プロパティを作成する

-   ファイル サーバー リソース マネージャーの [分類管理] で、新しいローカル プロパティを作成します。

    -   **[名前]** :「 **RMS**」と入力します

    -   **[説明]** : 「 **Rights Management の保護**」と入力します

    -   **[プロパティの型]** : **[はい/いいえ]** を選択します。

    -   **[値]** : **[はい]** を選択します

このプロパティを使用する分類規則を作成できるようになります。

### <a name="create-a-classification-rule-classify-for-rms"></a>分類規則を作成する (Classify for RMS)

-   新しい分類規則を作成します。

    -   **[全般]** タブで次のように設定します。

        -   **[名前]** :「 **Classify for RMS**」と入力します。

        -   **[有効]** : 既定のオンのままにします。

        -   **[説明]** : 「**Rights Management 用に &lt;フォルダー名&gt; フォルダーのすべてのファイルを分類する**」と入力します。

            *&lt;フォルダー名&gt;* は選択したフォルダーの名前に置き換えます。 例: **Classify all files in the C:\FileShare folder for Rights Management**。

        -   **[スコープ]** :選択したフォルダーを追加します。 例: **C:\FileShare**。

            チェック ボックスはオンにしません。

    -   **[分類]** タブで次のように設定します。

    -   **[分類方法]** : **[フォルダー分類子]** を選択します

    -   **[プロパティ]** の名前: **[RMS]** を選択します

    -   プロパティの **[値]** : **[はい]** を選択します

分類規則は手動でも実行できますが、継続的に運用する場合は、この規則を実行するスケジュールを設定し、新しいファイルが RMS プロパティで分類されるようにします。

### <a name="configure-the-classification-schedule"></a>分類スケジュールを構成する

-   **[自動分類]** タブで次のように設定します。

    -   **[固定スケジュールを有効にする]** :このチェック ボックスをオンにします。

    -   実行するすべての分類規則のスケジュールを構成します。これには、RMS のプロパティでファイルを分類する新しい規則も含まれます。

    -   **[新しいファイルの連続分類を許可する]** : 新しいファイルが分類されるように、このチェック ボックスをオンにします。

    -   省略可能:レポートと通知のオプションの構成など、他の必要な変更を行います。

分類の構成が完了したので、ファイルに RMS 保護を適用する管理タスクを構成できます。

### <a name="create-a-custom-file-management-task-protect-files-with-rms"></a>カスタム ファイル管理タスクを作成する (Protect files with RMS)

-   **[ファイル管理タスク]** で新しいファイル管理タスクを作成します。

    -   **[全般]** タブで次のように設定します。

        -   **[タスク名]** :「 **Protect files with RMS**」と入力します。

        -   **[有効]** チェック ボックスはオンのままにします。

        -   **説明**: 「 **&lt;フォルダー名&gt; のファイルを Windows PowerShell スクリプトを使用して Rights Management とテンプレートで保護する**」と入力します。

            *&lt;フォルダー名&gt;* は選択したフォルダーの名前に置き換えます。 例: **Protect files in C:\FileShare with Rights Management and a template by using a Windows PowerShell script**。

        -   **[スコープ]** :選択したフォルダーを選択します。 例: **C:\FileShare**。

            チェック ボックスはオンにしません。

    -   **[アクション]** タブで次のように設定します。

        -   **[種類]** : **[カスタム]** を選択します。

        -   **[実行可能ファイル]** :次のように指定します。

            ```
            C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
            ```
            Windows が C: ドライブにない場合は、このパスを変更するか、このファイルを参照します。

        -   **引数**: 次のように指定します。&lt;path&gt; と &lt;template ID&gt; は実際の値に置き換えます。

            ```
            -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID <template GUID> -OwnerMail '[Source File Owner Email]'"
            ```
            たとえば、スクリプトを C:\RMS-Protection にコピーし、前提条件で確認したテンプレート ID が e6ee2481-26b9-45e5-b34a-f744eacd53b0 である場合は、次のように指定します。

            `-Noprofile -Command "C:\RMS-Protection\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID e6ee2481-26b9-45e5-b34a-f744eacd53b0 -OwnerMail '[Source File Owner Email]'"`

            このコマンドで、 **[Source File Path]** (ソース ファイル パス) と **[Source File Owner Email]** (ソース ファイル所有者電子メール) はどちらも FCI 固有の値なので、上のコマンドで表示された値を正確に入力します。 最初の変数は、フォルダーで識別されたファイルを自動的に指定するために FCI によって使用され、2 番目の変数は、FCI が識別されたファイルの指定所有者の電子メール アドレスを自動的に取得するために使用されます。 このコマンドが、フォルダー内のファイルごとに繰り返されます。この例では、ファイル分類プロパティとして RMS が指定されている C:\FileShare フォルダー内の各ファイルです。

            > [!NOTE]
            > **-OwnerMail [Source File Owner Email]** パラメーターと値により、ファイルの元の所有者に、保護された後のファイルの Rights Management 所有者が付与されます。 この構成により、元のファイル所有者は自分のファイルに対するすべての Rights Management 権限を持ちます。 ファイルがドメイン ユーザーによって作成されると、ファイルの Owner プロパティのユーザー アカウント名を使用して Active Directory から電子メール アドレスが自動的に取得されます。 そのためには、ファイル サーバーがユーザーと同じドメインまたは信頼されるドメインに存在している必要があります。
            > 
            > 可能な場合は常に、元の所有者を保護されたドキュメントに割り当て、これらのユーザーが自分で作成したファイルを完全に制御し続けることができるようにしてください。 ただし、上のコマンドの [Source File Owner Email] 変数を使用した場合、ファイルに所有者として定義されたドメイン ユーザーがないと (たとえば、ファイルの作成にローカル アカウントが使用されて、所有者に SYSTEM と表示される場合)、スクリプトは失敗します。
            > 
            > 所有者としてのドメイン ユーザーがないファイルの場合は、ファイルをコピーし、自分をドメイン ユーザーとしてファイルを保存することにより、これらのファイルの所有者になることができます。 または、権限がある場合は、所有者を手動で変更できます。  または、[Source File Owner Email] 変数の代わりに、特定の電子メール アドレス (自分のアドレスや、IT 部門のグループ アドレスなど) を指定することもできます。これは、このスクリプトを使用して保護するすべてのファイルが、その電子メール アドレスを使用して新しい所有者を定義することを意味します。

    -   **[コマンドの実行]** : **[ローカル システム]** を選択します。

    -   **[条件]** タブで次のように設定します。

        -   **[プロパティ]** : **[RMS]** を選択します

        -   **[演算子]** : **[EQUAL]** を選択します。

        -   **[値]** : **[はい]** を選択します

    -   **[スケジュール]** タブで次のように設定します。

        -   **[実行時期]** :希望のスケジュールを構成します。

            スクリプトが完了するのに十分な時間を指定します。 このソリューションはフォルダー内のすべてのファイルを保護しますが、スクリプトは、毎回、ファイルごとに 1 回実行します。 これは Azure Information Protection クライアントがサポートするような同時にすべてのファイルを保護する方法より時間がかかりますが、FCI のファイル単位の構成の方がいっそう強力です。 たとえば、[Source File Owner Email] 変数を使用すると保護されるファイルの所有者が異なっていてもかまいません (元の所有者の維持)。また、フォルダー内のすべてのファイルではなく一部のファイルだけを選択して保護するように後で構成を変更する場合は、このファイル単位のアクションが必要になります。

        -   **[新しいファイルに対して連続実行する]** :このチェック ボックスをオンにします。

### <a name="test-the-configuration-by-manually-running-the-rule-and-task"></a>規則とタスクを手動で実行して構成をテストする

1.  分類規則を実行します。

    1.  **[分類規則]** &gt; **[すべての規則で今すぐ分類を実行する]** の順にクリックします。

    2.  **[分類の完了を待つ]** をクリックし、 **[OK]** をクリックします。

2.  **[分類を実行しています]** ダイアログ ボックスが閉じるまで待ってから、自動的に表示されるレポートで結果を確認します。 **[プロパティ]** フィールドは **1** になっていて、フォルダー内のファイルの数が表示されています。 ファイル エクスプローラーを使用して、選択したフォルダー内のファイルのプロパティを確認します。 **[分類]** タブには、プロパティの名前として「 **RMS** 」が、 **[値]** として **[はい]** が表示されます。

3.  ファイル管理タスクを実行します。

    1.  **[ファイル管理タスク]** &gt; **[Protect files with RMS (RMS でファイルを保護)]** &gt; **[ファイル管理タスクを今すぐ実行する]** の順にクリックします。

    2.  **[タスクの完了を待つ]** をクリックし、 **[OK]** をクリックします。

4.  **[ファイル管理タスクを実行中]** ダイアログ ボックスが閉じるまで待ってから、自動的に表示されるレポートで結果を確認します。 選択したフォルダーにあるファイルの数が、 **[ファイル]** フィールドに表示されます。 選択したフォルダー内のファイルが Rights Management によって保護されていることを確認します。 たとえば、フォルダー C:\FileShare を選択した場合は、Windows PowerShell セッションで次のコマンドを入力し、どのファイルの状態も **Unprotected** ではないことを確認します。

    ```
    foreach ($file in (Get-ChildItem -Path C:\FileShare -Force | where {!$_.PSIsContainer})) {Get-RMSFileStatus -f $file.PSPath}
    ```
    > [!TIP]
    > トラブルシューティングに関するヒント:
    > 
    > -   レポートにフォルダーのファイルの数ではなく **0** と表示されている場合は、この出力はスクリプトが実行されなかったことを示します。 まず、スクリプトを Windows PowerShell ISE に読み込んで内容を確認し、同じ PowerShell セッションで 1 回実行してみて、エラーが表示されるかどうかを調べます。 引数を指定しないと、スクリプトは Azure Rights Management サービスに接続して認証を試みます。
    > 
    >     -   スクリプトで Azure Rights Management サービス (Azure RMS) に接続できなかったことが示される場合は、そこで表示される、スクリプトで指定したサービス プリンシパル アカウントの値を確認します。 このサービス プリンシパル アカウントを作成する方法については、「Azure Information Protection クライアント管理者ガイド」の「[Prerequisite 3: To protect or unprotect files without interaction](client-admin-guide-powershell.md#prerequisite-3-to-protect-or-unprotect-files-without-user-interaction)」(前提条件 3: ユーザー操作なしでファイルの保護または保護の解除を行うには) を参照してください。
    >     -   スクリプトで Azure RMS に接続できたことが示される場合は、次にサーバー上で Windows PowerShell から直接 [Get-RMSTemplate](/powershell/azureinformationprotection/vlatest/get-rmstemplate) を実行して、指定されたテンプレートを見つけることができるかどうかを確認します。 指定したテンプレートが結果に返されます。
    > -   スクリプト自体を Windows PowerShell ISE で実行してもエラーが発生しない場合は、次のように保護するファイルの名前を指定し、-OwnerEmail パラメーターを指定しないで、PowerShell セッションからスクリプトを実行してみます。
    > 
    >     ```
    >     powershell.exe -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '<full path and name of a file>' -TemplateID <template GUID>"
    >     ```
    >     -   この Windows PowerShell セッションでスクリプトが正常に実行する場合は、ファイル管理タスク アクションでの **[実行可能ファイル]** と **[引数]** の指定を確認します。  **-OwnerEmail [Source File Owner Email]** を指定した場合は、このパラメーターを削除してみます。
    > 
    >         **-OwnerEmail [Source File Owner Email]** なしでファイル管理タスクが正常に動作する場合は、保護されていないファイルのファイル所有者として **SYSTEM** ではなくドメイン ユーザーが表示されるかどうかを確認します。  この確認を行うには、ファイルのプロパティの **[セキュリティ]** タブの **[高度]** をクリックします。 **[所有者]** の値はファイルの **[名前]** の直後に表示されます。 また、ファイル サーバーが同じドメインまたは信頼されたドメインにあって Active Directory ドメイン サービスからユーザーの電子メール アドレスを参照することを確認します。
    > -   正しいファイルの数がレポートで示されているにもかかわらず、ファイルが保護されていない場合は、 [Protect-RMSFile](/powershell/azureinformationprotection/vlatest/protect-rmsfile) コマンドレットを使用して手動でファイルを保護してみて、エラーが表示されるかどうかを確認します。

これらのタスクが正常に動作することを確認した後、ファイル リソース マネージャーを閉じることができます。 スケジュールしたタスクが実行されると、新しいファイルは自動的に分類および保護されます。 

## <a name="action-required-if-you-make-changes-to-the-rights-management-template"></a>Rights Management テンプレートに変更を加える場合に必要なアクション

スクリプトが参照する Rights Management テンプレートに変更を加える場合、ファイルを保護するスクリプトを実行するコンピューター アカウントは、更新されたテンプレートを自動的に取得しません。 スクリプトで、Set-RMSConnection 関数内のコメント アウトされた `Get-RMSTemplate -Force` コマンドを見つけ、行の先頭にあるコメント文字を削除します。 スクリプトが次回実行されると、更新されたテンプレートがダウンロードされます。 テンプレートが不必要にダウンロードされないようにパフォーマンスを最適化するには、この行をもう一度コメント アウトします。 

テンプレートへの変更が重要であり、ファイル サーバー上のファイルを再び保護する必要がある場合、そのファイルについてエクスポートやフル コントロールの使用権限を持つアカウントで Protect-RMSFile コマンドレットを対話的に実行することにより、これを行うことができます。 

FCI で使用する新しいテンプレートを発行し、カスタム ファイル管理タスクの引数行内のテンプレート ID を変更する場合にも、スクリプトでこの行を実行します。

## <a name="modifying-the-instructions-to-selectively-protect-files"></a>選択的にファイルを保護するための手順の変更
上の手順で問題がなければ、さらに高度な構成に変更することが簡単にできます。 たとえば、同じスクリプトを使用して個人識別情報を含むファイルだけを保護し、さらに制限の厳しい権限のテンプレートを選択できます。

この変更を行うには、組み込まれている分類プロパティのいずれかを使用するか (たとえば **[個人を特定できる情報]** )、新しいプロパティを作成します。 そして、このプロパティを使用する新しい規則を作成します。 たとえば、 **[コンテンツ分類子]** を選択し、 **[個人の身元を特定する情報]** プロパティと値 **[高]** を選択して、このプロパティ用に構成するファイルを識別する文字列または式パターンを構成します (たとえば、文字列"**Date of Birth**")。

そのためには、同じスクリプトとおそらく異なるテンプレートを使用する新しいファイル管理タスクを作成し、構成した分類プロパティの条件を構成する必要があります。 たとえば、前に構成した条件 ( **[RMS]** プロパティ、 **[EQUAL]** 、 **[はい]** ) の代わりに、 **[個人の身元を特定する情報]** プロパティを選択し、 **[演算子]** を **[EQUAL]** に、 **[値]** を **[高]** に設定します。

## <a name="next-steps"></a>次のステップ

[Windows Server FCI と Azure Information Protection スキャナーの違い](../faqs.md#whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner)についてご説明します。 

