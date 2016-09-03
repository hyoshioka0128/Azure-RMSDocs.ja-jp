---
title: "Windows Server ファイル分類インフラストラクチャ (FCI) での RMS の保護 | Azure RMS"
description: "この記事では、Rights Management (RMS) クライアントと RMS 保護ツールを使用して、ファイル サーバー リソース マネージャーおよびファイル分類インフラストラクチャ (FCI) を構成する方法とスクリプトを示します。"
author: cabailey
manager: mbaldwin
ms.date: 06/14/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 9aa693db-9727-4284-9f64-867681e114c9
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: 431eb994070391a78b0b8e34b1afb668f0981f0f


---

# Windows Server ファイル分類インフラストラクチャ (FCI) での RMS の保護

>*適用対象: Azure Rights Management、Windows Server 2012、Windows Server 2012 R2*

この記事では、Rights Management (RMS) クライアントと RMS 保護ツールを使用して、ファイル サーバー リソース マネージャーおよびファイル分類インフラストラクチャ (FCI) を構成する方法とスクリプトを示します。

このソリューションを使用すると、Windows Server を搭載するファイル サーバー上のフォルダー内のすべてのファイルを自動的に保護したり、特定の条件に一致するファイルを自動的に保護したりすることができます。 たとえば、機密性の高い情報が含まれるものとして分類されたファイルなどです。 このソリューションは Azure Rights Management (Azure RMS) を使用してファイルを保護するため、このテクノロジを組織にデプロイしておく必要があります。

