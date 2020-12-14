---
title: Rights Management コネクタのインストールと構成 - AIP
description: Azure Rights Management (RMS) コネクタをインストールして構成する場合に役立つ情報。 これらの手順では、「Deploying the Azure Rights Management connector」 (Azure Rights Management コネクタのデプロイ) の手順 1 から手順 4 を説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4fed9d4f-e420-4a7f-9667-569690e0d733
ms.subservice: connector
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ef3a9198af5fb44927438c66262e30acf439f2eb
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383858"
---
# <a name="installing-and-configuring-the-azure-rights-management-connector"></a>Azure Rights Management コネクタのインストールと構成

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows server 2019、2016、2012 R2、および Windows server 2012 *
>
>***関連**: [AIP のラベル付けクライアントと従来のクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

以下の情報は、Azure Rights Management (RMS) コネクタをインストールして構成する場合に役立ちます。 これらの手順では、「[Deploying the Azure Rights Management connector](deploy-rms-connector.md)」 (Azure Rights Management コネクタのデプロイ) の手順 1 から手順 4 を説明します。

作業を開始する前に、このデプロイの[前提条件](deploy-rms-connector.md#prerequisites-for-the-rms-connector)を確認してください。

セットアップと構成を完了するには、コネクタが適切な Azure ソブリン cloud インスタンスを認識していることを確認します。 
- **Azurecloud**: Azure の商用サービス
- **AzureChinaCloud**: 21vianet によって運営される Azure
- **Azureusgovernment**: AZURE GOVERNMENT (GCC High/DoD)
- **AzureUSGovernment2**: Azure Government 2
- **AzureUSGovernment3**: Azure Government 3


## <a name="installing-the-rms-connector"></a>RMS コネクタのインストール

1.  RMS コネクタを実行するコンピューター (2 つ以上) を特定します。 これらのコンピューターは、「前提条件」に記載されている最小仕様を満たしている必要があります。

    > [!NOTE]
    > テナント (Microsoft 365 テナントまたは Azure AD テナント) ごとに1つの RMS コネクタ (高可用性のために複数のサーバーで構成される) をインストールします。 Active Directory RMS とは異なり、RMS コネクタを各フォレストにインストールする必要はありません。

2.  [Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/?LinkId=314106)から RMS コネクタのソース ファイルをダウンロードします。

    RMS コネクタをインストールするには、RMSConnectorSetup.exe をダウンロードします。

    さらに:

    -   RMS コネクタのサーバー構成ツールを使用してオンプレミス サーバーのレジストリ設定を自動構成する場合は、GenConnectorConfig.ps1 もダウンロードします。

3.  RMS コネクタをインストールするコンピューターで、管理者特権を使用して **RMSConnectorSetup.exe** を実行します。

4.  Microsoft Rights Management Connector セットアップの [ようこそ] ページで、[ **microsoft Rights Management コネクタをコンピューターにインストールする**] を選択し、[ **次へ**] をクリックします。

5.  RMS コネクタのライセンス条項を読んで同意したら、[**次へ**] をクリックします。


## <a name="entering-credentials"></a>資格情報の入力

RMS コネクタを構成する前に、ソリューションに一致するクラウド環境を最初に選択する必要があります。   
- **Azurecloud**: Azure の商用サービス
- **AzureChinaCloud**: 21vianet によって運営される Azure
- **Azureusgovernment**: AZURE GOVERNMENT (GCC High/DoD)
- **AzureUSGovernment2**: Azure Government 2
- **AzureUSGovernment3**: Azure Government 3

:::image type="content" source="media/authenticate_tenant_rms_connector.png" alt-text="新しい AAD RM コネクタを認証するための適切な Azure 環境を選択します":::

クラウド環境を選択したら、 **ユーザー名** と **パスワード** を入力します。 RMS コネクタを構成するための十分な特権を持つアカウントの資格情報を入力してください。 たとえば、「」と入力し、 <strong>admin@contoso.com</strong> このアカウントのパスワードを指定します。


さらに、[オンボーディング コントロール](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)を実装済みの場合は、指定するアカウントでコンテンツを保護できることを確認してください。 たとえば、コンテンツの保護機能の使用を "IT 部門" グループに限り許可している場合、ここで指定するアカウントがそのグループのメンバーである必要があります。 それ以外の場合、" **管理サービスと組織の場所を検出できませんでした。" というエラーメッセージが表示されます。組織で Microsoft Rights Management サービスが有効になっていることを確認します。**

次のいずれかの特権を持つアカウントを使用できます。

-   **テナントのグローバル管理者**: Microsoft 365 テナントまたは Azure AD テナントのグローバル管理者であるアカウント。

-   **Azure Rights Management のグローバル管理者**: Azure RMS グローバル管理者ロールを割り当てられている Azure Active Directory のアカウント。

-   **Azure Rights Management のコネクタ管理者**: 組織の RMS コネクタをインストールおよび管理する権限が付与されている Azure Active Directory のアカウント。

    > [!NOTE]
    > Azure Rights Management のグローバル管理者ロールと Azure Rights Management コネクタ管理者ロールは、 [Add-Aipserviceroleベースの管理者](/powershell/module/aipservice/add-aipservicerolebasedadministrator) コマンドレットを使用してアカウントに割り当てられます。
    > 
    > RMS コネクタを最低限の特権で実行するには、この目的専用のアカウントを作成し、次のようにして Azure RMS コネクタ管理者ロールを割り当てます。
    >
    > 1. まだ行っていない場合は、AIPService PowerShell モジュールをダウンロードしてインストールします。 詳細については、「 [AIPService PowerShell モジュールのインストール](install-powershell.md)」を参照してください。
    >
    >     [ **管理者として実行** ] コマンドを使用して Windows PowerShell を起動し、 [Connect-aipservice](/powershell/module/aipservice/connect-aipservice) コマンドを使用して保護サービスに接続します。
    >
    >     ```
    >     Connect-AipService                   //provide Microsoft 365 tenant administrator or Azure RMS global administrator credentials
    >     ```
    > 2.  次に、次のパラメーターのいずれかを使用して、 [Add-Aipserviceroleの管理者](/powershell/module/aipservice/add-aipservicerolebasedadministrator) コマンドを実行します。
    >
    >     ```
    >     Add-AipServiceRoleBasedAdministrator -EmailAddress <email address> -Role "ConnectorAdministrator"
    >     ```
    >
    >     ```
    >     Add-AipServiceRoleBasedAdministrator -ObjectId <object id> -Role "ConnectorAdministrator"
    >     ```
    >
    >     ```
    >     Add-AipServiceRoleBasedAdministrator -SecurityGroupDisplayName <group Name> -Role "ConnectorAdministrator"
    >     ```
    >     たとえば、「 **Add-AipserviceroleEmailAddress melisa@contoso.com -Role "コネクタ管理者"」** と入力します。
    >
    >     これらのコマンドはコネクタ管理者ロールを割り当てますが、GlobalAdministrator ロールをここで使用することもできます。

RMS コネクタのインストール プロセスでは、すべての前提条件ソフトウェアが検証されてインストールされます。また、インターネット インフォメーション サービス (IIS) が存在しない場合はインストールされ、その後、コネクタ ソフトウェアがインストールされて構成されます。 さらに、以下のものを作成することで、Azure RMS の構成準備が行われます。

-   コネクタを使用して Azure RMS と通信することが許可されているサーバーの空テーブル。 後でこのテーブルにサーバーを追加します。

-   Azure RMS での操作を承認する、コネクタ用の一連のセキュリティ トークン。 これらのトークンは Azure RMS からダウンロードされ、ローカル コンピューター上のレジストリにインストールされます。 これらはデータ保護アプリケーション プログラム (DPAPI) およびローカル システム アカウントの資格情報を使用して保護されます。

ウィザードの最終ページで、次の操作を実行して [**完了**] をクリックします。

-   最初のコネクタをインストールした場合は、現時点で [**コネクタ管理者コンソールを起動してサーバーを承認する**] を選択しないでください。 このオプションは、2 つ目 (または最後) の RMS コネクタをインストールした後に選択します。 代わりに、少なくとも 1 つの他のコンピューターで、ウィザードをもう一度実行してください。 2 つ以上のコネクタをインストールする必要があります。

-   2 つ目 (または最後) のコネクタをインストールしたら、[**コネクタ管理者コンソールを起動してサーバーを承認する**] を選択します。

> [!TIP]
> この時点で、検証テストを実行して、RMS コネクタ用の Web サービスが機能しているかどうかを確認できます。
>
> -   Web ブラウザーから **http://&lt;connectoraddress&gt;/_wmcs/certification/servercertification.asmx** に接続します。*&lt;connectoraddress&gt;* は、RMS コネクタがインストールされているサーバーのアドレスまたは名前に置き換えてください。 接続に成功すると、**ServerCertificationWebService** ページが表示されます。

RMS コネクタをアンインストールする必要がある場合は、ウィザードを再実行してアンインストール オプションを選択します。

インストール中に問題が発生した場合は、インストールログ: **%LocalAppData%\Temp\Microsoft Rights Management connector_ \<date and time> ログ** を確認してください。 

例として、インストールログは **は c:\users\administrator\appdata\local\temp\microsoft Rights Management connector_20170803110352** のようになります。

## <a name="authorizing-servers-to-use-the-rms-connector"></a>RMS コネクタを使用するサーバーの承認
2 台以上のコンピューターに RMS コネクタをインストールしたら、RMS コネクタを使用するサーバーとサービスを承認することができます。 たとえば、Exchange Server 2013 や SharePoint Server 2013 を実行しているサーバーがあるとします。

これらのサーバーを定義するには、RMS コネクタ管理ツールを実行して、許可されているサーバーのリストにエントリを追加します。 このツールは、Microsoft Rights Management コネクタ セットアップ ウィザードの最終ページで [**コネクタ管理コンソールを起動してサーバーを承認する**] を選択して実行するか、またはウィザードとは別に実行することができます。

これらのサーバーを承認するときは、次の考慮事項に注意してください。

- 追加するサーバーには特別な特権が付与されます。 コネクタ構成で Exchange Server ロールとして指定したすべてのアカウントに、Azure RMS の[スーパー ユーザー ロール](configure-super-users.md)が付与されます。これにより、それらのアカウントはこの RMS テナントのすべてのコンテンツにアクセスすることができます。 スーパー ユーザー機能は、この時点で必要に応じて自動的に有効になります。 特権の昇格によるセキュリティ上のリスクを回避するため、組織の Exchange サーバーで使用されているアカウントのみを指定するように注意します。 SharePoint サーバー、または FCI を使用するファイル サーバーとして構成されているすべてのサーバーには、通常のユーザー特権が付与されます。

- 複数のサーバーを 1 つのエントリとして追加するには、Active Directory のセキュリティ グループや配布グループ、または複数のサーバーで使用されているサービス アカウントを指定します。 この構成を使用すると、サーバーのグループは同じ RMS 証明書を共有し、グループに属するすべてのサーバーは各サーバーが保護しているコンテンツの所有者と見なされます。 管理オーバーヘッドを最小限に抑えるため、個々のサーバー単位ではなく、この単一グループ構成を使用して組織の Exchange サーバーまたは SharePoint サーバー ファームを承認することをお勧めします。

[**コネクタの使用が許可されているサーバー**] ページで、[**追加**] をクリックします。

> [!NOTE]
> サーバーの承認は、サービスまたはサーバーのコンピューター アカウントの ServerCertification.asmx に NTFS アクセス許可を手動で適用して、Exchange アカウントにユーザー スーパー権限を手動で付与する AD RMS 構成に対する Azure RMS の同等の構成です。 コネクタでは、ServerCertification.asmx に NTFS アクセス許可を適用する必要はありません。


### <a name="add-a-server-to-the-list-of-allowed-servers"></a>許可されたサーバーのリストへのサーバーの追加
[**コネクタの使用をサーバーに許可**] ページで、承認するオブジェクトの名前を入力するか、または承認するオブジェクトを参照して指定します。

正しいオブジェクトを承認することが重要です。 サーバーでコネクタを使用するには、オンプレミス サービス (Exchange や SharePoint など) を実行するアカウントを選択して承認する必要があります。 たとえば、構成済みのサービス アカウントとしてサービスが実行されている場合、そのサービス アカウントの名前をリストに追加します。 ローカル システムとしてサービスが実行されている場合は、コンピューター オブジェクトの名前 (SERVERNAME$ など) を追加します。 これらのアカウントが含まれるグループを作成し、個々のサーバー名の代わりにそのグループを指定することをお勧めします。

さまざまなサーバー ロールの詳細を以下に示します。

-   Exchange を実行するサーバー: セキュリティ グループを指定する必要があり、既定のグループ (**Exchange サーバー**) を使用できます。このグループは Exchange によって自動的に作成され、フォレスト内のすべての Exchange サーバーが保持されています。

-   SharePoint を実行するサーバー:

    -   SharePoint 2010 サーバーが (サービス アカウントを使用しないで) ローカル システムとして実行するように構成されている場合は、Active Directory ドメイン サービスにセキュリティ グループを手動で作成し、この構成でのサーバーのコンピューター名オブジェクトを、このグループに追加します。

    -   SharePoint サーバーがサービス アカウントを使用するように構成されている場合は (SharePoint 2010 の場合は推奨される方法、SharePoint 2016 と SharePoint 2013 の場合は唯一のオプション)、次のようにします。

        1.  SharePoint サーバーの全体管理サービスを実行するサービス アカウントを追加して、SharePoint を管理者コンソールから構成できるようにします。

        2.  SharePoint アプリケーション プール用に構成されているアカウントを追加します。

        > [!TIP]
        > これらの 2 つのアカウントが異なる場合は、管理オーバーヘッドを最小限に抑えるために、両方のアカウントを含む単一グループを作成することを検討してください。

-   ファイル分類インフラストラクチャを使用するファイルサーバーの場合、関連するサービスはローカルシステムアカウントとして実行されるため、ファイルサーバーのコンピューターアカウント ( **SERVERNAME $** など)、またはそれらのコンピューターアカウントを含むグループを承認する必要があります。

一覧へのサーバーの追加が完了したら、[**閉じる**] をクリックします。

次に、RMS コネクタがインストールされているサーバーの負荷分散を構成する必要があります (未構成の場合)。また、これらのサーバーと承認されたサーバーの間の接続に HTTPS を使用するかどうかを検討します。

## <a name="configuring-load-balancing-and-high-availability"></a>負荷分散と高可用性の構成
RMS コネクタの2つ目または最後のインスタンスをインストールしたら、コネクタ URL のサーバー名を定義し、負荷分散システムを構成します。

コネクタ URL のサーバー名には、管理している名前空間で任意の名前を指定できます。 たとえば、DNS システムの **rmsconnector.contoso.com** にエントリを作成し、負荷分散システムの IP アドレスを使用するようにこのエントリを構成することができます。 この名前に特別な要件はありません。また、コネクタ サーバー自体での構成は不要です。 Exchange および SharePoint サーバーがインターネット経由でコネクタと通信する予定がない限り、この名前はインターネット上で解決する必要はありません。

> [!IMPORTANT]
> コネクタを使用するように Exchange サーバーまたは SharePoint サーバーを構成した後は、この名前を変更しないことをお勧めします。名前を変更すると、これらのサーバーですべての IRM 構成を消去し、再構成する必要があります。

DNS で名前を作成して IP アドレスを構成したら、そのアドレスに対する負荷分散を構成し、トラフィックを複数のコネクタ サーバーに振り分けます。 その場合、Windows Server のネットワーク負荷分散 (NLB) 機能など、IP ベースの任意のロード バランサーを使用できます。 詳細については、[負荷分散デプロイに関するガイド](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754833(v=ws.10))を参照してください。

次の設定を使用して、NLB クラスターを構成します。

-   **ポート**:80 (HTTP の場合) または 443 (HTTPS の場合)

    HTTP または HTTPS のどちらを使用するかについては、次のセクションを参照してください。

-   **アフィニティ**: なし

-  **配布方法**: 等しい

(RMS コネクタ サービスを実行しているサーバーの) 負荷分散システム用に定義したこの名前は、組織の RMS コネクタ名です。この名前は、後で Azure RMS を使用するオンプレミス サーバーを構成するときに使用します。

## <a name="configuring-the-rms-connector-to-use-https"></a>HTTPS を使用するための RMS コネクタの構成
> [!NOTE]
> この構成手順は省略可能ですが、セキュリティ強化のために推奨されます。

RMS コネクタでの TLS や SSL の使用は省略可能ですが、セキュリティ上の注意が必要な HTTP ベースのサービスでは使用することをお勧めします。 この構成では、コネクタを使用する Exchange および SharePoint サーバーに対してコネクタを実行しているサーバーを認証します。 さらに、これらのサーバーからコネクタに送信されるすべてのデータは暗号化されます。

RMS コネクタで TLS の使用を有効にするには、RMS コネクタを実行する各サーバーに、コネクタで使用する名前が含まれるサーバー認証証明書をインストールします。 たとえば、DNS で定義した RMS コネクタ名が **rmsconnector.contoso.com** の場合、証明書サブジェクトの共通名に **rmsconnector.contoso.com** が含まれるサーバー認証証明書をデプロイします。 または、証明書の別名に DNS 値として **rmsconnector.contoso.com** を指定します。 証明書にサーバーの名前を含める必要はありません。 その後、IIS で、この証明書を既定の Web サイトにバインドします。

HTTPS オプションを使用する場合は、コネクタを実行するすべてのサーバーに有効なサーバー認証証明書が存在し、Exchange および SharePoint サーバーが信頼するルート CA にその証明書がチェーンされていることを確認してください。 さらに、コネクタ サーバーの証明書を発行した証明機関 (CA) が証明書失効リスト (CRL) を公開している場合、Exchange および SharePoint サーバーはこの CRL をダウンロードできる必要があります。

> [!TIP]
> 次の情報とリソースを使用して、サーバー認証証明書を要求してインストールし、その証明書を IIS の既定の Web サイトにバインドできます。
>
> - Active Directory 証明書サービス (AD CS) とエンタープライズ証明機関 (CA) を使用して、これらのサーバー認証証明書を展開する場合は、Web サーバー証明書テンプレートを複製して使用することができます。 この証明書テンプレートでは、証明書のサブジェクト名で [**要求に含まれる**] オプションを使用しています。これにより、証明書を要求する際に、証明書のサブジェクト名またはサブジェクトの別名に RMS コネクタ名の FQDN を指定できます。
> -   スタンドアロン CA を使用する場合や、この証明書を別の会社から購入している場合は、TechNet の「[Web Server (IIS)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753433(v=ws.10))」 (Web サーバー (IIS)) ドキュメント ライブラリにある「[Configuring Internet Server Certificates (IIS 7)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731977(v=ws.10))」 (インターネット サーバー証明書の構成 (IIS 7)) 参照してください。
> - 証明書を使用するように IIS を構成する場合は、TechNet の「[Web Server (IIS)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753433(v=ws.10))」 (Web サーバー (IIS)) ドキュメント ライブラリにある「[Add a Binding to a Site (IIS 7)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731692(v=ws.10))」 (サイトにバインドを追加する (IIS 7)) を参照してください。

## <a name="configuring-the-rms-connector-for-a-web-proxy-server"></a>Web プロキシ サーバー用の RMS コネクタの構成
コネクタサーバーがインターネットに直接接続されていないネットワークにインストールされており、インターネットに発信アクセスするために web プロキシサーバーを手動で構成する必要がある場合は、これらのサーバーのレジストリを RMS コネクタ用に構成する必要があります。

#### <a name="to-configure-the-rms-connector-to-use-a-web-proxy-server"></a>Web プロキシ サーバーを使用するように RMS コネクタを構成するには

1.  RMS コネクタが実行されている各サーバーで、レジストリ エディター (Regedit など) を開きます。

2.  **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AADRM\Connector** に移動します。

3.  文字列値の **ProxyAddress** を追加し、この値のデータを **http://&lt;MyProxyDomainOrIPaddress&gt;:&lt;MyProxyPort&gt;** に設定します。

    例: **http://proxyserver.contoso.com:8080**

4.  レジストリ エディターを閉じて、サーバーを再起動するか、または IISReset コマンドを実行して IIS を再起動します。

## <a name="installing-the-rms-connector-administration-tool-on-administrative-computers"></a>管理用コンピューターへの RMS コネクタ管理ツールのインストール
RMS コネクタがインストールされていないコンピューターが次の要件を満たしている場合は、RMS コネクタ管理ツールを実行することができます。

-   Windows Server 2019、2016、2012、または Windows Server 2012 R2 (すべてのエディション)、Windows 10、Windows 8.1、Windows 8 を実行する物理または仮想コンピューター。

-   1 GB 以上の RAM。

-   64 GB 以上のディスク領域。

-   1 つ以上のネットワーク インターフェイス。

-   ファイアウォール (または web プロキシ) 経由でインターネットにアクセスします。

RMS コネクタ管理ツールをインストールするには、次のファイルを実行します。

-   64 ビット コンピューターの場合: RMSConnectorSetup.exe

これらのファイルをまだダウンロードしていない場合は、[Microsoft ダウンロード センター](https://go.microsoft.com/fwlink/?LinkId=314106)からダウンロードできます。


## <a name="next-steps"></a>次のステップ
これで RMS コネクタのインストールと構成が完了したので、コネクタを使用するようにオンプレミス サーバーを構成することができます。 「[Azure Rights Management コネクタ用にサーバーを構成する](configure-servers-rms-connector.md)」に進みます。