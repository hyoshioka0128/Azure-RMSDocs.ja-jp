---
title: Configure servers for the Rights Management コネクタ用にサーバーを構成する - AIP
description: Azure Rights Management (RMS) コネクタを使用するオンプレミス サーバーの構成に役立つ情報です。 これらの手順では、「Azure Rights Management コネクタを展開する」の手順 5 について説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/10/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 75846ee1-2370-4360-81ad-e2b6afe3ebc9
ms.subservice: connector
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: a0b8df95c28b6d49610411b8f93678b70cf7226a
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "95570582"
---
# <a name="configuring-servers-for-the-azure-rights-management-connector"></a>Azure Rights Management コネクタ用にサーバーを構成する

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows server 2016、windows Server 2012 R2、windows server 2012*


Azure Rights Management (RMS) コネクタを使用するオンプレミス サーバーを構成するには、次の情報を活用してください。 これらの手順 [では、「Azure Rights Management コネクタのデプロイ](deploy-rms-connector.md)」の手順5について説明します。

作業を開始する前に、RMS コネクタをインストールして構成し、コネクタを使用するサーバーに適用される[前提条件](deploy-rms-connector.md#prerequisites-for-the-rms-connector)をチェックしておいてください。


## <a name="configuring-servers-to-use-the-rms-connector"></a>RMS コネクタを使用するためのサーバーの構成
RMS コネクタのインストールと構成が完了したら、Azure Rights Management サービスに接続し、コネクタを使ってこの保護テクノロジを使用するオンプレミス サーバーを構成することができます。 つまり、次のサーバーを構成します。

-   **Exchange 2016 および Exchange 2013** の場合: クライアント アクセス サーバーおよびメールボックス サーバー

-   **Exchange 2010 および exchange 2019 の場合**: クライアントアクセスサーバーとハブトランスポートサーバー

-   **SharePoint の場合**: フロントエンド SharePoint Web サーバー (全体管理サーバーをホストするサーバーを含みます)

-   **ファイル分類インフラストラクチャの場合**: ファイルリソースマネージャーがインストールされている Windows Server コンピューター

この構成にはレジストリの設定が必要です。 レジストリの構成は、Microsoft RMS コネクタのサーバー構成ツールを使用することによって自動で、 またはレジストリを編集することによって手動で行うことができます。

---

**Microsoft RMS コネクタ用のサーバー構成ツールを使用した自動構成:**

- 利点:

    - レジストリを直接編集する必要はありません。 スクリプトを使用して自動構成されます。

    - Windows PowerShell コマンドレットを実行して Microsoft RMS の URL を取得する必要はありません。

    - ツールをローカルで実行すると、必須コンポーネントが自動的に確認されます (ただし、自動修復されることはありません)。

短所:

- ツールを実行する際は、RMS コネクタが既に実行されているサーバーに接続する必要があります。

---

**レジストリの編集による手動構成:**

- 利点:

    - RMS コネクタが実行されているサーバーに接続する必要はありません。

- 短所:

    - 管理オーバーヘッドが増大し、間違いが発生しやすくなります。

    - Microsoft RMS の URL を取得する必要があります。このために Windows PowerShell コマンドを実行する必要があります。

    - すべての必須コンポーネントを常にユーザー自身で確認する必要があります。


---

> [!IMPORTANT]
> いずれの場合でも、前提条件を手動でインストールし、Rights Management を使用するように Exchange、SharePoint、およびファイル分類インフラストラクチャを構成する必要があります。

ほとんどの場合、Microsoft RMS コネクタ用のサーバー構成ツールを使用した自動構成が推奨されます。手動構成よりも効率良く確実に構成できるためです。

Exchange または SharePoint を実行しており、AD RMS を使用するように構成済みの場合、これらのサーバーの構成を変更した後に再起動する必要があります。 Rights Management 用に初めて構成する場合は、サーバーを再起動する必要はありません。 ファイル分類インフラストラクチャを使用するようにファイル サーバーを構成している場合、構成の変更後に、必ず再起動する必要があります。

### <a name="how-to-use-the-server-configuration-tool-for-microsoft-rms-connector"></a>Microsoft RMS コネクタ用のサーバー構成ツールの使用方法

1.  Microsoft RMS コネクタ用のサーバー構成ツール (GenConnectorConfig.ps1) のスクリプトをまだダウンロードしていない場合は、 [Microsoft ダウンロードセンター](https://go.microsoft.com/fwlink/?LinkId=314106)からダウンロードしてください。

2.  ツールを実行するコンピューターに GenConnectorConfig.ps1 ファイルを保存します。 ツールをローカルで実行する場合、これは RMS コネクタと通信するように構成したサーバーである必要があります。 そうでない場合は、任意のコンピューターに保存できます。

3.  ツールの実行方法を決定します。

    -   **ローカル**:ツールは、RMS コネクタと通信するように構成されたサーバーから対話的に実行できます。 この方法は、テスト環境のような 1 回限りの構成に便利です。

    -   **ソフトウェア デプロイ**:ツールを実行して生成したレジストリ ファイルを、ソフトウェア展開をサポートするシステム管理アプリケーション (System Center Configuration Manager など) を使用して、関連する 1 つ以上のサーバーに展開できます。

    -   **グループ ポリシー**:ツールを実行して生成したスクリプトを、構成対象のサーバーにグループ ポリシー オブジェクトを作成できる管理者に渡します。 このスクリプトを実行すると、構成対象の各サーバー タイプに 1 つのグループ ポリシー オブジェクトが作成されます。その後、管理者は関連するサーバーにそのグループ ポリシーを割り当てることができます。

    > [!NOTE]
    > このツールを使用して、このセクションの最初に記載されている、RMS コネクタと通信するサーバーを構成します。 このツールは、RMS コネクタを実行するサーバーで実行しないでください。

4.  [**管理者として実行**] オプションを使用して Windows PowerShell を起動し、Get-help コマンドを使用して、選択した構成方法でのツールの使用方法を確認します。

    ```
    Get-help .\GenConnectorConfig.ps1 -detailed
    ```

スクリプトを実行するには、組織の RMS コネクタの URL を入力する必要があります。 プロトコルのプレフィックス (HTTP:// または HTTPS://) に続いて、コネクタの負荷分散アドレス用に DNS で定義したコネクタ名を入力してください。 たとえば、https:/connector.contoso.com のように \/ なります。 ツールは、この URL を使用して RMS コネクタが実行されているサーバーに接続し、必要な構成を作成するために使用されるその他のパラメーターを取得します。

> [!IMPORTANT]
> このツールを実行する場合、RMS コネクタ サービスを実行する単一のサーバー名ではなく、組織の負荷分散された RMS コネクタ名を指定する必要があります。

各サービス タイプに固有の情報については、次のセクションを参照してください。

-   [コネクタを使用するように Exchange サーバーを構成する](#configuring-an-exchange-server-to-use-the-connector)

-   [コネクタを使用するための SharePoint サーバーの構成](#configuring-a-sharepoint-server-to-use-the-connector)

-   [コネクタを使用するためのファイル分類インフラストラクチャ用ファイル サーバーの構成](#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)

> [!NOTE]
> コネクタを使用するようにサーバーを構成すると、そのサーバーのローカルにインストールされたクライアント アプリケーションで RMS が動作しない場合があります。 この問題が発生するのは、アプリケーションが RMS を直接使用せずにコネクタを使用しようとする (これはサポートされていません) ことが原因です。
>
> さらに、Office 2010 が Exchange server にローカルでインストールされている場合、コネクタを使用するようにサーバーを構成した後、クライアントアプリの IRM 機能がそのコンピューターから機能する可能性がありますが、これはサポートされていません。
>
> いずれの場合も、コネクタを使用するように構成されていない別のコンピューターにクライアント アプリケーションをインストールする必要があります。 そうすれば、クライアント アプリケーションで RMS が直接使用されるようになります。

## <a name="configuring-an-exchange-server-to-use-the-connector"></a>コネクタを使用するための Exchange サーバーの構成
次の Exchange ロールは RMS コネクタと通信します。

-   Exchange 2016 および Exchange 2013 の場合: クライアント アクセス サーバーおよびメールボックス サーバー

-   Exchange 2010 および Exchange 2019 の場合: クライアントアクセスサーバーとハブトランスポートサーバー

RMS コネクタを使用するには、サーバーで実行されている Exchange が、次のいずれかのソフトウェア バージョンである必要があります。

-   Exchange Server 2016

-   Exchange 2013 累積更新プログラム 3 を適用した Exchange Server 2013

-   Exchange 2010 Service Pack 3 ロールアップ更新プログラム 6 を適用した Exchange Server 2010

-   Exchange Server 2019

さらに、これらのサーバーには、RMS 暗号化モード 2 をサポートするバージョン 1 の RMS クライアント (別名 MSDRM) が存在する必要があります。 どの Windows オペレーティング システムにも MSDRM クライアントは含まれていますが、初期のバージョンのクライアントは暗号化モード 2 をサポートしていませんでした。 Exchange サーバーのオペレーティング システムが Windows Server 2012 以上ならば、特に対応は必要ありません。オペレーティング システムとともにインストールされる RMS クライアントは、暗号化モード 2 をネイティブでサポートしているためです。 


> [!IMPORTANT]
> ここに示したバージョン以降の Exchange と MSDRM クライアントがインストールされていない場合は、コネクタを使用するように Exchange を構成することはできません。 続行する前に、これらのバージョンがインストールされていることを確認してください。

### <a name="to-configure-exchange-servers-to-use-the-connector"></a>コネクタを使用するように Exchange サーバーを構成するには

1. RMS コネクタ管理ツールと「[RMS コネクタを使用するサーバーを承認する](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)」セクションからの情報を使用して、Exchange サーバーに RMS コネクタを使用する権限が付与されていることを確認します。 Exchange が RMS コネクタを使用できるようにするには、この構成が必要です。

2. RMS コネクタと通信する Exchange サーバー ロールで、次のいずれかを実行します。

   -   Microsoft RMS コネクタのサーバー構成ツールを実行します。 詳細については、「[Microsoft RMS コネクタ用のサーバー構成ツールの使用方法](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector)」を参照してください。

       たとえば、ツールをローカルで実行して、Exchange 2016 または Exchange 2013 が実行されているサーバーを構成するには、次のコマンドを使います。

       ```
       .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetExchange2013
       ```

   -   「[RMS コネクタのレジストリ設定](rms-connector-registry-settings.md)」の情報を使用してサーバー上にレジストリ設定を追加し、手動でレジストリの編集を行います。 

3. Exchange 用の IRM 機能を有効にするには、Exchange PowerShell コマンドレットの [セット IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration) を使用し、 `InternalLicensingEnabled $true` とを設定し `ClientAccessServerEnabled $true` ます。


## <a name="configuring-a-sharepoint-server-to-use-the-connector"></a>コネクタを使用するための SharePoint サーバーの構成
次の SharePoint ロールは RMS コネクタと通信します。

-   フロントエンド SharePoint Web サーバー (全体管理サーバーをホストするサーバーを含みます)

RMS コネクタを使用するには、サーバーで実行されている SharePoint が、次のいずれかのソフトウェア バージョンである必要があります。

-   SharePoint Server 2019

-   SharePoint Server 2016

-   SharePoint Server 2013

-   SharePoint Server 2010

SharePoint 2019、2016、または SharePoint 2013 を実行するサーバーでは、RMS コネクタでサポートされている MSIPC client 2.1 のバージョンも実行している必要があります。 サポートされているバージョンであることを確認するには、 [Microsoft ダウンロードセンター](https://www.microsoft.com/download/details.aspx?id=38396)から最新のクライアントをダウンロードしてください。

> [!WARNING]
> MSIPC 2.1 クライアントには複数のバージョンがあるため、必ずバージョン 1.0.2004.0 以降を使用します。
>
> クライアントのバージョンを確認するには、MSIPC.dll のバージョン番号を確認します。このファイルは、**\Program Files\Active Directory Rights Management Services Client 2.1** にあります。 プロパティ ダイアログ ボックスに、MSIPC 2.1 クライアントのバージョン番号が表示されます。

SharePoint 2010 を実行するサーバーには、RMS 暗号化モード 2 のサポートが含まれる MSDRM クライアントのバージョンがインストールされている必要があります。 Windows Server 2012 と Windows Server 2012 R2 は、暗号化モード 2 をネイティブでサポートしています。

### <a name="to-configure-sharepoint-servers-to-use-the-connector"></a>コネクタを使用するように SharePoint サーバーを構成するには

1. RMS コネクタ管理ツールと「[RMS コネクタを使用するサーバーを承認する](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)」セクションからの情報を使用して、SharePoint サーバーに RMS コネクタを使用する権限が付与されていることを確認します。 SharePoint サーバーが RMS コネクタを使用できるようにするには、この構成が必要です。

2.  RMS コネクタと通信する SharePoint サーバーで、次のいずれかを実行します。

    -   Microsoft RMS コネクタのサーバー構成ツールを実行します。 詳細については、「[Microsoft RMS コネクタ用のサーバー構成ツールの使用方法](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector)」を参照してください。

        たとえば、ツールをローカルで実行して、SharePoint 2019、2016、または SharePoint 2013 が実行されているサーバーを構成するには、次のようにします。

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetSharePoint2013
        ```

    -   SharePoint 2019、2016、または SharePoint 2013 を使用している場合は、手動でレジストリの編集を行います。そのためには、 [RMS コネクタのレジストリ設定](rms-connector-registry-settings.md) に関する情報を参照して、サーバーにレジストリ設定を手動で追加します。 

3.  SharePoint で IRM を有効にします。 詳細については、SharePoint ライブラリの「 [Information Rights Management を構成する (SharePoint Server 2010)](/previous-versions/office/sharepoint-server-2010/hh545607(v=office.14)) 」をご覧ください。

    これらの手順に従う場合は、コネクタを使用するように SharePoint を構成する際に [**この RMS サーバーを使用する**] を指定し、構成した負荷分散コネクタ URL を入力する必要があります。 プロトコルのプレフィックス (HTTP:// または HTTPS://) に続いて、コネクタの負荷分散アドレス用に DNS で定義したコネクタ名を入力してください。 たとえば、コネクタ名が https:/connector.contoso.com の場合、 \/ 構成は次の図のようになります。

    ![RMS コネクタのための SharePoint サーバーの構成](./media/AzRMS_SharePointConnector.png)

    SharePoint ファームで IRM が有効になったら、各ライブラリの [**ライブラリの設定**] ページにある [**Information Rights Management**] オプションを使用して、個々のライブラリで IRM を有効にできます。


## <a name="configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector"></a>コネクタを使用するためのファイル分類インフラストラクチャ用ファイル サーバーの構成
RMS コネクタとファイル分類インフラストラクチャを使用して Office ドキュメントを保護する場合は、ファイル サーバーで次のいずれかのオペレーティング システムが実行されている必要があります。

- Windows Server 2016

- Windows Server 2012 R2

- Windows Server 2012

### <a name="to-configure-file-servers-to-use-the-connector"></a>コネクタを使用するようにファイル サーバーを構成するには

1. RMS コネクタ管理ツールと [RMS コネクタを使用するサーバーを承認する](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector) セクションからの情報を使用して、ファイルサーバーに RMS コネクタを使用する権限が付与されていることを確認します。 ファイル サーバーが RMS コネクタを使用できるようにするには、この構成が必要です。

2. ファイル分類インフラストラクチャ用に構成され、RMS コネクタと通信するファイル サーバーで、次のいずれかを実行します。

    -   Microsoft RMS コネクタのサーバー構成ツールを実行します。 詳細については、「[Microsoft RMS コネクタ用のサーバー構成ツールの使用方法](#how-to-use-the-server-configuration-tool-for-microsoft-rms-connector)」を参照してください。

        たとえば、ツールをローカルで実行し、FCI を実行しているファイル サーバーを構成します。

        ```
        .\GenConnectorConfig.ps1 -ConnectorUri https://rmsconnector.contoso.com -SetFCI2012
        ```

    - 「[RMS コネクタのレジストリ設定](rms-connector-registry-settings.md)」の情報を使用してサーバー上にレジストリ設定を追加し、手動でレジストリの編集を行います。 

3. RMS Encryption を使用してドキュメントを保護する分類ロールとファイル管理タスクを作成し、自動的に RMS ポリシーを適用するように RMS テンプレートを指定します。 詳細については、Windows Server ドキュメント ライブラリの「 [ファイル サーバー リソース マネージャーの概要](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831701(v=ws.11)) 」を参照してください。

## <a name="next-steps"></a>次のステップ
RMS コネクタのインストールと構成が完了し、RMS コネクタを使用するようにサーバーを構成しました。IT 管理者とユーザーは、Azure Rights Management サービスを使用して電子メール メッセージとドキュメントを保護し、使用することができます。 ユーザーがこの処理を実行しやすいように、Azure Information Protection クライアントをデプロイします。これによって、Office 用のアドオンがインストールされ、エクスプローラーに新しい右クリック オプションが追加されます。 詳細については、「[Azure Information Protection クライアント管理者ガイド](./rms-client/client-admin-guide.md)」を参照してください。

Exchange トランスポート ルールまたは Windows Server FCI と共に使用する部門別テンプレートを構成する場合は、**[アプリケーションでユーザー ID がサポートされていないときにこのテンプレートをすべてのユーザーに表示する]** チェック ボックスがオンになるように、スコープ構成にアプリケーション互換性オプションを含める必要があることに注意してください。

「[Azure Information Protection デプロイ ロードマップ](deployment-roadmap.md)」を参照して、Azure Rights Management をユーザーおよび管理者にロールアウトする前にその他の構成手順が必要かどうかを判断します。

RMS コネクタを監視するには、「[Azure Rights Management コネクタを監視する](monitor-rms-connector.md)」を参照してください。