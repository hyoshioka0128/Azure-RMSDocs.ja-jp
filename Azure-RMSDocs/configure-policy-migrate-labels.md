---
title: Azure Information Protection ラベルを Office 365 セキュリティ/コンプライアンス センターに移行する
description: 統合ラベル付けをサポートしているクライアントで Azure Information Protection ラベルを Office 365 セキュリティ/コンプライアンス センターに移行する
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/06/2018
ms.topic: article
ms.service: information-protection
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: 771cbb26a842cbf19184ace94ae47ba9d549a33f
ms.sourcegitcommit: b4118cd75db6478f86b9994e8d84d0ada15c7f95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2018
ms.locfileid: "52953331"
---
# <a name="how-to-migrate-azure-information-protection-labels-to-the-office-365-security--compliance-center"></a>Azure Information Protection ラベルを Office 365 セキュリティ/コンプライアンス センターに移行する方法

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

> [!IMPORTANT]
> この機能はプレビュー段階にあり、やはりプレビュー段階にある新しいプラットフォームにテナントが移行されます。 移行を元に戻すことはできません。 新しいプラットフォームでは統合ラベル付けがサポートされており、作成し、管理するラベルは複数のクライアントやサービスで使用できます。

Office 365 セキュリティ/コンプライアンス センターで使用できるようにする場合、ラベルを移行します。Office 365 セキュリティ/コンプライアンス センターでは、[統合ラベル付けをサポートしているクライアント](#clients-that-support-unified-labeling)でラベルを公開し、ダウンロードできます。 Azure Information Protection クライアントでは引き続き、Azure portal から Azure Information Protection ポリシーでラベルがダウンロードされます。 

移行後のラベルは Azure portal または Office 365 セキュリティ/コンプライアンス センターで変更できます。個々のクライアントで同じ変更内容がダウンロードされます。

### <a name="important-information-about-administrative-roles"></a>管理者ロールに関する重要な情報

**セキュリティ管理者**と **Information Protection 管理者**の [Azure AD ロール](/active-directory/users-groups-roles/directory-assign-admin-roles)は、統合ラベル付けのプラットフォームではサポートされていません。 組織でこれらの管理者ロールを使用する場合は、ラベルを移行する前に、これらのロールを持つユーザーを、Office 365 セキュリティ/コンプライアンス センターの**コンプライアンス管理者**ロール グループまたは**組織管理**ロール グループに追加しておきます。 代わりに、これらのユーザー用の新しいロール グループを作成して、このグループに**保持管理**、**組織の構成**のどちらのロールでも追加できます。 手順については、「[Give users access to the Office 365 Security & Compliance Center](https://docs.microsoft.com/office365/securitycompliance/grant-access-to-the-security-and-compliance-center)」(Office 365 セキュリティ/コンプライアンス センターへのアクセス権をユーザーに付与する) をご覧ください。

これらの構成のいずれかを使用して各ユーザーに 365 セキュリティ/コンプライアンス センターへのアクセス権を付与しないと、ラベルの移行後に各ユーザーは Azure portal でラベルとポリシーにアクセスできなくなります。

ラベルの移行後でも、テナントのグローバル管理者は Azure portal およびセキュリティ/コンプライアンス センターの両方でラベルとポリシーの管理を続けられます。


## <a name="considerations-for-unified-labels"></a>統合ラベルに関する考慮事項

ラベルを移行する前に、次の変更内容と考慮事項に注意してください。

- 現在のところ、一部のクライアントでは統合ラベルがサポートされていません。 [サポートされているクライアント](#clients-that-support-unified-labeling)を用意し、Azure portal (統合ラベルをサポートしていないクライアント用) とセキュリティ/コンプライアンス センター (統合ラベルをサポートしているクライアント用) の両方での管理のための準備をしてください。

- 使用するラベルを定義し、構成している最中であれば、Azure portal でこのプロセスを完了し、ラベルを移行することをお勧めします。 この方針によって、移行プロセス中にラベル重複が回避されます。ラベルが重複すると、セキュリティ/コンプライアンス センターで編集しなければなりません。

- ポリシーとすべてのクライアント詳細設定は移行されません。移行されないポリシーには、ポリシー設定とそれにアクセスできるユーザーが含まれます (スコープ付きポリシー)。 移行されない変更については、ラベルの移行後、セキュリティ/コンプライアンス センターで関連オプションを構成する必要があります。
    
    操作における一貫性を上げるために、セキュリティ/コンプライアンス センターでは同じスコープで同じラベルを公開することをお勧めします。

- セキュリティ/コンプライアンス センターでは、移行されたラベルの一部の設定がサポートされません。 セキュリティ/コンプライアンス センターでサポートされていないない設定を確認するには、「[セキュリティ/コンプライアンス センターでサポートされていないラベル設定](#label-settings-that-are-not-supported-in-the-security--compliance-center)」セクションの表を使います。

- 保護テンプレート:
    
    - クラウドベースのキーを使用し、ラベル構成に含まれるテンプレートもラベルと共に移行されます。 その他の保護テンプレートは移行されません。 
    
    - クラウドベースの保護設定のあるラベルが移行されると、保護テンプレートの結果的に生成されるスコープは、Azure portal で (あるいは、AADRM PowerShell モジュールを使用することで) 定義されるスコープであり、セキュリティ/コンプライアンス センターで定義されるスコープとなります。 

- ラベルを移行すると、移行結果にラベルが**作成された**か、**更新された**か、重複のため、**名前が変更**されたかが表示されます。

    - ラベルを作成したら、それをアプリケーションやサービスで利用できるようにするにはセキュリティ/コンプライアンス センターでラベルを公開する必要があります。
    
    - ラベルの名前が変更された場合、セキュリティ/コンプライアンス センターまたは Azure portal で編集する必要があります。 

- Azure portal では、各ラベルのラベル表示名のみが表示されます。この名前は編集できます。 セキュリティ/コンプライアンス センターには、ラベルのこの表示名とラベル名の両方が表示されます。 ラベル名は、ラベルが最初に作成されたときに指定した最初の名前です。このプロパティは、識別目的でバックエンド サービスによって使用されます。

- ラベルのローカライズされた文字列は移行されません。 セキュリティ/コンプライアンス センターで、移行されたラベルに対してローカライズされた文字列を新しく定義する必要があります。

- 移行後、移行したラベルを Azure portal で編集すると、セキュリティ/コンプライアンス センターで同じ変更内容が自動的に反映されます。 ただし、セキュリティ/コンプライアンス センターに移行したラベルを編集する場合は、Azure portal に戻って、**[Azure Information Protection - 統合ラベル付け]** ブレードで **[公開]** を選ぶ必要があります。 Azure Information Protection クライアントでラベルの変更を認識させるには、この追加のアクションが必要です。

### <a name="label-settings-that-are-not-supported-in-the-security--compliance-center"></a>セキュリティ/コンプライアンス センターでサポートされていないラベル設定

次の表を使って、移行されたラベルのどの構成設定が統合ラベル付けのクライアントにサポートされていないのか、または制限付きでサポートされているのかを識別します。 混乱を避けるために、統合ラベル付けのクライアントに影響がない設定は構成しないことをお勧めします。

Azure Information Protection クライアントでは、何の問題もなく、このようなラベル設定を使用できます。Azure portal から引き続きラベルをダウンロードするためです。

|ラベル構成|統合ラベル付けのクライアントによるサポート|セキュリティ/コンプライアンス センターで編集から除外する|
|-------------------|---------------------------------------------|-------------------------|
|有効または無効の状態<br /><br />注: セキュリティ/コンプライアンス センターには同期されません |適用できません|適用できません|
|ラベルの色: 一覧から選択するか、RGB コードを使用して指定します<br /><br />注: ラベルの色はセキュリティ/コンプライアンス センターではサポートされていません |適用できません|適用できません|
|事前定義テンプレートを使用するクラウドベースの保護または HYOK ベースの保護 |[いいえ]|はい|
|Word、Excel、PowerPoint でユーザー定義のアクセス許可を使用するクラウドベースの保護 |[いいえ]|はい|
|[転送不可] に関する Outlook のユーザー定義のアクセス許可を使用する HYOK ベースの保護 |[いいえ]|はい|
|保護を解除する |[いいえ]|はい|
|視覚的なマーキング (ヘッダー、フッター、透かし): カスタム フォントと RGB コードによるカスタム フォントの色|[いいえ]|変数の使用時に推奨<br /><br />- クライアントでは、変数は動的な値ではなく、テキストとして表示されます|
|アプリごとの視覚的なマーキング|[いいえ]|変数の使用時に推奨<br /><br />- クライアントでは、変数は動的な値ではなく、テキストとして表示されます|
|条件と関連設定 <br /><br />注: 自動の推奨ラベル付けとそのツールヒントが含まれます|適用できません|[いいえ]|


## <a name="to-migrate-azure-information-protection-labels"></a>Azure Information Protection ラベルを移行するには

次の手順に従い、テナントと Azure Information Protection ラベルを移行して、統合ラベル付けの新しいストアを使います。

ラベルを移行するには、グローバル管理者である必要があります。

1. 新しいブラウザー ウィンドウを開き、次のリンクから Azure portal にサインインします。 https://portal.azure.com/?ActivateMigration=true#blade/Microsoft_Azure_InformationProtection/DataClassGroupEditBlade/migrationActivationBlade 

2. **[Azure Information Protection - 統合ラベル付け]** ブレードで **[有効化]** を選択し、オンライン指示に従います。

正常に移行できたラベルは、[統合ラベル付けをサポートするクライアント](#clients-that-support-unified-labeling)で使用できます。 ただし、最初にセキュリティ/コンプライアンス センターでラベルを公開する必要があります。

> [!IMPORTANT]
> Azure Information Protection クライアントに対して、Azure portal の外部でラベルを編集する場合、この **[Azure Information Protection - 統合ラベル付け]** ブレードに戻り、**[公開]** を選びます。

### <a name="clients-that-support-unified-labeling"></a>統合ラベル付けをサポートするクライアント

現在、統合ラベル付けをサポートしているクライアント:

- [Windows 用 Azure Information Protection 統合ラベル付けクライアント](./rms-client/unifiedlabelingclient-version-release-history.md) - プレビュー

- Office Insiders プログラムからのアプリ。 詳細については、Office ドキュメントの「[現在、機能はどこで入手できますか?](https://support.office.com/article/2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9?ad=US#bkmk_whereavailable)」セクションを参照してください。
    
- [MIP SDK](https://docs.microsoft.com/azure/information-protection/develop/mip/mip-sdk-reference) を使用するソフトウェア ベンダー/開発者からのクライアント。


## <a name="next-steps"></a>次の手順

Office 365 セキュリティ/コンプライアンス センターで構成および公開できるようになった移行済みラベルについては、「[機密ラベルの概要](/Office365/SecurityCompliance/sensitivity-labels)」をご覧ください。

発表については、ブログ記事「[Announcing the availability of unified labeling management in the Security & Compliance Center](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492)」(セキュリティ/コンプライアンス センターにおける統合ラベル付けの管理の発表) をご覧ください。