---
title: "AD RMS から Azure Rights Management への移行 | Azure RMS"
description: "Active Directory Rights Management サービス (AD RMS) のデプロイを Azure Rights Management (Azure RMS) に移行するための手順です。 移行後もユーザーは AD RMS を使用して保護されていたドキュメントや電子メール メッセージにアクセスでき、新しく保護されるコンテンツは Azure RMS を使用します。"
author: cabailey
manager: mbaldwin
ms.date: 09/19/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5c20772240961bdd3052e55a19eaca21ef7da003
ms.openlocfilehash: 01c107979265abf0d34060eccf09ca32c0086ab8


---

# AD RMS から Azure Rights Management への移行

>*適用対象: Active Directory Rights Management サービス、Azure Rights Management*

Active Directory Rights Management サービス (AD RMS) のデプロイを Azure Rights Management (Azure RMS) に移行するには、次の命令セットを使用します。 移行後もユーザーは AD RMS を使用して保護されていたドキュメントや電子メール メッセージにアクセスでき、新しく保護されるコンテンツは Azure RMS を使用します。

この AD RMS の移行が組織にとって適切かどうかわからない場合は、次のようにしてください。

-   Azure RMS の概要、Azure RMS で解決できるビジネス上の問題、管理者およびユーザーから見た Azure RMS、Azure RMS のしくみについては、「[Azure Active Directory Rights Management の概要](../understand-explore/what-is-azure-rms.md)」を参照してください

-   Azure RMS と AD RMS の比較については、「[Azure Rights Management と AD RMS を構成する](../understand-explore/compare-azure-rms-ad-rms.md)」を参照してください。

## AD RMS から Azure RMS への移行の前提条件
Azure RMS への移行を始める前に、次の前提条件が満たされていること、および制限事項を理解していることを確認してください。


