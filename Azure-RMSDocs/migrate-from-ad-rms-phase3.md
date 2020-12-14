---
title: AD RMS から Azure Information Protection への移行 - フェーズ 3
description: AD RMS から Azure Information Protection への移行のフェーズ 3 には、手順 7 が含まれます。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: d0c643ea787d8ef9a977930aee270af5023c89a7
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97381529"
---
# <a name="migration-phase-3---client-side-configuration"></a>移行フェーズ 3 - クライアント側の構成

>***適用対象**: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連**: [AIP のラベル付けクライアントと従来のクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

AD RMS から Azure Information Protection への移行フェーズ 3 では、次の情報を使用してください。 これらの手順では、「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」の手順 7 を説明します。

## <a name="step-7-reconfigure-windows-computers-to-use-azure-information-protection"></a>手順 7. Azure Information Protection を使用するように Windows コンピューターを再構成する

次のいずれかの方法を使用して、Azure Information Protection を使用するように Windows コンピューターを再構成します。

- **DNS リダイレクト**。 サポートされている場合は、最も単純で推奨される方法です。 

    Office 2016 以降のデスクトップアプリを使用する Windows コンピューターでサポートされています。次にその一部を示します。

    - Microsoft 365 アプリ
    - Office 2019
    - Office 2016 クリックしてデスクトップアプリを実行する

    新しい SRV レコードを作成し、AD RMS 発行エンドポイントのユーザーに NTFS 拒否アクセス許可を設定する必要があります。

    詳細については、「 [DNS リダイレクトを使用](#client-reconfiguration-by-using-dns-redirection)したクライアントの再構成」を参照してください。

- **レジストリの編集**。 次の両方を含む、サポートされているすべての環境に関連します。

    - Office 2016 以降を使用する Windows コンピューターでは、上に示したように、デスクトップアプリを実行します。
    - 他のアプリを使用する Windows コンピューター
    
    必要なレジストリ変更を手動で行うか、ダウンロード可能なスクリプトを編集および展開して、レジストリを変更します。

    詳細については、「 [レジストリの編集を使用](#client-reconfiguration-by-using-registry-edits)したクライアントの再構成」を参照してください。


> [!TIP]
> DNS リダイレクトを使用できる、または使用できない Office のバージョンが混在している場合は、DNS リダイレクトを組み合わせて使用するか、レジストリを編集するか、すべての Windows コンピューターの単一の方法としてレジストリを編集することができます。


## <a name="client-reconfiguration-by-using-dns-redirection"></a>DNS リダイレクトを使用するクライアントの再構成

この方法は、Microsoft 365 アプリと Office 2016 (またはそれ以降) の [クリックして実行] デスクトップアプリを実行する Windows クライアントにのみ適しています。 

1. 次のような形式を使用して DNS SRV レコードを作成します。
    
    ```sh
    _rmsredir._http._tcp.<AD RMS cluster>. <TTL> IN SRV <priority> <weight> <port> <your tenant URL>.
    ```
    
    *\<AD RMS cluster>* では、AD RMS クラスターの FQDN を指定します。 例: **rmscluster.contoso.com**。
    
    代わりに、そのドメインに 1 つだけ AD RMS クラスターがある場合は、AD RMS クラスターのドメイン名だけを指定できます。 この例では、**contoso.com** になります。 このレコードにドメイン名を指定すると、リダイレクトがそのドメインの任意またはすべての AD RMS クラスターに適用されます。
    
    この *\<port>* 数値は無視されます。
    
    *\<your tenant URL\>* では、[テナントに独自の Azure Rights Management サービスの URL](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url)を指定します。
    
    Windows Server で DNS サーバー ロールを使用する場合、DNS マネージャー コンソールで SRV レコード プロパティを指定する方法の例として、次の表を使用できます。
    
    |フィールド|値|  
    |-----------|-----------|  
    |**ドメイン**|_tcp.rmscluster.contoso.com|  
    |**サービス**|_rmsredir|  
    |**プロトコル**|_http|  
    |**優先順位**|0|  
    |**Weight**|0|  
    |**ポート番号**|80|  
    |**このサービスを提供しているホスト**|5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com|  
    | | |

2. Microsoft 365 アプリまたは Office 2016 (またはそれ以降) を実行しているユーザーの AD RMS 発行エンドポイントに対する拒否アクセス許可を設定します。

    a. クラスター内の AD RMS サーバーのいずれかで、Internet Information Services (IIS) マネージャー コンソールを開始します。

    b. [ **既定の Web サイト** ] に移動し、[ **_wmcs**] を展開します。

    c. [ **ライセンス** ] を右クリックし、[ **コンテンツビューに切り替え**] を選択します。

    d. 詳細ペインで、[ライセンス] を右クリックし **ます。 .asmx**  >  **プロパティ** の  >  **編集**

    e. [ **Permissions のアクセス許可** ] ダイアログボックスで、すべてのユーザーにリダイレクトを設定する場合は [ **ユーザー** ] を選択し、[ **追加** ] をクリックして、リダイレクトするユーザーを含むグループを指定します。
    
    すべてのユーザーが DNS リダイレクトをサポートする Office のバージョンを使用している場合でも、段階的な移行のために、最初にユーザーのサブセットを指定したい場合があります。
    
    f. 選択したグループの **[読み取りと実行]** と **[読み取り]** のアクセス許可に **[拒否]** を選択して、**[OK]** を 2 回クリックします。

    g. この構成が想定どおりに動作することを確認するには、ブラウザーから直接 licensing.asmx ファイルへの接続を試みます。 次のエラーメッセージが表示されます。 Microsoft 365 アプリまたは Office 2019 または Office 2016 を実行しているクライアントをトリガーして SRV レコードを探します。
    
    **エラー メッセージ 401.3: 指定した資格情報を使用して、このディレクトリまたはページを表示するアクセス許可がありません (アクセス制御リストにより、アクセスが拒否されました)。**


## <a name="client-reconfiguration-by-using-registry-edits"></a>レジストリの編集を使用するクライアントの再構成

この方法は、すべての Windows クライアントに適しており、Microsoft 365 アプリ、または Office 2016 (またはそれ以降) を実行しない場合に使用する必要があります。 この方法では、2 つの移行スクリプトを使って AD RMS クライアントを再構成します。

- Migrate-Client.cmd

- Migrate-User.cmd

クライアント構成スクリプト (Migrate-Client.cmd) は、コンピューター レベルの設定をレジストリ内で構成します。つまり、それらの設定を変更できるセキュリティ コンテキストで、このスクリプトを実行する必要があります。 通常、次のいずれかの方法が使用されます。

- グループ ポリシーを使用して、コンピューターのスタートアップ スクリプトとしてスクリプトを実行します。

- グループ ポリシー ソフトウェア インストールを使用して、スクリプトをコンピューターに割り当てます。

- ソフトウェア デプロイ ソリューションを使用して、スクリプトをコンピューターにデプロイします。 たとえば、System Center Configuration Manager の[パッケージとプログラム](/sccm/apps/deploy-use/packages-and-programs)を使用します。 パッケージとプログラムのプロパティの **[実行モード]** で、デバイスに対して管理者アクセス許可でスクリプトが実行されるように指定します。 

- ユーザーがローカルの管理者特権を持つ場合は、ログオン スクリプトを使用します。

ユーザー構成スクリプト (Migrate-User.cmd) は、ユーザー レベルの設定を構成し、クライアントのライセンス ストアをクリーンアップします。 つまり、このスクリプトは、実際のユーザーのコンテキストで実行する必要があります。 次に例を示します。

- ログオン スクリプトを使用します。

- グループ ポリシー ソフトウェア インストールを使用して、ユーザーが実行するためのスクリプトを発行します。

- ソフトウェア デプロイ ソリューションを使用して、スクリプトをユーザーにデプロイします。 たとえば、System Center Configuration Manager の[パッケージとプログラム](/sccm/apps/deploy-use/packages-and-programs)を使用します。 パッケージとプログラムのプロパティの **[実行モード]** では、ユーザーのアクセス許可でスクリプトが実行されるように指定します。 

- コンピューターにサインインする場合に、スクリプトを実行するようにユーザーに求めます。

2 つのスクリプトは、バージョン番号を含んでおり、このバージョン番号が変更されるまで再実行されません。 すなわち、移行が完了するまで、スクリプトを所定の場所に置いておくことができます。 ただし、コンピューターに再実行させるスクリプトおよび Windows コンピューター上でユーザーに再実行させるスクリプトに変更を加えた場合は、両方のスクリプトの次の行をより大きな値に更新します。

```sh
SET Version=20170427
```

ユーザー構成スクリプトは、クライアント構成スクリプトの後で実行するように設計されており、バージョン番号を使用してその確認が行われます。 同じバージョンを持つクライアント構成スクリプトが実行されていない場合は、停止します。 この確認方法により、2 つのスクリプトは適切な順序で実行されます。 

すべての Windows クライアントを一度に移行できない場合は、クライアントのバッチ処理のための次の手順を実行します。 バッチで移行する Windows コンピューターを使用しているユーザーごとに、前に作成した **AIPMigrated** グループにユーザーを追加します。

### <a name="modifying-the-scripts-for-registry-edits"></a>レジストリの編集に使用するスクリプトを変更する

1. 移行スクリプト **Migrate-Client.cmd** および **Migrate-User.cmd** に戻ります。[準備段階](migrate-from-ad-rms-phase1.md#step-2-prepare-for-client-migration) でこれらのスクリプトをダウンロードしたときに抽出済みです。

2. **Migrate-client.cmd** の指示に従って、テナントの Azure Rights Management サービスの url と、AD RMS クラスターのエクストラネットライセンス url およびイントラネットライセンス url のサーバー名が含まれるようにスクリプトを変更します。 次に、前述したスクリプトのバージョンをインクリメントします。 スクリプトのバージョンを追跡する場合は、現在の日付を YYYYMMDD 形式で使用することをお勧めします。
    
   > [!IMPORTANT]
   > 前と同様に、アドレスの前後に余分なスペースが挿入されないように注意してください。
   > 
   > さらに、AD RMS サーバーが SSL/TLS サーバー証明書を使用している場合は、ライセンス URL の文字列にポート番号 **443** が含まれることを確認します。 (例: https://rms.treyresearch.net:443/_wmcs/licensing)。 この情報は、Active Directory Rights Management サービス コンソールでクラスター名をクリックして、**[クラスターの詳細]** で確認できます。 ポート番号 443 が URL に含まれる場合は、スクリプトを変更するときにこの値を含めます。 たとえば、https://rms.treyresearch.net:<strong>443</strong> のように指定します。 
    
   Azure Rights Management サービスの *&lt; &gt;* url を取得する必要がある場合は、「」に戻り、 [azure Rights Management サービスの url を確認](migrate-from-ad-rms-phase1.md#to-identify-your-azure-rights-management-service-url)してください。

3. この手順の先頭に示した説明に従って、AIPMigrated グループのメンバーによって使用されている Windows クライアント コンピューター上で **Migrate-Client.cmd** および **Migrate-User.cmd** を実行するようにスクリプト デプロイ方法を構成します。 

## <a name="next-steps"></a>次のステップ

移行を続行するには、「[移行フェーズ 4 - サービス構成のサポート](migrate-from-ad-rms-phase4.md)」に進んでください。
