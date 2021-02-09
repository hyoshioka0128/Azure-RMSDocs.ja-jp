---
title: Azure Information Protection クラシッククライアントに関する Faq
description: Azure Information Protection とその保護サービス、Azure Rights Management (Azure RMS) に関してよく寄せられる質問をいくつか示します。 ここに記載されている Faq は、AIP classic クライアントのみに関連しています。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/12/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.custom: admin
search.appverid:
- MET150
ms.openlocfilehash: 0e63208b1188ab9580f084832293ad25df3e424f
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97386507"
---
# <a name="frequently-asked-questions-for-the-azure-information-protection-classic-client"></a>Azure Information Protection クラシッククライアントに関してよく寄せられる質問

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連**: AIP の統合された [従来のクライアントのみ](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)。 詳細については、「 [Azure Information Protection に関してよく寄せられる質問](faqs.md)」を参照してください。

この記事では、Azure Information Protection クラシッククライアントのみに関連するよく寄せられる質問の一覧を示します。

>[!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>Azure Information Protection client は分類とラベル付けを含むサブスクリプション用のみでしょうか。

いいえ。 クラシック AIP クライアントは、Azure Rights Management サービスだけを含むサブスクリプションでも使用できます。データ保護のみが対象となります。

Azure Information Protection ポリシーを使用せずにクラシッククライアントをインストールすると、クライアントは [保護のみモード](./rms-client/client-protection-only-mode.md)で自動的に動作します。これにより、ユーザーは Rights Management テンプレートとカスタムアクセス許可を適用できます。 

分類とラベル付けを含むサブスクリプションを後で購入した場合、Azure Information Protection ポリシーをダウンロードする際に、クライアントは自動的に標準モードへと切り替わります。


## <a name="whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner"></a>Windows Server FCI と Azure Information Protection スキャナーの違いは何ですか。

[Rights Management コネクタ](deploy-rms-connector.md) (Office ドキュメントのみ) や [PowerShell スクリプト](./rms-client/configure-fci.md) (すべてのファイルの種類) を使用してドキュメントを分類して保護するために、これまでは Windows Server ファイル分類インフラストラクチャが選択されてきました。 

これからは、[Azure Information Protection スキャナー](deploy-aip-scanner.md)の使用をお勧めします。 スキャナーは Azure Information Protection クライアントと Azure Information Protection ポリシーを使用して、ドキュメント (すべてのファイルの種類) にラベルを付けるため、これらのドキュメントは分類され、必要に応じて保護されます。

この 2 つのトポロジの主な違いを次に示します。

|  |Windows Server FCI  |Azure Information Protection スキャナー  |
|---------|---------|---------|
|**サポートされているデータ ストア**    | Windows Server 上のローカルフォルダー        | - Windows ファイル共有とネットワーク接続ストレージ<br /><br />- SharePoint Server 2016 と SharePoint Server 2013。 [このバージョンの SharePoint の延長サポート](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010)が含まれるお客様向けに SharePoint Server 2010 もサポートされています。        |
|**操作モード**     |リアルタイム         |データストアを体系的に1回または繰り返しクロールする         |
|**サポートされているファイルの種類**     | - すべてのファイルの種類が既定で保護されます <br /><br />- レジストリを編集することで、特定のファイルの種類を保護から除外できます|ファイルの種類ごとのサポート: <br /><br />- Office ファイルの種類と PDF ドキュメントは既定で保護されます <br /><br />- レジストリを編集することで、保護に含めるファイルの種類を追加できます|

### <a name="setting-rights-management-owners"></a>Rights Management 所有者の設定

既定では、Windows Server FCI と Azure Information Protection スキャナーの両方について、 [Rights Management 所有者](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) は、ファイルを保護するアカウントに設定されます。

既定の設定を次のようにオーバーライドします。

- **Windows Server FCI**: すべてのファイルに対して1つのアカウントとして Rights Management 所有者を設定するか、または各ファイルの Rights Management 所有者を動的に設定します。 

    Rights Management 所有者を動的に設定するには、**-OwnerMail [ソース ファイルの所有者の電子メール]** パラメーターと値を使用します。 この構成では、ファイルの所有者プロパティのユーザー アカウント名を使用して、Active Directory からユーザーのメール アドレスを取得します。

- **Azure Information Protection スキャナー**: 新しく保護されたファイルについては、スキャナープロファイルの **既定の所有者** 設定を指定することにより、指定したデータストアのすべてのファイルに対して、Rights Management 所有者を1つのアカウントに設定します。 

    各ファイルの Rights Management 所有者を動的に設定することはできません。また、Rights Management 所有者は、以前に保護されていたファイルに対して変更されません。 

    > [!NOTE]
    > スキャナーで SharePoint サイトおよびライブラリのファイルを保護する場合、Rights Management 所有者は SharePoint エディターの値を使用して、ファイルごとに動的に設定されます。

## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>他のユーザーがラベルを削除または変更しないようにするには、どうすればいいですか?

分類ラベルを下げたり、ラベルを削除したり、保護を解除したりする理由をユーザーに示す [ポリシー設定](configure-policy-settings.md) がありますが、この設定によってこれらの操作が妨げられることはありません。 ユーザーがラベルを削除または変更できないようにするには、コンテンツが既に保護されている必要があります。また、保護アクセス許可によって、ユーザーにエクスポートまたはフルコントロールの[使用権限](configure-usage-rights.md)が付与されていません。

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>DLP ソリューションや他のアプリケーションは Azure Information Protection とどのように統合できますか?

Azure Information Protection は分類に永続的メタデータを使用し、これにはクリア テキストのラベルが含まれるので、DLP ソリューションや他のアプリケーションはこの情報を読み取ることができます。 

このメタデータの詳細については、「[メールやドキュメントに格納されるラベル情報](configure-policy.md#label-information-stored-in-emails-and-documents)」を参照してください。

Exchange Online のメール フロー ルールで、このメタデータを使用する例については、「[Azure Information Protection ラベルの Exchange Online メール フロー ルールの構成](configure-exo-rules.md)」をご覧ください。

## <a name="can-i-create-a-document-template-that-automatically-includes-the-classification"></a>分類が自動的に含まれるドキュメント テンプレートを作成できますか?

はい。 ラベルを構成して、[ラベル名を含むヘッダーまたはフッターを適用する](configure-policy-markings.md)ことができます。 ただし、それが要件を満たしていない場合は Azure Information Protection クラシッククライアントのみで、必要な書式を持つドキュメントテンプレートを作成し、フィールドコードとして分類を追加することができます。 

例として、ドキュメントのヘッダーに分類を表示するテーブルがあるとします。 または、概要向けにドキュメントの分類を参照する具体的な表現を使用します。

このフィールド コードをドキュメントに追加するには:

1. ドキュメントにラベルを付けて保存します。 このアクションにより新しいメタデータ フィールドが作成され、これをフィールド コード用に使用できます。

2. ドキュメント内で、ラベルの分類を追加したい位置にカーソルを合わせた後、**[挿入]** タブから **[テキスト]** > **[クイック パーツ]** > **[フィールド]** を選択します。

3. **[フィールド]** ダイアログ ボックスの **[カテゴリ]** ドロップダウンから、**[ドキュメント情報]** を選択します。 次に、**[フィールド名]** ドロップダウンから **[DocProperty (文書プロパティ)]** を選択します。

4. **[プロパティ]** ドロップダウンから **[秘密度]** を選択し、**[OK]** を選択します。

現在のラベルの分類がドキュメントに表示され、この値はドキュメントを開くかテンプレートを使用するたびに自動的に更新されます。 このため、ラベルが変更されると、このフィールド コードに対して表示される分類がドキュメント内で自動的に更新されます。

## <a name="how-is-classification-for-emails-using-azure-information-protection-different-from-exchange-message-classification"></a>Azure Information Protection を使用した電子メールの分類は、Exchange メッセージ分類とはどのように異なりますか。

Exchange メッセージ分類は、電子メールを分類できる古い機能であり、Azure Information Protection ラベルや分類を適用する機密ラベルとは別に実装されています。

ただし、この古い機能をラベルと統合すると、ユーザーが Outlook on the web および一部のモバイルメールアプリケーションを使用して電子メールを分類するときに、ラベル分類および対応するラベルマーキングが自動的に追加されるようになります。

同じ手法を使用して、Outlook on the web とこれらのモバイル用メール アプリケーションで独自のラベルを使用できます。

Outlook を Exchange Online と共に使用している場合は、これを行う必要はありません。これは、Office 365 セキュリティ & コンプライアンスセンター、Microsoft 365 Security center、または Microsoft コンプライアンスセンターから機密ラベルを公開する場合に、組み込みラベル付けをサポートするためです。

Web 上の Outlook で組み込みのラベル付けを使用できない場合は、この回避策の構成手順「[従来の Exchange メッセージ分類との統合](rms-client/client-admin-guide-customizations.md#integration-with-the-legacy-exchange-message-classification)」を参照してください。

## <a name="how-do-i-configure-a-mac-computer-to-protect-and-track-documents"></a>ドキュメントを保護および追跡するように Mac コンピューターを構成するにはどうすればよいですか。

まず、https://admin.microsoft.com のソフトウェア インストール リンクから Office for Mac がインストールされていることを確認します。 詳しい手順について [は、「PC または Mac で Microsoft 365 または Office 2019 をダウンロードしてインストールまたは再インストールする](https://support.office.com/article/Download-and-install-or-reinstall-Office-365-or-Office-2016-on-a-PC-or-Mac-4414EAAF-0478-48BE-9C42-23ADC4716658)」を参照してください。

Outlook を開き、Microsoft 365 職場または学校アカウントを使用してプロファイルを作成します。 次に新しいメッセージを作成し、次の操作を行って、Azure Rights Management サービスを使用してドキュメントや電子メールを保護できるように Office を構成します。

1. 新規のメッセージで、**[オプション]** タブの **[アクセス許可]** をクリックし、**[資格情報の確認]** をクリックします。

2. メッセージが表示されたら、Microsoft 365 職場または学校アカウントの詳細をもう一度指定し、[ **サインイン**] を選択します。

    これによって Azure Rights Management テンプレートがダウンロードされ、**[資格情報の確認]** が、**[無制限]**、**[転送不可]**、およびテナントに公開されたすべての Azure Rights Management テンプレートを含むオプションで置換されます。 この新しいメッセージは、ここで取り消すことができます。

電子メール メッセージやドキュメントを保護するには、**[オプション]** タブで **[アクセス許可]** をクリックし、電子メールやドキュメントを保護するオプションまたはテンプレートを選択します。

ドキュメントを保護した後に追跡するには: Azure Information Protection クラシッククライアントがインストールされている Windows コンピューターから、Office アプリケーションまたはエクスプローラーを使用してドキュメント追跡サイトにドキュメントを登録します。 手順については、[ドキュメントの追跡と取り消し](./rms-client/client-track-revoke.md)に関するページを参照してください。 Mac コンピューターからは、現在、Web ブラウザーを使用してドキュメント追跡サイト (https://track.azurerms.com)) に移動し、このドキュメントを追跡して取り消すことができます。

## <a name="when-i-test-revocation-in-the-document-tracking-site-i-see-a-message-that-says-people-can-still-access-the-document-for-up-to-30-daysis-this-time-period-configurable"></a>ドキュメント追跡サイトで失効をテストすると、最大 30 日間はドキュメントにアクセスできるというメッセージが表示されます。この期間を構成することはできますか。

はい。 このメッセージは、その特定のファイルの[使用ライセンス](configure-usage-rights.md#rights-management-use-license)を反映しています。

ファイルを取り消すと、そのアクションは、Azure Rights Management サービスでユーザーを認証する際にのみ適用できます。 そのため、ファイルに 30 日間の使用ライセンス有効期間があり、ユーザーが既にそのドキュメントを開いている場合、ユーザーはその使用ライセンスの期間中は引き続きドキュメントにアクセスすることができます。 使用ライセンスの期限が切れると、ユーザーの再認証が必要になりますが、ドキュメントが取り消されているため、その時点でユーザーのアクセスが拒否されます。

ドキュメントを保護したユーザーである [Rights Management 発行者](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)は、この取り消しから除外されており、常に自分のドキュメントにアクセスできます。

テナントに適用される使用ライセンスの有効期間の既定値は 30 日間です。ラベルまたはテンプレートで、この設定をより制限の厳しい値でオーバーライドできます。 使用ライセンスの詳細および構成方法については、「[Rights Management の使用ライセンス](configure-usage-rights.md#rights-management-use-license)」を参照してください。

## <a name="whats-the-difference-between-byok-and-hyok-and-when-should-i-use-them"></a>BYOK と HYOK の違いは何ですか。どのような場合に使用すればよいでしょうか。

Azure Information Protection において **独自キーを持ち込む** (BYOK) のは、Azure Rights Management 保護の独自キーをオンプレミスで作成する場合です。 そのキーを Azure Key Vault のハードウェア セキュリティ モジュール (HSM) に転送し、そこでそのキーの所有と管理を続行します。 このようにしない場合、Azure Rights Management 保護では Azure 内で自動的に作成、管理されるキーが使用されます。 この既定の構成は、"顧客管理" (BYOK オプション) ではなく "マイクロソフト管理" と呼ばれます。

BYOK の詳細と、組織でこのキー トポロジを選択するかどうかについては、「[Azure Information Protection テナント キーを計画して実装する](plan-implement-tenant-key.md)」を参照してください。

Azure Information Protection において **独自キーを保持する** (HYOK) 機能は、クラウドに格納されているキーで保護することができないドキュメントや電子メールのサブセットを持つような、少数の組織のためのものです。 こうした組織では、BYOK を使用してキーを作成し管理する場合でも、この制限が適用されます。 この制限は多くの場合、規制やコンプライアンス上の理由によるもので、HYOK 構成は "最高機密" 情報のみに適用されます。つまり、組織外には決して共有されず、内部ネットワークのみで利用され、モバイル デバイスからアクセスする必要のない情報です。

これらの例外 (通常は、保護する必要のあるすべてのコンテンツの 10% 未満) については、オンプレミスのソリューションである Active Directory Rights Management サービスを使用して、オンプレミスのキーを作成することができます。 このソリューションでは、コンピューターはクラウドから Azure Information Protection ポリシーを取得しますが、この識別されたコンテンツはオンプレミスのキーを使用して保護することができます。

HYOK の詳細、制限についての正しい理解、およびどのような場合に使用するかのガイダンスについては、「[AD RMS 保護の Hold Your Own Key (HYOK) の要件と制限事項](configure-adrms-restrictions.md)」を参照してください。

## <a name="what-do-i-do-if-my-question-isnt-here"></a>質問がここにない場合はどうすればよいですか。

まず、分類とラベル付け、またはデータ保護に固有のよく寄せられる質問を確認してください。 [Azure Rights Management サービス (Azure RMS)](what-is-azure-rms.md)は、Azure Information Protection のデータ保護テクノロジを提供します。 Azure RMS は分類およびラベル付けと併用するか、単体で使用できます。 

- [Azure Information Protection に関してよく寄せられる質問](faqs.md)

- [分類とラベル付けに関してよく寄せられる質問](faqs-infoprotect.md)

- [データ保護に関してよく寄せられる質問](faqs-rms.md)

質問に答えがない場合は、「 [Azure Information Protection の情報とサポート](information-support.md)」に記載されているリンクとリソースを参照してください。

さらに、エンドユーザー向けの FAQ が用意されています。

- [iOS 用と Android 用の Azure Information Protection の FAQ](./rms-client/mobile-app-faq.md)

- [Mac コンピューター用 RMS 共有アプリの FAQ](/previous-versions/msdn10/dn451248(v=msdn.10))