- **サポートされる RMS のデプロイ:**
    
    - AD RMS の次のリリースでは、Azure RMS への移行をサポートします。
    
        - Windows Server 2008 R2 (x64)
        
        - Windows Server 2012 (x64)
        
        - Windows Server 2012 R2 (x64)
        
    - 暗号化モード 2:
    
        - Azure RMS への移行を開始する前に、AD RMS サーバーとクライアントを暗号化モード 2 で実行する必要があります。 現在のサーバー ライセンサー証明書 (SLC) キーは暗号化モード 2 を使用している必要がありますが、以前のキーが暗号化モード 1 を使用するように構成されていた場合も、Azure RMS ではアーカイブされたキーとしてサポートされます。 暗号化モードの詳細と暗号化モード 2 への移行方法については、「[AD RMS の暗号化モード](https://technet.microsoft.com/library/hh867439(v=ws.10).aspx)」を参照してください。
        
    - すべての有効な AD RMS トポロジがサポートされます。
    
        - 単一フォレスト、単一 RMS クラスター
        
        - 単一フォレスト、複数のライセンス専用 RMS クラスター
        
        - 複数フォレスト、複数 RMS クラスター
        
    注: 既定では、複数の RMS クラスターが 1 つの Azure RMS テナントに移行します。 個別の Azure RMS テナントが必要な場合は、それぞれ異なる移行として処理する必要があります。 1 つの RMS クラスターからのキーを、複数の Azure RMS テナントにインポートすることはできません。

- **Azure RMS テナント (非アクティブ) など、Azure RMS を実行するためのすべての要件:**

    「[Azure Rights Management の要件](../get-started/requirements-azure-rms.md)」を参照してください。

    AD RMS からの移行を行うには、その前に Azure RMS テナントを用意しておく必要がありますが、移行前に Rights Management サービスをアクティブにしないことをお勧めします。 アクティブ化は、AD RMS からキーとテンプレートをエクスポートし、それらを Azure RMS にインポートした後で、移行プロセスによって行われます。 ただし、Azure RMS が既にアクティブ化されている場合でも、AD RMS から移行することはできます。


- **Azure RMS 用の準備:**

    - オンプレミス ディレクトリと Azure Active Directory の間でのディレクトリ同期

    - Azure Active Directory でのメールが有効なグループ

    「[Azure Rights Management の準備を行う](prepare.md)」を参照してください。


- **AD RMS で Exchange Server** (たとえば、トランスポート ルールと Outlook Web Access) または SharePoint Server の Information Rights Management (IRM) 機能を使用していた場合:

    - 短時間これらのサーバーで IRM が利用できなくなることを予定しておきます。
 
    移行後は Azure RMS を使用してこれらのサーバーで IRM を引き続き使用できます。 ただし、移行手順には、IRM サービスの一時的な無効化、コネクタのインストールと構成、サーバーの再構成、IRM の再有効化が含まれます。

    移行プロセス中にサービスが中断するのはこのときだけです。

- **HSM で保護されたキーを使用して自主的に Azure RMS テナント キーを管理する場合**:

    - このオプション構成では、Azure Key Vault と、HSM で保護されたキーを保持する Key Vault をサポートする Azure サブスクリプションが必要です。 詳細については、[Azure Key Vault の価格のページ](https://azure.microsoft.com/en-us/pricing/details/key-vault/)を参照してください。 


制限事項:

-   移行プロセスは、サーバー ライセンス証明書 (SLC) キーから Azure RMS のハードウェア セキュリティ モジュール (HSM) への移行をサポートしていますが、Exchange Online では現時点ではこの構成はサポートされていません。 Azure RMS への移行後に Exchange Online で完全な IRM 機能を使用する場合は、ご使用の Azure RMS テナント キーが[マイクロソフトによって管理](../plan-design/plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok)される必要があります。 または、Azure RMS テナントがユーザーにより管理される場合 (BYOK)、Exchange Online では IRM の機能を制限付きで実行できます。 Exchange Online と Azure RMS の使用の詳細については、「[手順 6. これらの移行手順の「](migrate-from-ad-rms-phase3.md#step-6-configure-irm-integration-for-exchange-online)IRM と Exchange Online の統合を構成する」を参照してください。

-   Azure RMS でサポートされていないソフトウェアおよびクライアントは、Azure RMS によって保護されているコンテンツを保護したり使用したりすることはできません。 記事「[Azure Rights Management の要件](../get-started/requirements-azure-rms.md)」のサポートされているアプリケーションとクライアントのセクションを確認してください。

-   オンプレミスのキーをアーカイブとして Azure RMS にインポートし (インポート プロセス中に TPD をアクティブには設定しないでください)、バッチ内のユーザーを段階的に移行する場合は、AD RMS のユーザーは、移行されたユーザーにより新規に保護されたコンテンツにアクセスすることはできません。 この場合は、可能な限り短い移行時間で論理バッチ内のユーザーを移行します。これにより、関連付けられたユーザーが一緒に移行されます。

    インポート処理中に TPD をアクティブにした場合は、すべてのユーザーが同じキーを使用してコンテンツを保護するため、この制限は適用されません。 すべてのユーザーを個別に自分のペースで移行できるため、この構成を使用することをお勧めします。

-   外部のパートナーと (たとえば、信頼されたユーザー ドメインやフェデレーションを使用して) コラボレーションしている場合は、同時にまたは可能な限り速やかにパートナーも Azure RMS に移行する必要があります。 移行前に AD RMS を使用して保護されていたコンテンツに引き続きアクセスするには、外部パートナーも同じようにこのドキュメントで説明されているクライアント構成の変更を行う必要があります。

    パートナーの構成は異なる可能性があるので、このドキュメントで再構成を正確に説明することはできません。 支援が必要な場合は、[Microsoft サポートに連絡](../get-started/information-support.md#support-options-and-community-resources)してください。

## AD RMS から Azure RMS への移行手順の概要


移行手順は 4 つのフェーズに分けることができ、異なるタイミングに異なる管理者が実行できます。

[**フェーズ 1 - AD RMS のサーバー側の構成**](migrate-from-ad-rms-phase1.md)

- **手順 1: Azure RMS 管理ツールをダウンロードする**

    移行プロセスでは、Azure RMS 管理ツールと共にインストールされる Azure RMS モジュールから、1 つ以上の Windows PowerShell コマンドレットを実行する必要があります。

- **手順 2. AD RMS から構成データをエクスポートし、それを Azure RMS にインポートする**

    構成データ (キー、テンプレート、URL) を AD RMS から XML ファイルにエクスポートした後、Import-AadrmTpd Windows PowerShell コマンドレットを使用してそのファイルを Azure RMS にアップロードします。 AD RMS のキー構成によっては、追加の手順が必要になる可能性があります。

    - **ソフトウェアで保護されているキーからソフトウェアで保護されているキーへの移行**:

        AD RMS の一元管理されたパスワード ベースのキーを、マイクロソフトが管理する Azure RMS テナント キーに移行します。 これは、最も簡単な移行パスであり、追加の手順は必要ありません。

    - **HSM で保護されているキーから HSM で保護されているキーへの移行**:

        AD RMS 用の HSM により保存されているキーを、顧客管理の Azure RMS テナント キーに移行します (“Bring Your Own Key” つまり BYOK シナリオ)。 これには、オンプレミスの Thales HSM から Azure Key Vault にキーを転送し、Azure RMS にこのキーの使用を承認する追加手順が必要です。 HSM で保護されている既存のキーは、モジュールで保護する必要があります。OCS で保護されているキーは、Rights Management サービスでサポートされていません。

    - **ソフトウェアで保護されているキーから HSM で保護されているキーへの移行**:

        AD RMS の一元管理されたパスワード ベースのキーを、顧客が管理する Azure RMS テナント キーに移行します (“bring your own key” つまり BYOK シナリオ)。 最初にソフトウェア キーを抽出してオンプレミス HSM にインポートした後、オンプレミス Thales HSM から Azure Key Vault HSM にキーを転送し、キーを格納するキー コンテナーの使用を Azure RMS に承認する追加手順が必要になるため、必要な構成はこの方法が最も多くなります。

- **手順 3. Azure RMS テナントをアクティブ化する**

    可能であれば、インポート処理の前ではなく後に、この手順を実行します。

- **手順 4. インポートされたテンプレートを構成する**

    権限ポリシー テンプレートをインポートするときに、それらの状態がアーカイブされます。 ユーザーが権限ポリシー テンプレートを表示および使用できるようにする場合は、Azure クラシック ポータルでテンプレートの状態を公開に変更する必要があります。


[**フェーズ 2 - クライアント側の構成**](migrate-from-ad-rms-phase2.md)


- **手順 5: Azure RMS を使用するようにクライアントを再構成する**

    既存の Windows コンピューターを、AD RMS ではなく Azure RMS サービスを使用するように再構成する必要があります。 この手順は、自分の組織内のコンピューターに適用されるだけでなく、AD RMS を実行していた間に外部パートナーとコラボレーションしていた場合はパートナー組織のコンピューターにも適用されます。

    また、iOS 搭載の携帯電話や iPad、Android 端末およびタブレット、Windows Phone、Mac コンピューターなどのモバイル デバイスをサポートする[モバイル デバイス拡張機能](http://technet.microsoft.com/library/dn673574.aspx)をデプロイした場合、これらのクライアントが AD RMS を使用するようにリダイレクトした SRV レコードを DNS から削除する必要があります。


[**フェーズ 3 - サポート サービスの構成**](migrate-from-ad-rms-phase3.md)


- **手順 6: IRM と Exchange Online の統合を構成する**

    Exchange Online で Azure RMS を使用する場合、この手順は必須です。


- **手順 7: RMS コネクタをデプロイする**

    次のようなオンプレミス サービスを Azure RMS で使用する場合は、この手順が必要です。

    - Exchange Server (たとえば、トランスポート ルールおよび Outlook Web Access)

    - SharePoint Server

    - ファイル分類インフラストラクチャ (FCI) を実行している Windows Server


[**フェーズ 4 - 移行後のタスク**](migrate-from-ad-rms-phase4.md )

- **手順 8. AD RMS の使用を停止する**

    すべてのクライアントが Azure RMS を使用していて、AD RMS サーバーにアクセスしていないことを確認した後、AD RMS のデプロイの使用を停止できます。


- **手順 9: Azure RMS テナント キーを更新する**

    この手順は省略できますが、手順 2 で Azure RMS テナント キー トポロジとして "マイクロソフト管理" を選択した場合は、実行することを推奨します。 選択した Azure RMS テナント キー トポロジが顧客管理 (BYOK) である場合、この手順は適用できません。


## 次のステップ
移行を開始するには「[フェーズ 1 - サーバー側の構成](migrate-from-ad-rms-phase1.md)」に進みます。




<!--HONumber=Sep16_HO3-->


