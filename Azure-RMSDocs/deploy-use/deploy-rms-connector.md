---
title: "Azure Rights Management コネクタをデプロイする | Azure RMS"
description: "Azure Rights Management (RMS) コネクタを デプロイする方法について説明します。RMS コネクタにより、Microsoft Exchange Server または Microsoft SharePoint Server を使用する既存のオンプレミス デプロイ、または Windows Server とファイル分類インフラストラクチャ (FCI) 機能を実行するファイル サーバーの情報が保護されます。"
author: cabailey
manager: mbaldwin
ms.date: 09/09/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 90e7e33f-9ecc-497b-89c5-09205ffc5066
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a96018818f81787720021b661db10e818f388772
ms.openlocfilehash: 2d962f168dafb1b8c207fa6b5d353a6a3ea4d1b2


---

# Azure Rights Management コネクタをデプロイする

>*適用対象: Azure Rights Management、Windows Server 2012、Windows Server 2012 R2*

ここでは、Azure Rights Management コネクタについて説明してから、このコネクタを適切にデプロイする方法について説明します。 このコネクタを利用すると、既にオンプレミスでデプロイされている **Microsoft Exchange Server**、**SharePoint Server**、またはファイル サーバー (Windows Server と**ファイル分類インフラストラクチャ** (FCI) 機能を実行していること) のデータを保護することができます。