> [!NOTE]
> Azure RMS にはファイル分類インフラストラクチャをサポートする[コネクタ](../deploy-use/deploy-rms-connector.md)が含まれますが、そのソリューションはネイティブな保護 (たとえば Office ファイル) のみをサポートします。
> 
> ファイル分類インフラストラクチャですべてのファイルの種類をサポートするには、この記事で説明するように、Windows PowerShell の **RMS 保護** モジュールを使用する必要があります。 RMS 保護コマンドレットは、RMS 共有アプリケーションのように、一般的な保護だけでなくネイティブな保護もサポートするため、すべてのファイルが保護されることを意味します。 各種の保護レベルの詳細については、「[Rights Management 共有アプリケーション管理者ガイド](sharing-app-admin-guide.md)」の「[保護のレベル - ネイティブと汎用](sharing-app-admin-guide-technical.md#levels-of-protection-native-and-generic)」セクションを参照してください。

以下の手順は、Windows Server 2012 R2 または Windows Server 2012 に対するものです。 サポートされている他のバージョンの Windows を使用する場合は、バージョンの違いに合わせてこの記事で説明されている手順の調整が必要な場合があります。

## Windows Server FCI での Azure RMS 保護の前提条件
次のような前提条件があります。

-   ファイル分類インフラストラクチャでファイル リソース マネージャーを実行する各ファイル サーバーでの前提条件:

    -   ファイル サービス ロールのロール サービスの 1 つとして、ファイル サーバー リソース マネージャーをインストールしておきます。

    -   Rights Management で保護するファイルを含むローカル フォルダーを特定しておきます。 C:\FileShare など。

    -   RMS 保護ツールをインストールしておきます。これには、ツールに必要なもの (RMS クライアントなど) および Azure RMS に必要なもの (サービス プリンシパル アカウントなど) も含まれます。 詳細については、「 [RMS Protection Cmdlets (RMS 保護コマンドレット)](https://msdn.microsoft.com/library/azure/mt433195.aspx)」を参照してください。

    -   特定のファイル名拡張子に対する既定の RMS 保護レベル (ネイティブまたは汎用) を変更する場合は、「[File API configuration (File API の構成)](https://msdn.microsoft.com/library/dn197834%28v=vs.85%29.aspx)」ページの説明に従ってレジストリを編集します。

    -   インターネット接続を設定し、プロキシ サーバーに必要な場合はコンピューターの設定を構成します。 例: `netsh winhttp import proxy source=ie`

-   「 [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx)」の説明に従って、Azure Rights Management のデプロイメントに関する他の前提条件を構成しておきます。 具体的には、サービス プリンシパルを使用して Azure RMS に接続するには次の値があります。

    -   BposTenantId

    -   AppPrincipalId

    -   対称キー

-   オンプレミスの Active Directory ユーザー アカウントと Azure Active Directory または Office 365 を同期しました (電子メール アドレスを含みます)。 これは、FCI および Azure RMS によって保護された後でファイルにアクセスする必要がある可能性のあるすべてのユーザーに必要です。 この手順を実行しないと (たとえばテスト環境で)、ユーザーはこれらのファイルにアクセスできない可能性があります。 このアカウント構成の詳細については、「[Azure Rights Management の準備を行う](../plan-design/prepare.md)」を参照してください。

-   ファイルの保護に使用する Rights Management テンプレートを特定しておきます。 [Get-RMSTemplate](https://msdn.microsoft.com/library/azure/mt433197.aspx) コマンドレットを使用して、このテンプレートの ID を確認します。

## Azure RMS 保護のためのファイル サーバー リソース マネージャー FCI の構成手順
Windows PowerShell スクリプトをカスタム タスクとして使用してフォルダー内のすべてのファイルを自動的に保護するには、以下の手順に従います。 以下の手順をこの順序で実行します。

1.  Windows PowerShell スクリプトを保存する

2.  Rights Management (RMS) の分類プロパティを作成する

3.  分類規則を作成する (Classify for RMS)

4.  分類スケジュールを構成する

5.  カスタム ファイル管理タスクを作成する (Protect files with RMS)

6.  規則とタスクを手動で実行して構成をテストする

この手順が終了すると、選択したフォルダー内のすべてのファイルは RMS のカスタム プロパティで分類され、Rights Management によって保護されるようになります。 一部のファイルだけを選択的に保護するさらに複雑な構成の場合は、異なる分類プロパティと規則、そしてそれらのファイルだけを保護するファイル管理タスクを、作成または使用できます。

### Windows PowerShell スクリプトを保存する

1.  ファイル サーバー リソース マネージャーを使用して、Azure RMS 保護のための [Windows PowerShell スクリプト](fci-script.md)の内容をコピーします。 自分のコンピューターで、スクリプトの内容を **RMS-Protect-FCI.ps1** という名前のファイルに貼り付けます。

2.  スクリプトを確認し、次のように変更します。

    -   次の文字列を探し、Azure RMS に接続するために [Set-RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) コマンドレットで実際に使用する AppPrincipalId に置き換えます。

        ```
        <enter your AppPrincipalId here>
        ```
        たとえば、次のようなスクリプトになります。

        `[Parameter(Mandatory = $false)]`

        `[Parameter(Mandatory = $false)]             [string]$AppPrincipalId = "b5e3f76a-b5c2-4c96-a594-a0807f65bba4",`

    -   次の文字列を探し、Azure RMS に接続するために [Set-RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) コマンドレットで実際に使用する対称キーに置き換えます。

        ```
        <enter your key here>
        ```
        たとえば、次のようなスクリプトになります。

        `[Parameter(Mandatory = $false)]`

        `[string]$SymmetricKey = "zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA="`

    -   次の文字列を探し、Azure RMS に接続するために [Set-RMSServerAuthentication](https://msdn.microsoft.com/library/mt433199.aspx) コマンドレットで実際に使用する BposTenantId (テナント ID) に置き換えます。

        ```
        <enter your BposTenantId here>
        ```
        たとえば、次のようなスクリプトになります。

        `[Parameter(Mandatory = $false)]`

        `[string]$BposTenantId = "23976bc6-dcd4-4173-9d96-dad1f48efd42",`

    -   サーバーが Windows Server 2012 を搭載している場合は、スクリプトの先頭で RMSProtection モジュールを手動で読み込むことが必要な場合があります。 次のコマンドを追加します ("Program Files" フォルダーが C: ドライブ以外にある場合はそれに合わせます)。

        ```
        Import-Module "C:\Program Files\WindowsPowerShell\Modules\RMSProtection\RMSProtection.dll"
        ```

3.  スクリプトに署名します。 スクリプトに署名 (セキュリティを強化) しない場合は、スクリプトを実行するサーバーで Windows PowerShell を構成する必要があります。 たとえば、**[管理者として実行]** オプションを使用して Windows PowerShell セッションを実行し、「**Set-ExecutionPolicy RemoteSigned**」と入力します。 ただし、この構成を使用すると、署名されていないすべてのスクリプトは、このサーバーに保存されている場合に実行できます (セキュリティは低下)。

    Windows PowerShell スクリプトへの署名の詳細については、PowerShell のドキュメント ライブラリの「 [about_Signing](https://technet.microsoft.com/library/hh847874.aspx) 」を参照してください。

4.  ファイル リソース マネージャーとファイル分類インフラストラクチャを実行する各ファイル サーバーにローカルにファイルを保存します。 たとえば、ファイルを **C:\RMS-Protection** に保存します。 承認されていないユーザーが変更できないように、NTFS アクセス許可を使用してこのファイルをセキュリティ保護します。

これで、ファイル サーバー リソース マネージャーの構成を開始する準備ができました。

### Rights Management (RMS) の分類プロパティを作成する

-   ファイル サーバー リソース マネージャーの [分類管理] で、新しいローカル プロパティを作成します。

    -   [**名前**]:「 **RMS**」と入力します

    -   [**説明**]: 「 **Rights Management の保護**」と入力します

    -   **[プロパティの型]**: **[はい/いいえ]** を選択します。

    -   [**値**]:[ **はい**] を選択します

このプロパティを使用する分類規則を作成できるようになります。

### 分類規則を作成する (Classify for RMS)

-   新しい分類規則を作成します。

    -   [ **全般** ] タブで次のように設定します。

        -   [**名前**]:「 **Classify for RMS**」と入力します。

        -   [**有効**]:既定のオンのままにします。

        -   **[説明]**: 「**Rights Management 用に &lt;フォルダー名&gt; フォルダーのすべてのファイルを分類する**」と入力します。

            *&lt;フォルダー名&gt;* は選択したフォルダーの名前に置き換えます。 例: **Classify all files in the C:\FileShare folder for Rights Management**。

        -   [**スコープ**]:選択したフォルダーを追加します。 例: **C:\FileShare**。

            チェック ボックスはオンにしません。

    -   [ **分類** ] タブで次のように設定します。

    -   [**分類方法**]:[ **フォルダー分類子**] を選択します

    -   [**プロパティ** ] の名前:[ **RMS**] を選択します

    -   プロパティの [ **値**]:[ **はい**] を選択します

分類規則は手動でも実行できますが、継続的に運用する場合は、この規則を実行するスケジュールを設定し、新しいファイルが RMS プロパティで分類されるようにします。

### 分類スケジュールを構成する

-   [ **自動分類** ] タブで次のように設定します。

    -   [**固定スケジュールを有効にする**]:このチェック ボックスをオンにします。

    -   実行するすべての分類規則のスケジュールを構成します。これには、RMS のプロパティでファイルを分類する新しい規則も含まれます。

    -   [**新しいファイルの連続分類を許可する**]:新しいファイルが分類されるように、このチェック ボックスをオンにします。

    -   省略可能:レポートと通知のオプションの構成など、他の必要な変更を行います。

分類の構成が完了したので、ファイルに RMS 保護を適用する管理タスクを構成できます。

### カスタム ファイル管理タスクを作成する (Protect files with RMS)

-   [ **ファイル管理タスク**] で新しいファイル管理タスクを作成します。

    -   [ **全般** ] タブで次のように設定します。

        -   [**タスク名**]:「 **Protect files with RMS**」と入力します。

        -   [ **有効** ] チェック ボックスはオンのままにします。

        -   **説明**: 「**&lt;フォルダー名&gt; のファイルを Windows PowerShell スクリプトを使用して Rights Management とテンプレートで保護する**」と入力します。

            *&lt;フォルダー名&gt;* は選択したフォルダーの名前に置き換えます。 例: **Protect files in C:\FileShare with Rights Management and a template by using a Windows PowerShell script**。

        -   [**スコープ**]:選択したフォルダーを選択します。 例: **C:\FileShare**。

            チェック ボックスはオンにしません。

    -   [ **アクション** ] タブで次のように設定します。

        -   [**種類**]:[ **カスタム**] を選択します。

        -   [**実行可能ファイル**]:次のように指定します。

            ```
            C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
            ```
            Windows が C: ドライブにない場合は、このパスを変更するか、このファイルを参照します。

        -   **引数**: 次のように指定します。&lt;path&gt; と &lt;template ID&gt; は実際の値に置き換えます。

            ```
            -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID <template GUID> -OwnerMail [Source File Owner Email]"
            ```
            たとえば、スクリプトを C:\RMS-Protection にコピーし、前提条件で確認したテンプレート ID が e6ee2481-26b9-45e5-b34a-f744eacd53b0 である場合は、次のように指定します。

            `-Noprofile -Command "C:\RMS-Protection\RMS-Protect-FCI.ps1 -File '[Source File Path]' -TemplateID e6ee2481-26b9-45e5-b34a-f744eacd53b0 -OwnerMail [Source File Owner Email]"`

            このコマンドで、**[Source File Path]** (ソース ファイル パス) と **[Source File Owner Email]** (ソース ファイル所有者電子メール) はどちらも FCI 固有の値なので、上のコマンドで表示された値を正確に入力します。 1 番目は、フォルダーで識別されたファイルを自動的に指定するために FCI によって使用され、2 番目は、FCI が識別されたファイルの指定所有者の電子メール アドレスを自動的に取得するために使用されます。 このコマンドが、フォルダー内のファイルごとに繰り返されます。この例では、ファイル分類プロパティとして RMS が指定されている C:\FileShare フォルダー内の各ファイルです。

            > [!NOTE]
            > **-OwnerMail [Source File Owner Email]** パラメーターと値により、ファイルの元の所有者に、保護された後のファイルの Rights Management 所有者が付与されます。 これにより、元のファイル所有者は自分のファイルに対するすべての Rights Management 権限を持ちます。 ファイルがドメイン ユーザーによって作成されると、ファイルの Owner プロパティのユーザー アカウント名を使用して Active Directory から電子メール アドレスが自動的に取得されます。 そのためには、ファイル サーバーがユーザーと同じドメインまたは信頼されるドメインに存在している必要があります。
            > 
            > 可能な場合は常に、元の所有者を保護されたドキュメントに割り当て、これらのユーザーが自分で作成したファイルを完全に制御し続けることができるようにしてください。 ただし、上の [Source File Owner Email] 変数を使用した場合、ファイルに所有者として定義されたドメイン ユーザーがないと (たとえば、ファイルの作成にローカル アカウントが使用されて、所有者に SYSTEM と表示される場合)、スクリプトは失敗します。
            > 
            > 所有者としてのドメイン ユーザーがないファイルの場合は、ファイルをコピーし、自分をドメイン ユーザーとしてファイルを保存することにより、これらのファイルの所有者になることができます。 または、権限がある場合は、所有者を手動で変更できます。  または、[Source File Owner Email] 変数の代わりに、特定の電子メール アドレス (自分のアドレスや、IT 部門のグループ アドレスなど) を指定することもできます。これは、このスクリプトを使用して保護するすべてのファイルが、その電子メール アドレスを使用して新しい所有者を定義することを意味します。

    -   [**コマンドの実行**]:[ **ローカル システム**] を選択します。

    -   [ **条件** ] タブで次のように設定します。

        -   [**プロパティ**]:[ **RMS**] を選択します

        -   [**演算子**]:[ **EQUAL**] を選択します。

        -   [**値**]:[ **はい**] を選択します

    -   [ **スケジュール** ] タブで次のように設定します。

        -   [**実行時期**]:希望のスケジュールを構成します。

            スクリプトが完了するのに十分な時間を指定します。 このソリューションはフォルダー内のすべてのファイルを保護しますが、スクリプトは、毎回、ファイルごとに 1 回実行します。 これは RMS 保護ツールがサポートするような同時にすべてのファイルを保護する方法より時間がかかりますが、FCI のファイル単位の構成の方がいっそう強力です。 たとえば、[Source File Owner Email] 変数を使用すると保護されるファイルの所有者が異なっていてもかまいません (元の所有者の維持)。また、フォルダー内のすべてのファイルではなく一部のファイルだけを選択して保護するように後で構成を変更する場合は、このファイル単位のアクションが必要になります。

        -   [**新しいファイルに対して連続実行する**]:このチェック ボックスをオンにします。

### 規則とタスクを手動で実行して構成をテストする

1.  分類規則を実行します。

    1.  **[分類規則]** &gt; **[すべての規則で今すぐ分類を実行する]** の順にクリックします。

    2.  [ **分類の完了を待つ**] をクリックし、[ **OK**] をクリックします。

2.  [ **分類を実行しています** ] ダイアログ ボックスが閉じるまで待ってから、自動的に表示されるレポートで結果を確認します。 [ **プロパティ** ] フィールドは **1** になっていて、フォルダー内のファイルの数が表示されています。 ファイル エクスプローラーを使用して、選択したフォルダー内のファイルのプロパティを確認します。 [ **分類** ] タブには、プロパティの名前として「 **RMS** 」が、[ **値** ] として [ **はい**] が表示されます。

3.  ファイル管理タスクを実行します。

    1.  **[ファイル管理タスク]** &gt; **[Protect files with RMS (RMS でファイルを保護)]** &gt; **[ファイル管理タスクを今すぐ実行する]** の順にクリックします。

    2.  [ **タスクの完了を待つ**] をクリックし、[ **OK**] をクリックします。

4.  [ **ファイル管理タスクを実行中** ] ダイアログ ボックスが閉じるまで待ってから、自動的に表示されるレポートで結果を確認します。 選択したフォルダーにあるファイルの数が、[ **ファイル** ] フィールドに表示されます。 選択したフォルダーのファイルが RMS によって保護されていることを確認します。 たとえば、フォルダー C:\FileShare を選択した場合は、Windows PowerShell セッションで次のコマンドを入力し、どのファイルの状態も **UnProtected** ではないことを確認します。

    ```
    foreach ($file in (Get-ChildItem -Path C:\FileShare -Force | where {!$_.PSIsContainer})) {Get-RMSFileStatus -f $file.PSPath}
    ```
    > [!TIP]
    > トラブルシューティングに関するヒント:
    > 
    > -   レポートにフォルダーのファイルの数ではなく **0** と表示されている場合は、スクリプトが実行されなかったことを示します。 まず、スクリプトを Windows PowerShell ISE に読み込んで内容を確認し、実行してエラーが表示されるかどうかを調べます。 引数を指定しないと、スクリプトは Azure RMS に接続して認証を試みます。
    > 
    >     -   スクリプトで Azure RMS に接続できなかったことが示される場合は、そこで表示される、スクリプトで指定したサービス プリンシパル アカウントの値を確認します。  このサービス プリンシパル アカウントを作成する方法の詳細は、「 [about_RMSProtection_AzureRMS](https://msdn.microsoft.com/library/mt433202.aspx)」の 2 番目の前提条件を参照してください。
    >     -   スクリプトで Azure RMS に接続できたことが示される場合は、次にサーバー上で Windows PowerShell から直接 [Get-RMSTemplate](https://msdn.microsoft.com/library/mt433197.aspx) を実行して、指定されたテンプレートを見つけることができるかどうかを確認します。 指定したテンプレートが結果に返されます。
    > -   スクリプト自体を Windows PowerShell ISE で実行してもエラーが発生しない場合は、次のように保護するファイルの名前を指定し、-OwnerEmail パラメーターを指定しないで、PowerShell セッションからスクリプトを実行してみます。
    > 
    >     ```
    >     powershell.exe -Noprofile -Command "<path>\RMS-Protect-FCI.ps1 -File '<full path and name of a file>' -TemplateID <template GUID>"
    >     ```
    >     -   この Windows PowerShell セッションでスクリプトが正常に実行する場合は、ファイル管理タスク アクションでの [ **実行可能ファイル** ] と [ **引数** ] の指定を確認します。  **-OwnerEmail [Source File Owner Email]** を指定した場合は、このパラメーターを削除してみます。
    > 
    >         **-OwnerEmail [Source File Owner Email]** なしでファイル管理タスクが正常に動作する場合は、保護されていないファイルのファイル所有者として **SYSTEM** ではなくドメイン ユーザーが表示されるかどうかを確認します。  そのためには、ファイルのプロパティの **[セキュリティ]** タブの **[高度]** をクリックします。 **[所有者]** の値はファイルの **[名前]** の直後に表示されます。 また、ファイル サーバーが同じドメインまたは信頼されたドメインにあって Active Directory ドメイン サービスからユーザーの電子メール アドレスを参照することを確認します。
    > -   正しいファイルの数がレポートで示されているにもかかわらず、ファイルが保護されていない場合は、 [Protect-RMSFile](https://msdn.microsoft.com/library/azure/mt433201.aspx) コマンドレットを使用して手動でファイルを保護してみて、エラーが表示されるかどうかを確認します。

これらのタスクが正常に動作することを確認した後、ファイル リソース マネージャーを閉じることができます。 新しいファイルが自動的に保護され、スケジュールが実行するとすべてのファイルが再び保護されます。 ファイルを再保護すると、テンプレートへの変更がファイルに適用されることが保証されます。


## 選択的にファイルを保護するための手順の変更
前期の手順で問題がなければ、より高度な構成用に非常に簡単に変更できます。 たとえば、同じスクリプトを使用して個人識別情報を含むファイルだけを保護し、さらに制限の厳しい権限のテンプレートを選択できます。

そのためには、組み込まれている分類プロパティのいずれかを使用するか (たとえば **[Personally Identifiable Information]** (個人を特定できる情報))、新しいプロパティを作成します。 そして、このプロパティを使用する新しい規則を作成します。 たとえば、[ **コンテンツ分類子**] を選択し、[ **個人の身元を特定する情報** ] プロパティと値 [ **高**] を選択して、このプロパティ用に構成するファイルを識別する文字列または式パターンを構成します (たとえば、文字列"**Date of Birth**")。

そのためには、同じスクリプトとおそらく異なるテンプレートを使用する新しいファイル管理タスクを作成し、構成した分類プロパティの条件を構成する必要があります。 たとえば、前に構成した条件 ([**RMS** ] プロパティ、[ **EQUAL**]、[ **はい**]) の代わりに、[ **個人の身元を特定する情報** ] プロパティを選択し、[ **演算子** ] を [ **EQUAL** ] に、[ **値** ]を [ **高**] に設定します。




<!--HONumber=Aug16_HO4-->


