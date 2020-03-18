---
title: Azure Information Protection ラベルを統合された秘密度ラベルに移行する-AIP
description: Microsoft Information Protection framework をサポートするクライアントとサービスの統合された秘密度ラベルに Azure Information Protection ラベルを移行します。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: labelmigrate
ms.reviewer: demizets
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: a7413026bc85c93063c5eb490c559e52db63b718
ms.sourcegitcommit: 8c39347d9b7a120014120860fff89c5616641933
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79482319"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-unified-sensitivity-labels"></a>Azure Information Protection ラベルを統合秘密度ラベルに移行する方法

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
> *手順: [Windows 用の Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と**ラベル管理**は、**2021 年 3 月 31 日**で**非推奨**になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Azure Information Protection ラベルを統一されたラベル付けプラットフォームに移行して、統一されたラベル付けを[サポートするクライアントとサービス](#clients-and-services-that-support-unified-labeling)による機密ラベルとして使用できるようにします。

> [!NOTE]
> Azure Information Protection サブスクリプションが非常に新しい場合は、テナントが既に統合されたラベル付けプラットフォームにあるため、ラベルを移行する必要はありません。 詳細については、「[テナントが統一されたラベル付けプラットフォームにあるかどうかを確認する方法](faqs.md#how-can-i-determine-if-my-tenant-is-on-the-unified-labeling-platform)」を参照してください。

ラベルを移行しても、Azure Information Protection クライアント (クラシック) との違いはありません。このクライアントは、Azure portal から Azure Information Protection ポリシーを使用してラベルをダウンロードし続けるためです。 ただし、ラベルを Azure Information Protection 統合されたラベル付けクライアントや、機密ラベルを使用するその他のクライアントやサービスで使用できるようになりました。

ラベルを移行するための手順を確認する前に、次のよく寄せられる質問が役に立つ場合があります。

- [Office 365 の Azure Information Protection ラベルとラベルの違いは何ですか。](faqs.md#whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365)

- [ラベルを移行するのに最適なタイミング](faqs.md#when-is-the-right-time-to-migrate-my-labels)

- [ラベルを移行した後に使用する管理ポータルはどれですか。](faqs.md?#after-ive-migrated-my-labels-which-management-portal-do-i-use )

### <a name="administrative-roles-that-support-the-unified-labeling-platform"></a>統一されたラベル付けプラットフォームをサポートする管理者ロール

組織内の代理管理に管理者ロールを使用する場合は、統一されたラベル付けプラットフォームに対していくつかの変更を行う必要があります。

**Azure Information Protection 管理者**(旧称**Information Protection administrator**) の[Azure AD ロール](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)は、統一されたラベル付けプラットフォームではサポートされていません。 この管理者ロールを使用して Azure Information Protection を管理する場合は、このロールを持つユーザーを、**コンプライアンス管理者**、**コンプライアンスデータ管理者**、または**セキュリティ管理者**の Azure AD ロールに追加します。 この手順に関してサポートが必要な場合は、「[Office 365 セキュリティ&コンプライアンスセンターへのアクセス権をユーザーに付与する](https://docs.microsoft.com/microsoft-365/security/office-365-security/grant-access-to-the-security-and-compliance-center)」をご覧ください。 Azure AD ポータル、Microsoft 365 セキュリティ センター、および Microsoft 365 コンプライアンス センターで、これらのロールを割り当てることもできます。

これらのロールを使用する代わりに、管理センターで、これらのユーザー用の新しいロール グループを作成し、そのグループに **[秘密度ラベル管理者]** ロールまたは **[組織構成]** ロールを追加できます。

これらの構成のいずれかを使用してユーザーに管理センターへのアクセス権を付与しなかった場合、これらのユーザーはラベルの移行後に Azure portal で Azure Information Protection を構成することはできません。

ラベルの移行後も、テナントのグローバル管理者は Azure portal および管理センターの両方でラベルとポリシーの管理を続けられます。

## <a name="before-you-begin"></a>始める前に

ラベルの移行には多くの利点がありますが、元に戻すことはできません。そのため、次の変更と考慮事項に注意してください。

- [統合ラベルをサポートするクライアント](#clients-and-services-that-support-unified-labeling)があることを確認し、必要に応じて、Azure portal (統合ラベルをサポートしていないクライアントの場合) と管理センター (統合ラベルをサポートするクライアントの場合) の両方で管理用に準備します。

- ポリシーとすべてのクライアント詳細設定は移行されません。移行されないポリシーには、ポリシー設定とそれにアクセスできるユーザーが含まれます (スコープ付きポリシー)。 ラベルの移行後に、これらの設定を構成するためのオプションは次のとおりです。
    - 機密ラベルの管理センター。
    - [Office 365 Security & Compliance PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/office-365-scc-powershell?view=exchange-ps)。これは、[高度なクライアント設定](./rms-client/clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を構成するために使用する必要があります。
    

- 管理センターでは、移行されたラベルの一部の設定がサポートされません。 「[管理センターでサポートされていないラベル設定](#label-settings-that-are-not-supported-in-the-admin-centers)」セクションに記載された表を使用すると、それらの設定と推奨される一連の措置を容易に確認できます。

- 保護テンプレート:
    
    - クラウドベースのキーを使用し、ラベル構成に含まれるテンプレートもラベルと共に移行されます。 その他の保護テンプレートは移行されません。 
    
    - 定義済みのテンプレート用に構成されているラベルがある場合は、これらのラベルを編集し、 **[アクセス許可を設定]** オプションを選択して、ご自分のテンプレートで使用していたのと同じ保護設定を構成します。 定義済みのテンプレートでのラベルによってラベルの移行はブロックされません。しかし、このラベル構成は管理センターではサポートされていません。
        
        ヒント: これらのラベルを再構成するには、2つのブラウザーウィンドウが役に立つことがあります。1つは、保護設定を表示するためにラベルの **[テンプレートの編集]** ボタンを選択するウィンドウと、 **[アクセス許可の設定]** を選択したときに同じ設定を構成するためのウィンドウです。
    
    - クラウドベースの保護設定を含むラベルを移行すると、保護テンプレートのスコープは、Azure portal (または AIPService PowerShell モジュールを使用) で定義されているスコープと、管理センターで定義されているスコープになります。 

- Azure portal では、各ラベルのラベル表示名のみが表示されます。この名前は編集できます。 ユーザーは、アプリにこのラベル名を表示します。 管理センターには、ラベルのこの表示名とラベル名の両方が表示されます。 ラベル名は、ラベルを最初に作成するときに指定する初期名です。このプロパティは、バックエンドサービスによって識別のために使用されます。 ラベルを移行すると、表示名は変わりません。ラベル名は、Azure portal のラベル ID に変更されます。

- ラベルのローカライズされた文字列は移行されません。 Office 365 Security & Compliance PowerShell と、 *LocaleSettings*パラメーターを使用して、移行されたラベルの新しいローカライズされた文字列を定義[します。](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps)

- 移行後、移行したラベルを Azure portal で編集すると、管理センターで同じ変更内容が自動的に反映されます。 ただし、管理センターの1つで移行したラベルを編集する場合は、Azure portal、 **[Azure Information Protection 統合]** されたラベル付け ウィンドウに戻り、 **[発行]** を選択する必要があります。 この追加の操作は、Azure Information Protection クライアント (クラシック) がラベルの変更を取得するために必要です。

### <a name="label-settings-that-are-not-supported-in-the-admin-centers"></a>管理センターでサポートされていないラベル設定

次の表を使用すると、移行されたラベルのうち Office 365 セキュリティ/コンプライアンス センター、Microsoft 365 セキュリティ センター、または Microsoft コンプライアンス センターでサポートされていない構成設定を識別できます。 これらの設定を含むラベルがある場合は、移行が完了したら、最後の列にある管理のガイダンスを使用して、参照先の管理センターのいずれかでラベルを公開します。

ラベルがどのように構成されているか不明な場合は、Azure portal でそれらの設定を表示してください。 この手順に関してサポートが必要な場合は、「[Azure Information Protection ポリシーの構成](configure-policy.md)」を参照してください。

Azure Information Protection クライアント (クラシック) は、Azure portal からラベルをダウンロードし続けているため、問題なくすべてのラベル設定を使用できます。

|ラベル構成|統合ラベル付けのクライアントによるサポート| 管理センターのガイダンス|
|-------------------|---------------------------------------------|-------------------------|
|有効または無効の状態<br /><br />この状態は管理センターと同期されていません |適用できません|ラベルが発行されているかどうかに対応します。 |
|一覧から選択するか、RGB コードを使用して指定するラベルの色 |はい|ラベルの色に対する構成オプションはありません。 代わりに、Azure portal でラベルの色を構成することも、 [PowerShell](./rms-client/clientv2-admin-guide-customizations.md#specify-a-color-for-the-label)を使用することもできます。|
|事前定義テンプレートを使用するクラウドベースの保護または HYOK ベースの保護 |いいえ|事前に定義されたテンプレート用の構成オプションはありません。 この構成を使用してラベルを発行することはお勧めしません。|
|Word、Excel、PowerPoint に対するユーザー定義のアクセス許可を使用するクラウドベースの保護 |はい|管理センターには、ユーザー定義のアクセス許可の構成オプションが含まれるようになりました。 <br /><br /> この構成でラベルを発行する場合は、[次の表](#comparing-the-behavior-of-protection-settings-for-a-label)のラベルを適用した結果を確認してください。|
|Outlook のユーザー定義のアクセス許可を使用する HYOK ベースの保護 ([転送不可]) |いいえ|HYOK に対する構成オプションはありません。 この構成を使用してラベルを発行することはお勧めしません。 それを行った場合は、ラベルの適用結果が[次の表](#comparing-the-behavior-of-protection-settings-for-a-label)に一覧表示されます。|
|視覚的なマーキング (ヘッダー、フッター、透かし) 向けのカスタム フォントと RGB コードによるカスタム フォントの色|はい|視覚的なマーキングの構成は、色とフォント サイズの一覧に限定されます。 構成した値が管理センターで確認できなくても、このラベルは変更なしで発行することができます。 <br /><br />これらのオプションを変更するには、Azure portal を使用します。 しかし、管理をより簡単にするには、管理センターに一覧されるオプションのいずれかに、色を変更することを検討してください。|
|視覚的なマーキングの変数 (ヘッダー、フッター)|いいえ|変更なしでこのラベルを発行した場合、変数は動的な値を表示するのでなく、クライアント上でテキストとして表示されます。 ラベルを発行する前に、文字列を編集して変数を削除してください。|
|アプリごとの視覚的なマーキング|いいえ|変更なしでこのラベルを発行した場合、アプリ変数は、選択したアプリ上にご利用のテキスト文字列を表示するのでなく、クライアント上ですべてのアプリにテキストとして表示されます。 このラベルはすべてのアプリに適している場合にのみ発行します。文字列を編集してアプリ変数を削除します。|
|"自分のためにのみ" 保護 |はい|管理センターでは、ユーザーを指定せずに、今すぐ適用する暗号化設定を保存することはできません。 この Azure portal では、この構成により、 ["自分だけ" の保護](configure-policy-protection.md#example-6-label-that-applies-just-for-me-protection)が適用されるラベルが生成されます。 <br /><br /> 別の方法として、暗号化を適用するラベルを作成し、任意のアクセス許可を持つユーザーを指定してから、PowerShell を使用して関連する保護テンプレートを編集します。 まず、 [AipServiceRightsDefinition](https://docs.microsoft.com/powershell/module/aipservice/new-aipservicerightsdefinition)コマンドレットを使用し (例3を参照)、次に*RightsDefinitions*パラメーターを指定して[-Aipservicetemplateproperty を設定](https://docs.microsoft.com/powershell/module/aipservice/set-aipservicetemplateproperty?view=azureipps#examples)します。|
|条件と関連設定 <br /><br /> 自動の推奨ラベル付けとそのヒントが含まれます|適用できません|自動ラベル付けを使用して、ラベル設定とは個別の構成としてご自分の条件を再構成します。|

### <a name="comparing-the-behavior-of-protection-settings-for-a-label"></a>ラベルの保護設定の動作を比較する

次の表を使用して、ラベルの同じ保護設定が、Azure Information Protection クライアント (クラシック)、Azure Information Protection の統合ラベル付けクライアント、または Office アプリのどちらで使用されているかに応じて異なる動作を指定します。ラベルが組み込まれている ("ネイティブオフィスラベル" とも呼ばれます)。 ラベルの動作の違いによって、ラベルを公開するかどうかの決定が変わることがあります。これは、組織内にクライアントが混在している場合に特に当てはまります。

保護設定がどのように構成されているかわからない場合は、**保護** ウィンドウの Azure portal の設定を参照してください。 この手順に関してサポートが必要な場合は、「[保護設定用のラベルを構成するには](configure-policy-protection.md#to-configure-a-label-for-protection-settings)」をご覧ください。

同じ動作をする保護設定は一覧に含まれませんが、次の例外があります。
- ラベル付けが組み込まれた Office アプリを使用すると、Azure Information Protection 統合ラベル付けクライアントもインストールされていない限り、ラベルはエクスプローラーに表示されません。
- ラベル付けが組み込まれた Office アプリを使用すると、保護が以前にラベルから独立して適用されていた場合、その保護は保持されます [[1]](#footnote-1)。

|ラベル用の保護設定 |Azure Information Protection クライアント (クラシック) |Azure Information Protection 統合ラベル付けクライアント| ラベル付けが組み込まれた Office アプリ
|-------------------|-----------------------------------|-----------------------------------------------------------|---------------
|ユーザー定義のアクセス許可が Word、Excel、PowerPoint、およびエクスプローラーを対象とする Azure (クラウド キー):| Word、Excel、PowerPoint、およびエクスプローラーで表示されます <br /><br /> ラベルが適用された場合:<br /><br /> - ユーザーはカスタムのアクセス許可の入力を求められます。それはクラウドベースのキーを使用する保護として適用されます| Word、Excel、PowerPoint、およびエクスプローラーで表示されます <br /><br /> ラベルが適用された場合:<br /><br /> - ユーザーはカスタムのアクセス許可の入力を求められます。それはクラウドベースのキーを使用する保護として適用されます|Word、Excel、PowerPoint、および Outlook で表示されます: <br /><br /> ラベルが適用された場合:<br /><br /> - ユーザーはカスタム アクセス許可の入力を求められず、保護は適用されません。 <br /><br /> - 保護が以前にラベルから独立して適用されていた場合、その保護は保持されます [[1]](#footnote-1)|
|テンプレートを使用した HYOK (AD RMS):| Word、Excel、PowerPoint、Outlook、およびエクスプローラーで表示されます<br /><br /> このラベルが適用された場合: <br /><br />- HYOK 保護はドキュメントや電子メールに適用されます。 | Word、Excel、PowerPoint、Outlook、およびエクスプローラーで表示されます  <br /><br /> このラベルが適用された場合: <br /><br />- 保護が以前にラベルによって適用されている場合、その保護は適用されず削除されます [[2]](#footnote-2) <br /><br />- 保護が以前にラベルから独立して適用されていた場合、その保護は保持されます |Word、Excel、PowerPoint、および Outlook で表示されます <br /><br /> このラベルが適用された場合: <br /><br />- 保護が以前にラベルによって適用されている場合、その保護は適用されず削除されます [[2]](#footnote-2) <br /><br />- 保護が以前にラベルから独立して適用されていた場合、その保護は保持されます [[1]](#footnote-1) |
|ユーザー定義のアクセス許可が Word、Excel、PowerPoint、およびエクスプローラーを対象とする HYOK (AD RMS):| Word、Excel、PowerPoint、およびエクスプローラーで表示されます<br /><br /> このラベルが適用された場合:<br /><br /> - HYOK 保護はドキュメントや電子メールに適用されます。| Word、Excel、PowerPoint で表示されます <br /><br /> このラベルが適用された場合: <br /><br />- 保護が以前にラベルによって適用されている場合、その保護は適用されず削除されます [[2]](#footnote-2) <br /><br />- 保護が以前にラベルから独立して適用されていた場合、その保護は保持されます|Word、Excel、PowerPoint で表示されます <br /><br /> このラベルが適用された場合: <br /><br />- 保護が以前にラベルによって適用されている場合、その保護は適用されず削除されます [[2]](#footnote-2) <br /><br />- 保護が以前にラベルから独立して適用されていた場合、その保護は保持されます |
|ユーザー定義のアクセス許可が Outlook を対象とする HYOK (AD RMS):|Outlook で表示されます<br /><br />このラベルが適用された場合:<br /><br />- HYOK 保護を使用した転送不可が電子メールに適用されます|Outlook で表示されます<br /><br />このラベルが適用された場合:<br /><br /> - 保護が以前にラベルによって適用されている場合、その保護は適用されず削除されます [[2]](#footnote-2) <br /><br />- 保護が以前にラベルから独立して適用されていた場合、その保護は保持されます|Outlook で表示されます<br /><br />このラベルが適用された場合:<br /><br />- 保護が以前にラベルによって適用されている場合、その保護は適用されず削除されます [[2]](#footnote-2) <br /><br />- 保護が以前にラベルから独立して適用されていた場合、その保護は保持されます [[1]](#footnote-1)|

###### <a name="footnote-1"></a>脚注 1:

Outlook では、保護は保持されます。ただし、暗号化のみのオプションで電子メールが保護されている場合、その保護は削除されます。


###### <a name="footnote-2"></a>脚注 2:

次の操作をサポートする使用権限またはロールをユーザーが持っている場合、保護は削除されます。
- [使用権限](configure-usage-rights.md#usage-rights-and-descriptions)エクスポートまたはフル コントロール。
- [Rights Management 発行者もしくは Rights Management 所有者](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)、または[スーパー ユーザー](configure-super-users.md)のロール。

ユーザーがこれらの使用権限またはロールをいずれも持っていない場合、ラベルは適用されず、元の保護が維持されます。


## <a name="to-migrate-azure-information-protection-labels"></a>Azure Information Protection ラベルを移行するには

次の手順を使用して、テナントと Azure Information Protection ラベルを移行し、統一されたラベル付けストアを使用するようにします。

ラベルを移行するには、コンプライアンス管理者、コンプライアンスデータ管理者、セキュリティ管理者、または全体管理者である必要があります。

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、 **[Azure Information Protection]** ペインに移動します。
    
    たとえば、リソース、サービス、ドキュメントの検索ボックスで、「**情報**の入力を開始し、 **[Azure Information Protection]** を選択します。

2. **[管理]** メニューオプションから、 **[統合ラベル]** を選択します。

3. **[Azure Information Protection 統合ラベル]** ウィンドウで、 **[アクティブ化]** を選択し、オンラインの指示に従います。
    
    アクティブ化するためのオプションが使用できない場合は、**統合ラベルの状態**を確認します。 [**アクティブ化**済み] が表示されている場合、テナントは既に統一されたラベル付けストアを使用しているため、ラベルを移行する必要はありません。

正常に移行されたラベルについては、[統合ラベル付けをサポートするクライアントおよびサービス](#clients-and-services-that-support-unified-labeling)で使用できるようになりました。 ただし、まず、Office 365 セキュリティ/コンプライアンスセンター、Microsoft 365 Security center、Microsoft 365 コンプライアンスセンターのいずれかの管理センターで[これらのラベルを発行](/microsoft-365/compliance/create-sensitivity-labels#publish-sensitivity-labels-by-creating-a-label-policy)する必要があります。

> [!IMPORTANT]
> Azure portal の外部にあるラベルを編集する場合は Azure Information Protection クライアント (クラシック) の場合は、この**Azure Information Protection の統合**されたラベル付けウィンドウに戻り、 **[発行]** を選択します。

### <a name="copy-policies"></a>ポリシーのコピー

> [!NOTE]
> このオプションはプレビュー段階であり、変更される可能性があります。

ラベルを移行したら、ポリシーをコピーするオプションを選択できます。 このオプションを選択すると、[ポリシー設定](configure-policy-settings.md)と[詳細なクライアント設定](./rms-client/client-admin-guide-customizations.md#available-advanced-client-settings)を含むポリシーの1回限りのコピーが、ラベルを管理する管理センター (Office 365 セキュリティ/コンプライアンスセンター、Microsoft 365 Security center、Microsoft 365 コンプライアンスセンター) に送信されます。 

ポリシーが設定されて正常にコピーされ、ラベルが、Azure portal のポリシーに割り当てられたユーザーとグループに自動的に発行されます。 グローバルポリシーでは、これはすべてのユーザーを意味します。 コピーしたポリシー内の移行されたラベルを公開する準備ができていない場合は、ポリシーをコピーした後で、管理者ラベルセンターのラベルポリシーからラベルを削除できます。

**[Azure Information Protection の統合ラベル]** ウィンドウで **[ポリシーのコピー (プレビュー)]** オプションを選択する前に、次の点に注意してください。

- テナントに対して統合ラベルをアクティブ化するまで、 **[ポリシーのコピー (プレビュー)]** オプションは使用できません。

- コピーするポリシーと設定を選択的に選択することはできません。 すべてのポリシー (**グローバル**ポリシーとスコープ付きポリシー) が自動的に選択されてコピーされ、ラベルポリシー設定としてサポートされているすべての設定がコピーされます。 同じ名前のラベルポリシーが既にある場合は、Azure portal のポリシー設定で上書きされます。

- Azure Information Protection 統合ラベル付けクライアントの場合、ポリシー設定ではなく*ラベルの詳細設定*としてサポートされるため、一部のアドバンストクライアント設定はコピーされません。 [Office 365 セキュリティ/コンプライアンスセンター PowerShell](./rms-client/clientv2-admin-guide-customizations.md#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用して、これらのラベルの詳細設定を構成できます。 コピーされないアドバンストクライアントの設定:
    - [LabelbyCustomProperty](./rms-client/client-admin-guide-customizations.md#migrate-labels-from-secure-islands-and-other-labeling-solutions)
    - [LabelToSMIME](./rms-client/client-admin-guide-customizations.md#configure-a-label-to-apply-smime-protection-in-outlook)

- ラベルへの後続の変更が同期されるラベルの移行とは異なり、 **[ポリシーのコピー]** アクションでは、ポリシーまたはポリシー設定に対する後続の変更は同期されません。 Azure portal に変更を加えた後、[ポリシーのコピー] アクションを繰り返すと、既存のポリシーとその設定が再度上書きされます。 または、Office 365 セキュリティ/コンプライアンスセンター PowerShell の *[設定] パラメーターを*使用して、Set labelpolicy または Set-label コマンドレットを使用します。

- ポリシーの**コピー**操作では、ポリシーがコピーされる前に、次のことを確認します。
    
    - ポリシーに割り当てられているユーザーとグループは、現在 Azure AD にあります。 1つまたは複数のアカウントがない場合、ポリシーはコピーされません。 グループメンバーシップは確認されません。
    
    - グローバルポリシーに少なくとも1つのラベルが含まれています。 管理者ラベル付けセンターではラベルのないラベルポリシーはサポートされていないため、ラベルのないグローバルポリシーはコピーされません。

- ポリシーをコピーして管理者ラベルセンターから削除した場合は、 **[ポリシーのコピー]** アクションをもう一度実行してから、削除がレプリケートされるのに十分な時間を確保してから、少なくとも2時間待機してください。

- Azure Information Protection からコピーされたポリシーの名前は同じではなく、 **AIP_** のプレフィックスを使用して名前が付けられます。 ポリシー名を後で変更することはできません。 

Azure Information Protection の統一されたラベル付けクライアントのポリシー設定、クライアントの詳細設定、およびラベル設定の構成の詳細については、管理者ガイドの「 [Azure Information Protection 統合ラベル付けクライアントのカスタム構成](./rms-client/clientv2-admin-guide-customizations.md)」を参照してください。

### <a name="clients-and-services-that-support-unified-labeling"></a>統合ラベル付けをサポートするクライアントおよびサービス

使用するクライアントとサービスが、統一されたラベル付けをサポートしているかどうかを確認するには、ドキュメントを参照して、管理センターの1つから発行された機密ラベルを使用できるかどうかを確認します。 Office 365 セキュリティ/コンプライアンスセンター、Microsoft 365security center または Microsoft 365 コンプライアンスセンター。 

##### <a name="clients-that-currently-support-unified-labeling-include"></a>現在、統合ラベル付けをサポートしているクライアント:

- [Windows 用の Azure Information Protection 統合ラベル付け](./rms-client/unifiedlabelingclient-version-release-history.md)されたクライアント。 このクライアントと Azure Information Protection クライアント (クラシック) の比較については、「 [Windows コンピューターのラベル付けクライアントの比較](./rms-client/use-client.md#compare-the-labeling-clients-for-windows-computers)」を参照してください。

- 可用性の段階が異なる Office からのアプリ。 詳細については、Microsoft 365 の準拠に関するドキュメントの「[アプリでの機密ラベル機能のサポート](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps)」を参照してください。
    
- [Microsoft Information Protection SDK](https://docs.microsoft.com/information-protection/develop/overview) を使用しているソフトウェア ベンダーおよび開発者からのアプリです。

##### <a name="services-that-currently-support-unified-labeling-include"></a>現在、統合ラベル付けをサポートしているサービス:

- [Power BI (プレビュー)](https://docs.microsoft.com/power-bi/admin/service-security-data-protection-overview)

- Office Online (プレビュー中) および Outlook (web 上)

- SharePoint Online、OneDrive for Business、Microsoft Teams、Office 365 グループ (プレビュー)
    
    詳細については、「 [Microsoft Teams、office 365 グループ、sharepoint サイトでの秘密度ラベルの使用 (パブリックプレビュー)](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-teams-groups-sites) 」および「 [sharepoint と OneDrive での Office ファイルの秘密度ラベルの有効化 (パブリックプレビュー)](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files)」を参照してください。

- Microsoft Defender Advanced Threat Protection

- Microsoft Cloud App Security
    
    このサービスでは、統合ラベル付けストアに移行する前と後の両方で、次のロジックを使用してラベルがサポートされます。
    
    - 管理センターに機密ラベルがある場合、これらのラベルは管理センターから取得されます。 Cloud App Security でこれらのラベルを選択するには、少なくとも 1 つのユーザーに少なくとも 1 つのラベルを発行する必要があります。
    
    - 管理センターに機密ラベルがない場合は、Azure Information Protection ラベルが Azure portal から取得されます。

- [Microsoft Information Protection SDK](https://docs.microsoft.com/information-protection/develop/overview) を使用しているソフトウェア ベンダーおよび開発者からのサービスです。

## <a name="next-steps"></a>次のステップ:

カスタマーエクスペリエンスチームのその他のガイダンスとヒントについては、次のリソースを参照してください。

- ブログの投稿: 統合された[ラベル付けの移行につい](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Understanding-Unified-Labeling-migration/ba-p/783185)て

- ウェビナー:[ラベル記録、デッキ、faq の統合](https://github.com/nihendle/MIP-Comp/tree/master/MIP/Webinars/Unified%20Labeling%20Migration)

ラベル管理センターで構成および発行できるようになった移行済みラベルの詳細については、「[感度ラベルについて](/microsoft-365/compliance/sensitivity-labels)」および「[秘密度ラベルとそのポリシーの作成と構成](https://docs.microsoft.com/microsoft-365/compliance/create-sensitivity-labels)」を参照してください。

まだインストールしていない場合は、Azure Information Protection 統合されたラベル付けクライアントをインストールします。 リリース情報、管理者ガイド、およびユーザーガイドについては、「 [Windows 用の統合ラベルクライアント Azure Information Protection](./rms-client/aip-clientv2.md)」を参照してください。
