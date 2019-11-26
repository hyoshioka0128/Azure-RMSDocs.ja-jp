---
title: AD RMS から Azure Information Protection への移行
description: Active Directory Rights Management サービス (AD RMS) のデプロイを Azure Information Protection に移行する方法を説明します。 After the migration, users still have access to documents and email messages that your organization protected by using AD RMS.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/25/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 978feb26639a3c8f05ac2576a2e922c744cae9cf
ms.sourcegitcommit: fed1df1858f8316f7dd45e751c6910b444651a87
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2019
ms.locfileid: "74474304"
---
# <a name="migrating-from-ad-rms-to-azure-information-protection"></a>AD RMS から Azure Information Protection への移行

>*適用対象: Active Directory Rights Management サービス[、Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Active Directory Rights Management サービス (AD RMS) デプロイを Azure Information Protection に移行するには、以下の一連の手順を使います。 

移行が済むと、AD RMS サーバーは使われなくなりますが、ユーザーは AD RMS を使って組織で保護されていたドキュメントやメール メッセージに引き続きアクセスできます。 新しく保護されるコンテンツでは、Azure Information Protection の Azure Rights Management サービス (Azure RMS) が使われます。

この AD RMS の移行が組織にとって適切かどうかわからない場合は、次のようにしてください。

- Azure Information Protection の概要については、「[Azure Information Protection とは](./what-is-information-protection.md)」をご覧ください。

- Azure Information Protection と AD RMS の比較については、「[Azure Information Protection と AD RMS の比較](./compare-on-premise.md)」をご覧ください。

## <a name="recommended-reading-before-you-migrate-to-azure-information-protection"></a>Azure Information Protection に移行する前に推奨されるドキュメント

以下のドキュメントは必須ではありませんが、移行を開始する前に読んでおくと役に立つ場合があります。 このナレッジによって、お客様の移行手順と関係のあるテクノロジが、どのような仕組みで動作するかを、より詳しく理解できます。

- [Azure Information Protection テナント キーを計画して実装する](./plan-implement-tenant-key.md): クラウドで SLC キーと同等のキーを Microsoft が管理するか (既定)、ユーザーが管理するか ("Bring Your Own Key" (BYOK) 構成) という、Azure Information Protection テナントで利用できるキー管理オプションについて説明しています。 

- [RMS service discovery](./rms-client/client-deployment-notes.md#rms-service-discovery): This section of the RMS client deployment notes explains that the order for service discovery is **registry**, then **service connection point (SCP)** , then **cloud**. SCP がインストールされている環境の移行プロセスでは、SCP から返される AD RMS クラスターを使用しないように、レジストリ設定で Azure Information Protection テナントのクライアントを構成します。

- [Microsoft Rights Management コネクタの概要](./deploy-rms-connector.md#overview-of-the-microsoft-rights-management-connector): RMS コネクタに関するドキュメントのこのセクションでは、オンプレミス サービスから Azure Rights Management サービスに接続してドキュメントと電子メールを保護する方法について説明しています。

In addition, if you are familiar with how AD RMS works, you might find it useful to read [How does Azure RMS work? Under the hood](./how-does-it-work.md) to help you identify which technology processes are the same or different for the cloud version.

## <a name="prerequisites-for-migrating-ad-rms-to-azure-information-protection"></a>AD RMS から Azure Information Protection への移行の前提条件

Azure Information Protection への移行を始める前に、次の前提条件が満たされていること、および制限事項を理解していることを確認してください。

- **サポートされる RMS のデプロイ:**
    
  - AD RMS の次のリリースでは、Azure Information Protection への移行をサポートします。
    
      - Windows Server 2008 R2 (x64)
        
      - Windows Server 2012 (x64)
        
      - Windows Server 2012 R2 (x64)
        
      - Windows Server 2016 (x64)
        
  - すべての有効な AD RMS トポロジがサポートされます。
    
      - 単一フォレスト、単一 RMS クラスター
        
      - 単一フォレスト、複数のライセンス専用 RMS クラスター
        
      - 複数フォレスト、複数 RMS クラスター
        
    注: 既定では、複数の AD RMS クラスターが Azure Information Protection の 1 つのテナントに移行します。 個別の Azure Information Protection テナントが必要な場合は、それぞれ異なる移行として処理する必要があります。 1 つの RMS クラスターからのキーを、複数のテナントにインポートすることはできません。

- **Azure Information Protection のサブスクリプション (Azure Rights Management は非アクティブです) など、Azure Information Protection を実行するためのすべての要件:**

    「[Azure Information Protection の要件](./requirements.md)」をご覧ください。

    Note that if you have computers that run Office 2010, you must install the [Azure Information Protection client or the Azure Information Protection unified labeling client for users](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client), because these clients provide the ability to authenticate users to cloud services. For later versions of Office, these clients are required for classification and labeling, and the Azure Information Protection client is optional but recommended if you want to only protect data. For more information, see the admin guides for the [Azure Information Protection client](./rms-client/client-admin-guide.md) and the [Azure Information Protection unified labeling client](./rms-client/clientv2-admin-guide.md).

    AD RMS からの移行を行うには、その前に Azure Information Protection のサブスクリプションを用意しておく必要がありますが、移行を始める前はテナントの Rights Management サービスをアクティブにしないことをお勧めします。 移行プロセスには、AD RMS からキーとテンプレートをエクスポートし、それらを Azure Information Protection のテナントにインポートした後の、このアクティブ化の手順が含まれています。 ただし、Rights Management サービスが既にアクティブ化されている場合でも、いくつかの追加手順を行って AD RMS から移行することができます。


- **Azure Information Protection の準備:**

  - オンプレミス ディレクトリと Azure Active Directory の間でのディレクトリ同期

  - Azure Active Directory でのメールが有効なグループ

    「[Azure Information Protection 向けのユーザーとグループの準備](prepare.md)」をご覧ください。

- **AD RMS で Exchange Server** (たとえば、トランスポート ルールと Outlook Web Access) または SharePoint Server の Information Rights Management (IRM) 機能を使用していた場合:

  - 短時間これらのサーバーで IRM が利用できなくなることを予定しておきます。
 
    移行後もこれらのサーバーで IRM を引き続き使用できます。 ただし、移行手順には、IRM サービスの一時的な無効化、コネクタのインストールと構成、サーバーの再構成、IRM の再有効化が含まれます。

    移行プロセス中にサービスが中断するのはこのときだけです。

- **HSM で保護されたキーを使用して自分で Azure Information Protection テナント キーを管理する場合**:

    - このオプション構成では、Azure Key Vault と、HSM で保護されたキーを保持する Key Vault をサポートする Azure サブスクリプションが必要です。 詳細については、[Azure Key Vault の価格のページ](https://azure.microsoft.com/pricing/details/key-vault/)を参照してください。 


### <a name="cryptographic-mode-considerations"></a>暗号化モードに関する注意事項

AD RMS クラスターが現在暗号化モード 1 の場合は、移行を開始する前にクラスターを 暗号化モード 2 にアップグレードしないでください。 代わりに暗号化モード 1 を使用して移行し、移行後タスクの 1 つとして移行の終了時にテナント キーを更新できます。

AD RMS 暗号化モードを確認するには:
 
- Windows Server 2012 R2 および Windows 2012 の場合: AD RMS クラスターのプロパティ > **[全般]** タブ。 

- Windows Server 2008 R2 の場合: 「[RSA key length is increased to 2048 bits for AD RMS in Windows Server 2008 R2 and in Windows Server 2008 (Windows Server 2008 R2 と Windows Server 2008 の AD RMS では、RSA キーの長さが 2048 ビットに増加しました)](https://support.microsoft.com/help/2627272/rsa-key-length-is-increased-to-2048-bits-for-ad-rms-in-windows-server )」の修正プログラムがインストールされているかを確認します。 インストールされていない場合は、ご使用の AD RMS クラスターは暗号化モード 1 で実行されています。

### <a name="migration-limitations"></a>移行の制限

- Azure Information Protection で使われる Rights Management サービスによってサポートされていないソフトウェアやクライアントでは、Azure Rights Management によって保護されているコンテンツを保護または使用できません。 Be sure to check the supported applications and clients sections from [Requirements for Azure Information Protection](./requirements.md).

- AD RMS デプロイが外部のパートナーと (たとえば、信頼されたユーザー ドメインやフェデレーションを使用して) コラボレーションするように構成されている場合は、同時にまたは可能な限り速やかにパートナーも Azure Information Protection に移行する必要があります。 移行前に Azure Information Protection を使用して保護されていたコンテンツに引き続きアクセスするには、外部パートナーも同じようにこのドキュメントで説明されているクライアント構成の変更を行う必要があります。
    
    パートナーの構成は異なる可能性があるので、このドキュメントで再構成を正確に説明することはできません。 ただし、次のセクションの計画ガイドラインを参照し、詳細を [Microsoft サポートにお問い合わせ](./information-support.md#support-options-and-community-resources)ください。

## <a name="migration-planning-if-you-collaborate-with-external-partners"></a>外部のパートナーとコラボレーションしている場合の移行計画

AD RMS パートナーも Azure Information Protection に移行する必要があるため、移行の計画フェーズにパートナーを含めます。 後述する移行手順を実行する前に、次の要件が満たされていることを確認します。

- パートナーが、Azure Rights Management サービスをサポートする Azure Active Directory テナントを持っていること。  
    
    たとえば、Office 365 E3 または E5 サブスクリプション、Enterprise Mobility + Security サブスクリプション、Azure Information Protection のスタンドアロン サブスクリプションなどが必要です。

- パートナーの Azure Rights Management サービスはまだアクティブ化されていないが、Azure Rights Management サービスの URL はわかっていること。

    They can get this information by installing the Azure Rights Management Tool, connecting to the service ([Connect-AipService](/powershell/module/aipservice/connect-aipservice)), and then viewing their tenant information for the Azure Rights Management service ([Get-AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration)).

- パートナーの AD RMS で保護されたコンテンツへの要求をパートナーのテナントの Azure Rights Management サービスにリダイレクトするよう、移行後のクライアントを構成できるように、パートナーの AD RMS クラスターの URL と Azure Rights Management サーバーの URL をパートナーから提供されていること。 クライアントのリダイレクトを構成する手順については、手順 7 で説明します。

- こちら側のユーザーの移行を始める前に、パートナーが AD RMS クラスターのルート キー (SLC) をテナントにインポートしていること。 同様に、パートナーが自分たちのユーザーの移行を始める前に、こちら側の AD RMS クラスターのルート キーをインポートしておく必要があります。 Instructions for importing the key are covered in this migration process, [Step 4. Export configuration data from AD RMS and import it to Azure Information Protection](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection). 

## <a name="overview-of-the-steps-for-migrating-ad-rms-to-azure-information-protection"></a>AD RMS から Azure Information Protection への移行手順の概要

移行手順は 5 つのフェーズに分けることができ、異なるタイミングで、異なる管理者によって実行できます。

[**フェーズ 1: 移行の準備**](migrate-from-ad-rms-phase1.md)

- **Step 1: Install the AIPService PowerShell module and identify your tenant URL**

    The migration process requires you to run one or more of the PowerShell cmdlets from the AIPService module. 多くの移行手順を完了するには、テナントの Azure Rights Management サービス URL が必要です。この値は、PowerShell を使って特定することができます。

- **Step 2. Prepare for client migration**

    すべてのクライアントを一度に移行できず、少しずつ移行する場合は、オンボーディング制御を使い、移行前スクリプトをデプロイします。 ただし、段階的な移行ではなく同時にすべてを移行する場合は、この手順をスキップできます。

- **手順 3: Exchange の展開を移行用に準備する**

    この手順は、現在 Exchange Online またはオンプレミスの Exchange の IRM 機能を使ってメールを保護している場合に必要です。 ただし、段階的な移行ではなく同時にすべてを移行する場合は、この手順をスキップできます。

[**フェーズ 2: AD RMS のサーバー側の構成**](migrate-from-ad-rms-phase2.md)

- **Step 4. Export configuration data from AD RMS and import it to Azure Information Protection**

    You export the configuration data (keys, templates, URLs) from AD RMS to an XML file, and then upload that file to the Azure Rights Management service from Azure Information Protection, by using the Import-AipServiceTpd PowerShell cmdlet. 次に、Azure Rights Management サービスのテナント キーとして使用するインポート済みのサーバー ライセンサー証明書 (SLC) キーを指定します。 AD RMS のキー構成によっては、追加の手順が必要になる可能性があります。

    - **ソフトウェアで保護されているキーからソフトウェアで保護されているキーへの移行**:

        AD RMS の一元管理されたパスワード ベースのキーを、Microsoft が管理する Azure Information Protection テナント キーに移行します。 これは、最も簡単な移行パスであり、追加の手順は必要ありません。

    - **HSM で保護されているキーから HSM で保護されているキーへの移行**:

        AD RMS 用の HSM により保存されているキーを、顧客管理の Azure Information Protection テナント キーに移行します ("Bring Your Own Key" つまり BYOK シナリオ)。 This requires additional steps to transfer the key from your on-premises nCipher HSM to Azure Key Vault and authorize the Azure Rights Management service to use this key. HSM で保護されている既存のキーは、モジュールで保護する必要があります。OCS で保護されているキーは、Rights Management サービスでサポートされていません。

    - **ソフトウェアで保護されているキーから HSM で保護されているキーへの移行**:

        AD RMS の一元管理されたパスワード ベースのキーを、顧客が管理する Azure Information Protection テナント キーに移行します (“bring your own key” つまり BYOK シナリオ)。 This requires the most configuration because you must first extract your software key and import it to an on-premises HSM, and then do the additional steps to transfer the key from your on-premises nCipher HSM to an Azure Key Vault HSM and authorize the Azure Rights Management service to use the key vault that stores the key.

- **Step 5. Activate the Azure Rights Management service**

    可能であれば、インポート処理の前ではなく後に、この手順を実行します。 インポート前にこのサービスをアクティブした場合は、追加の手順が必要になります。

- **Step 6. Configure imported templates**

    権限ポリシー テンプレートをインポートするときに、それらの状態がアーカイブされます。 ユーザーが権限ポリシー テンプレートを表示および使用できるようにする場合は、Azure クラシック ポータルでテンプレートの状態を公開に変更する必要があります。


[**フェーズ 3: クライアント側の構成**](migrate-from-ad-rms-phase3.md)

- **手順 7: Azure Information Protection を使用するように Windows コンピューターを再構成する**

    既存の Windows コンピューターを、AD RMS ではなく Azure Rights Management サービスを使うように再構成する必要があります。 この手順は、自分の組織内のコンピューターに適用されるだけでなく、AD RMS を実行していた間に外部パートナーとコラボレーションしていた場合はパートナー組織のコンピューターにも適用されます。

[**フェーズ 4: サポート サービスの構成**](migrate-from-ad-rms-phase4.md)

- **手順 8: IRM と Exchange Online の統合を構成する**

    この手順では、Exchange Online の AD RMS への移行を完了し、Azure Rights Management サービスを使うようにします。

- **手順 9: Exchange サーバーおよび SharePoint サーバー用に IRM 統合を構成する**

    この手順では、オンプレミスの Exchange または SharePoint の AD RMS への移行を完了し、Azure Rights Management サービスを使うようにします。これには、Rights Management コネクタをデプロイする必要があります。


[**フェーズ 5: 移行後のタスク**](migrate-from-ad-rms-phase5.md )

- **手順 10: AD RMS のプロビジョニング解除**

    すべての Windows コンピューターが Azure Rights Management サービスを使っていて、AD RMS サーバーにアクセスしていないことを確認した後は、AD RMS デプロイをプロビジョニング解除できます。

- **手順 11: クライアントの移行タスクを完了する**

    iOS 搭載の携帯電話や iPad、Android 携帯電話とタブレット、Windows 携帯電話とタブレット、Mac コンピューターなどのモバイル デバイスをサポートする[モバイル デバイス拡張機能](https://technet.microsoft.com/library/dn673574.aspx)をデプロイしてある場合は、これらのクライアントが AD RMS を使うようにリダイレクトした SRV レコードを DNS から削除する必要があります。 
    
    準備フェーズ中に構成したオンボーディング制御はもう必要ありません。 ただし、段階的な移行ではなく、同時にすべてを移行することを選んだためにオンボーディング制御を使用しなかった場合は、この手順をスキップしてオンボーディング制御を削除することができます。
    
    Windows コンピューターで Office 2010 を実行している場合は、"**AD RMS Rights Policy Template Management (Automated) (AD RMS 権利ポリシー テンプレート管理 (自動))** " タスクを無効にする必要があるかどうかを確認します。

- **手順 12: Azure Information Protection テナント キーを更新する**

    移行前に暗号化モード 2 で実行されていない場合は、この手順の使用をお勧めします。


## <a name="next-steps"></a>次のステップ
移行を始めるには、「[フェーズ 1 - 準備](migrate-from-ad-rms-phase1.md)」に進んでください。

