---
title: Azure Information Protection の HYOK 保護
description: Azure Information Protection による HYOK (AD RMS) 保護の概要、サポートされるシナリオ、制限事項、前提条件、推奨事項。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7667b5b0-c2e9-4fcf-970f-05577ba51126
ms.openlocfilehash: 6ba22afad4ef9e1e8fc5da98efdff965dd6b3dfa
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60182145"
---
# <a name="hold-your-own-key-hyok-protection-for-azure-information-protection"></a>Azure Information Protection の Hold your own key (HYOK) 保護

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> "*手順:[Windows 用 Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*"

次の情報を使用して、Azure Information Protection の Hold your own key (HYOK) 保護とは何か、およびクラウド ベースの既定の保護と異なる点について把握してください。 HYOK 保護を使用する前に、適切な場合、サポートされるシナリオ、制限事項、要件を理解していることを確認してください。 

## <a name="cloud-based-protection-vs-hyok"></a>クラウド ベースの保護とHYOK

Azure Information Protection を使用して最も機密性の高いドキュメントや電子メールを保護する場合、通常、次のような利点がある Azure Rights Management (Azure RMS) 保護を使用するクラウドベースのキーを適用します。

- サーバー インフラストラクチャが不要で、問題の解決が迅速になり、オンプレミス ソリューションよりもデプロイと保守のコスト効率が高くなる。

- クラウドベースの認証を使用して、他の組織のパートナーやユーザーと簡単に共有することができる。

- 検索、Web ビューアー、ピボット ビュー、マルウェア対策、電子情報開示、Delve などの、他の Azure や Office 365 サービスと密接に統合されている。

- 共有した機密ドキュメントの追跡、取り消し、電子メール通知機能を使用できる。

クラウドベースのキーは、Microsoft または自社 ("Bring Your Own Key" (BYOK) シナリオ) が管理する組織の秘密キーを使用して組織のドキュメントと電子メールを保護します。 テナント キー オプションの詳細については、「[Azure Information Protection テナント キーを計画して実装する](plan-implement-tenant-key.md)」を参照してください。

保護するドキュメントと電子メールは、クラウドまたはオンプレミスに格納することができます。 このクラウドベースのキーの保護プロセスのしくみについては、「[Azure Rights Management とは](what-is-azure-rms.md )」を参照してください。

重要なビジネス機能 (検索、インデックス、アーカイブ、マルウェア対策サービスなど) が、Azure Information Protection で保護されているコンテンツに対してシームレスに動作し続けられるように、Office 365 サービスと、ご利用のテナントのクラウド ベースのアプリケーションを Azure Information Protection に統合することができます。 これらのシナリオの暗号化されたコンテンツを読み取るこの機能は、“データに対する推論” と呼ばれることがあります。 たとえば、この機能により、Exchange Online はマルウェア スキャンのために電子メールの暗号化を解除したり、暗号化された電子メールにデータ損失防止 (DLP) ルールを実行したりすることができます。

ただし、規制の要件に関して、一部の組織ではクラウドから分離されたキーを使用したコンテンツの暗号化が必要な場合があります。 この分離は、暗号化されたコンテンツが、オンプレミスのアプリケーションとオンプレミス サービスでのみ読み取ることができることを意味します。 このキー管理オプションは、Azure Information Protection によってサポートされ、"hold your own key" または HYOK と呼ばれます。 Azure Information Protection と HYOK を使用すると、テナントがクラウド ベースのキーと、オンプレミスのキーの両方を持つことになります。

## <a name="hyok-guidance-and-best-practices"></a>HYOK のガイダンスとベスト プラクティス

HYOK 保護は、暗号化キーをクラウドから分離する必要があるドキュメントと電子メールだけに使用します。 HYOK 保護には、クラウドベースのキー保護の場合ほど多くの利点はなく、"データの不透明度" が失われることが多々あります。 これは、オンプレミスのアプリケーションとサービスのみが、HYOK で保護されたデータを開くことできることを意味します。クラウド ベースのサービスとアプリケーションは、HYOK で保護されたデータに対して推論することはできません。

HYOK 保護を使用している組織であっても、通常は、保護する必要があるドキュメントの数が少ない場合に適しています。 ガイダンスとして、次のすべての条件に一致するドキュメントのみに使用します。

- コンテンツは組織内で最上位に分類され ("最高機密")、アクセスは数名だけに制限されている

- コンテンツが組織外で共有されることはない

- コンテンツは、内部ネットワーク上でのみ使用される

