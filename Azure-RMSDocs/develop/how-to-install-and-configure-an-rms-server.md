---
# required metadata

title: サーバーのインストールと構成 | Azure RMS
description: 権限保護対応アプリケーションのテスト用に RMS Server をインストールおよび構成します。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 32C7F387-CF7E-4CE0-AFC9-4C63FE1E134A
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# サーバーのインストールと構成

このトピックでは、権限保護対応アプリケーションをテストするために、RMS サーバーをインストールおよび構成する手順を説明します。

**重要** アプリケーションを 1-box RMS ISV 環境で実行してテストする場合は、1-box 環境に既にインストールおよび構成されているため、RMS サーバーをインストールする必要はありません。
1-box AD RMS ISV 環境の詳細については、「[テスト環境のセットアップ](how-to-set-up-your-test-environment.md)」を参照してください。

 

## 手順

### 手順 1: RMS サーバーをセットアップする

次の手順で RMS サーバーをセットアップする方法について説明します。この手順には、次が含まれています。

-   レジストリを構成する
-   サーバーをインストールする
-   サーバーを登録する

1.  **レジストリを構成する**

    運用前証明書の階層を使用することを指定するために、次のレジストリ値を設定します。

    **注** Windows Server 2008 R2 または Windows Server 2008 を使用している場合は、AD RMS サービスをインストールする前にこれらのレジストリ値を設定します。

    Windows Server 2008 R2 で AD RMS を使用している場合は、次の **REG\_DWORD** 値を設定する必要があります。 運用階層に切り替えるには、この値を 0 (ゼロ) に変更します。

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**Hierarchy** = 0x00000001

    Windows Server 2008 R2 で AD RMS を使用していて、運用前サービスとして Active Directory に別の AD RMS サービスを既に展開している場合は、次の空の文字列値をレジストリに追加します。

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**GICURL** = ""

    Windows Server 2008 で AD RMS を使用している場合は、次の **REG\_DWORD** 値を設定する必要があります。 運用階層に切り替えるには、この値を 0 (ゼロ) に変更します。

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**2.0**\\**Hierarchy** = 0x00000001

    Windows Server 2008 で AD RMS を使用していて、運用前サービスとして Active Directory に別の AD RMS サービスを既に展開している場合は、次の空の文字列値をレジストリに追加します。

    **Computer**\\**HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**2.0**\\**GICURL** = ""

2.  **サーバーをインストールする**

    Active Directory Rights Management サービス (AD RMS) は、個別のクライアントとサーバー コンポーネントで構成されます。 サーバー コンポーネントは、RMS インフラストラクチャの管理、コンテンツのコンシューマーとパブリッシャーへのライセンスの発行、およびコンピューターとユーザーへの証明書の発行に使用できる一連の Web サービスとして実装されます。

    Windows Server 2008 以降は、クライアント コンポーネントとサーバーコンポーネントの両方がオペレーティング システムに含まれています。 以前のオペレーティング システムのサーバー コンポーネントは、次の場所からダウンロードできます。

    -   [RMS サーバー v1.0 SP2](http://go.microsoft.com/fwlink/p/?linkid=73722)

    Windows Server 2008 でサーバー コンポーネントを構成するには、AD RMS ロールをインストールする必要があります。 ただし、これを行う前に、レジストリを構成して、運用階層ではなく運用前証明書の階層を使用することを指定する必要があります。 ただし、以前のサーバー オペレーティング システムに対してアプリケーションを開発している場合は、RMS サーバー v1.0 SP2 のインストール後、RMS サービスをプロビジョニングする前に、レジストリを構成します。

    詳細については、前の手順の手順 1 「レジストリを構成する」を参照してください。

3.  **サーバーを登録する**

    運用前階層と運用階層のどちらに配置するのかを指定するために、Rights Management サービス (RMS) サーバーを登録する必要があります。 登録プロセスでは、サーバー コンピューターにサーバー ライセンサー証明書が残されます。 この証明書から、Microsoft の信頼のルートを辿ることができます。 サーバーを登録する方法は、使用している RMS バージョンによって異なります。

    -   **自己登録**

        Windows Server 2008 以降では、Microsoft に情報を送信せずに、適切な階層に RMS サーバーを登録できます。 RMS ロールをインストールするときに、自己登録証明書と秘密キーもインストールされます。 これらは、サーバー ライセンサー証明書の自動作成に使用されます。 Microsoft と情報は交換されません。

    -   **オンライン登録** AD RMS v1.0 SP2 を使用している場合は、オンラインでサーバーを登録できます。 登録は、プロビジョニング プロセス中にバックグラウンドで行われますが、インターネット接続が必要です。サーバーを登録する階層を識別するための適切なレジストリ値を指定しておく必要もあります。 運用前階層に登録するには、次の **REG\_SZ** 値を追加し、サーバーをプロビジョニングします。 運用階層に登録するには、この値をクリアして、サーバーをプロビジョニングします。

        詳細については、前の手順の手順 1 「レジストリを構成する」を参照してください。

        **HKEY\_LOCAL\_MACHINE**\\**Software**\\**Microsoft**\\**DRMS**\\**1.0**\\**UddiProvider** = 0e3d9bb8-b765-4a68-a329-51548685fed3

## 関連項目

* [使用方法](how-to-use-msipc.md)
 

 





<!--HONumber=Apr16_HO4-->


