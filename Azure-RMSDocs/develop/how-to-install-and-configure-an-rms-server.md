---
title: RMS サーバーをインストールし、構成し、それでテストする方法 | Azure RMS
description: 権限保護対応アプリケーションのテスト用に RMS Server をインストールおよび構成します。
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 32C7F387-CF7E-4CE0-AFC9-4C63FE1E134A
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 5a3fabd4d76dc86b52d0d8891b7032d1e017cf28
ms.sourcegitcommit: d06594550e7ff94b4098a2aa379ef2b19bc6123d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2018
ms.locfileid: "53023301"
---
# <a name="how-to-install-configure-and-test-with-an-rms-server"></a>方法: RMS サーバーをインストールし、構成し、それでテストする

このトピックでは、権限保護対応アプリケーションをテストするために、RMS サーバーまたは Azure RMS に接続する手順について説明します。
 
## <a name="instructions"></a>手順

### <a name="step-1-setup-your-rms-server"></a>手順 1: RMS サーバーをセットアップする

次の手順で RMS サーバーをセットアップする方法について説明します。この手順には、次が含まれています。

-   サーバーをインストールする
-   サーバーを登録する

1.  **サーバーをインストールする**

    Active Directory Rights Management サービス (AD RMS) は、個別のクライアントとサーバー コンポーネントで構成されます。 サーバー コンポーネントは、RMS インフラストラクチャの管理、コンテンツのコンシューマーとパブリッシャーへのライセンスの発行、およびコンピューターとユーザーへの証明書の発行に使用できる一連の Web サービスとして実装されます。

    Windows Server 2008 以降は、クライアント コンポーネントとサーバーコンポーネントの両方がオペレーティング システムに含まれています。 以前のオペレーティング システムのサーバー コンポーネントは、次の場所からダウンロードできます。

    -   [RMS サーバー v1.0 SP2](https://go.microsoft.com/fwlink/p/?linkid=73722)

    Windows Server 2008 でサーバー コンポーネントを構成するには、AD RMS ロールをインストールする必要があります。 以前のサーバー オペレーティング システムに対してアプリケーションを開発している場合は、RMS サーバー v1.0 SP2 のインストール後、RMS サービスをプロビジョニングする前に、レジストリを構成します。

2.  **サーバーを登録する**

    運用前階層と運用階層のどちらに配置するのかを指定するために、Rights Management サービス (RMS) サーバーを登録する必要があります。 登録プロセスでは、サーバー コンピューターにサーバー ライセンサー証明書が残されます。 この証明書から、Microsoft の信頼のルートを辿ることができます。 サーバーを登録する方法は、使用している RMS バージョンによって異なります。

    -   **自己登録**

        Windows Server 2008 以降では、Microsoft に情報を送信することなく、適切な階層に RMS サーバーを登録できます。 RMS ロールをインストールするときに、自己登録証明書と秘密キーもインストールされます。 これらは、サーバー ライセンサー証明書の自動作成に使用されます。 Microsoft と情報は交換されません。

    -   **オンライン登録**

        AD RMS v1.0 SP2 を使用している場合は、オンラインでサーバーを登録できます。 登録はプロビジョニング プロセスの背後でで行われますが、インターネット接続が必要です。

        **HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**1.0**\\**UddiProvider** = 0e3d9bb8-b765-4a68-a329-51548685fed3

3. **RMS サーバーでテストする**

    RMS サーバーでテストするには、サーバー側の検出とクライアント側の検出のいずれかを構成し、Rights Management Service Client 2.1 を有効にして RMS サーバーを検出し、通信を確立します。

    > [!Note]
    > Azure RMS でテストするとき、検出構成は必要ありません。

  - サーバー側の検出では、管理者が Active Directory により RMS ルート クラスターに対してサービス接続ポイント (SCP) を登録すると、クライアントは Active Directory にクエリを実行して SCP を検出し、サーバーとの接続を確立します。
  - クライアント側の検出では、RMS クライアント 2.1 が実行されるコンピューター上のレジストリに RMS サービス検出の設定を構成します。 これにより、RMS クライアント 2.1 が RMS サーバーを使用するように設定されます。 これらの設定がある場合、サーバー側の検出は実行されません。

  クライアント側の検出を構成する場合、次のレジストリ キーを RMS サーバーをポイントするように設定できます。 サービス側の検出を構成する方法については、「[RMS クライアントのデプロイに関する注意事項](https://technet.microsoft.com/library/jj159267(WS.10).aspx)」を参照してください。

1. **EnterpriseCertification**

        HKEY_LOCAL_MACHINE
          SOFTWARE
            Microsoft
              MSIPC
                ServiceLocation
                  EnterpriseCertification

   **値**: (既定): **[http|https]**://RMSClusterName/**_wmcs/Certification**

2. **EnterprisePublishing**

        HKEY_LOCAL_MACHINE
          SOFTWARE
            Microsoft
              MSIPC
                ServiceLocation
                  EnterprisePublishing
                  
   **値**: (既定): **[http|https]**://RMSClusterName/**_wmcs/Licensing**

>[!NOTE] 
> 既定では、これらのキーはレジストリに存在しないため、作成する必要があります。

>[!IMPORTANT] 
> 64 ビット バージョンの Windows で 32 ビット アプリケーションを実行する場合は、これらのキーを次のキーの場所に設定する必要があります。<p>
  ```    
  HKEY_LOCAL_MACHINE
    SOFTWARE
      Wow6432Node
        Microsoft
          MSIPC
            ```