HYOK 保護は、ラベルに対する管理者の構成オプションであるため、クラウド ベースのキーまたは HYOK を保護に使用しているかどうかにかかわらず、ユーザーのワークフローは変わりません。

[スコープ ポリシー](configure-policy-scope.md)は、HYOK 保護を適用する必要があるユーザーのみに HYOK 保護で構成されているラベルを確実に表示する優れた方法です。 

## <a name="supported-scenarios-for-hyok"></a>HYOK のサポートされるシナリオ

HYOK 保護を適用するには、Azure Information Protection のラベルを使用します。 

HYOK 向けに構成されているラベルを使用して、HYOK によって保護されているコンテンツを開き (消費し) コンテンツを保護するための、サポートされているシナリオを次の表に示します。

|プラットフォーム|アプリケーション|Supported|
|----------------------|----------|-----------|
|Windows|Azure Information Protection クライアントと Office 365 アプリ、Office 2019、Office 2016、および Office 2013 <br /><br />- Word、Excel、PowerPoint|保護:はい<br /><br />消費: はい|
|Windows|Azure Information Protection クライアントと Office 365 アプリ、Office 2019、Office 2016、および Office 2013 <br /><br />- Outlook|保護:はい<br /><br />消費: はい|
|Windows|Azure Information Protection クライアントとファイル エクスプローラー|保護:はい <br /><br />消費: はい|
|Windows|Azure Information Protection ビューアー|保護:適用なし<br /><br />消費: はい|
|Windows|Azure Information Protection クライアントと PowerShell のラベル付けコマンドレット|保護:はい<br /><br />消費: はい|
|Windows|Azure Information Protection スキャナー|保護:はい<br /><br />消費: はい|
|Windows|Rights Management 共有アプリ|保護:いいえ<br /><br />消費: はい|
|MacOS|Office for Mac <br /><br /> - Word、Excel、PowerPoint|保護:いいえ<br /><br />消費: はい|
|MacOS|Office for Mac<br /><br />- Outlook|保護:いいえ<br /><br />消費: はい|
|MacOS|Rights Management 共有アプリ|保護:いいえ<br /><br />消費: はい|
|iOS|Office Mobile <br /><br />- Word、Excel、PowerPoint|保護:いいえ<br /><br />消費: はい|
|iOS|Office Mobile <br /><br />-Outlook|保護:いいえ<br /><br />消費: いいえ|
|iOS|Azure Information Protection ビューアー|保護:適用なし<br /><br />消費: はい|
|Android|Office Mobile <br /><br />- Word、Excel、PowerPoint|保護:いいえ<br /><br />消費: はい|
|Android|Office Mobile <br /><br />- Outlook|保護:いいえ<br /><br />消費: いいえ|
|Android|Azure Information Protection ビューアー|保護:適用なし<br /><br />消費: はい|
|Web|Outlook on the web|保護:いいえ<br /><br />消費: いいえ|
|Web|Office Online<br /><br />- Word、Excel、PowerPoint|保護:いいえ<br /><br />消費: いいえ|
|ユニバーサル|Office のユニバーサル アプリ<br /><br />- Word、Excel、PowerPoint|保護:いいえ<br /><br />消費: いいえ|


## <a name="additional-limitations-when-using-hyok"></a>HYOK を使用する際の追加制限事項

さらに、HYOK 保護と Azure Information Protection ラベルを使用する場合、次の制限があります。

- Office 2013 より前のバージョンの Office をサポートしません。

- Office 365 サービスと他のオンライン サービスは、HYOK で保護されたドキュメントと電子メールの暗号化を解除して内容を調べたり操作を実行することはできません。 この制限は、Rights Management コネクタで保護されている HYOK で保護されたドキュメントおよび電子メールにも適用されます。 
    
    この HYOK で保護された電子メールで失われる機能には、マルウェア スキャナー、データ損失防止 (DLP) ソリューション、メール ルーティング規則、ジャーナル、電子情報開示、アーカイブ ソリューション、Exchange ActiveSync が含まれます。 さらに、ユーザーは、一部のデバイスで自分の HYOK で保護された電子メールが開けない理由がわからないため、ヘルプ デスクに問い合わせる可能性があります。 こうした多くの制限のため、電子メールに HYOK 保護を使用することはお勧めしません。

## <a name="implementing-hyok"></a>HYOK を実装する

