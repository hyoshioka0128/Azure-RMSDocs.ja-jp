---
title: Azure Information Protection ラベルを Office 365 に移行する - AIP
description: 統合ラベルをサポートしているクライアントとサービスで、Azure Information Protection のラベルを Office 365 の機密ラベルに移行します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/08/2019
ms.topic: article
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 56d23160e685325cc18a2c14b52cf23f950df7a0
ms.sourcegitcommit: 886aebde3b2df0f54b7bd41105823db44aea72d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2019
ms.locfileid: "66815542"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-office-365-sensitivity-labels"></a>Azure Information Protection のラベルを Office 365 の機密ラベルに移行する方法

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
> *手順:[Windows 用 Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection でラベルを秘密度ラベルとして使用することができるように移行[統一されたラベル付けをサポートするクライアントとサービス](#clients-and-services-that-support-unified-labeling)します。

移行後も管理し、Office 365 のセキュリティとコンプライアンス センター、または Microsoft 365 セキュリティ センター、Microsoft 365 コンプライアンス センターからこれらのラベルを発行します。 これらのラベルは、Azure Information Protection の統合されたラベル付けクライアントで使用できます。 Azure Information Protection クライアントを使用するように続行すると、このクライアントは引き続き Azure portal から Azure Information Protection ポリシーを使用してラベルをダウンロードします。

ラベルを移行する方法についての詳細な手順を読む前に、次のよく寄せられる質問が役立つ場合があります。

- [Azure Information Protection のラベルと Office 365 のラベルにはどのような違いがありますか。](faqs.md#whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365)

- [Office 365 にラベルを移行する適切なタイミングはいつですか。](faqs.md#when-is-the-right-time-to-migrate-my-labels-to-office-365)

- [ラベルを移行した後に使用する管理ポータルはどれですか。](faqs.md?#after-ive-migrated-my-labels-which-management-portal-do-i-use )

### <a name="important-information-about-administrative-roles"></a>管理者ロールに関する重要な情報

[Azure AD ロール](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)の**Azure Information Protection 管理者**(旧称**Information Protection 管理者**)、統一されたラベルでサポートされていませんプラットフォームです。 ラベルを移行する前に、この管理者の役割は、組織で使用する場合は、Azure AD ロールには、このロールを持つユーザーを追加の**コンプライアンス管理者**、**コンプライアンス データ管理者**、または**セキュリティ管理者**します。 この手順に関してサポートが必要な場合は、「[Office 365 セキュリティ&コンプライアンスセンターへのアクセス権をユーザーに付与する](https://docs.microsoft.com/office365/securitycompliance/grant-access-to-the-security-and-compliance-center)」をご覧ください。 Azure AD ポータル、Microsoft 365 セキュリティ センター、および Microsoft 365 コンプライアンス センターで、これらのロールを割り当てることもできます。

これらのロールを使用する代わりに、管理センターで、これらのユーザー用の新しいロール グループを作成し、そのグループに **[秘密度ラベル管理者]** ロールまたは **[組織構成]** ロールを追加できます。

これらの構成のいずれかを使用してユーザーに管理センターへのアクセス権を付与しなかった場合、これらのユーザーはラベルの移行後に Azure portal で Azure Information Protection を構成することはできません。

ラベルの移行後も、テナントのグローバル管理者は Azure portal および管理センターの両方でラベルとポリシーの管理を続けられます。


## <a name="considerations-for-unified-labels"></a>統合ラベルに関する考慮事項

ラベルを移行する前に、次の変更内容と考慮事項に注意してください。

- 現在のところ、一部のクライアントでは統合ラベルがサポートされていません。 [サポートされているクライアント](#clients-and-services-that-support-unified-labeling)を用意し、Azure portal (統合ラベルをサポートしていないクライアント用) と管理センター (統合ラベルをサポートしているクライアント用) の両方での管理のための準備をしてください。

- ポリシーとすべてのクライアント詳細設定は移行されません。移行されないポリシーには、ポリシー設定とそれにアクセスできるユーザーが含まれます (スコープ付きポリシー)。 移行されない変更については、ラベルの移行後、管理センターで関連オプションを構成する必要があります。
    
    操作における一貫性を上げるために、管理センターでは同じスコープで同じラベルを発行することをお勧めします。

- 管理センターでは、移行されたラベルの一部の設定がサポートされません。 「[管理センターでサポートされていないラベル設定](#label-settings-that-are-not-supported-in-the-admin-centers)」セクションに記載された表を使用すると、それらの設定と推奨される一連の措置を容易に確認できます。

- 保護テンプレート:
    
    - クラウドベースのキーを使用し、ラベル構成に含まれるテンプレートもラベルと共に移行されます。 その他の保護テンプレートは移行されません。 
    
    - 定義済みのテンプレート用に構成されているラベルがある場合は、これらのラベルを編集し、 **[アクセス許可を設定]** オプションを選択して、ご自分のテンプレートで使用していたのと同じ保護設定を構成します。 定義済みのテンプレートでのラベルによってラベルの移行はブロックされません。しかし、このラベル構成は管理センターではサポートされていません。
        
        ヒント:これらのラベルを再構成する場合は、次の 2 つのブラウザー ウィンドウを使用すると便利です。1 つのウィンドウでは、ラベル用の **[テンプレートの編集]** ボタンを選択して保護設定を表示します。もう 1 つのウィンドウでは **[アクセス許可の設定]** を選択したときと同じ設定を構成します。
    
    - クラウドベースの保護設定のあるラベルが移行されると、保護テンプレートの結果的に生成されるスコープは、Azure portal で (あるいは、AADRM PowerShell モジュールを使用することで) 定義されるスコープであり、管理センターで定義されるスコープとなります。 

- ラベルを移行すると、移行結果にラベルが**作成された**か、**更新された**か、重複のため、**名前が変更**されたかが表示されます。

    - ラベルを作成したら、それをアプリケーションやサービスで利用できるようにするには、いずれかの管理センターでラベルを発行する必要があります。
    
    - ラベルの名前が変更された場合は、いずれかの管理センターまたは Azure portal で編集する必要があります。

- Azure portal では、各ラベルのラベル表示名のみが表示されます。この名前は編集できます。 管理センターには、ラベルのこの表示名とラベル名の両方が表示されます。 ラベル名は、ラベルが最初に作成されたときに指定した最初の名前です。このプロパティは、識別目的でバックエンド サービスによって使用されます。

- ラベルのローカライズされた文字列は移行されません。 管理センターで、移行されたラベルに対してローカライズされた文字列を新しく定義する必要があります。

- 移行後、移行したラベルを Azure portal で編集すると、管理センターで同じ変更内容が自動的に反映されます。 ただし、いずれかの管理センターで移行したラベルを編集する場合は、Azure portal に戻って、 **[Azure Information Protection - 統合ラベル付け]** ブレードで **[公開]** を選ぶ必要があります。 Azure Information Protection クライアントでラベルの変更を認識させるには、この追加のアクションが必要です。

### <a name="label-settings-that-are-not-supported-in-the-admin-centers"></a>管理センターでサポートされていないラベル設定

次の表を使用すると、移行されたラベルのうち Office 365 セキュリティ/コンプライアンス センター、Microsoft 365 セキュリティ センター、または Microsoft コンプライアンス センターでサポートされていない構成設定を識別できます。 そのような設定が含まれているラベルがある場合は、移行の完了時に、最後の列にある管理ガイダンスを確認してから、いずれかの管理センターで自分のラベルを発行してください。

ラベルがどのように構成されているか不明な場合は、Azure portal でそれらの設定を表示してください。 この手順に関してサポートが必要な場合は、「[Azure Information Protection ポリシーの構成](configure-policy.md)」を参照してください。

Azure Information Protection クライアントでは、一覧表示されているラベル設定をすべて何の問題もなく使用できます。これは Azure portal から引き続きラベルがダウンロードされるからです。

|ラベル構成|統合ラベル付けのクライアントによるサポート| 管理センターのガイダンス|
|-------------------|---------------------------------------------|-------------------------|
|有効または無効の状態<br /><br />注:管理センターには同期されません |適用なし|ラベルが発行されているかどうかに対応します。 |
|一覧から選択するか、RGB コードを使用して指定するラベルの色 |はい|ラベルの色に対する構成オプションはありません。 代わりに、Azure portal でラベルの色を構成できます。|
|事前定義テンプレートを使用するクラウドベースの保護または HYOK ベースの保護 |いいえ|事前に定義されたテンプレート用の構成オプションはありません。 この構成を使用してラベルを発行することはお勧めしません。|
|Word、Excel、PowerPoint に対するユーザー定義のアクセス許可を使用するクラウドベースの保護 |いいえ|これらの Office アプリ用のユーザー定義のアクセス許可については構成オプションはありません。 この構成を使用してラベルを発行することはお勧めしません。 それを行った場合は、ラベルの適用結果が[次の表](#comparing-the-behavior-of-protection-settings-for-a-label)に一覧表示されます。|
|Outlook のユーザー定義のアクセス許可を使用する HYOK ベースの保護 ([転送不可]) |いいえ|HYOK に対する構成オプションはありません。 この構成を使用してラベルを発行することはお勧めしません。 それを行った場合は、ラベルの適用結果が[次の表](#comparing-the-behavior-of-protection-settings-for-a-label)に一覧表示されます。|
|保護を解除する |いいえ|保護を削除するための構成オプションはありません。 この構成を使用してラベルを発行することはお勧めしません。<br /><br /> 適用されたときに、このラベルを発行するは、ラベルで適用されていた場合に保護が削除されます。 保護が以前にラベルから独立して適用されていた場合、保護は保持されます。|
|視覚的なマーキング (ヘッダー、フッター、透かし) 向けのカスタム フォントと RGB コードによるカスタム フォントの色|はい|視覚的なマーキングの構成は、色とフォント サイズの一覧に限定されます。 構成した値が管理センターで確認できなくても、このラベルは変更なしで発行することができます。 <br /><br />これらのオプションを変更するには、Azure portal を使用します。 しかし、管理をより簡単にするには、管理センターに一覧されるオプションのいずれかに、色を変更することを検討してください。|
|視覚的なマーキングの変数 (ヘッダー、フッター)|いいえ|変更なしでこのラベルを発行した場合、変数は動的な値を表示するのでなく、クライアント上でテキストとして表示されます。 ラベルを発行する前に、文字列を編集して変数を削除してください。|
|アプリごとの視覚的なマーキング|いいえ|変更なしでこのラベルを発行した場合、アプリ変数は、選択したアプリ上にご利用のテキスト文字列を表示するのでなく、クライアント上ですべてのアプリにテキストとして表示されます。 このラベルはすべてのアプリに適している場合にのみ発行します。文字列を編集してアプリ変数を削除します。|
|条件と関連設定 <br /><br />注:自動の推奨ラベル付けとそのヒントが含まれます|適用なし|自動ラベル付けを使用して、ラベル設定とは個別の構成としてご自分の条件を再構成します。|

### <a name="comparing-the-behavior-of-protection-settings-for-a-label"></a>ラベルの保護設定の動作を比較する

次の表を使用して、どのラベルに同じ保護設定によって動作が、Azure Information Protection クライアント、Azure Information Protection の統合されたラベル付けクライアント、または必要とする Office アプリケーションの使用かどうかを識別するために組み込み (別名"ネイティブな Office のラベル付け 

保護設定がどのように構成されているか不明な場合は、Azure portal の **[保護]** ブレードでそれらの設定を表示して確認してください。 この手順に関してサポートが必要な場合は、「[保護設定用のラベルを構成するには](configure-policy-protection.md#to-configure-a-label-for-protection-settings)」をご覧ください。

同じ動作をする保護設定は一覧に含まれませんが、次の例外があります。
- ラベル付けが組み込まれた Office アプリを使用すると、Azure Information Protection 統合ラベル付けクライアントもインストールされていない限り、ラベルはエクスプローラーに表示されません。
- ラベル付けが組み込まれた Office アプリを使用すると、保護が以前にラベルから独立して適用されていた場合、その保護は保持されます [[1]](#footnote-1)。

|ラベル用の保護設定 |Azure Information Protection クライアント|Azure Information Protection 統合ラベル付けクライアント| ラベル付けが組み込まれた Office アプリ
|-------------------|-----------------------------------|-----------------------------------------------------------|---------------
|ユーザー定義のアクセス許可が Word、Excel、PowerPoint、およびエクスプローラーを対象とする Azure (クラウド キー):| Word、Excel、PowerPoint、およびエクスプローラーで表示されます <br /><br /> ラベルが適用された場合:<br /><br /> - ユーザーはカスタムのアクセス許可の入力を求められます。それはクラウドベースのキーを使用する保護として適用されます| 表示されません |Word、Excel、PowerPoint、および Outlook で表示されます: <br /><br /> ラベルが適用された場合:<br /><br /> - ユーザーはカスタム アクセス許可の入力を求められず、保護は適用されません。 <br /><br /> - 保護が以前にラベルから独立して適用されていた場合、その保護は保持されます [[1]](#footnote-1)|
|テンプレートを使用した HYOK (AD RMS):| Word、Excel、PowerPoint、Outlook、およびエクスプローラーで表示されます<br /><br /> このラベルが適用された場合: <br /><br />- HYOK 保護はドキュメントや電子メールに適用されます。 | Word、Excel、PowerPoint、Outlook、およびエクスプローラーで表示されます  <br /><br /> このラベルが適用された場合: <br /><br />- 保護が以前にラベルによって適用されている場合、その保護は適用されず削除されます [[2]](#footnote-2) <br /><br />- 保護が以前にラベルから独立して適用されていた場合、その保護は保持されます |Word、Excel、PowerPoint、および Outlook で表示されます <br /><br /> このラベルが適用された場合: <br /><br />- 保護が以前にラベルによって適用されている場合、その保護は適用されず削除されます [[2]](#footnote-2) <br /><br />- 保護が以前にラベルから独立して適用されていた場合、その保護は保持されます [[1]](#footnote-1) |
|ユーザー定義のアクセス許可が Word、Excel、PowerPoint、およびエクスプローラーを対象とする HYOK (AD RMS):| Word、Excel、PowerPoint、およびエクスプローラーで表示されます<br /><br /> このラベルが適用された場合:<br /><br /> - HYOK 保護はドキュメントや電子メールに適用されます。| Word、Excel、PowerPoint で表示されます <br /><br /> このラベルが適用された場合: <br /><br />- 保護が以前にラベルによって適用されている場合、その保護は適用されず削除されます [[2]](#footnote-2) <br /><br />- 保護が以前にラベルから独立して適用されていた場合、その保護は保持されます|Word、Excel、PowerPoint で表示されます <br /><br /> このラベルが適用された場合: <br /><br />- 保護が以前にラベルによって適用されている場合、その保護は適用されず削除されます [[2]](#footnote-2) <br /><br />- 保護が以前にラベルから独立して適用されていた場合、その保護は保持されます |
|ユーザー定義のアクセス許可が Outlook を対象とする HYOK (AD RMS):|Outlook で表示されます<br /><br />このラベルが適用された場合:<br /><br />- HYOK 保護を使用した転送不可が電子メールに適用されます|Outlook で表示されます<br /><br />このラベルが適用された場合:<br /><br /> - 保護が以前にラベルによって適用されている場合、その保護は適用されず削除されます [[2]](#footnote-2) <br /><br />- 保護が以前にラベルから独立して適用されていた場合、その保護は保持されます|Outlook で表示されます<br /><br />このラベルが適用された場合:<br /><br />- 保護が以前にラベルによって適用されている場合、その保護は適用されず削除されます [[2]](#footnote-2) <br /><br />- 保護が以前にラベルから独立して適用されていた場合、その保護は保持されます [[1]](#footnote-1)|

###### <a name="footnote-1"></a>脚注 1

Outlook for Mac では、保護は保持されますが例外が 1 つあります。[暗号化のみ] オプションを使用して電子メールが保護されている場合、その保護は削除されます。


###### <a name="footnote-2"></a>脚注 2

次の操作をサポートする使用権限またはロールをユーザーが持っている場合、保護は削除されます。
- [使用権限](configure-usage-rights.md#usage-rights-and-descriptions)エクスポートまたはフル コントロール。
- [Rights Management 発行者もしくは Rights Management 所有者](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)、または[スーパー ユーザー](configure-super-users.md)のロール。

ユーザーがこれらの使用権限またはロールをいずれも持っていない場合、ラベルは適用されず、元の保護が維持されます。


## <a name="to-migrate-azure-information-protection-labels"></a>Azure Information Protection ラベルを移行するには

次の手順に従い、テナントと Azure Information Protection ラベルを移行して、統合ラベル付けの新しいストアを使います。

ラベルを移行する、コンプライアンス管理者、コンプライアンス データ管理者、セキュリティ管理者、またはグローバル管理者があります。

> [!NOTE]
> 保有期間のラベルやデータ損失防止ポリシーがある Office 365 の場合は、コンプライアンス管理者ロール、準拠データ管理者の役割、または、ラベルを移行するグローバル管理者ロールがあることをお勧めします。
> 
> セキュリティ管理者しない保有期間のラベルやデータ損失防止ポリシーにアクセス、ため場合、これらのいずれかがある場合と同じ名前の Azure Information Protection ラベルがある、移行プロセスを手動で表示されるまで完了できません名前を変更します。重複します。 ただし、他のロールのいずれかがある場合、移行プロセス名前を変更できます、Azure Information Protection ラベル、移行を完了できるようにします。

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、 **[Azure Information Protection]** ブレードに移動します。
    
    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. **管理**メニュー オプションを選択し**統合がラベル付け**します。

3. **[Azure Information Protection - 統合ラベル付け]** ブレードで **[有効化]** を選択し、オンライン指示に従います。
    
    アクティブ化するためのオプションを使用できない場合は、 **[統合ラベル付けの状態]** をチェックください。 **[アクティブ化]** と表示されている場合は、お客様のテナントでは既に統合ラベル付けストアが使用されているため、ラベルを移行する必要はありません。

正常に移行されたラベルについては、[統合ラベル付けをサポートするクライアントおよびサービス](#clients-and-services-that-support-unified-labeling)で使用できるようになりました。 ただし、次のいずれかの管理センターでラベルを発行する必要があります: Office 365 セキュリティ/コンプライアンス センター、Microsoft 365 セキュリティ センター、Microsoft 365 コンプライアンス センター。

> [!IMPORTANT]
> Azure Information Protection クライアントに対して、Azure portal の外部でラベルを編集する場合、この **[Azure Information Protection - 統合ラベル付け]** ブレードに戻り、 **[公開]** を選びます。

### <a name="clients-and-services-that-support-unified-labeling"></a>統合ラベル付けをサポートするクライアントおよびサービス

使用しているクライアントとサービスによって統合ラベル付けがサポートされているかどうかを確認するには、該当するドキュメントを参照して、次のいずれかの管理センターから発行された機密ラベルをそれらで使用できるかどうかを確認します: Office 365 セキュリティ/コンプライアンス センター、Microsoft 365 セキュリティ センター、Microsoft 365 コンプライアンス センター。 

##### <a name="clients-that-currently-support-unified-labeling-include"></a>現在、統合ラベル付けをサポートしているクライアント:

- [Azure Information Protection unified Windows 用のラベル付けクライアント](./rms-client/unifiedlabelingclient-version-release-history.md)します。 Azure Information Protection クライアントでは、このクライアントの比較は、次を参照してください。[クライアントの比較](./rms-client/use-client.md#compare-the-clients)します。

- 可用性の段階が異なる Office からのアプリ。 詳細については、Office ドキュメントの「[Office 内の文書やメールに機密ラベルを適用する](https://support.office.com/en-us/article/apply-sensitivity-labels-to-your-documents-and-email-within-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9)」から「**現在、機能はどこで入手できますか?** 」のセクションを参照してください。
    
- [Microsoft Information Protection SDK](https://docs.microsoft.com/en-us/information-protection/develop/overview) を使用しているソフトウェア ベンダーおよび開発者からのアプリです。

##### <a name="services-that-currently-support-unified-labeling-include"></a>現在、統合ラベル付けをサポートしているサービス:

- Microsoft Defender Advanced Threat Protection

- Microsoft Cloud App Security
    
    このサービスでは、統合ラベル付けストアに移行する前と後の両方で、次のロジックを使用してラベルがサポートされます。
    
    - 管理センターに Azure portal と同じラベルがある場合: 統合ラベルは管理センターから取得されます。 Cloud App Security でこれらのラベルを選択するには、少なくとも 1 つのユーザーに少なくとも 1 つのラベルを発行する必要があります。
    
    - 管理センターに Azure portal と同じラベルがない場合: 統合ラベルは、管理センターからは使用されず、代わりに Azure portal から取得されます。

- [Microsoft Information Protection SDK](https://docs.microsoft.com/en-us/information-protection/develop/overview) を使用しているソフトウェア ベンダーおよび開発者からのサービスです。

## <a name="next-steps"></a>次の手順

いずれかの管理センターで構成および発行できるようになった移行済みラベルについて詳しくは、「[機密ラベルの概要](/Office365/SecurityCompliance/sensitivity-labels)」をご覧ください。

既に同意していない場合、は、Azure Information Protection の統合されたラベル付けクライアントをインストールします。 リリースについては、管理者ガイド、およびユーザー ガイドを参照してください。 [Azure Information Protection unified Windows 用のラベル付けクライアント](./rms-client/aip-clientv2.md)します。
