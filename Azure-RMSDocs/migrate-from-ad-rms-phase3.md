---
title: AD RMS から Azure Information Protection への移行 - フェーズ 3
description: AD RMS から Azure Information Protection への移行のフェーズ 3 には、手順 7 が含まれます。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 01/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: bdd5d17bc947b25f312baa498da057b409dcd07e
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184129"
---
# <a name="migration-phase-3---client-side-configuration"></a>移行フェーズ 3 - クライアント側の構成

>*適用対象: Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

AD RMS から Azure Information Protection への移行フェーズ 3 では、次の情報を使用してください。 これらの手順では、「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」の手順 7 を説明します。

## <a name="step-7-reconfigure-windows-computers-to-use-azure-information-protection"></a>手順 7. Azure Information Protection を使用するように Windows コンピューターを再構成する

Office 365 アプリ、Office 2019、または Office 2016 のクイック実行デスクトップ アプリを使用する Windows コンピューターの場合:

- DNS リダイレクトを使用して、Azure Information Protection を使用するようにこれらのクライアントを再構成することができます。 これが最も簡単なため、クライアントの移行にお勧めの方法です。 ただし、この方法は Windows コンピューター用の Office 2016 (またはそれ以降) のクイック実行デスクトップ アプリに制限されます。
    
    この方法では、新しい SRV レコードを作成して、AD RMS の発行エンドポイントのユーザーに NTFS の拒否のアクセス許可を設定する必要があります。

- Office 2019 または Office 2016 のクイック実行を使用しない Windows コンピューターの場合:
    
    DNS リダイレクトは使用できません。代わりに、レジストリの編集を使用する必要があります。 DNS リダイレクトを使用できる Office のバージョンと使用できない Office のバージョンが混在している場合は、すべての Windows コンピューターでこの単一の方法を使用することも、DNS リダイレクトとレジストリの編集を組み合わせて使用することもできます。 
    
    ダウンロードできるスクリプトを編集およびデプロイすると、レジストリの変更が簡単になります。 

Windows クライアントを再構成する方法の詳細については、次のセクションを参照してください。

## <a name="client-reconfiguration-by-using-dns-redirection"></a>DNS リダイレクトを使用するクライアントの再構成

この方法は、Office 365 アプリおよび Office 2016 (またはそれ以降) のクイック実行デスクトップ アプリを実行する Windows クライアントにのみ適しています。 

1. 次のような形式を使用して DNS SRV レコードを作成します。
    
    `_rmsredir._http._tcp.<AD RMS cluster>. <TTL> IN SRV <priority> <weight> <port> <your tenant URL>.`
    
    *\<AD RMS クラスター>* には、お客様の AD RMS クラスターの FQDN を指定します。 例: **rmscluster.contoso.com**。
    
    代わりに、そのドメインに 1 つだけ AD RMS クラスターがある場合は、AD RMS クラスターのドメイン名だけを指定できます。 この例では、**contoso.com** になります。 このレコードにドメイン名を指定すると、リダイレクトがそのドメインの任意またはすべての AD RMS クラスターに適用されます。
    
    *\<ポート>* 番号は無視されます。
    
    *\<使用しているテナント URL\>* には、[テナントの自分の Azure Rights Management サービス URL](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url) を指定します。
    
    Windows Server で DNS サーバー ロールを使用する場合、DNS マネージャー コンソールで SRV レコード プロパティを指定する方法の例として、次の表を使用できます。
    
    |フィールド|値|  
    |-----------|-----------|  
    |**[ドメイン]**|_tcp.rmscluster.contoso.com|  
    |**サービス**|_rmsredir|  
    |**[プロトコル]**|_http|  
    |**優先度**|0|  
    |**重み**|0|  
    |**ポート番号**|80|  
    |**このサービスを提供しているホスト**|5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com|  

2. Office 365 アプリまたは Office 2016 (またはそれ以降) を実行しているユーザーに対し、AD RMS の発行エンドポイントで拒否のアクセス許可を設定します。

    A. クラスター内の AD RMS サーバーのいずれかで、Internet Information Services (IIS) マネージャー コンソールを開始します。

    B. **既定の Web サイト** > **_wmcs** > **licensing** > **licensing.asmx** に移動します。

    c. **licensing.asmx** > **[プロパティ]** > **[編集]** を右クリックして選択します。

    d. **[licensing.asmx の権限]** ダイアログ ボックスで、すべてのユーザーにリダイレクトを設定するために **[ユーザー]** を選択するか、**[追加]** を選択してリダイレクトするユーザーを含むグループを指定します。
    
    すべてのユーザーが DNS リダイレクトをサポートする Office のバージョンを使用している場合でも、段階的な移行のために、最初にユーザーのサブセットを指定したい場合があります。
    
    e. 選択したグループの **[読み取りと実行]** と **[読み取り]** のアクセス許可に **[拒否]** を選択して、**[OK]** を 2 回クリックします。

    f. この構成が想定どおりに動作することを確認するには、ブラウザーから直接 licensing.asmx ファイルへの接続を試みます。 次のエラー メッセージが表示されます。これにより、Office 365 アプリ、Office 2019、または Office 2016 を実行しているクライアントが SRV レコードの検索を開始します。
    
    **エラー メッセージ 401.3: 指定した資格情報を使用して、このディレクトリまたはページを表示するアクセス許可がありません (アクセス制御リストにより、アクセスが拒否されました)。**


