---
title: Rights Management コネクタをデプロイする - AIP
description: RMS コネクタをデプロイする手順について説明します。RMS コネクタは、Exchange Server、SharePoint Server、または Windows Server とファイル分類インフラストラクチャ (FCI) を使用する既存のオンプレミス デプロイのデータ保護サービスとして機能します。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 06/10/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 90e7e33f-9ecc-497b-89c5-09205ffc5066
ms.subservice: connector
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 405989dae3fb7f37edc4fdd8b213ae5dae3ac592
ms.sourcegitcommit: f32928f7dcc03111fc72d958cda9933d15065a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/10/2020
ms.locfileid: "84665913"
---
# <a name="deploying-the-azure-rights-management-connector"></a>Azure Rights Management コネクタをデプロイする

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows server 2019、2016、windows Server 2012 R2、windows server 2012*

ここでは、Azure Rights Management コネクタについて説明してから、このコネクタを適切にデプロイする方法について説明します。 このコネクタは、Microsoft **Exchange Server**、 **SharePoint Server**、または Windows Server および**ファイル分類インフラストラクチャ**(fci) を実行するファイルサーバーを使用する既存の内部設置型の配置に対してデータ保護を提供します。


## <a name="overview-of-the-microsoft-rights-management-connector"></a>Microsoft Rights Management コネクタの概要
Microsoft Rights Management (RMS) コネクタを使用すると、既存のオンプレミス サーバーで Information Rights Management (IRM) 機能とクラウドベースの Microsoft Rights Management サービス (Azure RMS) を迅速に使用できるようになります。 この機能により、IT 担当者およびユーザーは、組織の内外にあるドキュメントや画像を簡単に保護することができます。追加のインフラストラクチャをインストールしたり、他の組織との間に信頼関係を確立したりする必要はありません。 

RMS コネクタは、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012 を実行するサーバーに、オンプレミスでインストールする小規模なサービスです。 コネクタは、物理コンピューター上だけでなく、Azure IaaS VM などの仮想マシン上でも実行できます。 デプロイされたコネクタは、次の図に示すように、オンプレミス サーバーとクラウド サービスとの間の通信インターフェイス (リレー) の役割を果たします。 矢印は、ネットワーク接続が開始される方向を示しています。

![RMS コネクタ アーキテクチャの概要](./media/RMS_connector.png)


### <a name="on-premises-servers-supported"></a>サポートされるオンプレミス サーバー

RMS コネクタでサポートされるオンプレミス サーバーは、Exchange Server と SharePoint Server、また、Windows Server を実行しておりファイル分類インフラストラクチャ (フォルダー内の Office ドキュメントを分類してポリシーを適用します) を使用するファイル サーバーです。 

> [!NOTE]
> Office ドキュメントだけでなく、複数の種類のファイルをファイル分類インフラストラクチャで保護したい場合は、RMS コネクタではなく [AzureInformationProtection コマンドレット](/powershell/azureinformationprotection/vlatest/aip)を使用してください。

これらのオンプレミス サーバーのうち、どのバージョンが RMS コネクタでサポートされるかについては、「[Azure RMS をサポートするオンプレミス サーバー](requirements-servers.md)」をご覧ください。


### <a name="support-for-hybrid-scenarios"></a>ハイブリッド シナリオのサポート

RMS コネクタは、組織のユーザーのうち一部だけがオンライン サービスに接続する場合でも使用でき、これをハイブリッド シナリオといいます。 たとえば、ユーザーのメールボックスの中に Exchange Online を使用するものと、Exchange Server を使用するものがあるとします。 RMS コネクタをインストールすると、すべてのユーザーが Azure RMS を使用して電子メールと添付ファイルを保護し、使用できるようになります。2 つのデプロイメント構成の間で、情報はシームレスに保護されます。

### <a name="support-for-customer-managed-keys-byok"></a>自主管理キー (BYOK) のサポート

Azure RMS の自分のテナント キーを管理する場合 (Bring Your Own Key または BYOK シナリオ)、そのキーを使用する RMS コネクタとオンプレミス サーバーには、テナント キーを含むハードウェア セキュリティ モジュール (HSM) に対するアクセス権がありません。 これは、テナント キーを使用するすべての暗号操作は、オンプレミスではなく、Azure RMS で実行されるためです。

このような、テナント キーを独自に管理するシナリオについて詳しくは、「[Azure Information Protection テナント キーを計画して実装する](plan-implement-tenant-key.md)」を参照してください。

## <a name="prerequisites-for-the-rms-connector"></a>RMS コネクタの前提条件
RMS コネクタをインストールする前に、次の要件を満たしていることを確認してください。

