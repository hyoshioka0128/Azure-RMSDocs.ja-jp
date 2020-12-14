---
title: AD RMS から Azure Information Protection への移行
description: Active Directory Rights Management サービス (AD RMS) のデプロイを Azure Information Protection に移行する方法を説明します。 移行後も、ユーザーは AD RMS を使用して組織が保護したドキュメントや電子メールメッセージにアクセスできます。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/11/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172
ms.subservice: migration
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 6846829cec153eb02bb1ad3e6900537f3d0024e2
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97381869"
---
# <a name="migrating-from-ad-rms-to-azure-information-protection"></a>AD RMS から Azure Information Protection への移行

>***適用対象**: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連**: [AIP のラベル付けクライアントと従来のクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

Active Directory Rights Management サービス (AD RMS) デプロイを Azure Information Protection に移行するには、以下の一連の手順を使います。 

移行が済むと、AD RMS サーバーは使われなくなりますが、ユーザーは AD RMS を使って組織で保護されていたドキュメントやメール メッセージに引き続きアクセスできます。 新しく保護されるコンテンツでは、Azure Information Protection の Azure Rights Management サービス (Azure RMS) が使われます。

この AD RMS の移行が組織にとって適切かどうかわからない場合は、次のようにしてください。

- Azure Information Protection の概要については、「[Azure Information Protection とは](./what-is-information-protection.md)」をご覧ください。

- Azure Information Protection と AD RMS の比較については、「[Azure Information Protection と AD RMS の比較](./compare-on-premise.md)」をご覧ください。

## <a name="recommended-reading-before-you-migrate-to-azure-information-protection"></a>Azure Information Protection に移行する前に推奨されるドキュメント

以下のドキュメントは必須ではありませんが、移行を開始する前に読んでおくと役に立つ場合があります。 このナレッジによって、お客様の移行手順と関係のあるテクノロジが、どのような仕組みで動作するかを、より詳しく理解できます。

- [Azure Information Protection テナント キーを計画して実装する](./plan-implement-tenant-key.md): クラウドで SLC キーと同等のキーを Microsoft が管理するか (既定)、ユーザーが管理するか ("Bring Your Own Key" (BYOK) 構成) という、Azure Information Protection テナントで利用できるキー管理オプションについて説明しています。 

- [Rms サービスの検出](./rms-client/client-deployment-notes.md#rms-service-discovery): rms クライアントのデプロイに関するメモのこのセクションでは、サービス検出の順序が **レジストリ**、 **サービス接続ポイント (SCP)**、 **クラウド** の順に説明されています。 SCP がインストールされている環境の移行プロセスでは、SCP から返される AD RMS クラスターを使用しないように、レジストリ設定で Azure Information Protection テナントのクライアントを構成します。

- [Microsoft Rights Management コネクタの概要](./deploy-rms-connector.md#overview-of-the-microsoft-rights-management-connector): RMS コネクタに関するドキュメントのこのセクションでは、オンプレミス サービスから Azure Rights Management サービスに接続してドキュメントと電子メールを保護する方法について説明しています。

また、AD RMS の動作に慣れていない場合は、Azure RMS のしくみを確認すると役立つことがあり [ます。内部で](./how-does-it-work.md) は、クラウドのバージョンと同じまたは異なるテクノロジプロセスを特定するのに役立ちます。

## <a name="prerequisites-for-migrating-ad-rms-to-azure-information-protection"></a>AD RMS から Azure Information Protection への移行の前提条件

Azure Information Protection への移行を始める前に、次の前提条件が満たされていること、および制限事項を理解していることを確認してください。

- **サポートされている RMS 展開**:
    
  - AD RMS の次のリリースでは、Azure Information Protection への移行をサポートします。
           
      - Windows Server 2012 (x64)
        
      - Windows Server 2012 R2 (x64)
        
      - Windows Server 2016 (x64)
        
  - すべての有効な AD RMS トポロジがサポートされます。
    
      - 単一フォレスト、単一 RMS クラスター
        
      - 単一フォレスト、複数のライセンス専用 RMS クラスター
        
      - 複数フォレスト、複数 RMS クラスター
        
    注: 既定では、複数の AD RMS クラスターが Azure Information Protection の 1 つのテナントに移行します。 個別の Azure Information Protection テナントが必要な場合は、それぞれ異なる移行として処理する必要があります。 1 つの RMS クラスターからのキーを、複数のテナントにインポートすることはできません。

- **Azure Information Protection のサブスクリプション (Azure Rights Management サービスはアクティブ化されていません) を含む Azure Information Protection を実行するためのすべての要件** は次のとおりです。

    「[Azure Information Protection の要件](./requirements.md)」をご覧ください。

    Office 2010 を実行しているコンピューターがある場合は、 [Azure Information Protection クライアント](rms-client/use-client.md) をインストールして、クラウドサービスに対してユーザーを認証する機能を提供する必要があることに注意してください。 

    新しいバージョンの Office では、これらのクライアントは分類とラベル付けに必要であり、Azure Information Protection クライアントは省略可能ですが、データの保護のみを行う場合に推奨されます。 詳細については、 [Azure Information Protection 統合ラベル付けクライアント](./rms-client/clientv2-admin-guide.md)の管理者ガイドを参照してください。

    AD RMS からの移行を行うには、その前に Azure Information Protection のサブスクリプションを用意しておく必要がありますが、移行を始める前にテナントの Rights Management サービスをアクティブにしないことをお勧めします。 このアクティブ化手順は、AD RMS からキーとテンプレートをエクスポートし、それらを Azure Information Protection のテナントにインポートした後で、移行プロセスによって行われます。 ただし、Azure Information Protection が既にアクティブ化されている場合でも、いくつかの追加手順を行って AD RMS から移行することはできます。


- **Azure Information Protection の準備**:

  - オンプレミス ディレクトリと Azure Active Directory の間でのディレクトリ同期

  - Azure Active Directory でのメールが有効なグループ

    「[Azure Information Protection 向けのユーザーとグループの準備](prepare.md)」をご覧ください。

- **AD RMS で Exchange Server** (たとえば、トランスポート ルールと Outlook Web Access) または SharePoint Server の Information Rights Management (IRM) 機能を使用していた場合:

  - 短時間これらのサーバーで IRM が利用できなくなることを予定しておきます。
 
    移行後もこれらのサーバーで IRM を引き続き使用できます。 ただし、移行手順には、IRM サービスの一時的な無効化、コネクタのインストールと構成、サーバーの再構成、IRM の再有効化が含まれます。

    移行プロセス中にサービスが中断するのはこのときだけです。

- **HSM で保護されたキーを使用して自分で Azure Information Protection テナント キーを管理する場合**:

    - このオプション構成では、Azure Key Vault と、HSM で保護されたキーを保持する Key Vault をサポートする Azure サブスクリプションが必要です。 詳細については、 [Azure Key Vault の価格](https://azure.microsoft.com/pricing/details/key-vault/)に関するページを参照してください。 


### <a name="cryptographic-mode-considerations"></a>暗号化モードに関する注意事項

AD RMS クラスターが現在暗号化モード 1 の場合は、移行を開始する前にクラスターを 暗号化モード 2 にアップグレードしないでください。 代わりに暗号化モード 1 を使用して移行し、移行後タスクの 1 つとして移行の終了時にテナント キーを更新できます。

Windows Server 2012 R2 および Windows 2012 の AD RMS 暗号化モードを確認するには **AD RMS クラスター** のプロパティ > **全般** ] タブを使用します。 

### <a name="migration-limitations"></a>移行の上限

- Azure Information Protection によって使用されている Rights Management サービスによってサポートされていないソフトウェアやクライアントは、Azure Rights Management によって保護されているコンテンツを保護または使用できません。 「 [Azure Information Protection の要件](./requirements.md)」の「サポートされているアプリケーションとクライアント」セクションを必ず確認してください。

- AD RMS デプロイが外部のパートナーと (たとえば、信頼されたユーザー ドメインやフェデレーションを使用して) コラボレーションするように構成されている場合は、同時にまたは可能な限り速やかにパートナーも Azure Information Protection に移行する必要があります。 移行前に Azure Information Protection を使用して保護されていたコンテンツに引き続きアクセスするには、外部パートナーも同じようにこのドキュメントで説明されているクライアント構成の変更を行う必要があります。
    
    パートナーの構成は異なる可能性があるので、このドキュメントで再構成を正確に説明することはできません。 ただし、次のセクションの計画ガイドラインを参照し、詳細を [Microsoft サポートにお問い合わせ](./information-support.md#support-options-and-community-resources)ください。

## <a name="migration-planning-if-you-collaborate-with-external-partners"></a>外部のパートナーとコラボレーションしている場合の移行計画

AD RMS パートナーも Azure Information Protection に移行する必要があるため、移行の計画フェーズにパートナーを含めます。 後述する移行手順を実行する前に、次の要件が満たされていることを確認します。

- パートナーが、Azure Rights Management サービスをサポートする Azure Active Directory テナントを持っていること。  
    
    たとえば、Office 365 E3 または E5 サブスクリプション、Enterprise Mobility + Security サブスクリプション、Azure Information Protection のスタンドアロン サブスクリプションなどが必要です。

- パートナーの Azure Rights Management サービスはまだアクティブ化されていないが、Azure Rights Management サービスの URL はわかっていること。

    この情報を取得するには、Azure Rights Management ツールをインストールし、サービス ([接続-AipService](/powershell/module/aipservice/connect-aipservice)) に接続して、azure Rights Management サービス ([AipServiceConfiguration](/powershell/module/aipservice/get-aipserviceconfiguration)) のテナント情報を表示します。

- パートナーの AD RMS で保護されたコンテンツへの要求をパートナーのテナントの Azure Rights Management サービスにリダイレクトするよう、移行後のクライアントを構成できるように、パートナーの AD RMS クラスターの URL と Azure Rights Management サーバーの URL をパートナーから提供されていること。 クライアントのリダイレクトを構成する手順については、手順 7 で説明します。

- こちら側のユーザーの移行を始める前に、パートナーが AD RMS クラスターのルート キー (SLC) をテナントにインポートしていること。 同様に、パートナーが自分たちのユーザーの移行を始める前に、こちら側の AD RMS クラスターのルート キーをインポートしておく必要があります。 キーをインポートする手順については、移行プロセスの [手順4を参照してください。構成データを AD RMS からエクスポートし、Azure Information Protection にインポート](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection)します。 

## <a name="overview-of-the-steps-for-migrating-ad-rms-to-azure-information-protection"></a>AD RMS から Azure Information Protection への移行手順の概要

移行手順は 5 つのフェーズに分けることができ、異なるタイミングで、異なる管理者によって実行できます。

### <a name="phase-1-migration-preparation"></a>フェーズ 1: 移行の準備

詳細については、「 [**フェーズ 1: 移行の準備**](migrate-from-ad-rms-phase1.md)」を参照してください。

**手順 1: AIPService PowerShell モジュールをインストールし、テナントの URL を指定する**

移行プロセスでは、AIPService モジュールから1つまたは複数の PowerShell コマンドレットを実行する必要があります。 多くの移行手順を完了するには、テナントの Azure Rights Management サービス URL が必要です。この値は、PowerShell を使って特定することができます。

**手順 2.クライアントの移行の準備**

すべてのクライアントを一度に移行できず、少しずつ移行する場合は、オンボーディング制御を使い、移行前スクリプトをデプロイします。 ただし、段階的な移行ではなく同時にすべてを移行する場合は、この手順をスキップできます。

**手順 3: Exchange の展開を移行用に準備する**

この手順は、現在 Exchange Online またはオンプレミスの Exchange の IRM 機能を使ってメールを保護している場合に必要です。 ただし、段階的な移行ではなく同時にすべてを移行する場合は、この手順をスキップできます。

### <a name="phase-2-server-side-configuration-for-ad-rms"></a>フェーズ 2: AD RMS のサーバー側の構成

詳細については、「 [**フェーズ 2: AD RMS のサーバー側の構成**](migrate-from-ad-rms-phase2.md)」を参照してください。

**手順 4.構成データを AD RMS からエクスポートして Azure Information Protection にインポートする**

構成データ (キー、テンプレート、Url) を AD RMS から XML ファイルにエクスポートし、Import-AipServiceTpd PowerShell コマンドレットを使用して Azure Information Protection から Azure Rights Management サービスにそのファイルをアップロードします。 次に、Azure Rights Management サービスのテナント キーとして使用するインポート済みのサーバー ライセンサー証明書 (SLC) キーを指定します。 AD RMS のキー構成によっては、追加の手順が必要になる可能性があります。

- **ソフトウェアで保護されているキーからソフトウェアで保護されているキーへの移行**:

    AD RMS の一元管理されたパスワード ベースのキーを、マイクロソフトが管理する Azure Information Protection テナント キーに移行します。 これは、最も簡単な移行パスであり、追加の手順は必要ありません。

- **HSM で保護されているキーから HSM で保護されているキーへの移行**:

    AD RMS 用の HSM により保存されているキーを、顧客管理の Azure Information Protection テナント キーに移行します ("Bring Your Own Key" つまり BYOK シナリオ)。 これには、オンプレミスの nCipher HSM から Azure Key Vault にキーを転送し、このキーを使用するように Azure Rights Management サービスを承認するための追加の手順が必要です。 HSM で保護されている既存のキーは、モジュールで保護する必要があります。OCS で保護されているキーは、Rights Management サービスでサポートされていません。

- **ソフトウェアで保護されているキーから HSM で保護されているキーへの移行**:

    AD RMS の一元管理されたパスワード ベースのキーを、顧客が管理する Azure Information Protection テナント キーに移行します (“bring your own key” つまり BYOK シナリオ)。 最初にソフトウェアキーを抽出し、オンプレミスの HSM にインポートしてから、オンプレミスの nCipher HSM から Azure Key Vault HSM にキーを転送し、キーを格納する key Vault を使用するように Azure Rights Management サービスを承認する必要があるため、ほとんどの構成が必要です。

**手順 5.Azure Rights Management サービスをアクティブ化する**

可能であれば、インポート処理の前ではなく後に、この手順を実行します。 インポート前にこのサービスをアクティブした場合は、追加の手順が必要になります。

**手順 6.インポートされたテンプレートの構成**

権限ポリシー テンプレートをインポートするときに、それらの状態がアーカイブされます。 ユーザーが権限ポリシー テンプレートを表示および使用できるようにする場合は、Azure クラシック ポータルでテンプレートの状態を公開に変更する必要があります。


### <a name="phase-3-client-side-configuration"></a>フェーズ 3: クライアント側の構成

詳細については、「 [**フェーズ 3: クライアント側の構成**](migrate-from-ad-rms-phase3.md)」を参照してください。

**手順 7: Azure Information Protection を使用するように Windows コンピューターを再構成する**

既存の Windows コンピューターを、AD RMS ではなく Azure Rights Management サービスを使うように再構成する必要があります。 この手順は、自分の組織内のコンピューターに適用されるだけでなく、AD RMS を実行していた間に外部パートナーとコラボレーションしていた場合はパートナー組織のコンピューターにも適用されます。

### <a name="phase-4-supporting-services-configuration"></a>フェーズ 4: サポートサービスの構成

詳細については、「 [**フェーズ 4: サービス構成のサポート**](migrate-from-ad-rms-phase4.md)」を参照してください。

**手順 8: IRM と Exchange Online の統合を構成する**

この手順では、Exchange Online の AD RMS への移行を完了し、Azure Rights Management サービスを使うようにします。

**手順 9: Exchange サーバーおよび SharePoint サーバー用に IRM 統合を構成する**

この手順では、オンプレミスの Exchange または SharePoint の AD RMS への移行を完了し、Azure Rights Management サービスを使うようにします。これには、Rights Management コネクタをデプロイする必要があります。

### <a name="phase-5-post-migration-tasks"></a>フェーズ 5: 移行後のタスク

詳細については、「 [**フェーズ 5: 移行後のタスク**](migrate-from-ad-rms-phase5.md)」を参照してください。

**手順 10: AD RMS のプロビジョニング解除**

すべての Windows コンピューターが Azure Rights Management サービスを使っていて、AD RMS サーバーにアクセスしていないことを確認した後は、AD RMS デプロイをプロビジョニング解除できます。

**手順 11: クライアントの移行タスクを完了する**

iOS 搭載の携帯電話や iPad、Android 携帯電話とタブレット、Windows 携帯電話とタブレット、Mac コンピューターなどのモバイル デバイスをサポートする[モバイル デバイス拡張機能](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn673574(v=ws.11))をデプロイしてある場合は、これらのクライアントが AD RMS を使うようにリダイレクトした SRV レコードを DNS から削除する必要があります。 
    
準備フェーズ中に構成したオンボーディング制御はもう必要ありません。 ただし、段階的な移行ではなく、同時にすべてを移行することを選んだためにオンボーディング制御を使用しなかった場合は、この手順をスキップしてオンボーディング制御を削除することができます。
    
Windows コンピューターで Office 2010 を実行している場合は、"**AD RMS Rights Policy Template Management (Automated) (AD RMS 権利ポリシー テンプレート管理 (自動))**" タスクを無効にする必要があるかどうかを確認します。

**手順 12: Azure Information Protection テナントキーのキーを更新する**

移行前に暗号化モード 2 で実行されていない場合は、この手順の使用をお勧めします。

## <a name="next-steps"></a>次のステップ
移行を始めるには、「[フェーズ 1 - 準備](migrate-from-ad-rms-phase1.md)」に進んでください。