## <a name="client-reconfiguration-by-using-registry-edits"></a>レジストリの編集を使用するクライアントの再構成

この方法はすべての Windows クライアントに適用され、Office 365 アプリ、Office 2019、 または Office 2016 を実行せずに、以前のバージョンを実行している場合に使用されます。 この方法では、2 つの移行スクリプトを使って AD RMS クライアントを再構成します。

- Migrate-Client.cmd

- Migrate-User.cmd

クライアント構成スクリプト (Migrate-Client.cmd) は、コンピューター レベルの設定をレジストリ内で構成します。つまり、それらの設定を変更できるセキュリティ コンテキストで、このスクリプトを実行する必要があります。 通常、次のいずれかの方法が使用されます。

- グループ ポリシーを使用して、コンピューターのスタートアップ スクリプトとしてスクリプトを実行します。

- グループ ポリシー ソフトウェア インストールを使用して、スクリプトをコンピューターに割り当てます。

- ソフトウェア デプロイ ソリューションを使用して、スクリプトをコンピューターにデプロイします。 たとえば、System Center Configuration Manager の[パッケージとプログラム](/sccm/apps/deploy-use/packages-and-programs)を使用します。 パッケージとプログラムのプロパティの **[実行モード]** で、デバイスに対して管理者アクセス許可でスクリプトが実行されるように指定します。 

- ユーザーがローカルの管理者特権を持つ場合は、ログオン スクリプトを使用します。

ユーザー構成スクリプト (Migrate-User.cmd) は、ユーザー レベルの設定を構成し、クライアントのライセンス ストアをクリーンアップします。 つまり、このスクリプトは、実際のユーザーのコンテキストで実行する必要があります。 以下に例を示します。

- ログオン スクリプトを使用します。

- グループ ポリシー ソフトウェア インストールを使用して、ユーザーが実行するためのスクリプトを発行します。

- ソフトウェア デプロイ ソリューションを使用して、スクリプトをユーザーにデプロイします。 たとえば、System Center Configuration Manager の[パッケージとプログラム](/sccm/apps/deploy-use/packages-and-programs)を使用します。 パッケージとプログラムのプロパティの **[実行モード]** では、ユーザーのアクセス許可でスクリプトが実行されるように指定します。 

- コンピューターにサインインする場合に、スクリプトを実行するようにユーザーに求めます。

2 つのスクリプトは、バージョン番号を含んでおり、このバージョン番号が変更されるまで再実行されません。 すなわち、移行が完了するまで、スクリプトを所定の場所に置いておくことができます。 ただし、コンピューターに再実行させるスクリプトおよび Windows コンピューター上でユーザーに再実行させるスクリプトに変更を加えた場合は、両方のスクリプトの次の行をより大きな値に更新します。

    SET Version=20170427

ユーザー構成スクリプトは、クライアント構成スクリプトの後で実行するように設計されており、バージョン番号を使用してその確認が行われます。 同じバージョンを持つクライアント構成スクリプトが実行されていない場合は、停止します。 この確認方法により、2 つのスクリプトは適切な順序で実行されます。 

すべての Windows クライアントを一度に移行できない場合は、クライアントのバッチ処理のための次の手順を実行します。 バッチで移行する Windows コンピューターを使用しているユーザーごとに、前に作成した **AIPMigrated** グループにユーザーを追加します。

### <a name="modifying-the-scripts-for-registry-edits"></a>レジストリの編集に使用するスクリプトを変更する

1. 移行スクリプト **Migrate-Client.cmd** および **Migrate-User.cmd** に戻ります。[準備段階](migrate-from-ad-rms-phase1.md#step-2-prepare-for-client-migration) でこれらのスクリプトをダウンロードしたときに抽出済みです。

2. **MigrateClient.cmd** の指示に従ってスクリプトを修正し、テナントの Azure Rights Management サービスの URL と、AD RMS クラスターのエクストラネット ライセンス URL およびイントラネット ライセンス URL のサーバー名を追加します。 次に、前述したスクリプトのバージョンをインクリメントします。 スクリプトのバージョンを追跡するには、今日の日付を次の形式で表現することをお勧めします: YYYYMMDD
    
   > [!IMPORTANT]
   > 前と同様に、アドレスの前後に余分なスペースが挿入されないように注意してください。
   > 
   > さらに、AD RMS サーバーが SSL/TLS サーバー証明書を使用している場合は、ライセンス URL の文字列にポート番号 **443** が含まれることを確認します。 たとえば、「 https://rms.treyresearch.net:443/_wmcs/licensing」のように入力します。 この情報は、Active Directory Rights Management サービス コンソールでクラスター名をクリックして、**[クラスターの詳細]** で確認できます。 ポート番号 443 が URL に含まれる場合は、スクリプトを変更するときにこの値を含めます。 たとえば、 https://rms.treyresearch.net:<strong>443</strong> のように指定します。 
    
   *&lt;YourTenantURL&gt;* の Azure Rights Management サービス URL を取得する必要がある場合は、前の「[Azure Rights Management サービス URL を識別するには](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url)」をご覧ください。

3. この手順の先頭に示した説明に従って、AIPMigrated グループのメンバーによって使用されている Windows クライアント コンピューター上で **Migrate-Client.cmd** および **Migrate-User.cmd** を実行するようにスクリプト デプロイ方法を構成します。 

## <a name="next-steps"></a>次の手順
移行を続行するには、「[移行フェーズ 4 - サービス構成のサポート](migrate-from-ad-rms-phase4.md)」に進んでください。
