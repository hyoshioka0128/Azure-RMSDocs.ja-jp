---
title: Azure Information Protection ラベルを Office 365 セキュリティ/コンプライアンス センターに移行する - AIP
description: 統合ラベル付けをサポートしているクライアントで Azure Information Protection ラベルを Office 365 セキュリティ/コンプライアンス センターに移行する
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 03/14/2019
ms.topic: article
ms.collection: M365-security-compliance
ms.service: information-protection
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: ed3c77df8da01a4b87b30875a315eac5c075b438
ms.sourcegitcommit: d716d3345a6a5adc63814dee28f7c01b55b96770
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2019
ms.locfileid: "57829061"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-the-office-365-security--compliance-center"></a>Azure Information Protection ラベルを Office 365 セキュリティ/コンプライアンス センターに移行する方法

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!IMPORTANT]
> この機能はプレビュー段階にあり、新しいプラットフォームにテナントが移行されます。 移行を元に戻すことはできません。 新しいプラットフォームでは統合ラベル付けがサポートされいます。このため、作成し管理するラベルを、[Microsoft Information Protection](faqs.md#whats-the-difference-between-azure-information-protection-and-microsoft-information-protection) ソリューションをサポートするクライアントおよびサービスで使用できます。

ご自分のラベルを Office 365 セキュリティ/コンプライアンス センターから Office 365 機密ラベルとして使用できるようにしたい場合は、[統合ラベル付けをサポートしているクライアントおよびサービス](#clients-and-services-that-support-unified-labeling)で使用されるようにラベルを移行します。 移行後、Azure Information Protection クライアントによって、引き続き Azure portal からラベルとその Azure Information Protection ポリシーがダウンロードされます。 

ラベルを移行する方法についての詳細な手順を読む前に、次のよく寄せられる質問が役立つ場合があります。

- [Azure Information Protection のラベルと Office 365 のラベルにはどのような違いがありますか。](faqs.md#whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365)

- [Office 365 にラベルを移行する適切なタイミングはいつですか。](faqs.md#when-is-the-right-time-to-migrate-my-labels-to-office-365)

- [ラベルを移行した後に使用する管理ポータルはどれですか。](faqs.md?#after-ive-migrated-my-labels-which-management-portal-do-i-use )

### <a name="important-information-about-administrative-roles"></a>管理者ロールに関する重要な情報

**セキュリティ管理者**と **Information Protection 管理者**の [Azure AD ロール](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)は、統合ラベル付けのプラットフォームではサポートされていません。 組織でこれらの管理者ロールを使用する場合は、ラベルを移行する前に、これらのロールを持つユーザーを、Office 365 セキュリティ/コンプライアンス センターの**コンプライアンス管理者**ロール グループまたは**組織管理**ロール グループに追加しておきます。 代わりに、これらのユーザー用の新しいロール グループを作成して、このグループに**保持管理**、**組織の構成**のどちらのロールでも追加できます。 手順については、「[Give users access to the Office 365 Security & Compliance Center](https://docs.microsoft.com/office365/securitycompliance/grant-access-to-the-security-and-compliance-center)」(Office 365 セキュリティ/コンプライアンス センターへのアクセス権をユーザーに付与する) をご覧ください。

これらの構成のいずれかを使用して各ユーザーに 365 セキュリティ/コンプライアンス センターへのアクセス権を付与しないと、ラベルの移行後に各ユーザーは Azure portal でラベルとポリシーにアクセスできなくなります。

ラベルの移行後も、テナントのグローバル管理者は Azure portal およびセキュリティ/コンプライアンス センターの両方でラベルとポリシーの管理を続けられます。


## <a name="considerations-for-unified-labels"></a>統合ラベルに関する考慮事項

ラベルを移行する前に、次の変更内容と考慮事項に注意してください。

- 現在のところ、一部のクライアントでは統合ラベルがサポートされていません。 [サポートされているクライアント](#clients-and-services-that-support-unified-labeling)を用意し、Azure portal (統合ラベルをサポートしていないクライアント用) とセキュリティ/コンプライアンス センター (統合ラベルをサポートしているクライアント用) の両方での管理のための準備をしてください。

- 使用するラベルを定義し、構成している最中であれば、Azure portal でこのプロセスを完了し、ラベルを移行することをお勧めします。 この方針によって、移行プロセス中にラベル重複が回避されます。ラベルが重複すると、セキュリティ/コンプライアンス センターで編集しなければなりません。

- ポリシーとすべてのクライアント詳細設定は移行されません。移行されないポリシーには、ポリシー設定とそれにアクセスできるユーザーが含まれます (スコープ付きポリシー)。 移行されない変更については、ラベルの移行後、セキュリティ/コンプライアンス センターで関連オプションを構成する必要があります。
    
    操作における一貫性を上げるために、セキュリティ/コンプライアンス センターでは同じスコープで同じラベルを公開することをお勧めします。

- セキュリティ/コンプライアンス センターでは、移行されたラベルの一部の設定がサポートされません。 「[セキュリティ/コンプライアンス センターでサポートされていないラベル設定](#label-settings-that-are-not-supported-in-the-security--compliance-center)」セクションに記載された表を使用すると、それらの設定と推奨される一連の措置を容易に確認できます。

- 保護テンプレート:
    
    - クラウドベースのキーを使用し、ラベル構成に含まれるテンプレートもラベルと共に移行されます。 その他の保護テンプレートは移行されません。 
    
    - 定義済みのテンプレート用に構成されたラベルがある場合、ラベルを移行する前に[これらのテンプレートをラベルに変換](configure-policy-templates.md#to-convert-templates-to-labels)します。 この構成はラベルの移行をブロックしませんが、セキュリティ/コンプライアンス センターではサポートされていません。
    
    - クラウドベースの保護設定のあるラベルが移行されると、保護テンプレートの結果的に生成されるスコープは、Azure portal で (あるいは、AADRM PowerShell モジュールを使用することで) 定義されるスコープであり、セキュリティ/コンプライアンス センターで定義されるスコープとなります。 

- ラベルを移行すると、移行結果にラベルが**作成された**か、**更新された**か、重複のため、**名前が変更**されたかが表示されます。

    - ラベルを作成したら、それをアプリケーションやサービスで利用できるようにするにはセキュリティ/コンプライアンス センターでラベルを公開する必要があります。
    
    - ラベルの名前が変更された場合、セキュリティ/コンプライアンス センターまたは Azure portal で編集する必要があります。 

- Azure portal では、各ラベルのラベル表示名のみが表示されます。この名前は編集できます。 セキュリティ/コンプライアンス センターには、ラベルのこの表示名とラベル名の両方が表示されます。 ラベル名は、ラベルが最初に作成されたときに指定した最初の名前です。このプロパティは、識別目的でバックエンド サービスによって使用されます。

- ラベルのローカライズされた文字列は移行されません。 セキュリティ/コンプライアンス センターで、移行されたラベルに対してローカライズされた文字列を新しく定義する必要があります。

- 移行後、移行したラベルを Azure portal で編集すると、セキュリティ/コンプライアンス センターで同じ変更内容が自動的に反映されます。 ただし、セキュリティ/コンプライアンス センターに移行したラベルを編集する場合は、Azure portal に戻って、**[Azure Information Protection - 統合ラベル付け]** ブレードで **[公開]** を選ぶ必要があります。 Azure Information Protection クライアントでラベルの変更を認識させるには、この追加のアクションが必要です。

### <a name="label-settings-that-are-not-supported-in-the-security--compliance-center"></a>セキュリティ/コンプライアンス センターでサポートされていないラベル設定

次の表を使用すると、移行されたラベルのうちセキュリティ/コンプライアンス センターでサポートされていない構成設定を識別できます。 そのような設定が含まれているラベルがある場合は、移行の完了時に、最後の列にある管理ガイダンスを確認してから Office 365 セキュリティ/コンプライアンス センターでご自分のラベルを発行してください。

Azure Information Protection クライアントでは、一覧表示されているラベル設定をすべて何の問題もなく使用できます。これは Azure portal から引き続きラベルがダウンロードされるからです。

|ラベル構成|統合ラベル付けのクライアントによるサポート| セキュリティ/コンプライアンス センターのガイダンス|
|-------------------|---------------------------------------------|-------------------------|
|有効または無効の状態<br /><br />注:セキュリティ/コンプライアンス センターには同期されません |適用できません|ラベルが発行されているかどうかに対応します。 |
|一覧から選択するか、RGB コードを使用して指定するラベルの色 |はい|ラベルの色に対する構成オプションはありません。 代わりに、Azure portal でラベルの色を構成できます。|
|事前定義テンプレートを使用するクラウドベースの保護または HYOK ベースの保護 |[いいえ]|事前に定義されたテンプレート用の構成オプションはありません。 この構成を使用してラベルを発行することはお勧めしません。|
|Word、Excel、PowerPoint に対するユーザー定義のアクセス許可を使用するクラウドベースの保護 |[いいえ]|これらの Office アプリ用のユーザー定義のアクセス許可については構成オプションはありません。 この構成を使用してラベルを発行することはお勧めしません。|
|Outlook のユーザー定義のアクセス許可を使用する HYOK ベースの保護 ([転送不可]) |[いいえ]|HYOK に対する構成オプションはありません。 この構成を使用してラベルを発行することはお勧めしません。|
|保護を解除する |[いいえ]|保護を削除するための構成オプションはありません。 この構成を使用してラベルを発行することはお勧めしません。<br /><br /> このラベルを発行した場合、それが適用されると、保護は以前にラベルによって適用されていた場合は削除されます。 保護が以前にラベルから独立して適用されていた場合、保護は保持されます。|
|視覚的なマーキング (ヘッダー、フッター、透かし) 向けのカスタム フォントと RGB コードによるカスタム フォントの色|はい|視覚的なマーキングの構成は、色とフォント サイズの一覧に限定されます。 構成した値がセキュリティ/コンプライアンス センターで確認できなくても、このラベルは変更なしで発行することができます。 <br /><br />これらのオプションを変更するには、Azure portal を使用します。 しかし、管理をより簡単にするには、セキュリティ/コンプライアンス センターに一覧されるオプションのいずれかに、色を変更することを検討してください。|
|視覚的なマーキングの変数 (ヘッダー、フッター)|[いいえ]|変更なしでこのラベルを発行した場合、変数は動的な値を表示するのでなく、クライアント上でテキストとして表示されます。 ラベルを発行する前に、文字列を編集して変数を削除してください。|
|アプリごとの視覚的なマーキング|[いいえ]|変更なしでこのラベルを発行した場合、アプリ変数は、選択したアプリ上にご利用のテキスト文字列を表示するのでなく、クライアント上ですべてのアプリにテキストとして表示されます。 このラベルはすべてのアプリに適している場合にのみ発行します。文字列を編集してアプリ変数を削除します。|
|条件と関連設定 <br /><br />注:自動の推奨ラベル付けとそのヒントが含まれます|適用できません|自動ラベル付けを使用して、ラベル設定とは個別の構成としてご自分の条件を再構成します。|


## <a name="to-migrate-azure-information-protection-labels"></a>Azure Information Protection ラベルを移行するには

次の手順に従い、テナントと Azure Information Protection ラベルを移行して、統合ラベル付けの新しいストアを使います。

ラベルを移行するには、グローバル管理者である必要があります。

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、**[Azure Information Protection]** ブレードに移動します。
    
    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. **[管理]** メニュー オプションから **[統合ラベル付け (プレビュー)]** を選択します。

3. **[Azure Information Protection - 統合ラベル付け]** ブレードで **[有効化]** を選択し、オンライン指示に従います。

正常に移行されたラベルについては、[統合ラベル付けをサポートするクライアントおよびサービス](#clients-and-services-that-support-unified-labeling)で使用できるようになりました。 ただし、最初にセキュリティ/コンプライアンス センターでラベルを公開する必要があります。

> [!IMPORTANT]
> Azure Information Protection クライアントに対して、Azure portal の外部でラベルを編集する場合、この **[Azure Information Protection - 統合ラベル付け]** ブレードに戻り、**[公開]** を選びます。

### <a name="clients-and-services-that-support-unified-labeling"></a>統合ラベル付けをサポートするクライアントおよびサービス

使用しているクライアントとサービスによって統合ラベル付けがサポートされているかどうかを確認するには、該当するドキュメントを参照して、Office 365 セキュリティ/コンプライアンス センターから発行された機密ラベルをそれらで使用できるかどうかを確認してください。 

##### <a name="clients-that-currently-support-unified-labeling-include"></a>現在、統合ラベル付けをサポートしているクライアント: 

- [Windows 用 Azure Information Protection 統合ラベル付けクライアント](./rms-client/unifiedlabelingclient-version-release-history.md) - プレビュー

- 可用性の段階が異なる Office からのアプリ。 詳細については、Office ドキュメントの「[Office 内の文書やメールに機密ラベルを適用する](https://support.office.com/en-us/article/apply-sensitivity-labels-to-your-documents-and-email-within-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9)」から「**現在、機能はどこで入手できますか?**」のセクションを参照してください。
    
- [Microsoft Information Protection SDK](https://docs.microsoft.com/en-us/information-protection/develop/overview) を使用しているソフトウェア ベンダーおよび開発者からのアプリです。

##### <a name="services-that-currently-support-unified-labeling-include"></a>現在、統合ラベル付けをサポートしているサービス: 

- Windows Defender Azure Threat Protection

- Microsoft Cloud App Security
    
    このサービスでは、統合ラベル付けストアに移行する前と後の両方で、次のロジックを使用してラベルがサポートされます。
    
    - Azure portal にあるのと同じラベルが Office 365 セキュリティ/コンプライアンス センターに存在する場合: 統合ラベルは Office 365 セキュリティ/コンプライアンス センターから取得されます。 Cloud App Security でこれらのラベルを選択するには、少なくとも 1 つのユーザーに少なくとも 1 つのラベルを発行する必要があります。
    
    - Azure portal にあるのと同じラベルが Office 365 セキュリティ/コンプライアンス センターに存在しない場合: 統合ラベルは Office 365 セキュリティ/コンプライアンス センターからは使用されません。代わりに、ラベルは Azure portal から取得されます。

- [Microsoft Information Protection SDK](https://docs.microsoft.com/en-us/information-protection/develop/overview) を使用しているソフトウェア ベンダーおよび開発者からのサービスです。

## <a name="next-steps"></a>次の手順

Office 365 セキュリティ/コンプライアンス センターで構成および公開できるようになった移行済みラベルについては、「[機密ラベルの概要](/Office365/SecurityCompliance/sensitivity-labels)」をご覧ください。

発表については、ブログ記事「[Announcing the availability of unified labeling management in the Security & Compliance Center](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492)」 (セキュリティ/コンプライアンス センターにおける統合ラベル付けの管理の発表) をご覧ください。