HYOK は、有効な Active Directory Rights Management サービス (AD RMS) デプロイがある場合に Azure Information Protection でサポートされます。次のセクションでは、その要件について説明します。 このシナリオでは、使用権限ポリシーとそのポリシーを保護する組織の秘密キーの管理と保存はオンプレミスで行われますが、ラベル付けと分類の Azure Information Protection ポリシーの管理と保存は Azure で行われます。 

HYOK と Azure Information Protection を、AD RMS と Azure Information Protection の完全なデプロイの使用と混同しないでください。また、AD RMS から Azure Information Protection への移行の代替手段として使用しないでください。 HYOK はラベルを適用することでのみサポートされます。HYOK は、AD RMS に機能パリティを提供していませんし、すべての AD RMS デプロイの構成をサポートしているわけではありません。

- コンテンツの保護および保護されたコンテンツの使用について HYOK がサポートするシナリオに関する詳細は、「[HYOK のサポートされるシナリオ](#supported-scenarios-for-hyok)」セクションを参照してください。

- AD RMS からの移行の手順については、「[AD RMS から Azure Information Protection への移行](migrate-from-ad-rms-to-azure-rms.md)」を参照してください。

- AD RMS のデプロイ要件の詳細については、次のセクションをご覧ください。

### <a name="requirements-for-ad-rms-to-support-hyok"></a>HYOK をサポートするための AD RMS の要件

Azure Information Protection ラベルに HYOK 保護を適用するには、AD RMS のデプロイで次の要件を満たす必要があります。

- AD RMS の構成:
    
  - Windows Server 2012 R2 の最小バージョン: 運用環境では必須ですが、テストまたは評価を目的とする場合は、Windows Server 2008 R2 Service Pack 1 の最小バージョンを使用できます。
    
  - 次のいずれかのトポロジ:
        
    - AD RMS ルート クラスターを 1 つ持つ単一のフォレスト。 
        
    - それぞれが独立した AD RMS ルート クラスターを持つ複数のフォレスト。ユーザーは他のフォレスト内のユーザーによって保護されているコンテンツにアクセスすることはできません。
        
    - それぞれが AD RMS クラスターを持つ複数のフォレスト。 各 AD RMS クラスターは、同じ AD RMS クラスターを指すライセンス URL を共有します。 この AD RMS クラスターには、その他のすべての AD RMS クラスターからすべての信頼されたユーザー ドメイン (TUD) の証明書をインポートする必要があります。 このトポロジについて詳しくは、「[Trusted User Domain (信頼されたユーザー ドメイン)](https://technet.microsoft.com/library/dd983944(v=ws.10).aspx)」をご覧ください。
        
    個々のフォレスト内に複数の AD RMS クラスターがある場合は、HYOK (AD RMS) 保護を適用するグローバル ポリシー内のラベルを削除し、クラスターごとに [スコープ付きポリシー](configure-policy-scope.md) を構成します。 次に、各クラスターのユーザーを、対応するスコープ付きポリシーに割り当てて、ユーザーが複数のスコープ付きポリシーに割り当てられていることになるグループを使用しないようにします。 結果として、各ユーザーは 1 つの AD RMS クラスターのみのラベルを持つことになります。 
    
  - [暗号化モード 2](https://technet.microsoft.com/library/hh867439.aspx): AD RMS クラスター プロパティの **[全般]** タブから、モードを確認できます。
    
  - 各 AD RMS サーバーが証明書の URL 用に構成されます。 [手順](#configuring-ad-rms-servers-to-locate-the-certification-url) 
    
  - サービス接続ポイント (SCP) が Active Directory に登録されていません。SCP は Azure Information Protection で AD RMS 保護を使用する場合には使用されません。 
    
      - AD RMS デプロイに SCP を登録している場合、Azure Rights Management 保護の[サービス検索](./rms-client/client-deployment-notes.md#rms-service-discovery)を正常に実行するには、SCP を削除する必要があります。 
        
      - HYOK の新しい AD RMS クラスターをインストールする場合は、最初のノードの構成時に SCP を登録する手順をスキップしてください。 各追加ノードについて、AD RMS の役割を追加して、既存のクラスターに参加する前に、証明書の URL についてサーバーが構成されていることを確認します。
    
  - AD RMS サーバーは接続先のクライアントによって信頼されている有効な x.509 証明書が含まれる SSL/TLS を使用するために構成されます。運用環境では必要ですが、テストまたは評価目的では必要ありません。
    
  - 構成済みの権利テンプレート。
    
  - Exchange IRM 用に構成されていない。
    
  - モバイル デバイスと Mac コンピューターの場合: [Active Directory Rights Management サービス モバイル デバイス拡張機能](https://technet.microsoft.com/library/dn673574.aspx) がインストールされ構成されている。

- オンプレミスの Active Directory と Azure Active Directory 間にディレクトリ同期が構成され、HYOK 保護を使用するユーザーのシングル サインオンが構成されている。

- HYOK で保護されているドキュメントや電子メールを組織外のユーザーと共有する場合: AD RMS は、信頼されたユーザー ドメイン (TUD) または Active Directory フェデレーション サービス (AD FS) を使用して作成したフェデレーションによる信頼関係を使用して、他の組織との直接のポイントツーポイントの関係で明示的に定義された信頼関係に対して構成されます。

- ユーザーは、Information Rights Management (IRM) をサポートしている Office のバージョンと、Windows 7 Service Pack 1 以降で実行されている Office 2013 Professional Plus Service Pack 1 以降を持っている。 ただし、このシナリオでは、Office 2010 と Office 2007 は、サポートされません。
    
    - Office 2016 の Microsoft インストーラー (.msi) ベースのエディションの場合: [2018 年 3 月 6 日にリリースされた Microsoft Office 2016 の更新プログラム 4018295](https://support.microsoft.com/en-us/help/4018295/march-6-2018-update-for-office-2016-kb4018295) をインストールしておきます。

> [!IMPORTANT]
> HYOK 保護が提供する高い確実性を実現するために、AD RMS サーバーは DMZ に配置せず、マネージド デバイスでのみ使用することをお勧めします。 
> 
> また、AD RMS クラスターでハードウェア セキュリティ モジュール (HSM) を使用することをお勧めします。これを使用すれば、AD RMS のデプロイが侵入または侵害されても、サーバー ライセンサー証明書 (SLC) の秘密キーが公開または盗難されることはありません。 

AD RMS のデプロイの情報と手順については、Windows Server ライブラリの「[Active Directory Rights Management Services の概要](https://technet.microsoft.com/library/hh831364.aspx)」を参照してください。 


### <a name="configuring-ad-rms-servers-to-locate-the-certification-url"></a>証明書の URL を確認するように AD RMS サーバーを構成する

1. クラスターの各 AD RMS サーバーで、次のレジストリ エントリを作成します。

    `Computer\HKEY_LOCAL_MACHINE\Software\Microsoft\DRMS\GICURL = "<string>"`
    
    \<文字列値> の場合、次のいずれかを指定します。
    
    - SSL/TLS を使用した AD RMS クラスターの場合:

            https://<cluster_name>/_wmcs/certification/certification.asmx
    
    - SSL/TLS を使用しない AD RMS クラスターの場合 (テスト ネットワークのみ):
        
            http://<cluster_name>/_wmcs/certification/certification.asmx

2. IIS を再起動します。

### <a name="locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label"></a>Azure Information Protection ラベルによる AD RMS の保護を指定する情報の確認

**HYOK (AD RMS)** の保護のラベルを構成する場合、AD RMS クラスターのライセンス URL を指定する必要があります。 さらに、ユーザーを許可するためにアクセス許可に構成したテンプレートを指定するか、またはユーザーがアクセス許可とユーザーを定義できるようにする必要があります。 

テンプレート GUID とライセンス URL の値は、Active Directory Rights Management サービス コンソールで確認できます。

- テンプレート GUID を確認するには: クラスターを展開し、**[権利ポリシー テンプレート]** をクリックします。 **[配布権利ポリシー テンプレート]** の情報から、使用するテンプレートの GUID をコピーできます。 以下に例を示します。82bf3474-6efe-4fa1-8827-d1bd93339119

- ライセンス URL を確認するには: クラスター名を指定します。 **[クラスターの詳細]** の情報から、**[ライセンス]** 値の **/_wmcs/licensing** 文字列以外をコピーします。 たとえば次のようになります。 https://rmscluster.contoso.com 
    
    エクストラネットのライセンスの値とイントラネットのライセンス値がある場合、それらは次のように異なります。エクストラネットの値は、保護されたドキュメントまたは電子メールを、明示的なポイントツーポイントの信頼関係によって定義されたパートナーと共有する場合にのみ指定してください。 それ以外の場合、イントラネット値を使用し、Azure Information Protection 接続で AD RMS の保護を使用するすべてのクライアント コンピューターが、イントラネット接続を使用して接続するようにします (たとえば、リモート コンピューターは VPN 接続を使用する)。


## <a name="next-steps"></a>次の手順

HYOK 保護のラベルを構成するには、「[Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)」を参照してください。 
