---
# required metadata

title: テナント キーを生成して転送する – インターネット経由 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1bff9b06-8c5a-4b1d-9962-6668219210e6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# テナント キーを生成して転送する – インターネット経由

*適用対象: Azure Rights Management、Office 365*

[独自のテナント キーを管理する](plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok-)ことを選択し、Microsoft の施設まで移動してテナント キーを持参するのではなく、インターネット経由で転送する場合は、以下の手順を行います。


## インターネット接続ワークステーションを準備する
インターネットに接続したワークステーションを準備するには、次の 3 つの手順を実行します。

-   [手順 1.Azure Rights Management 用に Windows PowerShell をインストールする](#step-1-install-windows-powershell-for-azure-rights-management)

-   [手順 2:Azure Active Directory テナント ID を取得する](#step-2-get-your-azure-active-directory-tenant-id)

-   [手順 3:BYOK ツールセットをダウンロードする](#step-3-download-the-byok-toolset)

### 手順 1.Azure Rights Management 用に Windows PowerShell をインストールする
インターネット接続ワークステーションから、Azure Rights Management 用の Windows PowerShell モジュールをダウンロードしてインストールします。

> [!NOTE]
> この Windows PowerShell モジュールを既にダウンロードしている場合は、次のコマンドを実行してバージョン番号が 2.1.0.0 以上であることを確認します。 `(Get-Module aadrm -ListAvailable).Version`

インストール手順については、「[Azure Rights Management 用 Windows PowerShell をインストールする](../deploy-use/install-powershell.md)」を参照してください。.

### 手順 2:Azure Active Directory テナント ID を取得する
[ **管理者として実行** ] オプションを指定して Windows PowerShell を起動し、次のコマンドを実行します。

-   [Connect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629415.aspx) コマンドレットを使用して Azure RMS サービスに接続します。

    ```
    Connect-AadrmService
    ```
    プロンプトが表示されたら、[!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] のテナント管理者資格情報を入力します (通常は、Azure Active Directory または Office 365 のグローバル管理者であるアカウントを使用します)。

-   [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) コマンドレットを使用してテナントの構成を表示します。

    ```
    Get-AadrmConfiguration
    ```
    出力の先頭行にある GUID を保存します (BPOSId)。 これが Azure Active Directory テナント ID です。後で、アップロードするテナント キーを準備するときに必要になります。

-   [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) コマンドレットを使用して、Azure RMS サービスとの接続を解除します。キーをアップロードする準備ができるまで再接続しません。

    ```
    Disconnect-AadrmService
    ```

Windows PowerShell ウィンドウを閉じないでください。

### 手順 3:BYOK ツールセットをダウンロードする
Microsoft ダウンロード センターにアクセスし、ご利用の地域の [BYOK ツールセットをダウンロード](http://go.microsoft.com/fwlink/?LinkId=335781) します。

|地域|パッケージ名|
|----------|----------------|
|北米|AzureRMS-BYOK-tools-UnitedStates.zip|
|ヨーロッパ|AzureRMS-BYOK-tools-Europe.zip|
|アジア|AzureRMS-BYOK-tools-AsiaPacific.zip|
ツールセットの構成内容は次のとおりです。

-   キー交換のキー (KEK) パッケージ。名前の先頭に **BYOK-KEK-pkg-** が付きます。.

-   セキュリティ ワールド パッケージ。名前の先頭に **BYOK-SecurityWorld-pkg-** が付きます。.

-   Python スクリプト。名前は **verifykeypackage.py** です。.

-   コマンド ライン実行可能ファイル (**KeyTransferRemote.exe**)、メタデータ ファイル (**KeyTransferRemote.exe.config**)、および関連 DLL。

-   Visual C++ 再頒布可能パッケージ。名前は **vcredist_x64.exe** です。.

パッケージを USB ドライブまたはその他のポータブル ストレージにコピーします。

## 未接続ワークステーションを準備する
ネットワーク (インターネットまたは社内ネットワーク) に接続していないワークステーションを準備するには、次の 2 つの手順を実行します。

-   [手順 1.Thales HSM を設定した未接続ワークステーションを準備する](#step-1-prepare-the-disconnected-workstation-with-thales-hsm)

-   [手順 2:未接続ワークステーションに BYOK ツールセットをインストールする](#step-2-install-the-byok-toolset-on-the-disconnected-workstation)

### 手順 1.Thales HSM を設定した未接続ワークステーションを準備する
未接続ワークステーションで Windows コンピューターに nCipher (Thales) サポート ソフトウェアをインストールし、そのコンピューターに Thales HSM をアタッチします。

Thales ツールがパス **(%nfast_home%\bin** と **%nfast_home%\python\bin**) にあることを確認します。 たとえば、次のように入力します。

```
set PATH=%PATH%;”%nfast_home%\bin”;”%nfast_home%\python\bin”
```
詳細については、Thales HSM に付属のユーザー ガイドを参照するか、または Thales 社の Web サイトの Azure RMS に関するページ ([http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud)) にアクセスしてください。.

### 手順 2:未接続ワークステーションに BYOK ツールセットをインストールする
USB ドライブまたはその他のポータブル ストレージから BYOK ツールセット パッケージをコピーし、次を実行します。

1.  ダウンロードしたパッケージのファイルを任意のフォルダーに展開します。

2.  そのフォルダーから vcredist_x64.exe を実行します。

3.  指示に従って Visual Studio 2012 用の Visual C++ ランタイム コンポーネントをインストールします。

## テナント キーの生成
未接続ワークステーションで次の 3 つの手順を実行して独自のテナント キーを生成します。

-   [手順 1.セキュリティ ワールドの作成](#step-1-create-a-security-world)

-   [手順 2:ダウンロードしたパッケージを検証する](#step-2-validate-the-downloaded-package)

-   [手順 3:新しいキーの作成](#step-3-create-a-new-key)

### 手順 1.セキュリティ ワールドの作成
コマンド プロンプトを起動し、Thales 社が提供する new-world プログラムを実行します。

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
このプログラムによって、**セキュリティ ワールド** ファイルが %NFAST_KMDATA%\local\world に作成されます。この場所は、C:\ProgramData\nCipher\Key Management Data\local フォルダーに対応します。 クォーラムに別の値を使用することもできますが、この例では、空のカード 3 枚を挿入し、それぞれの暗証番号 (PIN) を入力するよう求められます。 次に、セキュリティ ワールド (指定したクォーラム) への管理アクセスを行うには、任意の 2 つのカードが必要になります。  これらのカードは、新しいセキュリティ ワールドの **管理者カード セット** になります。 この段階で、各 ACS カードのパスワードまたは PIN を指定することも、コマンドを使用して後でパスワードまたは PIN を追加することもできます。

> [!TIP]
> `nkminfo` コマンドを使用して HSM の現在の構成状態を確認することができます。

その後、次の手順を実行します。

1.  Thales 社が提供するドキュメントの説明に従って Thales CNG プロバイダーをインストールし、新しいセキュリティ ワールドを使用するように構成します。

2.  **%nfast_kmdata%\local** にあるワールド ファイルをバックアップします。 セキュリティ ワールド ファイル、管理者カード、およびカードの暗証番号 (PIN) を安全に保管し、1 人の人物が複数のカードにアクセスできないようにしてください。

### 手順 2:ダウンロードしたパッケージを検証する
この手順は省略できますが、次の項目を検証できるので推奨しています。

-   ツールセットに含まれ、真正の Thales HSM から生成されたキー交換のキー。

-   ツールセットに含まれ、真正の Thales HSM から生成された Azure RMS セキュリティ ワールドのハッシュ。

-   キー交換のキーはエクスポート不可能かどうか。

> [!NOTE]
> ダウンロードしたパッケージを検証するには、HSM が接続されていて、電源がオンで、セキュリティ ワールド (先ほど作成したものなど) が設定されている必要があります。

#### ダウンロードしたパッケージを検証するには

1.  地域により次のいずれかを入力して verifykeypackage.py スクリプトを実行します。

    -   北アメリカ:

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
        ```

    -   ヨーロッパ:

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
        ```

    -   アジア:

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
        ```

    > [!TIP]
    > Thales ソフトウェアには %NFAST_HOME%\python\bin に Python インタープリターが含まれています。

2.  検証が成功したことを示す次のメッセージが表示されることを確認します: **結果:成功**

このスクリプトでは署名者の Thales ルート キーまでのチェーンが検証されます。 このルート キーのハッシュはスクリプトに埋め込まれていて、値は **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**です。 また、[Thales の Web サイト](http://www.thalesesec.com/)でも、別途この値を確認できます。.

RMS テナント キーとなる新しいキーを作成する準備ができました。

### 手順 3:新しいキーの作成
Thales 社が提供する **generatekey** および **cngimport** プログラムを使用して、CNG キーを生成します。

キーを生成するには、次のコマンドを実行します。

```
generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=
```
このコマンドを実行する際は、次の指示に従ってください。

-   ここに示したように、パラメーター **protect** の値は **module** に設定する必要があります。 こうすることで、モジュールで保護されたキーが作成されます。 BYOK ツールセットは、OCS で保護されたキーをサポートしていません。

-   キーのサイズは 2048 を推奨しますが、1024 ビットの RSA キーを保有しており、Azure RMS に移行している既存の AD RMS ユーザーのために 1024 もサポートしています。

-   *ident* および **plainname** の値 **contosokey** は、任意の文字列値に置き換えてください。 管理オーバーヘッドを最小限に抑えて、エラーが発生するリスクを減らすため、ident および plainname の両方に小文字のみを使用した同じ値を指定することを推奨します。

-   pubexp は、この例では空白 (既定値) になっていますが、特定の値を指定することもできます。 詳細については、Thales 社が提供するドキュメントを参照してください。

その後、次のコマンドを実行して、キーを CNG にインポートします。

```
cngimport --import -M --key=contosokey --appname=simple contosokey
```
このコマンドを実行する際は、次の指示に従ってください。

-   *contosokey* を「*テナント キーの生成*」セクションの「[手順 1.セキュリティ ワールドの作成](#step-1-create-a-security-world)」で指定した値に置き換えます。

-   キーがこのシナリオに適したものになるように、**-M** オプションを使用します。 指定しない場合、インポートされたキーは現在のユーザーに固有のキーになります。

-   **appname** オプションは、キー ファイルの中でレポートされるアプリの名前です。 これらの手順を使用して新しいキーを作成した場合は、コマンドに示されているような単純な値を使用しました。 ただし、AD RMS から Azure RMS への移行時に HSM で保護された既存のキーを移行する場合は、このコマンドと、appname オプションを使用する後続のコマンドで既存の名前を指定します。

このコマンドにより、トークン化されたキー ファイルが %NFAST_KMDATA%\local フォルダーに作成されます。キー ファイル名は **key_caping_`_`** で始まり SID が続きます。 たとえば、**key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb** となります。 このファイルには暗号化されたキーが含まれています。

> [!TIP]
> `nkminfo –k` コマンドを使用して、キーの現在の構成状態を確認することができます。

このトークン化されたキー ファイルは、安全な場所にバックアップしてください。

> [!IMPORTANT]
> 後でキーを Azure RMS に転送する場合、Microsoft でこのキーをエクスポートして返すことはできないので、キーとセキュリティ ワールドのバックアップを作成して安全な場所に保管することがきわめて重要です。 キーのバックアップに関するガイダンスとベスト プラクティスについては、Thales 社に問い合わせてください。

これで、テナント キーを Azure RMS に転送する準備ができました。

## テナント キーの転送を準備する
未接続ワークステーションで次の 4 つの手順を実行してテナント キーを準備します。

-   [手順 1.権限が制限されたキーのコピーを作成する](#step-1-create-a-copy-of-your-key-with-reduced-permissions)

-   [手順 2:キーの新しいコピーを検証する](#step-2-inspect-the-new-copy-of-the-key)

-   [手順 3:Microsoft のキー交換のキーを使用してキーを暗号化する](#step-3-encrypt-your-key-by-using-microsoft-s-key-exchange-key)

-   [手順 4 :キー転送パッケージをインターネット接続ワークステーションにコピーする](#step-4-copy-your-key-transfer-package-to-the-internet-connected-workstation)

### 手順 1.権限が制限されたキーのコピーを作成する
テナント キーの権限を制限するには、次の手順を実行します。

-   コマンド プロンプトで、地域に応じて次のいずれかを実行します。

    -   北アメリカ:

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
        ```

    -   ヨーロッパ:

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
        ```

    -   アジア:

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
        ```

このコマンドを実行するときは、*contosokey* を「*テナント キーの生成*」セクションの「[手順 1.セキュリティ ワールドの作成](##step-1-create-a-security-world)」で指定した値に置き換えます。

セキュリティ ワールド ACS カードの挿入が求められます。また、指定した場合は、パスワードまたは PIN も求められます。

コマンドが完了すると、**Result: SUCCESS** と表示され、権限が制限されたテナント キーのコピーが、key_xferacId_*&lt;contosokey&gt;* という名前のファイルに保存されます。.

### 手順 2:キーの新しいコピーを検証する
オプションで、Thales ユーティリティを実行して新しいテナント キーの最小の権限を確認します。

-   aclprint.py:

    ```
    "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
    ```

-   kmfile-dump.exe:

    ```
    "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
    ```

これらのコマンドを実行するときは、*contosokey* を「*テナント キーの生成*」セクションの「[手順 1.セキュリティ ワールドの作成](##step-1-create-a-security-world)」で指定した値に置き換えます。

### 手順 3:Microsoft のキー交換のキーを使用してキーを暗号化する
地域に応じて次のいずれかのコマンドを実行します。

-   北アメリカ:

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

-   ヨーロッパ:

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

-   アジア:

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

このコマンドを実行する際は、次の指示に従ってください。

-   *contosokey* を、「*テナント キーの生成*」セクションの「[手順 1.セキュリティ ワールドの作成](##step-1-create-a-security-world)」でキーの生成に使用した ID に置き換えます。

-   *GUID* を、「*インターネット接続ワークステーションを準備する*」セクションの「[手順 2:Azure Active Directory テナント ID を取得する](#step-2-get-your-azure-active-directory-tenant-id)」で取得した Azure Active Directory テナント ID に置き換えます。

-   *ContosoFirstKey* を出力ファイル名で使用するラベルに置き換えます。

これが正常に完了すると、**Result: SUCCESS** と表示され、現在のフォルダーに TransferPackage-*ContosoFirstkey*.byok という新しいファイルが作成されます。

### 手順 4 :キー転送パッケージをインターネット接続ワークステーションにコピーする
USB ドライブまたはその他のポータブル ストレージを使用して、前の手順の出力ファイル (KeyTransferPackage-*ContosoFirstkey*.byok) をインターネット接続ワークステーションにコピーします。

> [!NOTE]
> ファイルには秘密キーが含まれているため、セキュリティ プラクティスを使用して保護します。

## テナント キーの Azure RMS への転送
インターネット接続ワークステーションで、次の 3 つの手順を行って新しいテナント キーを Azure RMS に転送します。

-   [手順 1.Azure RMS に接続する](#step-1-connect-to-azure-rms)

-   [手順 2:キー パッケージをアップロードする](#step-2-upload-the-key-package)

-   [手順 3:テナント キーを必要に応じて列挙する](#step-3-enumerate-your-tenant-keys-as-needed)

### 手順 1.Azure RMS に接続する
Windows PowerShell ウィンドウに戻り、次のように入力します。

1.  [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] サービスに再接続します。

    ```
    Connect-AadrmService
    ```

2.  [Get-AadrmKeys](http://msdn.microsoft.com/library/windowsazure/dn629420.aspx) コマンドレットを使用して現在のテナント キーの構成を表示します。

    ```
    Get-AadrmKeys
    ```

### 手順 2:キー パッケージをアップロードする
[Add-aadrmkey](http://msdn.microsoft.com/library/windowsazure/dn629418.aspx) コマンドレットを使用して、切断されたワークステーションからコピーしたキー転送パッケージをアップロードします。

```
Add-AadrmKey –KeyFile <PathToPackageFile> -Verbose
```
> [!WARNING]
> 操作を確認するメッセージが表示されます。 この操作は元に戻せないことを理解しておくことが重要です。 テナント キーをアップロードすると、このキーが自動的に組織のプライマリ テナント キーになり、ユーザーがドキュメントやファイルを保護する際はこのテナント キーを使用することになります。

アップロードに成功すると、次のメッセージが表示されます: **Rights Management サービスによってキーが正常に追加されました。**

変更内容が複製されてすべての [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] データ センターに反映されるまで時間がかかることを見込んでおいてください。

### 手順 3:テナント キーを必要に応じて列挙する
Get-AadrmKeys コマンドレットをもう一度使用してテナント キーの変更内容を表示します。いつでもテナント キーの一覧を表示できます。 表示されたテナント キーには、Microsoft で生成された最初のテナント キーと、お客様が追加した任意のテナント キーが含まれます。

```
Get-AadrmKeys
```
**Active** マークが付いたテナント キーは、現在組織でドキュメントやファイルの保護に使用しているキーです。

これで、インターネット経由での BYOK (Bring Your Own Key) に必要なすべての手順が完了したので、テナント キーを計画して実装する次のステップに進むことができます。


> [!div class="button"]
[次の手順 >>](plan-implement-tenant-key.md#next-steps)




<!--HONumber=Apr16_HO4-->