|要件|詳細情報|
|---------------|--------------------|
|保護サービスがアクティブ化されています|[Azure Information Protection からの保護サービスのアクティブ化](activate-service.md)|
|オンプレミス Active Directory フォレストと Azure Active Directory の間のディレクトリ同期|RMS をアクティブ化した後に、Azure Active Directory を構成して Active Directory データベース内のユーザーおよびグループを使用できるようにする必要があります。<br /><br />**重要**: RMS コネクタが動作するためには、テスト ネットワークに対してもこのディレクトリ同期手順を実行する必要があります。 Office 365 および Azure Active Directory では、Azure Active Directory で手動作成したアカウントを使用できますが、このコネクタでは、Azure Active Directory のアカウントが Active Directory Domain Services と同期している必要があります。手動によるパスワードの同期では不十分です。<br /><br />詳細については、次のリソースを参照してください。<br /><br />- [オンプレミスの Active Directory ドメインと Azure Active Directory を統合する](/azure/architecture/reference-architectures/identity/azure-ad)<br /><br />- [ハイブリッド Id ディレクトリ統合ツールの比較](/azure/active-directory/hybrid/plan-hybrid-identity-design-considerations-tools-comparison)|
|RMS コネクタをインストールする 2 台以上のメンバー コンピューター:<br /><br />-次のオペレーティングシステムのいずれかを実行している64ビットの物理または仮想コンピューター: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012。<br /><br />- 1 GB 以上の RAM。<br /><br />- 64 GB 以上のディスク領域。<br /><br />- 1 つ以上のネットワーク インターフェイス。<br /><br />-認証を必要としないファイアウォール (または web プロキシ) 経由でインターネットにアクセスします。<br /><br />- 所属するフォレストまたはドメインが、RMS コネクタを使用する Exchange または SharePoint サーバーが含まれている組織内の他のフォレストと信頼関係にあること。|フォールト トレランスと高可用性を構成するには、RMS コネクタを 2 台以上のコンピューターにインストールする必要があります。<br /><br />**ヒント**: Outlook Web Access、または Exchange ActiveSync IRM を使用するモバイル デバイスを使用しており、Azure RMS で保護されているメールと添付ファイルへのアクセスを維持する必要がある場合、負荷分散されたコネクタ サーバー グループをデプロイして高可用性を確保することをお勧めします。<br /><br />専用サーバーでコネクタを実行する必要はありませんが、コネクタを使用するサーバーとは別のコンピューターにインストールする必要があります。<br /><br />**重要**: Exchange Server または SharePoint Server が実行されているコンピューター、およびファイル分類インフラストラクチャ用に構成されたファイル サーバーには、コネクタをインストールしないでください。そうしないと、これらのサービスの機能を Azure RMS で使用できなくなります。 また、このコネクタをドメイン コントローラーにインストールしないでください。<br /><br />RMS コネクタで使用するサーバー ワークロードがあり、コネクタを実行するドメインによって信頼されていないドメインにそのワークロードのサーバーがある場合、それらの信頼されていないドメインまたはフォレスト内の他のドメインに、追加の RMS コネクタ サーバーをインストールできます。 <br /><br />組織で実行可能なコネクタ サーバーの数に制限はなく、組織にインストールされているすべてのコネクタ サーバーが同じ構成を共有します。 ただし、コネクタでサーバーを承認するように構成するには、承認されるサーバーまたはサーバー アカウントを参照できる必要があります。つまり、それらのアカウントを参照できるフォレスト内で RMS 管理ツールを実行する必要があります。|


## <a name="steps-to-deploy-the-rms-connector"></a>RMS コネクタをデプロイする手順

コネクタは適切にデプロイするために必要なすべての[前提条件](deploy-rms-connector.md#prerequisites-for-the-rms-connector)を自動的にチェックするわけではないため、開始する前に前提条件がすべて満たされていることを確認してください。 コネクタのインストールとコネクタの構成が完了した後で、そのコネクタを使用するサーバーを構成する必要があります。 

-   **手順 1.**  [RMS コネクタのインストール](install-configure-rms-connector.md#installing-the-rms-connector)

-   **手順 2.**  [資格情報の入力](install-configure-rms-connector.md#entering-credentials)

-   **手順 3.**  [RMS コネクタを使用するサーバーの承認](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)

-   **手順 4 :**  [負荷分散と高可用性の構成](install-configure-rms-connector.md#configuring-load-balancing-and-high-availability)

-   省略可能: [HTTPS を使用するための RMS コネクタの構成](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https)

-   省略可能: [Web プロキシ サーバーを使用するための RMS コネクタの構成](install-configure-rms-connector.md#configuring-the-rms-connector-for-a-web-proxy-server)

-   省略可能: [管理用コンピューターへの RMS コネクタ管理ツールのインストール](install-configure-rms-connector.md#installing-the-rms-connector-administration-tool-on-administrative-computers)

-   **手順 5.**  [RMS コネクタを使用するためのサーバーの構成](configure-servers-rms-connector.md)

    -   [コネクタを使用するように Exchange サーバーを構成する](configure-servers-rms-connector.md#configuring-an-exchange-server-to-use-the-connector)

    -   [コネクタを使用するための SharePoint サーバーの構成](configure-servers-rms-connector.md#configuring-a-sharepoint-server-to-use-the-connector)

    -   [コネクタを使用するためのファイル分類インフラストラクチャ用ファイル サーバーの構成](configure-servers-rms-connector.md#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)


## <a name="next-steps"></a>次のステップ

手順 1: [Azure Rights Management コネクタのインストールと構成](install-configure-rms-connector.md) に進みます。
