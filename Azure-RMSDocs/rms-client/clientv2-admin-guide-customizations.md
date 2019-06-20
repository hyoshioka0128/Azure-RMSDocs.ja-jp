---
title: カスタムの構成 - Azure Information Protection ラベル付けのクライアントの統合
description: Windows 用 Azure Information Protection の統合されたラベル付けクライアントのカスタマイズに関する情報。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/20/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.reviewer: maayan
ms.suite: ems
ms.openlocfilehash: 1dbd1589a9e3aaec39b13f553f6ce3af6107ce02
ms.sourcegitcommit: a26e4e50165107efd51280b5c621dfe74be51a7a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2019
ms.locfileid: "67236912"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-unified-labeling-client"></a>管理者ガイド: Azure Information Protection の統合されたラベル付けクライアントのカスタム構成

>*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2*
>
> *手順:[Azure Information Protection unified Windows 用のラベル付けのクライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection の統合されたラベル付けクライアントを管理するときに、特定のシナリオまたはユーザーのサブセットは必要な高度な構成の次の情報を使用します。

これらの設定では、Office 365 セキュリティ/コンプライアンス センターの PowerShell を使用しての詳細設定のレジストリを編集またはを指定する必要があります。

### <a name="how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell"></a>Office 365 セキュリティ/コンプライアンス センターの PowerShell を使用して、クライアントの高度な設定を構成する方法

使用すると[Office 365 セキュリティ/コンプライアンス センターの PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/office-365-scc-powershell?view=exchange-ps)ポリシーのラベルとラベルのカスタマイズをサポートする高度な設定を構成することができます。 以下に例を示します。

- Office アプリで Information Protection バーを表示する設定は、***ポリシー設定の詳細にラベルを付ける***します。
- ラベルの色を指定する設定は、***ラベルの設定を高度な***します。

どちらの場合も、指定した、 *AdvancedSettings*ポリシーまたはラベルの id (名前または GUID) を持つパラメーターでキー/値ペアを指定し、[ハッシュ テーブル](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_hash_tables)、次の構文を使用します。

ラベルのポリシー設定では、単一の文字列値を。

    Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key="value1,value2"}

ラベルのポリシー設定について複数の文字列は、同じキーの値します。

    Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}

ラベルの設定では、単一の文字列値を。

    Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key="value1,value2"}

ラベルの設定、同じキーに対して複数の文字列値。

    Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}

高度な設定を削除するには、のと同じ構文を使用して、null 文字列値を指定します。


#### <a name="examples-for-setting-advanced-settings"></a>高度な設定を設定する例

例 1 : 1 つの文字列値の設定を高度なラベルのポリシーを設定します。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}

例 2:1 つの文字列値の設定を高度なラベルを設定します。

    Set-Label -Identity Internal -AdvancedSettings @{smimesign="true"}

例 3: 複数の文字列値の設定を高度なラベルを設定します。

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}

例 4:設定を null 文字列値を指定することで高度なラベル ポリシーを削除します。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions=""}

#### <a name="specifying-the-identity-for-the-label-policy-or-label"></a>ポリシーのラベルまたはラベルの id を指定します。

PowerShell のラベルのポリシー名を指定する*Identity*ラベルのポリシーを管理する管理センターでポリシー名を 1 つだけを表示するために、パラメーターは簡単です。 ただし、ラベルの表示両方、**名前**と**表示名**管理ツールで中央揃えにします。 場合によっては、両方の値は同じになりますが、異なる可能性があります。

- **名前**ラベルの元の名前であり、すべてのラベルの間で一意であります。 作成後に、ラベルの名前を変更する場合は、この値は変わりません。

- **表示名**ユーザーに表示され、すべてのラベルで一意である必要はありませんが、ラベルの名前を指定します。 たとえば、ユーザーが 1 つ表示**すべての従業員**の sublabel、**社外秘**ラベル、および別**すべての従業員**の sublabel、**機密性の高い**ラベル。 これらのサブラベル両方が、同じ名前を表示、同じラベルではなく、さまざまな設定があります。

詳細設定については、ラベルを構成するには、使用、**名前**値。 たとえば、次の図のラベルを特定するには指定した`-Identity "All Company"`:

!['表示名' ではなく 'Name' を使用して機密ラベルを識別するために](../media/labelname_scc.png)

ラベルの GUID を指定する場合は、この値は、ラベルを管理する管理センターでは表示されません。 ただし、この値を検索するのに次の Office 365 セキュリティ/コンプライアンス センターの PowerShell コマンドを使用できます。

    Get-Label | Format-Table -Property DisplayName, Name, Guid


#### <a name="order-of-precedence---how-conflicting-settings-are-resolved"></a>優先順位の設定は、解決された競合する方法

秘密度ラベルを管理する管理センターのいずれかを使用して、次のラベルのポリシー設定を構成できます。

- **ドキュメントや電子メールに既定ではこのラベルを適用します。**

- **ユーザーの正当性を提供する必要がありますラベルまたは下位の分類ラベルを削除します。**

- **ユーザーの電子メールやドキュメントにラベルを適用する必要があります。**

- **カスタム ヘルプ ページへのリンクをユーザーに提供します。**