> [!TIP]
> スクリーンショット付きの概要レベルのサンプル シナリオについては、「[Azure RMS in action (Azure RMS の動作)](../understand-explore/what-admins-users-see.md)」の「[Automatically protecting files on file servers running Windows Server and File Classification Infrastructure (Windows Server およびファイル分類インフラストラクチャを実行しているファイル サーバー上のファイルの自動的な保護)](../understand-explore/what-admins-users-see.md#automatically-protecting-files-on-file-servers-running-windows-server-and-file-classification-infrastructure)」セクションを参照してください。

## Microsoft Rights Management コネクタの概要
Microsoft Rights Management (RMS) コネクタを使用すると、既存のオンプレミス サーバーで Information Rights Management (IRM) 機能とクラウドベースの Microsoft Rights Management サービス (Azure RMS) を迅速に使用できるようになります。 この機能により、IT 担当者およびユーザーは、組織の内外にあるドキュメントや画像を簡単に保護することができます。追加のインフラストラクチャをインストールしたり、他の組織との間に信頼関係を確立したりする必要はありません。 

RMS コネクタはコンパクトなサービスであり、Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2 を実行しているサーバーにオンプレミスでインストールできます。 コネクタは、物理コンピューター上だけでなく、Azure IaaS VM などの仮想マシン上でも実行できます。 デプロイされたコネクタは、次の図に示すように、オンプレミス サーバーとクラウド サービスとの間の通信インターフェイス (リレー) の役割を果たします。

![RMS コネクタ アーキテクチャの概要](../media/RMS_connector.png)


### サポートされるオンプレミス サーバー

RMS コネクタでサポートされるオンプレミス サーバーは、Exchange Server と SharePoint Server、また、Windows Server を実行しておりファイル分類インフラストラクチャ (フォルダー内の Office ドキュメントを分類してポリシーを適用します) を使用するファイル サーバーです。 

> [!NOTE]
> Office ドキュメントだけでなく、すべての種類のファイルをファイル分類インフラストラクチャで保護したい場合は、RMS コネクタではなく [RMS 保護コマンドレット](https://msdn.microsoft.com/library/azure/mt433195.aspx)を使用してください。

これらのオンプレミス サーバーのうち、どのバージョンが RMS コネクタでサポートされるかについては、「[Azure RMS をサポートするオンプレミス サーバー](..\get-started\requirements-servers.md)」をご覧ください。


### ハイブリッド シナリオのサポート

RMS コネクタは、組織のユーザーのうち一部だけがオンライン サービスに接続する場合でも使用でき、これをハイブリッド シナリオといいます。 たとえば、ユーザーのメールボックスの中に Exchange Online を使用するものと、Exchange Server を使用するものがあるとします。 RMS コネクタをインストールすると、すべてのユーザーが Azure RMS を使用して電子メールと添付ファイルを保護し、使用できるようになります。2 つのデプロイメント構成の間で、情報はシームレスに保護されます。

### 自主管理キー (BYOK) のサポート

Azure RMS の自分のテナント キーを管理する場合 (Bring Your Own Key または BYOK シナリオ)、そのキーを使用する RMS コネクタとオンプレミス サーバーには、テナント キーを含むハードウェア セキュリティ モジュール (HSM) に対するアクセス権がありません。 これは、テナント キーを使用するすべての暗号操作は、オンプレミスではなく、Azure RMS で実行されるためです。

このような、テナント キーを自主管理するシナリオの詳細については、「[Azure Rights Management テナント キーを計画して実装する](../plan-design\plan-implement-tenant-key.md)」を参照してください。

## RMS コネクタの前提条件
RMS コネクタをインストールする前に、次の要件を満たしていることを確認してください。

|要件|詳細情報|
|---------------|--------------------|
|Rights Management (RMS) サービスがアクティブ化されている|[Rights Management をアクティブにする](activate-service.md)|
|オンプレミス Active Directory フォレストと Azure Active Directory の間のディレクトリ同期|RMS をアクティブ化した後に、Azure Active Directory を構成して Active Directory データベース内のユーザーおよびグループを使用できるようにする必要があります。<br /><br />**重要**: RMS コネクタが動作するためには、テスト ネットワークに対してもこのディレクトリ同期手順を実行する必要があります。 Office 365 および Azure Active Directory では、Azure Active Directory で手動作成したアカウントを使用できますが、このコネクタでは、Azure Active Directory のアカウントが Active Directory ドメイン サービスと同期している必要があります。手動によるパスワードの同期では不十分です。<br /><br />詳細については、次のリソースを参照してください。<br /><br />[オンプレミス ID と Azure Active Directory の統合](/active-directory/active-directory-aadconnect)<br /><br />[ハイブリッド ID ディレクトリ統合ツールの比較](/active-directory/active-directory-hybrid-identity-design-considerations-tools-comparison)|
|省略可能ですが、推奨されます:<br /><br />オンプレミス Active Directory と Azure Active Directory の間でのフェデレーションの有効化|オンプレミス ディレクトリと Azure Active Directory の間で ID フェデレーションを有効にすることができます。 この構成により、RMS サービスへのシングル サインオンを使用して、よりシームレスなユーザー エクスペリエンスを提供できます。 シングル サインオンを使用できない場合、ユーザーは、権限で保護されたコンテンツを使用する前に資格情報の入力を求められます。<br /><br />Active Directory ドメイン サービスと Azure Active Directory の間で、Active Directory フェデレーション サービス (AD FS) を使用したフェデレーションを構成する手順については、Windows Server ライブラリの「 [チェックリスト:AD FS を使用してシングル サインオンを実装および管理する](http://technet.microsoft.com/library/jj205462.aspx) 」をご覧ください。|
|RMS コネクタをインストールする 2 台以上のメンバー コンピューター:<br /><br />- 次のいずれかのオペレーティング システムが搭載されている 64 ビットの物理または仮想コンピューター: Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2。<br /><br />- 1 GB 以上の RAM。<br /><br />- 64 GB 以上のディスク領域。<br /><br />- 1 つ以上のネットワーク インターフェイス。<br /><br />- 認証が不要な、ファイアウォール (または Web プロキシ) 経由のインターネット アクセス。<br /><br />- 所属するフォレストまたはドメインが、RMS コネクタを使用する Exchange または SharePoint サーバーが含まれている組織内の他のフォレストと信頼関係にあること。|フォールト トレランスと高可用性を構成するには、RMS コネクタを 2 台以上のコンピューターにインストールする必要があります。<br /><br />**ヒント**: Outlook Web Access、または Exchange ActiveSync IRM を使用するモバイル デバイスを使用しており、Azure RMS で保護されているメールと添付ファイルへのアクセスを維持する必要がある場合、負荷分散されたコネクタ サーバー グループをデプロイして高可用性を確保することをお勧めします。<br /><br />専用サーバーでコネクタを実行する必要はありませんが、コネクタを使用するサーバーとは別のコンピューターにインストールする必要があります。<br /><br />**重要**: Exchange Server または SharePoint Server が実行されているコンピューター、およびファイル分類インフラストラクチャ用に構成されたファイル サーバーには、コネクタをインストールしないでください。そうしないと、これらのサービスの機能を Azure RMS で使用できなくなります。 また、このコネクタをドメイン コントローラーにインストールしないでください。|

## RMS コネクタをデプロイする手順

コネクタを適切にデプロイするための[前提条件](deploy-rms-connector.md#prerequisites-for-the-rms-connector)は自動的にはチェックされないため、開始する前に必ず、前提条件がすべて満たされていることを確認してください。 コネクタのインストールとコネクタの構成が完了した後で、そのコネクタを使用するサーバーを構成する必要があります。 

-   **手順 1.** [RMS コネクタのインストール](install-configure-rms-connector.md#installing-the-rms-connector)

-   **手順 2.** [資格情報の入力](install-configure-rms-connector.md#entering-credentials)

-   **手順 3.** [RMS コネクタを使用するサーバーの承認](install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector)

-   **手順 4.** [負荷分散と高可用性の構成](install-configure-rms-connector.md#configuring-load-balancing-and-high-availability)

-   省略可能: [HTTPS を使用するための RMS コネクタの構成](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https)

-   省略可能: [Web プロキシ サーバーを使用するための RMS コネクタの構成](install-configure-rms-connector.md#configuring-the-rms-connector-for-a-web-proxy-server)

-   省略可能: [管理用コンピューターへの RMS コネクタ管理ツールのインストール](install-configure-rms-connector.md#installing-the-rms-connector-administration-tool-on-administrative-computers)

-   **手順 5.** [RMS コネクタを使用するためのサーバーの構成](configure-servers-rms-connector.md)

    -   [コネクタを使用するための Exchange サーバーの構成](configure-servers-rms-connector.md#configuring-an-exchange-server-to-use-the-connector)

    -   [コネクタを使用するための SharePoint サーバーの構成](configure-servers-rms-connector.md#configuring-a-sharepoint-server-to-use-the-connector)

    -   [コネクタを使用するためのファイル分類インフラストラクチャ用ファイル サーバーの構成](configure-servers-rms-connector.md#configuring-a-file-server-for-file-classification-infrastructure-to-use-the-connector)


## 次のステップ

手順 1: [Azure Rights Management コネクタのインストールと構成](install-configure-rms-connector.md) に進みます。


<!--HONumber=Sep16_HO3-->


