---
title: Azure Information Protection に対して独自のキー (HYOK) 保護を保持する
description: Azure Information Protection による HYOK (AD RMS) 保護の概要、サポートされるシナリオ、制限事項、前提条件、推奨事項。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/14/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 7667b5b0-c2e9-4fcf-970f-05577ba51126
ms.subservice: hyok
ms.custom: admin
ms.openlocfilehash: cfd88d6356655e4f3ebe969935175302424a7a57
ms.sourcegitcommit: 6d10435c67434bdbbdd51b4a3535d0efaf8307da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86868830"
---
# <a name="hold-your-own-key-hyok-details-for-azure-information-protection"></a>Azure Information Protection の独自のキー (HYOK) の詳細を保持する

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順: [Azure Information Protection classic client For Windows](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と**ラベル管理**は、**2021 年 3 月 31 日**で**非推奨**になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

独自のキー (HYOK) 構成を保持することで、従来のクライアントを使用する AIP のお客様は、キーのフルコントロールを維持しながら、機密性の高いコンテンツを保護することができます。 HYOK は、機密性の高いコンテンツに対してオンプレミスに格納されている追加の顧客保持キー、および他のコンテンツに使用される既定のクラウドベースの保護を使用します。 

既定のクラウドベースのテナントルートキーの詳細については、「 [Azure Information Protection テナントキーの計画と実装](plan-implement-tenant-key.md)」を参照してください。

## <a name="cloud-based-protection-vs-hyok"></a>クラウドベースの保護と HYOK

通常、Azure Information Protection を使用して機密性の高いドキュメントや電子メールを保護するには、 [BYOK 構成を使用して、](byok-price-restrictions.md)Microsoft または顧客が[生成](plan-implement-tenant-key.md#tenant-root-keys-generated-by-microsoft)したクラウドベースのキーを使用します。 

クラウドベースのキーは Azure Key Vault で管理されます。これにより、次の利点が得られます。

- **サーバーインフラストラクチャの要件はありません。** クラウドソリューションは、オンプレミスソリューションよりも迅速かつコスト効率の高い方法でデプロイおよび保守できます。

- **クラウドベースの認証**を使用すると、他の組織のパートナーやユーザーと簡単に共有できます。 

- 検索、web ビューアー、ピボットビュー、マルウェア対策、電子情報開示、Delve など、**他の Azure や Office 365 サービスとの緊密な統合**。

- 共有している機密性の高いドキュメントの**ドキュメント追跡**、**失効**、**電子メール通知**。

ただし、組織によっては、クラウドから分離されたキーを使用して特定のコンテンツを暗号化する必要がある規制要件がある場合があります。 この分離により、暗号化されたコンテンツは、オンプレミスのアプリケーションとオンプレミスのサービスでのみ読み取ることができます。

HYOK の構成では、顧客のテナントはクラウドに格納できるコンテンツと共に使用する[クラウドベースのキー](plan-implement-tenant-key.md)と、オンプレミスのみで保護する必要があるコンテンツのオンプレミスのキーの両方を持ちます。

## <a name="hyok-guidance-and-best-practices"></a>HYOK のガイダンスとベスト プラクティス

HYOK を構成する場合は、次の推奨事項を考慮してください。

- [HYOK に適したコンテンツ](#content-suitable-for-hyok)
- [HYOK で構成されたラベルを表示できるユーザーを定義します](#define-the-users-who-can-see-hyok-configured-labels)
- [HYOK と電子メールサポート](#hyok-and-email-support)

> [!IMPORTANT]
> Azure Information Protection の HYOK 構成は、完全 AD RMS と Azure Information Protection の展開に代わるものではなく、AD RMS を[Azure Information Protection に移行](migrate-from-ad-rms-to-azure-rms.md)するための代替手段でもありません。 
>
> HYOK は、ラベルを適用することによってのみサポートされ、AD RMS との機能の同等の機能を提供しません。また、すべての AD RMS デプロイ構成をサポートしていません。

### <a name="content-suitable-for-hyok"></a>HYOK に適したコンテンツ

HYOK protection はクラウドベースの保護の利点を提供しないため、多くの場合、コンテンツはオンプレミスのアプリケーションやサービスによってのみアクセス可能であるため、"データの不透明度" の方がコストがかかります。 HYOK 保護を使用している組織であっても、通常は少数のドキュメントにのみ適しています。 

HYOK は、次の条件に一致するコンテンツに対してのみ使用することをお勧めします。

- 組織内で最高の分類を持つコンテンツ ("最高機密")。アクセスはごく少数のユーザーに制限されます。
- 組織外で共有されていないコンテンツ
- 内部ネットワークでのみ使用されるコンテンツ。

### <a name="define-the-users-who-can-see-hyok-configured-labels"></a>HYOK で構成されたラベルを表示できるユーザーを定義します

HYOK protection を適用する必要があるユーザーのみが HYOK に構成されたラベルを確認するには、[スコープ付きポリシー](configure-policy-scope.md)を使用してそれらのユーザーのポリシーを構成します。

### <a name="hyok-and-email-support"></a>HYOK と電子メールサポート

Office 365 サービスおよびその他のオンラインサービスは、HYOK で保護されたコンテンツの暗号化を解除できません。

電子メールの場合、この機能が失われるのは、マルウェアスキャナー、データ損失防止 (DLP) ソリューション、メールルーティングルール、ジャーナル、電子情報開示、アーカイブソリューション、および Exchange ActiveSync です。

HYOK で保護された電子メールを開けないデバイスがある理由をユーザーが理解していない可能性があります。 これらの追加のヘルプ呼び出しを回避するには、電子メールの HYOK protection を構成しないでください。

## <a name="supported-applications-for-hyok"></a>HYOK でサポートされているアプリケーション

Azure Information Protection ラベルを使用して、特定のドキュメントや電子メールに HYOK を適用します。 HYOK は、Office バージョン2013以降でサポートされています。

HYOK はラベルの管理者構成オプションであり、コンテンツがクラウドベースのキーとして使用されているか、HYOK として使用されているかに関係なく、ワークフローは変わりません。

次の表は、HYOK で構成されたラベルを使用してコンテンツを保護および使用するためにサポートされるシナリオを示しています。

- [HYOK の Windows アプリケーションサポート](#windows-application-support-for-hyok)
- [macOS アプリケーションの HYOK のサポート](#macos-application-support-for-hyok)
- [HYOK の iOS アプリケーションのサポート](#ios-application-support-for-hyok)
- [HYOK 向けの Android アプリケーションのサポート](#android-application-support-for-hyok)
- [HYOK の Web アプリケーションのサポート](#web-application-support-for-hyok)
- [HYOK のユニバーサルアプリケーションサポート](#universal-application-support-for-hyok)


### <a name="windows-application-support-for-hyok"></a>HYOK の Windows アプリケーションサポート

|Application  |保護  |従量課金  |
|---------|---------|---------|
|Office 365 アプリ、Office 2019、Office 2016、および Office 2013 を使用する Azure Information Protection クライアント:</br>Word、Excel、PowerPoint、Outlook     | ![はい](media/yes-icon.png)        | ![○](media/yes-icon.png)        |
|Azure Information Protection クライアントとファイル エクスプローラー     | ![はい](media/yes-icon.png)        | ![○](media/yes-icon.png) |
|Azure Information Protection ビューアー     |   適用なし      |  ![はい](media/yes-icon.png)       |
|Azure Information Protection クライアントと PowerShell のラベル付けコマンドレット     | ![はい](media/yes-icon.png)        | ![○](media/yes-icon.png)        |
|Azure Information Protection スキャナー     |![はい](media/yes-icon.png)       |   ![○](media/yes-icon.png)      |
|Rights Management 共有アプリ     |  ![no](media/no-icon.png)    |  ![はい](media/yes-icon.png)       |

### <a name="macos-application-support-for-hyok"></a>macOS アプリケーションの HYOK のサポート

|Application|保護|従量課金|
|----------------------|----------|-----------|
|Mac 用 Office: </br>Word、Excel、PowerPoint、Outlook|![no](media/no-icon.png)|![はい](media/yes-icon.png)|
|Rights Management 共有アプリ|![no](media/no-icon.png)| ![はい](media/yes-icon.png)|

### <a name="ios-application-support-for-hyok"></a>HYOK の iOS アプリケーションのサポート

|Application|保護|従量課金|
|----------------------|----------|-----------|
|Office Mobile: </br>Word、Excel、PowerPoint|![no](media/no-icon.png)| ![はい](media/yes-icon.png)|
|Office Mobile: </br>Outlook のみ|![×](media/no-icon.png)|![no](media/no-icon.png)|
|Azure Information Protection ビューアー|適用なし|![はい](media/yes-icon.png)|

### <a name="android-application-support-for-hyok"></a>HYOK 向けの Android アプリケーションのサポート

|Application|保護|従量課金|
|----------------------|----------|-----------|
|Office Mobile: </br>Word、Excel、PowerPoint|![no](media/no-icon.png)| ![はい](media/yes-icon.png)|
|Office Mobile: </br>Outlook のみ|![×](media/no-icon.png)|![no](media/no-icon.png)|
|Azure Information Protection ビューアー|適用なし| ![はい](media/yes-icon.png)|

### <a name="web-application-support-for-hyok"></a>HYOK の Web アプリケーションのサポート

|Application|保護|従量課金|
|----------------------|----------|-----------|
|Outlook on the web|![×](media/no-icon.png)|![no](media/no-icon.png)|
|Web 用 Office: </br>Word、Excel、PowerPoint|![×](media/no-icon.png)|![no](media/no-icon.png)|

### <a name="universal-application-support-for-hyok"></a>HYOK のユニバーサルアプリケーションサポート

|Application|保護|従量課金|
|----------------------|----------|-----------|
|Office ユニバーサルアプリ: </br>Word、Excel、PowerPoint|![×](media/no-icon.png)|![no](media/no-icon.png)|

## <a name="implementing-hyok"></a>HYOK を実装する

[次に示す](#requirements-for-ad-rms-to-support-hyok)すべての要件に準拠する Active Directory Rights Management サービス (AD RMS) がある場合、AZURE INFORMATION PROTECTION は HYOK をサポートします。

使用権限ポリシーと、これらのポリシーを保護する組織の秘密キーはオンプレミスで管理および保存されますが、ラベル付けと分類の Azure Information Protection ポリシーは、Azure で管理および保存されたままになります。

HYOK 保護を実装するには:

1. [システムが AD RMS の要件を満たしていることを確認する](#requirements-for-ad-rms-to-support-hyok)
1. [保護する情報の検索](#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label)

準備ができたら、 [Rights Management 保護のラベルを構成する方法](configure-policy-protection.md)に進みます。

### <a name="requirements-for-ad-rms-to-support-hyok"></a>HYOK をサポートするための AD RMS の要件

Azure Information Protection ラベルの HYOK 保護を提供するには、AD RMS の展開が次の要件を満たしている必要があります。

|要件  |説明  |
|---------|---------|
|**AD RMS 構成**     |HYOK をサポートするには、AD RMS システムを特定の方法で構成する必要があります。 詳細については、[以下](#ad-rms-configuration-requirements)を参照してください。          |
|**ディレクトリ同期**     |オンプレミスの Active Directory と Azure Active Directory の間でディレクトリ同期を構成する必要があります。 </br></br>HYOK protection ラベルを使用するユーザーは、シングルサインオン用に構成する必要があります。         |
|**明示的に定義された信頼の構成**     |HYOK で保護されたコンテンツを組織外の他のユーザーと共有する場合は、他の組織との直接のポイントツーポイントの関係において、明示的に定義された信頼の AD RMS を構成する必要があります。 </br></br>これは、Active Directory フェデレーションサービス (AD FS) (AD FS) を使用して作成された信頼されたユーザードメイン (TUDs) またはフェデレーション信頼を使用して行います。         |
|**サポートされるバージョン Microsoft Office**     | HYOK で保護されたコンテンツを保護または使用するユーザーには、次のものが必要です。 </br></br>-Information Rights Management (IRM) をサポートする Office のバージョン </br>-Microsoft Office Professional Plus バージョン2013以降、Windows 7 Service Pack 1 以降で実行されている Service Pack 1。 </br>-Office 2016 Microsoft Installer (.msi) ベースのエディションの場合、 [2018 でリリースされた Microsoft Office 2016 の4018295更新プログラム](https://support.microsoft.com/help/4018295/march-6-2018-update-for-office-2016-kb4018295)が必要です。 </br></br>**注:** Office 2010 と Office 2007 はサポートされていません。        |

> [!IMPORTANT]
> HYOK protection によって提供される高い確実性を実現するために、次のことをお勧めします。
> - AD RMS サーバーを DMZ の外部に配置し、管理されたデバイスでのみ使用されるようにします。
>
> - ハードウェアセキュリティモジュール (HSM) を使用して AD RMS クラスターを構成します。 これにより、AD RMS の展開が侵害されたり侵害されたりした場合に、サーバーライセンサー証明書 (SLC) の秘密キーが公開または盗難されるのを防ぐことができます。

> [!TIP]
> AD RMS のデプロイの情報と手順については、Windows Server ライブラリの「[Active Directory Rights Management Services の概要](https://technet.microsoft.com/library/hh831364.aspx)」を参照してください。 

#### <a name="ad-rms-configuration-requirements"></a>AD RMS 構成要件

HYOK をサポートするには、AD RMS システムに次の構成があることを確認します。

|要件  |説明  |
|---------|---------|
|**Windows のバージョン**     |少なくとも、次のいずれかの Windows バージョン。 </br></br>**運用環境:** Windows Server 2012 R2</br>**テスト/評価環境**: Windows Server 2008 R2 Service Pack 1        |
|**トポロジ**     |HYOK には、次のいずれかのトポロジが必要です。 </br>-単一のフォレストと1つの AD RMS クラスター </br>-複数のフォレスト。それぞれに AD RMS クラスターがあります。 </br></br>**複数のフォレストのライセンス**</br> 複数のフォレストがある場合、各 AD RMS クラスターは、同じ AD RMS クラスターを指すライセンス URL を共有します。 </br>この AD RMS クラスターで、他のすべての AD RMS クラスターからすべての信頼されたユーザードメイン (TUD) 証明書をインポートします。 </br>このトポロジについて詳しくは、「[Trusted User Domain (信頼されたユーザー ドメイン)](https://technet.microsoft.com/library/dd983944(v=ws.10).aspx)」をご覧ください。 </br></br>**複数のフォレストのグローバルポリシーラベル**</br>個々のフォレスト内に複数の AD RMS クラスターがある場合は、HYOK (AD RMS) 保護を適用するグローバル ポリシー内のラベルを削除し、クラスターごとに [スコープ付きポリシー](configure-policy-scope.md) を構成します。 <br>各クラスターのユーザーをスコープ付きポリシーに割り当て、ユーザーが複数のスコープ付きポリシーに割り当てられるようなグループを使用しないようにします。</br>結果として、各ユーザーは 1 つの AD RMS クラスターのみのラベルを持つことになります。          |
|**暗号化モード**     | AD RMS は、[暗号化モード 2](https://technet.microsoft.com/library/hh867439.aspx)で構成する必要があります。 </br>AD RMS クラスターのプロパティの **[全般**] タブを確認して、モードを確認します。        |
|**証明書 URL の構成**     | 各 AD RMS サーバーは、証明書の URL 用に構成されている必要があります。 </br>詳細については、[以下](#configuring-ad-rms-servers-to-locate-the-certification-url)を参照してください。        |
|**サービス接続ポイント**     | Azure Information Protection で AD RMS 保護を使用する場合、サービス接続ポイント (SCP) は使用されません。 </br></br>**AD RMS デプロイ用に SCP が登録さ**れている場合は、それを削除して、Azure Rights Management 保護に対して[サービスの検出](./rms-client/client-deployment-notes.md#rms-service-discovery)が成功したことを確認します。 </br></br>**HYOK の新しい AD RMS クラスターをインストールする場合**は、最初のノードを構成するときに SCP を登録しないでください。 各追加ノードについて、AD RMS の役割を追加して、既存のクラスターに参加する前に、証明書の URL についてサーバーが構成されていることを確認します。         |
|**SSL/TLS**     |運用環境では、接続しているクライアントによって信頼されている有効な x.509 証明書で SSL/TLS を使用するように AD RMS サーバーを構成する必要があります。 </br></br>これは、テストまたは評価のためには必要ありません。         |
|**権限テンプレート**     |AD RMS に対して権限テンプレートを構成しておく必要があります。         |
|**Exchange IRM**    |AD RMS を Exchange IRM 用に構成することはできません。         |
|**モバイルデバイス/Mac コンピューター**     | [Active Directory Rights Management サービスモバイルデバイス拡張機能](https://technet.microsoft.com/library/dn673574.aspx)をインストールして構成しておく必要があります。        |


#### <a name="configuring-ad-rms-servers-to-locate-the-certification-url"></a>証明書の URL を確認するように AD RMS サーバーを構成する

1. クラスターの各 AD RMS サーバーで、次のレジストリ エントリを作成します。

    ```sh
    Computer\HKEY_LOCAL_MACHINE\Software\Microsoft\DRMS\GICURL = "<string>"`
    ```

    では、 \<string value> 次のいずれかの文字列を指定します。

    |環境  |文字列値  |
    |---------|---------|
    |**運用** </br>(SSL/TLS を使用したクラスターの AD RMS)     | `https://<cluster_name>/_wmcs/certification/certification.asmx`        |
    |**テスト/評価** </br>(SSL/TLS なし)     |`http://<cluster_name>/_wmcs/certification/certification.asmx`         |

2. IIS を再起動します。

### <a name="locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label"></a>Azure Information Protection ラベルによる AD RMS の保護を指定する情報の確認

HYOK の保護ラベルを構成するには、AD RMS クラスターのライセンス URL を指定する必要があります。 

さらに、ユーザーに付与するアクセス許可を使用して構成したテンプレートを指定するか、ユーザーがアクセス許可とユーザーを定義できるようにする必要があります。 

次の手順を実行して、テンプレートの GUID とライセンス URL の値を Active Directory Rights Management サービスコンソールから見つけます。

#### <a name="locate-a-template-guid"></a>テンプレート GUID を見つける

1. クラスターを展開し、**[権利ポリシー テンプレート]** をクリックします。 

1. **配布権利ポリシーテンプレート**の情報から、使用するテンプレートから GUID をコピーします。 

例: **82bf3474-6efe-4fa1-8827-d1bd93339119** 

#### <a name="locate-the-licensing-url"></a>ライセンス URL を見つける

1. クラスター名をクリックします。
 
1. **[クラスターの詳細]** の情報から、**[ライセンス]** 値の **/_wmcs/licensing** 文字列以外をコピーします。 

例: **https://rmscluster.contoso.com** 
    
> [!NOTE]
> エクストラネットとイントラネットのライセンスの値が異なる場合は、保護されたコンテンツをパートナーと共有する場合にのみ、エクストラネットの値を指定します。 保護されたコンテンツを共有するパートナーは、明示的なポイントツーポイントの信頼を使用して定義する必要があります。 
> 
> 保護されたコンテンツを共有していない場合は、イントラネットの値を使用して、AD RMS 保護を使用しているすべてのクライアントコンピューターが、イントラネット接続経由で Azure Information Protection 接続していることを確認してください。 たとえば、リモートコンピューターでは VPN 接続を使用する必要があります。
> 

## <a name="next-steps"></a>次のステップ

HYOK をサポートするためのシステムの構成が完了したら、HYOK 保護のラベルの構成を続行します。 詳細については、「 [Rights Management 保護のラベルを構成する方法](configure-policy-protection.md)」を参照してください。