ユーザーのラベルの 1 つ以上のポリシーが構成されると、それぞれに異なる可能性のあるポリシー設定では、最後のポリシー設定が適用されます、管理センターでポリシーの順序。 詳細については、次を参照してください[ポリシーの優先順位 (順序が重要です) にラベルを付ける。](https://docs.microsoft.com/Office365/SecurityCompliance/sensitivity-labels#label-policy-priority-order-matters)

ラベルの詳細設定では、優先順位の同じロジックに従います。ラベルに複数のポリシーでは、ラベルは、そのラベルが 詳細設定、最後の高度な設定は、管理センターでポリシーの順序に従って適用されます。

高度な設定が逆の順序で適用されるポリシーのラベルを付けます。1 つの例外を除き、管理センターでポリシーの順序に従って、最初のポリシーから高度な設定は適用されます。 例外は、高度な設定*OutlookDefaultLabel*Outlook のさまざまな既定のラベルを設定します。 このラベルのポリシーの高度な設定のみ、最後の設定が適用されます、管理センターでポリシーの順序。

#### <a name="available-advanced-settings-for-label-policies"></a>ラベルのポリシーの詳細設定を利用可能

|設定|シナリオと手順|
|----------------|---------------|
|AttachmentAction|[添付ファイルのある電子メール メッセージの場合、その添付ファイルの最上位の分類と一致するラベルを適用します](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)
|AttachmentActionTip|[添付ファイルのある電子メール メッセージの場合、その添付ファイルの最上位の分類と一致するラベルを適用します](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments) 
|EnableCustomPermissions|[ファイル エクスプ ローラーでのカスタム アクセス許可を無効にします。](#disable-custom-permissions-in-file-explorer)|
|EnableCustomPermissionsForCustomProtectedFiles|[カスタム アクセス許可で保護されているファイルについて、ファイル エクスプローラーでカスタム アクセス許可を常にユーザーに表示する](#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer) |
|EnableLabelByMailHeader|[Secure Islands からのラベルの移行と、その他のラベル付けのソリューション](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|labelByCustomProperties|[Secure Islands からのラベルの移行と、その他のラベル付けのソリューション](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|LogMatchedContent|[ユーザーのサブセットに対して送信情報の種類の一致を無効にする](#disable-sending-information-type-matches-for-a-subset-of-users)|
|OutlookBlockTrustedDomains|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookBlockUntrustedCollaborationLabel|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookDefaultLabel|[Outlook に別の既定ラベルを設定する](#set-a-different-default-label-for-outlook)|
|OutlookJustifyTrustedDomains|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookJustifyUntrustedCollaborationLabel|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookRecommendationEnabled|[Outlook で推奨分類を有効にする](#enable-recommended-classification-in-outlook)|
|OutlookOverrideUnlabeledCollaborationExtensions|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnTrustedDomains|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnUntrustedCollaborationLabel|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|PostponeMandatoryBeforeSave|[必須のラベル付けを使用するときにドキュメントの "後で" を削除する](#remove-not-now-for-documents-when-you-use-mandatory-labeling)|
|RemoveExternalContentMarkingInApp|[他のラベル付けソリューションからヘッダーとフッターを削除する](#remove-headers-and-footers-from-other-labeling-solutions)|
|ReportAnIssueLink|[ユーザーの "問題の報告" を追加する](#add-report-an-issue-for-users)|
|RunAuditInformationTypeDiscovery|[ドキュメント内の機密情報を検出する Azure Information Protection 分析を有効にする](#enable-azure-information-protection-analytics-to-discover-sensitive-information-in-documents)|

ラベルのポリシーに対して有効なラベル ポリシー設定を確認する PowerShell コマンドの例では、"Global"という名前。

    (Get-LabelPolicy -Identity Global).settings

#### <a name="available-advanced-settings-for-labels"></a>ラベルの使用可能な高度な設定

|設定|シナリオと手順|
|----------------|---------------|
|色|[ラベルの色を指定します。](##specify-a-color-for-the-label)|
|customPropertyByLabel|[Secure Islands からのラベルの移行と、その他のラベル付けのソリューション](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|DefaultSubLabelId|[親ラベルの既定のサブラベルを指定します。](#specify-a-default-sublabel-for-a-parent-label) 
|labelByCustomProperties|[ラベルが適用されるときに、カスタム プロパティを適用します。](#apply-a-custom-property-when-a-label-is-applied)|
|SMimeEncrypt|[ラベルを構成して Outlook で S/MIME 保護を適用する](#configure-a-label-to-apply-smime-protection-in-outlook)|
|SMimeSign|[ラベルを構成して Outlook で S/MIME 保護を適用する](#configure-a-label-to-apply-smime-protection-in-outlook)|

ラベルに対して有効なラベル設定を確認する PowerShell コマンドの例では、"Public"という名前。

    (Get-Label -Identity Public).settings

## <a name="display-the-information-protection-bar-in-office-apps"></a>Display the Information Protection bar in Office apps\(Office アプリの Information Protection バーを表示する\)

この構成ポリシーを使用して[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)ことは、Office 365 セキュリティ/コンプライアンス センターの PowerShell を使用して構成する必要があります。 統一されたラベル付けクライアントのみのプレビュー バージョンでサポートされています。

既定では、ユーザーを選択する必要があります、**バーを表示する**オプションを**感度**Office アプリで Information Protection バーを表示するボタンをクリックします。 使用して、 **HideBarByDefault**キーし、値を設定**False**ユーザーに対してこのバーを自動的に表示できるように、ラベル、バーまたはボタンのいずれかから選択できます。 

選択したラベル ポリシーは、次の文字列を指定します。

- キー:**HideBarByDefault**

- 値: **False**

PowerShell コマンドの例、ラベル、ポリシーが"Global"をという名前:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{HideBarByDefault="False"}

## <a name="enable-recommended-classification-in-outlook"></a>Outlook で推奨分類を有効にする

この構成ポリシーを使用して[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)ことは、Office 365 セキュリティ/コンプライアンス センターの PowerShell を使用して構成する必要があります。 統一されたラベル付けクライアントのみのプレビュー バージョンでサポートされています。

推奨分類のラベルを設定すると、Word、Excel、PowerPoint では、推奨ラベルを受け入れるか、却下するように求められます。 また、このラベル推奨が Outlook でも表示されます。

選択したラベル ポリシーは、次の文字列を指定します。

- キー:**OutlookRecommendationEnabled**

- 値: **True**

PowerShell コマンドの例、ラベル、ポリシーが"Global"をという名前:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookRecommendationEnabled="True"}

## <a name="set-a-different-default-label-for-outlook"></a>Outlook に別の既定ラベルを設定します

この構成ポリシーを使用して[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)ことは、Office 365 セキュリティ/コンプライアンス センターの PowerShell を使用して構成する必要があります。 統一されたラベル付けクライアントのみのプレビュー バージョンでサポートされています。

Outlook がオプションのポリシー設定として構成されている既定のラベルを適用しないこの設定を構成するときに**ドキュメントや電子メールに既定ではこのラベルを適用**します。 別の既定のラベルを適用できるか、ラベルがありません。

選択したラベル ポリシーは、次の文字列を指定します。

- キー:**OutlookDefaultLabel**

- 値: \< **GUID のラベルを付ける**> または**なし**

PowerShell コマンドの例、ラベル、ポリシーが"Global"をという名前:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookDefaultLabel="None"}


## <a name="remove-not-now-for-documents-when-you-use-mandatory-labeling"></a>必須のラベル付けを使用するときにドキュメントの "後で" を削除する

この構成ポリシーを使用して[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)ことは、Office 365 セキュリティ/コンプライアンス センターの PowerShell を使用して構成する必要があります。 統一されたラベル付けクライアントのみのプレビュー バージョンでサポートされています。

ラベルのポリシー設定を使用すると**すべてのドキュメントや電子メールにラベルを付ける**、Office ドキュメントと電子メールを送信するときに最初に保存するときにラベルを選択するように求められます。 ドキュメントの場合、ユーザーは **[後で]** を選択して一時的にメッセージを無視し、ラベルを選んで、ドキュメントに戻ることができます。 ただし、ラベルを付けないと、保したドキュメントを閉じることはできません。 

この設定を構成すると、 **[後で]** オプションが削除され、ユーザーはドキュメントを初めて保存するときにラベルを選択する必要があります。

選択したラベル ポリシーは、次の文字列を指定します。

- キー:**PostponeMandatoryBeforeSaveProperty**

- 値: **False**

PowerShell コマンドの例、ラベル、ポリシーが"Global"をという名前:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{PostponeMandatoryBeforeSaveProperty="False"}

## <a name="remove-headers-and-footers-from-other-labeling-solutions"></a>他のラベル付けソリューションからヘッダーとフッターを削除する

この構成ポリシーを使用して[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)ことは、Office 365 セキュリティ/コンプライアンス センターの PowerShell を使用して構成する必要があります。 統一されたラベル付けクライアントのみのプレビュー バージョンでサポートされています。

この設定では、その視覚的マーキングが別のラベル付けソリューションによって適用されている場合に、テキスト ベースのヘッダーまたはフッターをドキュメントから削除したり置き換えたりできるようになります。 たとえば、古いフッターが含まれています古いラベルの名前に新しいラベル名と、独自のフッターを使用する機密ラベルを移行したようになりました。

統一されたラベル付けクライアントは、そのポリシーでこの構成を取得、古いヘッダーとフッターが削除または、Office アプリで、ドキュメントが開いているし、秘密度ラベルがドキュメントに適用されるときに置き換えられます。

この構成は Outlook ではサポートされていません。そのため、この構成を Word、Excel、PowerPoint で使用すると、ユーザーのこれらのアプリのパフォーマンスに悪影響が生じる場合があります。 この構成ではアプリケーションごとの設定を定義することができます。たとえば、Word 文書のヘッダーとフッターのテキストは検索し、Excel のスプレッドシートや PowerPoint のプレゼンテーションのテキストは検索しないようにできます。

Office アプリケーションの種類を制限することをお勧め、パターン マッチングが、ユーザーのパフォーマンスに影響を与えるので (**W**ord、 **E**xcel **P**owerPoint) のためだけに検索する必要があります。

選択したラベル ポリシーは、次の文字列を指定します。

- キー:**RemoveExternalContentMarkingInApp**

- 値: \<**Office アプリケーションの種類 WXP**> 

例 :

- Word 文書のみを検索するには、**W** を指定します。

- Word 文書と PowerPoint プレゼンテーションを検索するには、**WP** を指定します。

PowerShell コマンドの例、ラベル、ポリシーが"Global"をという名前:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInApp="WX"}

この後、ヘッダーまたはフッターの内容と、その削除または置換方法を指定したりするために、少なくとも 1 つのより詳細なクライアント設定 **ExternalContentMarkingToRemove** が必要です。

### <a name="how-to-configure-externalcontentmarkingtoremove"></a>ExternalContentMarkingToRemove を構成する方法

**ExternalContentMarkingToRemove** キーに文字列値を指定するときには、正規表現を使用する 3 つのオプションがあります。

- ヘッダーまたはフッターのすべてを削除する部分一致。
    
    例:ヘッダーまたはフッターに文字列 **TEXT TO REMOVE** が含まれている場合。 これらのヘッダーまたはフッターを完全に削除したいとします。 値 `*TEXT*` を指定します。

- ヘッダーまたはフッターの特定の単語のみを削除する完全一致。
    
    例:ヘッダーまたはフッターに文字列 **TEXT TO REMOVE** が含まれている場合。 単語 **TEXT** のみを削除し、ヘッダーまたはフッター文字列は **TO REMOVE** として残したいとします。 値 `TEXT ` を指定します。

- ヘッダーまたはフッターのすべてを削除する完全一致。
    
    例:ヘッダーまたはフッターに文字列 **TEXT TO REMOVE** が含まれている場合。 正確にこの文字列が含まれているヘッダーまたはフッターを削除したいとします。 値 `^TEXT TO REMOVE$` を指定します。
    

指定した文字列のパターン マッチングでは大文字と小文字が区別されます。 文字列の最大長は 255 文字です。

一部のドキュメントには非表示の文字やさまざまな種類のスペースやタブが含まれているため、語句や文に指定した文字列が検出されない可能性があります。 値には、できるだけ単独の特徴的な単語を指定し、運用環境に展開する前に結果をテストしてください。

同じラベル ポリシーでは、次の文字列を指定します。

- キー:**ExternalContentMarkingToRemove**

- 値: \<**正規表現として定義された、マッチングする文字列**> 

PowerShell コマンドの例、ラベル、ポリシーが"Global"をという名前:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*TEXT*"}

#### <a name="multiline-headers-or-footers"></a>複数行のヘッダーまたはフッター

ヘッダーまたはフッターのテキストが複数行にわたる場合は、行ごとにキーと値を作成します。 たとえば、2 行にわたる次のフッターがあるとします。

**ファイルは社外秘として分類**

**ラベルは手動で適用**

この複数行のフッターを削除するには、同じラベル ポリシーの次の 2 つのエントリを作成します。

- キー:**ExternalContentMarkingToRemove**

- キー値 1: **\*社外秘***

- キー値 2: **\*ラベルの適用*** 

PowerShell コマンドの例、ラベル、ポリシーが"Global"をという名前:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*Confidential*,*Label applied*"}


#### <a name="optimization-for-powerpoint"></a>PowerPoint 用の最適化

PowerPoint では、フッターが図形として実装されます。 指定したテキストのうち、ヘッダーまたはフッターでない図形が削除されるのを防ぐには、**PowerPointShapeNameToRemove** という名前の、追加のクライアントの詳細設定を使用します。 また、すべての図形のテキストのチェックはリソースを消費するプロセスであるため、この設定を使用して回避することをお勧めします。

この追加のクライアントの詳細設定を指定せず、PowerPoint が **RemoveExternalContentMarkingInApp** キーの値に含まれている場合、**ExternalContentMarkingToRemove** で指定したテキストがすべての図形でチェックされます。 

ヘッダーまたはフッターとして使用している図形の名前を検索するには:

1. PowerPoint で、 **[選択]** ウィンドウを表示し、 **[書式]** タブ > **[配置]** グループ > **[選択ウィンドウ]** の順に選択します。

2. ヘッダーまたはフッターを含むスライド上の図形を選択します。 選択した図形の名前が、**選択**ウィンドウで強調表示されます。

図形の名前を使用して、**PowerPointShapeNameToRemove** キーの文字列値を指定します。 

例:図形の名前は **fc** です。 この名前の図形を削除するには、値 `fc` を指定します。

- キー:**PowerPointShapeNameToRemove**

- 値: \<**PowerPoint の図形の名前**> 

PowerShell コマンドの例、ラベル、ポリシーが"Global"をという名前:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{PowerPointShapeNameToRemove="fc"}

削除する 1 つ以上の PowerPoint 図形がある場合は、図形を削除する必要がある限りの値を指定します。

既定では、マスター スライドのヘッダーとフッターのみがチェックされます。 この検索の対象をすべてのスライドに広げるには、**RemoveExternalContentMarkingInAllSlides** という名前の、追加のクライアントの詳細設定を使用します。ただし、このプロセスはリソースをより多く消費します。

- キー:**RemoveExternalContentMarkingInAllSlides**

- 値: **True**

PowerShell コマンドの例、ラベル、ポリシーが"Global"をという名前:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInAllSlides="True"}


## <a name="disable-custom-permissions-in-file-explorer"></a>ファイル エクスプ ローラーでのカスタム アクセス許可を無効にします。

この構成ポリシーを使用して[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)ことは、Office 365 セキュリティ/コンプライアンス センターの PowerShell を使用して構成する必要があります。 統一されたラベル付けクライアントのみのプレビュー バージョンでサポートされています。

既定では、ユーザーは、というオプションを参照してください。**カスタム アクセス許可で保護**ファイル エクスプ ローラーで右クリックして、選択した場合**分類および保護**します。 このオプションを使用して、ラベル構成を追加する可能性がある保護設定をオーバーライドできる、独自の保護設定を設定できます。 ユーザーには、保護を削除するオプションも表示されます。 この設定を構成するときにユーザーにこれらのオプションは表示されません。

この高度な設定を構成するには、ラベルを選択したポリシーの次の文字列を入力します。

- キー:**EnableCustomPermissions**

- 値: **False**

PowerShell コマンドの例、ラベル、ポリシーが"Global"をという名前:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}

## <a name="for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer"></a>カスタム アクセス許可で保護されているファイルについて、ファイル エクスプローラーでカスタム アクセス許可を常にユーザーに表示する

この構成ポリシーを使用して[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)ことは、Office 365 セキュリティ/コンプライアンス センターの PowerShell を使用して構成する必要があります。 統一されたラベル付けクライアントのみのプレビュー バージョンでサポートされています。

クライアントの詳細設定を構成するとき[ファイル エクスプ ローラーでのカスタム アクセス許可を無効にする](#disable-custom-permissions-in-file-explorer)既定では、ユーザーは、または保護されたドキュメントで既に設定されているカスタムのアクセス許可を変更できません。

ただしは別の高度なクライアント設定では、このシナリオでは、ユーザーは表示して、ファイル エクスプ ローラーを使用してファイルを右クリックすると、保護されたドキュメントのカスタム アクセス許可を変更できるように指定することができます。

この高度な設定を構成するには、ラベルを選択したポリシーの次の文字列を入力します。

- キー:**EnableCustomPermissionsForCustomProtectedFiles**

- 値: **True**

PowerShell コマンドの例:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissionsForCustomProtectedFiles="True"}


## <a name="for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments"></a>添付ファイル付きの電子メール メッセージの場合、添付ファイルの最上位の分類に一致するラベルを適用します

この構成ポリシーを使用して[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)ことは、Office 365 セキュリティ/コンプライアンス センターの PowerShell を使用して構成する必要があります。 統一されたラベル付けクライアントのみのプレビュー バージョンでサポートされています。

この設定は、ユーザーが電子メールにラベル付きのドキュメントを添付し、は、電子メール メッセージをラベル付けしないのです。 このシナリオでは、添付ファイルに適用されている分類ラベルに基づいてそれらのラベルが自動的に選択します。 最上位の分類ラベルが選択されます。

添付ファイルは物理ファイルである必要があり、ファイルへのリンク (たとえば、SharePoint または OneDrive for Business 上のファイルへのリンク) はできません。

この設定を構成することができます**推奨**、カスタマイズ可能なツールヒントに、自分の電子メール メッセージに、選択したラベルを適用するように求められます。 ユーザーは、推奨設定を受け入れるか、通知を閉じます。 またはには、この設定を構成する**自動**、場所、選択したラベルが自動的に適用されますが、ユーザーは、ラベルを削除したり、電子メールを送信する前に、別のラベルを選択します。

注:ユーザー定義のアクセス許可の設定で保護するため、最上位の分類ラベルの添付ファイルが構成されている場合。

- ラベルのユーザー定義アクセス許可には、Outlook (転送不可)、ラベルが選択されていること、および転送不可保護は、電子メールに適用が含まれています。 
- ラベルのユーザー定義のアクセス許可は、Word、Excel、PowerPoint、およびエクスプ ローラーのだけですが、そのラベルは、電子メール メッセージには適用されず、保護は、どちらもします。

この高度な設定を構成するには、ラベルを選択したポリシーの次の文字列を入力します。

- キー 1: **AttachmentAction**

- キー値 1: **推奨**または**自動**

- キー 2: **AttachmentActionTip**

- キーの値 2:"\<ツールヒントをカスタマイズ >"


PowerShell コマンドの例、ラベル、ポリシーが"Global"をという名前:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{AttachmentAction="Automatic"}

## <a name="add-report-an-issue-for-users"></a>ユーザー向けの "問題の報告" を追加する

この構成ポリシーを使用して[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)ことは、Office 365 セキュリティ/コンプライアンス センターの PowerShell を使用して構成する必要があります。 統一されたラベル付けクライアントのみのプレビュー バージョンでサポートされています。

次のクライアントの詳細設定を指定すると、ユーザーに、 **[ヘルプとフィードバック]** クライアント ダイアログ ボックスから選択できる **[問題の報告]** オプションが表示されます。 リンクの HTTP 文字列を指定します。 たとえば、ユーザーが問題を報告するための、カスタマイズされた独自の Web ページや、ヘルプ デスクに送信される電子メール アドレスです。 

この高度な設定を構成するには、ラベルを選択したポリシーの次の文字列を入力します。

- キー:**ReportAnIssueLink**

- 値: **\<HTTP 文字列>**

Web サイトの値の例: `https://support.contoso.com`

メール アドレスの値の例: `mailto:helpdesk@contoso.com`

PowerShell コマンドの例、ラベル、ポリシーが"Global"をという名前:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ReportAnIssueLink="mailto:helpdesk@contoso.com"}

## <a name="implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent"></a>Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する

この構成ポリシーを使用して[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)ことは、Office 365 セキュリティ/コンプライアンス センターの PowerShell を使用して構成する必要があります。 統一されたラベル付けクライアントのみのプレビュー バージョンでサポートされています。

次のクライアント詳細設定を作成して構成すると、Outlook でユーザーに対してポップアップ メッセージが表示されます。これにより、次のどちらかのシナリオで、電子メールを送信する前に警告したり、電子メールの送信理由の入力を求めたり、電子メールの送信を妨げることができます。

- **電子メール、または電子メールの添付ファイルに特定のラベルが含まれる**:
    - 添付ファイルはあらゆる種類のファイルである可能性がある

- **電子メール、または電子メールの添付ファイルにラベルがない**:
    - 添付ファイルは Office ドキュメントまたは PDF ドキュメントである可能性がある

これらの条件が満たされ、受信者の電子メール アドレスが指定した許可されているドメイン名の一覧に含まれていない、ときに、ユーザーに、次の操作のいずれかのポップアップ メッセージが表示されます。

- **警告**: ユーザーは確認して電子メールを送信またはキャンセルできます。

- **理由の入力**:ユーザーは理由 (定義済みオプションまたは自由形式) の入力を求められます。  その後、ユーザーは電子メールを送信またはキャンセルできます。 理由のテキストは、他のシステムで読み取ることができるように電子メールの X ヘッダーに書き込まれます。 たとえば、データ損失防止 (DLP) サービスです。

- **[ブロック]** : 条件が満たされている間、ユーザーは電子メールを送信できなくなります。 メッセージには、ユーザーが問題に対処できるように、電子メールをブロックする理由が含まれます。 たとえば、特定の受信者を削除する、電子メールにラベルを付けるなどです。 

結果としてアクションは、ローカル Windows イベント ログの **[アプリケーションとサービス ログ]**  >  **[Azure Information Protection]** に記録されます。

- 警告メッセージ: 情報 ID 301

- 理由メッセージ: 情報 ID 302

- ブロック メッセージ: 情報 ID 303

理由メッセージからのイベント エントリの例:

```
Client Version: 2.0.779.0
Client Policy ID: e5287fe6-f82c-447e-bf44-6fa8ff146ef4
Item Full Path: Price list.msg
Item Name: Price list
Process Name: OUTLOOK
Action: Justify
User Justification: My manager approved sharing of this content
Action Source: 
User Response: Confirmed
```
次のセクションでには、各クライアントの詳細設定の構成手順が含まれます。

> [!TIP]
> このチュートリアルでは、統一されたラベル付けクライアントではなく、Azure Information Protection クライアントが、これらの設定で自分のアクションの詳細を参照できます[チュートリアル。Outlook を使用して情報の oversharing を制御する Azure Information Protection を構成する](../infoprotect-oversharing-tutorial.md)します。

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels"></a>特定のラベルに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装するには:

選択したポリシーの次のキーを持つ 1 つ以上の次の高度な設定を作成します。 値については、その Guid をコンマで区切られたそれぞれで 1 つまたは複数のラベルを指定します。

コンマ区切りの文字列として複数のラベルの Guid の値の例: `dcf781ba-727f-4860-b3c1-73479e31912b,1ace2cc3-14bc-4142-9125-bf946a70542c,3e9df74d-3168-48af-8b11-037e3021813f`


- 警告メッセージ:
    
    - キー:**OutlookWarnUntrustedCollaborationLabel**
    
    - 値: \< **Guid、コンマ区切りのラベル**>

- 理由の入力メッセージ:
    
    - キー:**OutlookJustifyUntrustedCollaborationLabel**
    
    - 値: \< **Guid、コンマ区切りのラベル**>

- ブロック メッセージ:
    
    - キー:**OutlookBlockUntrustedCollaborationLabel**
    
    - 値: \< **Guid、コンマ区切りのラベル**>


PowerShell コマンドの例、ラベル、ポリシーが"Global"をという名前:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookWarnUntrustedCollaborationLabel="8faca7b8-8d20-48a3-8ea2-0f96310a848e,b6d21387-5d34-4dc8-90ae-049453cec5cf,bb48a6cb-44a8-49c3-9102-2d2b017dcead,74591a94-1e0e-4b5d-b947-62b70fc0f53a,6c375a97-2b9b-4ccd-9c5b-e24e4fd67f73"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyUntrustedCollaborationLabel="dc284177-b2ac-4c96-8d78-e3e1e960318f,d8bb73c3-399d-41c2-a08a-6f0642766e31,750e87d4-0e91-4367-be44-c9c24c9103b4,32133e19-ccbd-4ff1-9254-3a6464bf89fd,74348570-5f32-4df9-8a6b-e6259b74085b,3e8d34df-e004-45b5-ae3d-efdc4731df24"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockUntrustedCollaborationLabel="0eb351a6-0c2d-4c1d-a5f6-caa80c9bdeec,40e82af6-5dad-45ea-9c6a-6fe6d4f1626b"}


### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label"></a>ラベルのない電子メールまたは添付ファイルに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装するには:

同じラベル ポリシーでは、次のクライアント設定で、次の値のいずれかの詳細を作成します。

- 警告メッセージ:
    
    - キー:**OutlookUnlabeledCollaborationAction**
    
    - 値: **警告**

- 理由の入力メッセージ:
    
    - キー:**OutlookUnlabeledCollaborationAction**
    
    - 値: **理由の入力**

- ブロック メッセージ:
    
    - キー:**OutlookUnlabeledCollaborationAction**
    
    - 値: **ブロック**

- これらのメッセージをオフにする:
    
    - キー:**OutlookUnlabeledCollaborationAction**
    
    - 値: **Off**


PowerShell コマンドの例、ラベル、ポリシーが"Global"をという名前:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationAction="Warn"}


#### <a name="to-define-specific-file-name-extensions-for-the-warn-justify-or-block-pop-up-messages-for-email-attachments-that-dont-have-a-label"></a>警告の特定のファイル名拡張子を定義するには、正当化、またはラベルがない電子メール添付ファイルのポップアップ メッセージをブロック

既定では、警告を正当化、またはブロックするポップアップ メッセージがすべての Office ドキュメントと PDF ドキュメントに適用されます。 ファイル名拡張子が、警告を表示する必要があります、正当化すると、この一覧を指定することで調整できますか、ブロック メッセージの追加された高度な設定とファイルのコンマ区切りのリスト名の拡張子。

コンマ区切りの文字列として定義する複数のファイル名拡張子の値の例: `.XLSX,.XLSM,.XLS,.XLTX,.XLTM,.DOCX,.DOCM,.DOC,.DOCX,.DOCM,.PPTX,.PPTM,.PPT,.PPTX,.PPTM`

この例で、ラベル付けされていない PDF ドキュメントをされることはありませんで警告を表示、正当化、またはメッセージのポップアップをブロックします。

同じラベル ポリシーの場合は、次の文字列を入力します。 


- キー:**OutlookOverrideUnlabeledCollaborationExtensions**

- 値:  **\<** ファイル名拡張子をコンマ区切りのメッセージを表示するには **>**


PowerShell コマンドの例、ラベル、ポリシーが"Global"をという名前:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookOverrideUnlabeledCollaborationExtensions=".PPTX,.PPTM,.PPT,.PPTX,.PPTM"}

### <a name="to-specify-the-allowed-domain-names-for-recipients-exempt-from-the-pop-up-messages"></a>ポップアップ メッセージの対象外の受信者について、許可されるドメイン名を指定するには

その他の高度なクライアント設定でドメイン名を指定するとユーザーの電子メール アドレスに含まれるそのドメイン名を持つ受信者のポップアップ メッセージは表示されません。 この場合、電子メールは中断なく送信されます。 複数のドメインを指定するには、ドメインをコンマで区切って 1 つの文字列として追加します。

一般的な構成では、組織の外部の受信者、または組織の承認済みのパートナーではない受信者についてのみ、ポップアップ メッセージが表示されます。 この場合は、お客様の組織およびパートナーによって使用されるすべての電子メール ドメインを指定します。

同じラベル ポリシー、次のクライアント設定の詳細を作成し、値をコンマで区切られたそれぞれの 1 つまたは複数のドメインを指定します。

コンマ区切り文字列としての複数のドメインの値の例: `contoso.com,fabrikam.com,litware.com`

- 警告メッセージ:
    
    - キー:**OutlookWarnTrustedDomains**
    
    - 値: **\<** コンマ区切りのドメイン名 **>**

- 理由の入力メッセージ:
    
    - キー:**OutlookJustifyTrustedDomains**
    
    - 値: **\<** コンマ区切りのドメイン名 **>**

- ブロック メッセージ:
    
    - キー:**OutlookBlockTrustedDomains**
    
    - 値: **\<** コンマ区切りのドメイン名 **>**

たとえば、contoso.com の電子メール アドレスを持つユーザーに送信される電子メールをブロックしない、高度なクライアントを指定の設定**OutlookBlockTrustedDomains**と**contoso.com**します。 結果として、ユーザー表示されない警告のポップアップ メッセージを Outlook で電子メールを送信する際john@sales.contoso.comします。

PowerShell コマンドの例、ラベル、ポリシーが"Global"をという名前:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockTrustedDomains="gmail.com"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyTrustedDomains="contoso.com,fabrikam.com,litware.com"}

## <a name="enable-azure-information-protection-analytics-to-discover-sensitive-information-in-documents"></a>ドキュメント内の機密情報を検出する Azure Information Protection の分析を有効にする

この構成ポリシーを使用して[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)ことは、Office 365 セキュリティ/コンプライアンス センターの PowerShell を使用して構成する必要があります。 統一されたラベル付けクライアントのみのプレビュー バージョンでサポートされています。

[Azure Information Protection analytics](../reports-aip.md)ことが検出し、そのコンテンツには、機密情報が含まれている場合、Azure Information Protection によって保存されたドキュメントがラベル付けのクライアントを unified を報告します。 既定では、この情報は Azure Information Protection 分析には送信されません。

この情報は、統一されたラベル付けクライアントによって送信されるように、この動作を変更するには、選択したラベルのポリシーの次の文字列を入力します。

- キー:**RunAuditInformationTypeDiscovery**

- 値: **True**

この高度なクライアントを設定しない場合は設定すると、監査結果、統一されたラベル付けクライアントから送信されますが、情報は、ユーザーがラベル付けされたコンテンツへのアクセス時のレポートに制限されます。

以下に例を示します。

- これが設定されていない場合、**Confidential \ Sales** というラベル付きの Financial.docx にアクセスしたユーザーを確認できます。

- これを設定した場合、Financial.docx に 6 つのクレジット カード番号が含まれていることを確認できます。
    
    - [詳細な分析のためのコンテンツ一致](../reports-aip.md#content-matches-for-deeper-analysis)も有効にすると、これらのクレジット カードの番号も追加で確認できます。

PowerShell コマンドの例、ラベル、ポリシーが"Global"をという名前:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RunAuditInformationTypeDiscovery="True"}

## <a name="disable-sending-information-type-matches-for-a-subset-of-users"></a>ユーザーのサブセットに対して送信情報の種類の一致を無効にする

この構成ポリシーを使用して[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)ことは、Office 365 セキュリティ/コンプライアンス センターの PowerShell を使用して構成する必要があります。 統一されたラベル付けクライアントのみのプレビュー バージョンでサポートされています。

機密情報の種類またはカスタム条件に対するコンテンツ一致を収集する [[Azure Information Protection 分析]](../reports-aip.md) のチェック ボックスをオンにすると、既定で、すべてのユーザーによってこの情報が送信されます。 一部のユーザーにこのデータを送信する必要がありますが、ある場合は、次のクライアントでこれらのユーザーのラベルのポリシー設定の詳細を作成します。 

- キー:**LogMatchedContent**

- 値: **無効にします。**

PowerShell コマンドの例、ラベル、ポリシーが"Global"をという名前:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{LogMatchedContent="Disable"}

## <a name="migrate-labels-from-secure-islands-and-other-labeling-solutions"></a>Secure Islands からのラベルの移行と、その他のラベル付けのソリューション

この構成は、ラベルを使用[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)ことは、Office 365 セキュリティ/コンプライアンス センターの PowerShell を使用して構成する必要があります。 統一されたラベル付けクライアントのみのプレビュー バージョンでサポートされています。

この構成は、.ppdf ファイル名拡張子を持つ保護された PDF ファイルと互換性がありません。 ファイル エクスプ ローラー、PowerShell、またはスキャナーによっては、これらのファイルを開くことができません。

Secure Islands によってラベル付けされている Office ドキュメントは、定義したマッピングを使用して機密ラベルでこれらのドキュメントのラベルを変更できます。 また、この方法を使用して、他のソリューションからのラベルを、そのラベルが Office ドキュメントにある場合は再利用することができます。 

この構成オプションの結果として新しい機密ラベルは、Azure Information Protection の統一されたラベル付けクライアントによって次のように適用されます。

- Office ドキュメントの場合: デスクトップ アプリでドキュメントが開かれ、新しい機密ラベル セットとして表示されます文書を保存するときに適用されます。

- PowerShell の場合: [Set-aipfilelabel](/powershell/module/azureinformationprotection/set-aipfilelabel)と[セット AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification)新しい機密ラベルを適用することができます。 [Get-aipfilestatus](/powershell/module/azureinformationprotection/get-aipfilestatus)別の方法で設定されるまで、新しい機密ラベルを表示しません。

- ファイル エクスプローラーの場合:Azure Information Protection ダイアログ ボックスで、新しい機密ラベルが表示されますが設定されていません。

この構成では、高度なという名前の設定を指定する必要があります**labelByCustomProperties**古いラベルにマップする各の秘密度ラベル。 次に、各エントリに対して、次の構文を使用して値を設定します。

`[migration rule name],[Secure Islands custom property name],[Secure Islands metadata Regex value]`

任意の移行規則名を指定します。 使用して、前のラベル付けソリューションからどのように 1 つまたは複数のラベルを識別するのに役立つそのわかりやすい名前は、機密ラベルにマップする必要があります。 名前は、スキャナー レポートおよびイベント ビューアーに表示されます。

この設定では、ドキュメントから元のラベルが削除されたり、元のラベルが適用された可能性がある視覚的マーキングが削除されたりすることはありません。 ヘッダーとフッターを削除するには、前のセクションを参照してください。[ヘッダーとフッターを他のラベル付けソリューションから削除](#remove-headers-and-footers-from-other-labeling-solutions)します。

#### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>例 1 : 同じラベル名の 1 対 1 のマッピング

要件:Secure Islands の "Confidential" というラベルを持ったドキュメントは、Azure Information Protection の "Confidential" というラベルに変更されます。

この例では:

- Secure Islands のラベルは、**Confidential** という名前が付けられ、**Classification** という名前のカスタム プロパティに保存されます。

高度な設定:

- キー: **labelByCustomProperties**

- 値: **セキュリティで保護された Islands のラベルは Confidential、Classification、Confidential です。**

ラベルが「Confidential」という名前は、例 PowerShell コマンド:

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Confidential,Classification,Confidential"}

#### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>例 2:異なるラベル名の 1 対 1 のマッピング

要件:Secure Islands によって "Sensitive" というラベルを付けられたドキュメントは、Azure Information Protection によって "Highly Confidential" というラベルに変更されます。

この例では:

- Secure Islands のラベルは **Sensitive** という名前が付けられ、**Classification** という名前のカスタム プロパティに保存されます。

高度な設定:

- キー: **labelByCustomProperties**

- 値: **セキュリティで保護された Islands のラベルは、区別、Classification、Sensitive**

PowerShell コマンドの例、ラベルが"Highly Confidential"という:

    Set-Label -Identity "Highly Confidential" -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Sensitive,Classification,Sensitive"}

#### <a name="example-3-many-to-one-mapping-of-label-names"></a>例 3: ラベル名の多対一のマッピング

要件:"Internal"という単語を含む 2 つの Secure Islands のラベルがあるし、Azure Information Protection の統合されたラベル付けクライアントでラベルを「標準」Secure Islands のラベルはこれらのいずれかでドキュメントをします。

この例では:

- Secure Islands のラベルには、**Internal** という単語が含まれ、**Classification** という名前のカスタム プロパティに保存されます。

クライアントの詳細設定:

- キー: **labelByCustomProperties**

- 値: **セキュリティで保護された Islands のラベルには、内部、分類が含まれています。\*内部。\***

ラベルが「一般」という名前は、例 PowerShell コマンド:

    Set-Label -Identity General -AdvancedSettings @{labelByCustomProperties="Secure Islands label contains Internal,Classification,.*Internal.*"}

#### <a name="example-4-multiple-rules-for-the-same-label"></a>例 4:同じラベルに対して複数のルール

複数のルールを同じラベルの必要がある場合は、同じキーに対して複数の文字列値を定義します。 

この例では:

- Secure Islands のラベルの名前付きの"Confidential"と「シークレット」という名前のカスタム プロパティに格納されます * *、分類し、"Confidential"という名前の機密ラベルを適用する Azure Information Protection のクライアントを統一されたにラベル付け。

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}

### <a name="extend-your-label-migration-rules-to-emails"></a>ラベルのメール移行のルールを拡張します。

Office ドキュメントだけでなく Outlook 電子メールの設定を追加のラベルの高度なポリシー設定を指定することで高度な labelByCustomProperties を使用することができます。 ただし、この設定は、既知の Outlook のパフォーマンスに悪影響が及ぶのため、のみがある場合、強力なビジネス要件にこの追加設定を構成およびから移行を完了したときに、null 文字列値に設定してください、その他のラベル付けソリューションです。

この高度な設定を構成するには、ラベルを選択したポリシーの次の文字列を入力します。

- キー:**EnableLabelByMailHeader**

- 値: **(火)**

PowerShell コマンドの例、ラベル、ポリシーが"Global"をという名前:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableLabelByMailHeader="True"}

## <a name="apply-a-custom-property-when-a-label-is-applied"></a>ラベルが適用されるときに、カスタム プロパティを適用します。

この構成は、ラベルを使用[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)ことは、Office 365 セキュリティ/コンプライアンス センターの PowerShell を使用して構成する必要があります。 統一されたラベル付けクライアントのみのプレビュー バージョンでサポートされています。

機密ラベルが適用されているメタデータの他のドキュメントまたは電子メール メッセージを 1 つまたは複数のカスタム プロパティを適用する一部のシナリオがあります。

以下に例を示します。

- プロセスが[別のラベル付けソリューションから移行](#migrate-labels-from-secure-islands-and-other-labeling-solutions)、Secure Islands など。 移行中に相互運用性、機密ラベルも、その他のラベル付けソリューションによって使用されるカスタム プロパティを適用する必要があります。

- ラベルの GUID の代わりにわかりやすい名前と、ラベルの値が異なる一貫性のあるカスタム プロパティ名を使用する (SharePoint や他のベンダーのドキュメント管理ソリューション) など、コンテンツ管理システムは、します。

Office ドキュメントや Outlook の電子メール クライアントを使用して、Azure Information Protection 統合ラベル付け、そのユーザーのラベルを追加できますを定義する 1 つまたは複数のカスタム プロパティ。 統一されたラベル付けクライアントによってまだ記載されていないコンテンツの他のソリューションからのラベルとしてカスタム プロパティを表示するのに、統一されたラベル付けクライアントには、このメソッドを使用することもできます。

この構成オプションの結果としてその他のカスタム プロパティは、Azure Information Protection の統合されたラベル付けクライアントによって次のように適用されます。

- Office ドキュメントの場合: デスクトップ アプリでドキュメントがラベル付け、追加のカスタム プロパティは、ドキュメントを保存するときに適用されます。

- Outlook メール。電子メール メッセージが Outlook でラベルを付ける場合は、電子メールが送信されるときに x ヘッダーに追加のプロパティが適用されます。

- PowerShell の場合: [Set-aipfilelabel](/powershell/module/azureinformationprotection/set-aipfilelabel)と[セット AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification)ドキュメントがラベル付けされ、保存されたときに、追加のカスタム プロパティを適用します。 [Get-aipfilestatus](/powershell/module/azureinformationprotection/get-aipfilestatus)機密ラベルが適用されない場合は、マップのラベルとしてカスタム プロパティを表示します。

- ファイル エクスプローラーの場合:ユーザーは、ファイルを右クリックして、ラベルを適用、カスタム プロパティが適用されます。

この構成では、高度なという名前の設定を指定する必要があります**customPropertyByLabel**追加のカスタム プロパティを適用する各の秘密度ラベル。 次に、各エントリに対して、次の構文を使用して値を設定します。

`[custom property name],[custom property value]`

#### <a name="example-1-add-a-single-custom-property-for-a-label"></a>例 1 : ラベルの 1 つのカスタム プロパティを追加します。

要件:Azure Information Protection の統合されたラベル付けクライアントで"Confidential"というラベルの付いたドキュメントには、追加のカスタム プロパティ「分類」を「シークレット」の値を含むという必要があります。

この例では:

- 機密ラベルの名前は**社外秘**というカスタム プロパティと**分類**の値を持つ**シークレット**します。

高度な設定:

- キー: **customPropertyByLabel**

- 値: **分類、シークレット**

ラベルが「Confidential」という名前は、例 PowerShell コマンド:

    Set-Label -Identity Confidential -AdvancedSettings @{customPropertyByLabel="Classification,Secret"}

#### <a name="example-2-add-multiple-custom-properties-for-a-label"></a>例 2:ラベルの複数のカスタム プロパティを追加します。

同じラベルの 1 つ以上のカスタム プロパティを追加するには、同じキーの複数の文字列値を定義する必要があります。

例の PowerShell コマンドをラベルは「一般」という名前は、という名前の 1 つのカスタム プロパティを追加する**分類**の値を持つ**全般**という名前の2番目のカスタムプロパティと**感度**の値を持つ**内部**:

    Set-Label -Identity General -AdvancedSettings @{customPropertyByLabel=ConvertTo-Json("Classification,General", "Sensitivity,Internal")}

## <a name="configure-a-label-to-apply-smime-protection-in-outlook"></a>ラベルを構成して Outlook で S/MIME 保護を適用する

この構成はラベルを使用[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)ことは、Office 365 セキュリティ/コンプライアンス センターの PowerShell を使用して構成する必要があります。 統一されたラベル付けクライアントのみのプレビュー バージョンでサポートされています。

これらの設定を使用して、動作している場合にのみ[S/MIME 展開](https://docs.microsoft.com/office365/SecurityCompliance/s-mime-for-message-signing-and-encryption)し、Azure Information Protection からの Rights Management 保護ではなく、電子メールの場合は、この保護方法を自動的に適用するラベル。 結果として得られる保護は、ユーザーが Outlook から手動で S/MIME オプションを選択した場合と同じものです。

S/MIME のデジタル署名用の高度な設定を構成するには、選択したラベルの次の文字列を入力します。

- キー:**SMimeSign**

- 値: **True**

S/MIME 暗号化用の高度な設定を構成するには、選択したラベルの次の文字列を入力します。

- キー:**SMimeEncrypt**

- 値: **True**

暗号化は、Azure Information Protection の統合されたラベル付けクライアントのプレビュー バージョンを指定するラベルが構成されている場合、S/MIME の保護には、Outlook でのみ、Rights Management による保護が置き換えられます。 一般公開バージョンの統一されたラベル付けクライアントは引き続き管理センター内のラベルの指定された暗号化設定を使用します。 組み込みラベルが付けられた Office アプリではこれらは S/MIME 保護は適用されませんが、代わりに、転送不可の保護を適用します。

のみで Outlook で表示されるラベルを設定する場合に暗号化を適用するラベルを構成する**のみ Outlook でメッセージを電子メール**します。

例 PowerShell コマンド、ラベルが [受信者のみ] に名前付き。

    Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeSign="True"}

    Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeEncrypt="True"}

## <a name="specify-a-default-sublabel-for-a-parent-label"></a>親ラベルの既定のサブラベルを指定します。

この構成は、ラベルを使用[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)ことは、Office 365 セキュリティ/コンプライアンス センターの PowerShell を使用して構成する必要があります。 統一されたラベル付けクライアントのみのプレビュー バージョンでサポートされています。

ラベルにサブラベルを追加すると、ユーザーことができます、ドキュメントや電子メールに、親ラベルことは適用されません。 既定では、ユーザーは、サブラベルをそれらを適用して、そのサブラベルのいずれかを選択して、親ラベルを選択します。 このユーザーが、親ラベルを選択すると設定の詳細を構成すると場合、サブラベルが自動的に選択され、それらの適用。 

- キー:**DefaultSubLabelId**

- 値: \<sublabel GUID >

例の PowerShell コマンドを親ラベルでは、"Confidential"と「すべての従業員」サブラベルの名前はここでは、8faca7b8 8d 20-48a3-8ea2-0f96310a848e の GUID があります。

    Set-Label -Identity "Confidential" -AdvancedSettings @{defaultsublabels="8faca7b8-8d20-48a3-8ea2-0f96310a848e"}

## <a name="specify-a-color-for-the-label"></a>ラベルの色を指定します。

この構成はラベルを使用[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)ことは、Office 365 セキュリティ/コンプライアンス センターの PowerShell を使用して構成する必要があります。

ラベルの色を設定するのにには、この設定の詳細を使用します。 色を指定するには、色の赤、緑、および青 (RGB) コンポーネントの 16 進数コードを入力します。 たとえば、#40e0d0 は青緑色の RGB の 16 進値です。

便利なテーブルがありますの参照をこれらのコードが必要な場合、 [\<色 >](https://developer.mozilla.org/docs/Web/CSS/color_value) MSDN の web ドキュメントからページ。画像編集できるさまざまなアプリケーションでもコードを参照できます。 たとえば、Microsoft ペイントでは、パレットからカスタム色を選択できます。RGB 値が自動的に表示されるので、それをコピーできます。

ラベルの色の高度な設定を構成するには、選択したラベル、次の文字列を入力します。

- キー:**色**

- 値: \<RGB の 16 進値 >

ラベルが"Public"という名前は、例 PowerShell コマンド:

    Set-Label -Identity Public -AdvancedSettings @{color="#40e0d0"}

## <a name="sign-in-as-a-different-user"></a>別のユーザーでのサイン イン

運用環境でユーザーは、通常、統合されたクライアントのラベル付けを Azure Information Protection を使用しているときに、別のユーザーにサインインする必要はありません。 ただし管理者の場合は、テスト段階のときに別ユーザーとしてサインインする必要がある場合があります。 

**Microsoft Azure Information Protection** ダイアログ ボックスを使用して、現在サインインしているアカウントを確認することができます。Office アプリケーションを開くと、**ホーム** タブで、、**感度**ボタンをクリックし、**ヘルプとフィードバック**。 アカウント名が **[クライアント ステータス]** セクションに表示されます。

表示されるサインイン アカウントのドメイン名も必ず確認してください。 正しいアカウントでサインインしていてもドメインが間違っている、という状況は気付きにくいものです。 症状の間違ったアカウントを使用してダウンロードが失敗、ラベル、ラベルまたは予測される動作が表示されない場合またはします。

別のユーザーでサイン インする方法は以下の通りです。

1. **%localappdata%\Microsoft\MSIP** に移動し、**TokenCache** ファイルを削除します。

2. 開いている Office アプリケーションがあれば再起動し、別のユーザー アカウントでサインインします。 Azure Information Protection サービスにサインインするには、Office アプリケーションで、プロンプトが表示されない場合に戻って、 **Microsoft Azure Information Protection**  ダイアログ ボックスを選択します**サインイン**から、更新**クライアント ステータス**セクション。

補足:

- Azure Information Protection の統合されたラベル付けクライアントがサインインしたまま、古いアカウントこれらの手順が完了したら、Internet Explorer から、すべての cookie を削除し、手順 1. および 2. を繰り返します。

- シングル サインオンを使用する場合は、トークン ファイルを削除した後に Windows からサインアウトし、別のユーザー アカウントでサインインする必要があります。 Azure Information Protection の統合されたラベル付けクライアントし、自動的に認証し、現在サインインしてを使用してユーザー アカウントにします。

- このソリューションでは、同じテナントから別ユーザーとしてサインインする操作がサポートされています。 別のテナントから別のユーザーとしてサインインする操作はサポートされていません。 複数のテナントがある Azure Information Protection をテストするには、異なるコンピューターを使用します。

- 使用することができます、**設定にリセット**オプションを**ヘルプとフィードバック**サインアウトしてから、Office 365 セキュリティ/コンプライアンス センターでは、現在ダウンロードされているラベルとポリシーの設定を削除しますMicrosoft 365 セキュリティ センター、または Microsoft 365 コンプライアンス センター。


## <a name="change-the-local-logging-level"></a>ローカルのログ記録レベルを変更する

既定では、Azure Information Protection にユニファイド ラベル付けクライアント書き込みクライアント ログ ファイルを **%localappdata%\Microsoft\MSIP**フォルダー。 これらのファイルは、Microsoft サポートによるトラブルシューティングを目的としています。
 
これらのファイルのログ記録レベルを変更するには、レジストリ内で、次の値の名前を検索し、値のデータを必要なログ記録レベルに設定します。

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\LogLevel**

ログ記録レベルに次の値のいずれかを設定します。

- **Off**: ローカルのログ記録なし。

- **Error**: エラーのみ。

- **[情報]** :最小のログ記録 (イベント ID は含まれません)。

- **[デバッグ]** :完全な情報。

- **[トレース]** :詳細なログ記録 (クライアントの既定の設定)。

このレジストリ設定では、Azure Information Protection に送信される情報は変更されません[中央 reporting](../reports-aip.md)します。


## <a name="next-steps"></a>次の手順
これで、Azure Information Protection の統一されたラベル付けクライアントをカスタマイズして、このクライアントをサポートする必要があります追加情報については、次のリソースを参照してください。

- [クライアント ファイルおよび使用状況ログの記録](client-admin-guide-files-and-logging.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)
