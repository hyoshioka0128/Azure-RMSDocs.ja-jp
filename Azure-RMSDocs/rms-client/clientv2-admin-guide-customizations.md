---
title: カスタム構成-Azure Information Protection 統合されたラベル付けクライアント
description: Windows 用に Azure Information Protection 統合ラベルクライアントをカスタマイズする方法について説明します。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/09/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.subservice: v2client
ms.reviewer: maayan
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b18beab3c6a2dd3b01991fdb9755b943ec62fe5a
ms.sourcegitcommit: ad3e55f8dfccf1bc263364990c1420459c78423b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2020
ms.locfileid: "76117699"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-unified-labeling-client"></a>管理者ガイド: Azure Information Protection 統合されたラベル付けクライアントのカスタム構成

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012*
>
> *手順: [Windows 用の統一されたラベル付けクライアント Azure Information Protection](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

Azure Information Protection の統一されたラベル付けクライアントを管理するときに、特定のシナリオまたはユーザーのサブセットに必要となる可能性がある詳細な構成については、次の情報を参照してください。

これらの設定を行うには、レジストリを編集するか、詳細設定を指定する必要があります。 詳細設定では、 [Office 365 セキュリティ/コンプライアンスセンター PowerShell](https://docs.microsoft.com/powershell/exchange/office-365-scc/office-365-scc-powershell?view=exchange-ps)を使用します。

### <a name="how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell"></a>Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用してクライアントの詳細設定を構成する方法

PowerShell セキュリティ/コンプライアンスセンター Office 365 を使用すると、ラベルポリシーとラベルのカスタマイズをサポートする詳細設定を構成できます。 たとえば次のようになります。

- Office アプリの Information Protection バーを表示する設定は、***ラベルポリシーの詳細設定***です。
- ラベルの色を指定する設定は、***ラベルの詳細設定***です。

どちらの場合も、 [PowerShell セキュリティ/コンプライアンスセンター Office 365 に接続](https://docs.microsoft.com/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell?view=exchange-ps)した後で、ポリシーまたはラベルの id (名前または GUID) を使用して [*設定*] パラメーターを指定し、[ハッシュテーブル](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_hash_tables)でキーと値のペアを指定します。 次の構文を使用します。

ラベルポリシー設定の場合、単一の文字列値:

    Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key="value1,value2"}

ラベルポリシー設定の場合は、同じキーに対して複数の文字列値を指定します。

    Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}

ラベル設定の場合、単一の文字列値:

    Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key="value1,value2"}

ラベル設定の場合は、同じキーに対して複数の文字列値を指定します。

    Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}

詳細設定を削除するには、同じ構文を使用しますが、null 文字列値を指定します。


#### <a name="examples-for-setting-advanced-settings"></a>詳細設定の設定例

例 1: 1 つの文字列値のラベルポリシーの詳細設定を設定します。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}

例 2: 1 つの文字列値に対して、ラベルの詳細設定を設定します。

    Set-Label -Identity Internal -AdvancedSettings @{smimesign="true"}

例 3: 複数の文字列値に対して、ラベルの詳細設定を設定します。

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}

例 4: null 文字列値を指定して、ラベルポリシーの詳細設定を削除します。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions=""}

#### <a name="specifying-the-identity-for-the-label-policy-or-label"></a>ラベルポリシーまたはラベルの id の指定

ラベルポリシーを管理する管理センターには、ポリシー名が1つだけ表示されるため、PowerShell *id*パラメーターにラベルポリシー名を指定するのは簡単です。 ただし、ラベルの場合、管理センターには**名前**と**表示名**の両方が表示されます。 場合によっては、両方の値が同じになりますが、異なっていてもかまいません。

- **Name**はラベルの元の名前であり、すべてのラベルで一意です。 作成したラベルの名前を変更しても、この値は変わりません。 Azure Information Protection から移行されたラベルの場合、Azure portal のラベルのラベル ID が表示されることがあります。

- **[表示名]** はユーザーに表示されるラベルの名前であり、すべてのラベルで一意である必要はありません。 たとえば、"**社外**秘" と表示され**ている** **すべて**の従業員をサブラベル、他の**すべての従業員**にサブラベルを持つユーザーがいるとします。 これらのサブラベルの両方に同じ名前が表示されますが、ラベルは同じではなく、設定も異なります。

ラベルの詳細設定を構成するには、 **[名前]** の値を使用します。 たとえば、次の図でラベルを識別するには、`-Identity "All Company"`を指定します。

![秘密度ラベルを識別するには、' 表示名 ' ではなく ' Name ' を使用してください](../media/labelname_scc.png)

ラベル GUID を指定する場合、ラベルを管理する管理センターにはこの値が表示されません。 ただし、次の Office 365 セキュリティ/コンプライアンスセンター PowerShell コマンドを使用して、この値を見つけることができます。

    Get-Label | Format-Table -Property DisplayName, Name, Guid


#### <a name="order-of-precedence---how-conflicting-settings-are-resolved"></a>優先順位-競合する設定の解決方法

機密ラベルを管理する管理センターの1つを使用して、次のラベルポリシー設定を構成できます。

- **このラベルを既定でドキュメントと電子メールに適用する**

- **ユーザーはラベルまたは下位分類ラベルを削除する理由を指定する必要があります**

- **ユーザーに電子メールまたはドキュメントへのラベルの適用を要求する**

- **カスタムヘルプページへのリンクをユーザーに提供する**

1人のユーザーに対して複数のラベルポリシーが構成されており、それぞれが異なるポリシー設定を持っている場合は、管理センターのポリシーの順序に従って、最後のポリシー設定が適用されます。 詳細については、「[ラベルポリシーの優先度 (順序](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels#label-policy-priority-order-matters)の問題)」を参照してください。

[詳細設定] ラベルは同じロジックに従います。ラベルが複数のラベルポリシーにあり、そのラベルに詳細設定がある場合、管理センターのポリシーの順序に従って、最後の詳細設定が適用されます。

ラベルポリシーの詳細設定は、逆の順序で適用されます。1つの例外として、管理センターのポリシーの順序に従って、最初のポリシーの詳細設定が適用されます。 例外は、Outlook に別の既定のラベルを設定する、 *Outlookdefaultlabel*の詳細設定です。 このラベルポリシーの詳細設定のみの場合、最後の設定は管理センターのポリシーの順序に従って適用されます。

#### <a name="available-advanced-settings-for-label-policies"></a>ラベルポリシーの使用可能な詳細設定

[新しい-labelpolicy](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/new-labelpolicy?view=exchange-ps)と[設定-labelpolicy](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-labelpolicy?view=exchange-ps)を指定して、 *advanced settings*パラメーターを使用します。

|Setting|シナリオと手順|
|----------------|---------------|
|AttachmentAction|[添付ファイルのある電子メール メッセージの場合、その添付ファイルの最上位の分類と一致するラベルを適用します](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)
|AttachmentActionTip|[添付ファイルのある電子メール メッセージの場合、その添付ファイルの最上位の分類と一致するラベルを適用します](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments) 
|DisableMandatoryInOutlook|[必須ラベルから Outlook メッセージを除外する](#exempt-outlook-messages-from-mandatory-labeling)
|EnableAudit|[Azure Information Protection analytics への監査データの送信を無効にする](#disable-sending-audit-data-to-azure-information-protection-analytics)|
|EnableCustomPermissions|[エクスプローラーでカスタムアクセス許可を無効にする](#disable-custom-permissions-in-file-explorer)|
|EnableCustomPermissionsForCustomProtectedFiles|[カスタム アクセス許可で保護されているファイルについて、ファイル エクスプローラーでカスタム アクセス許可を常にユーザーに表示する](#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer) |
|EnableLabelByMailHeader|[Secure Islands からのラベルの移行と、その他のラベル付けのソリューション](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|EnableLabelBySharePointProperties|[Secure Islands からのラベルの移行と、その他のラベル付けのソリューション](#migrate-labels-from-secure-islands-and-other-labeling-solutions)
|HideBarByDefault デフォルト)|[Office アプリの Information Protection バーを表示します](#display-the-information-protection-bar-in-office-apps)|
|LogMatchedContent|[情報の種類の一致を Azure Information Protection analytics に送信する](#send-information-type-matches-to-azure-information-protection-analytics)|
|OutlookBlockTrustedDomains|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookBlockUntrustedCollaborationLabel|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookDefaultLabel|[Outlook に別の既定ラベルを設定する](#set-a-different-default-label-for-outlook)|
|Outlookジャスト Ifytrusteddomains|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookJustifyUntrustedCollaborationLabel|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookRecommendationEnabled|[Outlook で推奨分類を有効にする](#enable-recommended-classification-in-outlook)|
|OutlookOverrideUnlabeledCollaborationExtensions|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnTrustedDomains|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnUntrustedCollaborationLabel|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|PFileSupportedExtensions|[保護するファイルの種類を変更する](#change-which-file-types-to-protect)|
|PostponeMandatoryBeforeSave|[必須のラベル付けを使用するときにドキュメントの "後で" を削除する](#remove-not-now-for-documents-when-you-use-mandatory-labeling)|
|RemoveExternalContentMarkingInApp|[他のラベル付けソリューションからヘッダーとフッターを削除する](#remove-headers-and-footers-from-other-labeling-solutions)|
|ReportAnIssueLink|[ユーザーの "問題の報告" を追加する](#add-report-an-issue-for-users)|
|Runauditinformationタイプの検出|[ドキュメント内の検出された機密情報の Azure Information Protection analytics への送信を無効にする](#disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics)|
|ScannerConcurrencyLevel|[スキャナーで使用されるスレッドの数を制限する](#limit-the-number-of-threads-used-by-the-scanner)|

"Global" という名前のラベルポリシーに対してラベルポリシー設定が有効であることを確認する PowerShell コマンドの例を次に示します。

    (Get-LabelPolicy -Identity Global).settings

#### <a name="available-advanced-settings-for-labels"></a>ラベルに使用できる詳細設定

[新しいラベル](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/new-label?view=exchange-ps)と[セットラベル](https://docs.microsoft.com/powershell/module/exchange/policy-and-compliance/set-label?view=exchange-ps)を使用して、 *advanced settings*パラメーターを使用します。

|Setting|シナリオと手順|
|----------------|---------------|
|色|[ラベルの色を指定します](#specify-a-color-for-the-label)|
|customPropertiesByLabel|[ラベルが適用されたときにカスタムプロパティを適用する](#apply-a-custom-property-when-a-label-is-applied)|
|DefaultSubLabelId|[親ラベルに既定のサブラベルを指定する](#specify-a-default-sublabel-for-a-parent-label) 
|labelByCustomProperties|[Secure Islands からのラベルの移行と、その他のラベル付けのソリューション](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|SMimeEncrypt|[ラベルを構成して Outlook で S/MIME 保護を適用する](#configure-a-label-to-apply-smime-protection-in-outlook)|
|SMimeSign|[ラベルを構成して Outlook で S/MIME 保護を適用する](#configure-a-label-to-apply-smime-protection-in-outlook)|

"Public" という名前のラベルに対して有効なラベル設定を確認する PowerShell コマンドの例を次に示します。

    (Get-Label -Identity Public).settings

## <a name="display-the-information-protection-bar-in-office-apps"></a>Display the Information Protection bar in Office apps\(Office アプリの Information Protection バーを表示する\)

この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるポリシーの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

既定では、ユーザーは、 **[秘密度]** ボタンから **[バーの表示]** オプションを選択して、Office アプリの Information Protection バーを表示する必要があります。 **Hidebarbydefault デフォルト**キーを使用して、値を**False**に設定すると、ユーザーがバーまたはボタンからラベルを選択できるように、このバーが自動的に表示されます。 

選択したラベルポリシーについて、次の文字列を指定します。

- キー: **Hidebarbydefault デフォルト**

- 値: **False**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{HideBarByDefault="False"}

## <a name="exempt-outlook-messages-from-mandatory-labeling"></a>必須ラベルから Outlook メッセージを除外する

この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるポリシーの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

既定では、すべてのドキュメントのラベルポリシー設定を有効にし、**電子メールにラベルを付ける必要**がある場合、保存されているすべてのドキュメントと送信された電子メールにラベルが適用されている必要があります。 次の詳細設定を構成すると、ポリシー設定は Office ドキュメントにのみ適用され、Outlook メッセージには適用されません。

選択したラベルポリシーについて、次の文字列を指定します。

- キー: **DisableMandatoryInOutlook**

- 値: **True**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{DisableMandatoryInOutlook="True"}

## <a name="enable-recommended-classification-in-outlook"></a>Outlook で推奨分類を有効にする

この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるポリシーの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

推奨分類のラベルを設定すると、Word、Excel、PowerPoint では、推奨ラベルを受け入れるか、却下するように求められます。 また、このラベル推奨が Outlook でも表示されます。

選択したラベルポリシーについて、次の文字列を指定します。

- キー: **OutlookRecommendationEnabled**

- 値: **True**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookRecommendationEnabled="True"}

## <a name="set-a-different-default-label-for-outlook"></a>Outlook に別の既定ラベルを設定します

この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるポリシーの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

この設定を構成すると、Outlook では、 **[既定でドキュメントと電子メールにこのラベルを適用する]** オプションのポリシー設定として構成されている既定のラベルが適用されません。 別の既定のラベルを適用できるか、ラベルがありません。

選択したラベルポリシーについて、次の文字列を指定します。

- キー: **OutlookDefaultLabel**

- 値: \<**ラベル GUID**> または**None**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookDefaultLabel="None"}

## <a name="change-which-file-types-to-protect"></a>保護するファイルの種類を変更する

この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるポリシーの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

既定では、Azure Information Protection の統一されたラベル付けクライアントは、すべてのファイルの種類を保護します。クライアントのスキャナーは、Office のファイルの種類と PDF ファイルのみを保護します。

次のように指定すると、選択したラベルポリシーの既定の動作を変更できます。

- キー: **PFileSupportedExtensions**

- 値: **<string value>** 

次の表を使用して、指定する文字列値を指定します。

| 文字列値| クライアント| スキャナー|
|-------------|-------|--------|
|\*|既定値: すべてのファイルの種類に保護を適用します。|すべてのファイルの種類に保護を適用する|
|\<null 値 >| Office ファイルの種類と PDF ファイルに保護を適用する| 既定値: Office ファイルの種類と PDF ファイルに保護を適用する|
|Convertto-html (".jpg", ".png")|Office のファイルの種類と PDF ファイルに加えて、指定したファイル名拡張子に保護を適用します。 | Office のファイルの種類と PDF ファイルに加えて、指定したファイル名拡張子に保護を適用します。

例 1: Office ファイルの種類と PDF ファイルのみを保護する統合クライアント用の PowerShell コマンド。ラベルポリシーには "Client" という名前が付けられています。

    Set-LabelPolicy -Identity Client -AdvancedSettings @{PFileSupportedExtensions=""}

例 2: すべてのファイルの種類を保護するためのスキャナーの PowerShell コマンド: ラベルポリシーに "Scanner" という名前を付けます。

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions="*"}

例 3: スキャナーの PowerShell コマンドを使用して、Office ファイルと PDF ファイルに加え、.txt ファイルと .csv ファイルを保護します。ここで、ラベルポリシーには "Scanner" という名前を付けます。

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions=ConvertTo-Json(".txt", ".csv")}

この設定では、保護するファイルの種類を変更できますが、既定の保護レベルをネイティブから汎用に変更することはできません。 たとえば、統一されたラベル付けクライアントを実行しているユーザーに対しては、既定の設定を変更して、Office ファイルと PDF ファイルのみをすべてのファイルの種類ではなく保護するようにすることができます。 ただし、これらのファイルの種類は、pfile ファイル名拡張子で汎用的に保護されるように変更することはできません。

## <a name="remove-not-now-for-documents-when-you-use-mandatory-labeling"></a>必須のラベル付けを使用するときにドキュメントの "後で" を削除する

この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるポリシーの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

すべてのドキュメントにラベルポリシー設定を使用し、**電子メールにラベルを付ける必要が**ある場合、ユーザーは Office ドキュメントを最初に保存するときにラベルを選択し、電子メールを送信するように求められます。 ドキュメントの場合、ユーザーは **[後で]** を選択して一時的にメッセージを無視し、ラベルを選んで、ドキュメントに戻ることができます。 ただし、ラベルを付けないと、保したドキュメントを閉じることはできません。 

この設定を構成すると、 **[後で]** オプションが削除され、ユーザーはドキュメントを初めて保存するときにラベルを選択する必要があります。

選択したラベルポリシーについて、次の文字列を指定します。

- キー: **PostponeMandatoryBeforeSave**

- 値: **False**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{PostponeMandatoryBeforeSave="False"}

## <a name="remove-headers-and-footers-from-other-labeling-solutions"></a>他のラベル付けソリューションからヘッダーとフッターを削除する

この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるポリシーの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

他のラベル付けソリューションから分類を削除するには、次の2つの方法があります。 最初のメソッドは、図形名が詳細プロパティ**WordShapeNameToRemove**で定義されている名前と一致する word 文書から図形を削除します。2番目の方法では、 **Removeexternalcontentmarkinginapp**詳細プロパティで定義されている、word、Excel、および PowerPoint ドキュメントからテキストベースのヘッダーまたはフッターを削除または置換できます。 

### <a name="use-the-wordshapenametoremove-advanced-property-preview"></a>WordShapeNameToRemove advanced プロパティの使用 (プレビュー)

***WordShapeNameToRemove** advanced プロパティは、バージョン2.6.101.0 以降でサポートされています。*

この設定を使用すると、別のラベル付けソリューションによって視覚的なマーキングが適用されている場合に、Word 文書から図形ベースのラベルを削除または置換できます。 たとえば、図形には、新しいラベル名と独自の図形を使用するために、機密ラベルに移行した古いラベルの名前が含まれています。

この詳細プロパティを使用するには、Word 文書で図形名を検索し、図形の**WordShapeNameToRemove**詳細プロパティリストで定義する必要があります。 この詳細プロパティの図形の一覧で定義されている名前で始まる Word の図形は、サービスによって削除されます。

削除するすべての図形の名前を定義し、リソースを集中的に使用するプロセスであるすべての図形のテキストをチェックしないようにすることで、無視するテキストを含む図形を削除しないようにします。

この追加の詳細プロパティ設定で Word 図形を指定せず、 **Removeexternalcontentmarkinginapp**キー値に word が含まれている場合は、 **Externalcontentmarkingtorclean**値で指定したテキストのすべての図形がチェックされます。 

使用していて除外する図形の名前を検索するには、次のようにします。

1. Word で、**選択**ウィンドウを表示します。 **ホーム** タブ >**編集**グループ > 選択 ウィンドウの オプション > 選択 **ウィンドウ** **を選択**します。

2. 削除対象としてマークするページ上の図形を選択します。 マークした図形の名前が**選択**ウィンドウで強調表示されるようになりました。

図形の名前を使用して、* * * * WordShapeNameToRemove * * * キーの文字列値を指定します。 

例: シェイプ名は**dc**です。 この名前の図形を削除するには、値 `dc` を指定します。

- キー: **WordShapeNameToRemove**

- 値: \<**Word 図形の名前**> 

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{WordShapeNameToRemove="dc"}

複数の単語図形を削除する場合は、削除する図形の数を指定します。


### <a name="use-the-removeexternalcontentmarkinginapp-advanced-property"></a>RemoveExternalContentMarkingInApp 詳細設定プロパティの使用
この設定を使用すると、別のラベル付けソリューションによって視覚的なマーキングが適用されている場合に、テキストベースのヘッダーまたはフッターをドキュメントから削除したり置き換えることができます。 たとえば、古いフッターには、新しいラベル名とその独自のフッターを使用するために、機密ラベルに移行した古いラベルの名前が含まれています。

統一されたラベル付けクライアントがポリシーでこの構成を取得すると、Office アプリでドキュメントを開いたときに古いヘッダーとフッターが削除されるか、またはドキュメントに機密ラベルが適用されます。

この構成は Outlook ではサポートされていません。そのため、この構成を Word、Excel、PowerPoint で使用すると、ユーザーのこれらのアプリのパフォーマンスに悪影響が生じる場合があります。 この構成ではアプリケーションごとの設定を定義することができます。たとえば、Word 文書のヘッダーとフッターのテキストは検索し、Excel のスプレッドシートや PowerPoint のプレゼンテーションのテキストは検索しないようにできます。

パターンマッチングはユーザーのパフォーマンスに影響するため、Office アプリケーションの種類 (**W**Ord、E**X**セル、 **P**owerpoint) は、検索する必要があるものだけに制限することをお勧めします。

選択したラベルポリシーについて、次の文字列を指定します。

- キー: **RemoveExternalContentMarkingInApp**

- 値: \<**Office アプリケーションの種類 WXP**> 

次に例を示します。

- Word 文書のみを検索するには、**W** を指定します。

- Word 文書と PowerPoint プレゼンテーションを検索するには、**WP** を指定します。

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInApp="WX"}

この後、ヘッダーまたはフッターの内容と、その削除または置換方法を指定したりするために、少なくとも 1 つのより詳細なクライアント設定 **ExternalContentMarkingToRemove** が必要です。

### <a name="how-to-configure-externalcontentmarkingtoremove"></a>ExternalContentMarkingToRemove を構成する方法

**ExternalContentMarkingToRemove** キーに文字列値を指定するときには、正規表現を使用する 3 つのオプションがあります。

- ヘッダーまたはフッターのすべてを削除する部分一致。
    
    例: ヘッダーまたはフッターに文字列 **TEXT TO REMOVE** が含まれている場合。 これらのヘッダーまたはフッターを完全に削除したいとします。 値 `*TEXT*` を指定します。

- ヘッダーまたはフッターの特定の単語のみを削除する完全一致。
    
    例: ヘッダーまたはフッターに文字列 **TEXT TO REMOVE** が含まれている場合。 単語 **TEXT** のみを削除し、ヘッダーまたはフッター文字列は **TO REMOVE** として残したいとします。 値 `TEXT ` を指定します。

- ヘッダーまたはフッターのすべてを削除する完全一致。
    
    例: ヘッダーまたはフッターに文字列 **TEXT TO REMOVE** が含まれている場合。 正確にこの文字列が含まれているヘッダーまたはフッターを削除したいとします。 値 `^TEXT TO REMOVE$` を指定します。
    

指定した文字列のパターン マッチングでは大文字と小文字が区別されます。 文字列の最大長は 255 文字です。

一部のドキュメントには非表示の文字やさまざまな種類のスペースやタブが含まれているため、語句や文に指定した文字列が検出されない可能性があります。 値には、できるだけ単独の特徴的な単語を指定し、運用環境に展開する前に結果をテストしてください。

同じラベルポリシーについて、次の文字列を指定します。

- キー: **ExternalContentMarkingToRemove**

- 値: \<**正規表現として定義された、マッチングする文字列**> 

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*TEXT*"}

#### <a name="multiline-headers-or-footers"></a>複数行のヘッダーまたはフッター

ヘッダーまたはフッターのテキストが複数行にわたる場合は、行ごとにキーと値を作成します。 たとえば、2 行にわたる次のフッターがあるとします。

**ファイルは社外秘として分類**

**ラベルは手動で適用**

この複数行のフッターを削除するには、同じラベルポリシーに対して次の2つのエントリを作成します。

- キー: **ExternalContentMarkingToRemove**

- キーの値 1: **\*社外秘***

- キーの値 2: **\*ラベルの適用*** 

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*Confidential*,*Label applied*"}


#### <a name="optimization-for-powerpoint"></a>PowerPoint 用の最適化

PowerPoint では、フッターが図形として実装されます。 指定したテキストのうち、ヘッダーまたはフッターでない図形が削除されるのを防ぐには、**PowerPointShapeNameToRemove** という名前の、追加のクライアントの詳細設定を使用します。 また、すべての図形のテキストのチェックはリソースを消費するプロセスであるため、この設定を使用して回避することをお勧めします。

この追加のクライアントの詳細設定を指定せず、PowerPoint が **RemoveExternalContentMarkingInApp** キーの値に含まれている場合、**ExternalContentMarkingToRemove** で指定したテキストがすべての図形でチェックされます。 

ヘッダーまたはフッターとして使用している図形の名前を検索するには:

1. PowerPoint の**選択**ウィンドウを表示し、 **[書式]** タブ > **[配置]** グループ > **[選択ウィンドウ]** の順に選択します。

2. ヘッダーまたはフッターを含むスライド上の図形を選択します。 選択した図形の名前が、**選択**ウィンドウで強調表示されます。

図形の名前を使用して、**PowerPointShapeNameToRemove** キーの文字列値を指定します。 

例: 図形の名前は **fc** です。 この名前の図形を削除するには、値 `fc` を指定します。

- キー: **PowerPointShapeNameToRemove**

- 値: \<**PowerPoint の図形の名前**> 

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{PowerPointShapeNameToRemove="fc"}

複数の PowerPoint 図形を削除する場合は、削除する図形の数を指定します。

既定では、マスター スライドのヘッダーとフッターのみがチェックされます。 この検索の対象をすべてのスライドに広げるには、**RemoveExternalContentMarkingInAllSlides** という名前の、追加のクライアントの詳細設定を使用します。ただし、このプロセスはリソースをより多く消費します。

- キー: **RemoveExternalContentMarkingInAllSlides**

- 値: **True**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInAllSlides="True"}


## <a name="disable-custom-permissions-in-file-explorer"></a>エクスプローラーでカスタムアクセス許可を無効にする

この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるポリシーの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

既定では、ユーザーはエクスプローラーで右クリックして **[分類と保護]** を選択すると、 **[カスタムアクセス許可で保護]** する というオプションが表示されます。 このオプションを使用すると、ラベルの構成に含まれている可能性のある保護設定を上書きできる、独自の保護設定を設定できます。 ユーザーには、保護を削除するオプションも表示されます。 この設定を構成すると、ユーザーにはこれらのオプションが表示されません。

この詳細設定を構成するには、選択したラベルポリシーに対して次の文字列を入力します。

- キー: **EnableCustomPermissions**

- 値: **False**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}

## <a name="for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer"></a>カスタム アクセス許可で保護されているファイルについて、ファイル エクスプローラーでカスタム アクセス許可を常にユーザーに表示する

この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるポリシーの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

[エクスプローラーでカスタムアクセス許可を無効](#disable-custom-permissions-in-file-explorer)にするように [高度なクライアント] 設定を構成した場合、既定では、ユーザーは保護されたドキュメントで既に設定されているカスタムアクセス許可を表示または変更できません。

ただし、このシナリオでは、ユーザーがエクスプローラーを使用してファイルを右クリックして、保護されたドキュメントのカスタムアクセス許可を表示および変更できるように、さらに詳細なクライアント設定を指定することもできます。

この詳細設定を構成するには、選択したラベルポリシーに対して次の文字列を入力します。

- キー: **EnableCustomPermissionsForCustomProtectedFiles**

- 値: **True**

PowerShell コマンドの例:

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissionsForCustomProtectedFiles="True"}


## <a name="for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments"></a>添付ファイル付きの電子メール メッセージの場合、添付ファイルの最上位の分類に一致するラベルを適用します

この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるポリシーの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

この設定は、ユーザーがラベル付きドキュメントを電子メールに添付するときに、電子メールメッセージ自体にラベルを付けない場合に使用します。 このシナリオでは、添付ファイルに適用される分類ラベルに基づいて、ラベルが自動的に選択されます。 最高の分類ラベルが選択されます。

添付ファイルは物理ファイルである必要があり、ファイルへのリンク (たとえば、SharePoint または OneDrive for Business 上のファイルへのリンク) はできません。

この設定を **[推奨]** に構成すると、ユーザーは、カスタマイズ可能なツールヒントを使用して、選択したラベルを電子メールメッセージに適用するように求められます。 ユーザーは、推奨設定を受け入れるか、通知を閉じます。 または、この設定を **[自動]** に構成できます。選択したラベルは自動的に適用されますが、ユーザーは電子メールを送信する前に、ラベルを削除したり、別のラベルを選択したりできます。

注: 最高の分類ラベルを持つ添付ファイルが、ユーザー定義のアクセス許可の設定で保護するように構成されている場合:

- ラベルのユーザー定義のアクセス許可に Outlook ([転送不可]) が含まれている場合、そのラベルが選択され、電子メールに [転送防止] が適用されません。
- ラベルのユーザー定義アクセス許可が Word、Excel、PowerPoint、およびエクスプローラー専用の場合、そのラベルは電子メールメッセージには適用されず、保護もされません。

この詳細設定を構成するには、選択したラベルポリシーに対して次の文字列を入力します。

- キー 1: **Attachmentaction**

- キー値 1:**推奨**または**自動**

- キー 2: **Attachmentactiontip**

- キー値 2: "\<カスタマイズされたツールヒント >"

カスタマイズしたツールヒントでは、単一の言語のみがサポートされます。

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{AttachmentAction="Automatic"}

## <a name="add-report-an-issue-for-users"></a>ユーザー向けの "問題の報告" を追加する

この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるポリシーの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

次のクライアントの詳細設定を指定すると、ユーザーに、 **[ヘルプとフィードバック]** クライアント ダイアログ ボックスから選択できる **[問題の報告]** オプションが表示されます。 リンクの HTTP 文字列を指定します。 たとえば、ユーザーが問題を報告するための、カスタマイズされた独自の Web ページや、ヘルプ デスクに送信される電子メール アドレスです。 

この詳細設定を構成するには、選択したラベルポリシーに対して次の文字列を入力します。

- キー: **ReportAnIssueLink**

- 値: **\<HTTP string>**

Web サイトの値の例: `https://support.contoso.com`

メール アドレスの値の例: `mailto:helpdesk@contoso.com`

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{ReportAnIssueLink="mailto:helpdesk@contoso.com"}

## <a name="implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent"></a>Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する

この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるポリシーの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

次のクライアント詳細設定を作成して構成すると、Outlook でユーザーに対してポップアップ メッセージが表示されます。これにより、次のどちらかのシナリオで、電子メールを送信する前に警告したり、電子メールの送信理由の入力を求めたり、電子メールの送信を妨げることができます。

- **電子メール、または電子メールの添付ファイルに特定のラベルが含まれる**:
    - 添付ファイルはあらゆる種類のファイルである可能性がある

- **電子メール、または電子メールの添付ファイルにラベルがない**:
    - 添付ファイルは Office ドキュメントまたは PDF ドキュメントである可能性がある

これらの条件が満たされると、ユーザーには、次のいずれかの操作を含むポップアップメッセージが表示されます。

- **警告**: ユーザーは、確認して送信するか、キャンセルすることができます。

- **[ジャスティファイ]** : ユーザーに対して理由 (定義済みオプションまたは自由形式) の入力を求められます。  その後、ユーザーは電子メールを送信またはキャンセルできます。 理由のテキストは、他のシステムで読み取ることができるように電子メールの X ヘッダーに書き込まれます。 たとえば、データ損失防止 (DLP) サービスです。

- **ブロック**: 条件が残っている間、ユーザーは電子メールを送信できません。 メッセージには、ユーザーが問題に対処できるように、電子メールをブロックする理由が含まれます。 たとえば、特定の受信者を削除する、電子メールにラベルを付けるなどです。 

ポップアップメッセージが特定のラベルに対して実行されている場合は、ドメイン名を使用して受信者の例外を構成できます。

> [!TIP]
> これらの設定を構成する方法のチュートリアルの例については、ビデオ[Azure Information Protection Outlook のポップアップ構成](https://azure.microsoft.com/resources/videos/how-to-configure-azure-information-protection-popup-for-outlook/)を参照してください。

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels"></a>特定のラベルに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装するには:

選択したポリシーについて、次のキーを使用して次の詳細設定を1つ以上作成します。 値には、1つまたは複数のラベルを Guid で指定し、それぞれをコンマで区切って指定します。

複数のラベル Guid の値の例 (コンマ区切り文字列): `dcf781ba-727f-4860-b3c1-73479e31912b,1ace2cc3-14bc-4142-9125-bf946a70542c,3e9df74d-3168-48af-8b11-037e3021813f`


- 警告メッセージ:
    
    - キー: **OutlookWarnUntrustedCollaborationLabel**
    
    - 値: \<**ラベル guid、コンマ区切り**>

- 理由の入力メッセージ:
    
    - キー: **OutlookJustifyUntrustedCollaborationLabel**
    
    - 値: \<**ラベル guid、コンマ区切り**>

- ブロック メッセージ:
    
    - キー: **OutlookBlockUntrustedCollaborationLabel**
    
    - 値: \<**ラベル guid、コンマ区切り**>


PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookWarnUntrustedCollaborationLabel="8faca7b8-8d20-48a3-8ea2-0f96310a848e,b6d21387-5d34-4dc8-90ae-049453cec5cf,bb48a6cb-44a8-49c3-9102-2d2b017dcead,74591a94-1e0e-4b5d-b947-62b70fc0f53a,6c375a97-2b9b-4ccd-9c5b-e24e4fd67f73"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyUntrustedCollaborationLabel="dc284177-b2ac-4c96-8d78-e3e1e960318f,d8bb73c3-399d-41c2-a08a-6f0642766e31,750e87d4-0e91-4367-be44-c9c24c9103b4,32133e19-ccbd-4ff1-9254-3a6464bf89fd,74348570-5f32-4df9-8a6b-e6259b74085b,3e8d34df-e004-45b5-ae3d-efdc4731df24"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockUntrustedCollaborationLabel="0eb351a6-0c2d-4c1d-a5f6-caa80c9bdeec,40e82af6-5dad-45ea-9c6a-6fe6d4f1626b"}

#### <a name="to-exempt-domain-names-for-pop-up-messages-configured-for-specific-labels"></a>特定のラベル用に構成されたポップアップメッセージのドメイン名を除外するには

これらのポップアップメッセージで指定したラベルについては、特定のドメイン名を除外して、そのドメイン名が電子メールアドレスに含まれている受信者のメッセージがユーザーに表示されないようにすることができます。 この場合、電子メールは中断なく送信されます。 複数のドメインを指定するには、ドメインをコンマで区切って 1 つの文字列として追加します。

一般的な構成では、組織の外部の受信者、または組織の承認済みのパートナーではない受信者についてのみ、ポップアップ メッセージが表示されます。 この場合は、お客様の組織およびパートナーによって使用されるすべての電子メール ドメインを指定します。

同じラベルポリシーについて、次の高度なクライアント設定を作成し、値として1つ以上のドメインをコンマで区切って指定します。

コンマ区切り文字列としての複数のドメインの値の例: `contoso.com,fabrikam.com,litware.com`

- 警告メッセージ:
    
    - キー: **OutlookWarnTrustedDomains**
    
    - 値: **\<** コンマ区切りのドメイン名 **>**

- 理由の入力メッセージ:
    
    - キー: **Outlookジャスト Ifytrusteddomains**
    
    - 値: **\<** コンマ区切りのドメイン名 **>**

- ブロック メッセージ:
    
    - キー: **Outlookblocktrusteddomains**
    
    - 値: **\<** コンマ区切りのドメイン名 **>**

たとえば、 **[社外秘 \ すべての従業員]** ラベルに対して**OutlookBlockUntrustedCollaborationLabel**アドバンストクライアント設定を指定したとします。 ここで、 **Outlookジャスト Ifytrusteddomains**と**contoso.com**の追加のアドバンストクライアント設定を指定します。 その結果、ユーザーは**社外秘 \ すべての従業員**というラベルが付いたときに john@sales.contoso.com に電子メールを送信できますが、Gmail アカウントに同じラベルの電子メールを送信することは禁止されます。

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockTrustedDomains="gmail.com"}

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyTrustedDomains="contoso.com,fabrikam.com,litware.com"}

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label"></a>ラベルのない電子メールまたは添付ファイルに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装するには:

同じラベルポリシーについて、次のいずれかの値を使用して次のアドバンストクライアント設定を作成します。

- 警告メッセージ:
    
    - キー: **OutlookUnlabeledCollaborationAction**
    
    - 値: **Warn**

- 理由の入力メッセージ:
    
    - キー: **OutlookUnlabeledCollaborationAction**
    
    - 値:**均等**配置

- ブロック メッセージ:
    
    - キー: **OutlookUnlabeledCollaborationAction**
    
    - 値:**ブロック**

- これらのメッセージをオフにする:
    
    - キー: **OutlookUnlabeledCollaborationAction**
    
    - 値:**オフ**


PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationAction="Warn"}


#### <a name="to-define-specific-file-name-extensions-for-the-warn-justify-or-block-pop-up-messages-for-email-attachments-that-dont-have-a-label"></a>ラベルのない電子メールの添付ファイルのポップアップメッセージに対して、警告、配置、またはブロックを行うための特定のファイル名拡張子を定義するには

既定では、すべての Office ドキュメントおよび PDF ドキュメントに対して、ポップアップメッセージの警告、位置揃え、またはブロックが適用されます。 この一覧を調整するには、[警告]、[メッセージを表示する]、または [ブロックするメッセージ] に、追加の詳細設定とファイル名拡張子のコンマ区切りの一覧を表示するファイル名拡張子を指定します。

コンマ区切りの文字列として定義する複数のファイル名拡張子の値の例: `.XLSX,.XLSM,.XLS,.XLTX,.XLTM,.DOCX,.DOCM,.DOC,.DOCX,.DOCM,.PPTX,.PPTM,.PPT,.PPTX,.PPTM`

この例では、ラベル付けされていない PDF ドキュメントは、ポップアップメッセージの警告、配置、またはブロックにはなりません。

同じラベルポリシーについて、次の文字列を入力します。 


- キー: **OutlookOverrideUnlabeledCollaborationExtensions**

- 値: メッセージを表示するためのファイル名拡張子 **\<** 、コンマ区切り **>**


PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookOverrideUnlabeledCollaborationExtensions=".PPTX,.PPTM,.PPT,.PPTX,.PPTM"}

#### <a name="to-specify-a-different-action-for-email-messages-without-attachments"></a>添付ファイルのない電子メールメッセージに対して別のアクションを指定するには

既定では、ポップアップメッセージを表示するために OutlookUnlabeledCollaborationAction に指定する値は、ラベルのない電子メールまたは添付ファイルに適用されます。 添付ファイルのない電子メールメッセージに対して、別の詳細設定を指定することで、この構成を調整できます。

次のいずれかの値を使用して、次のクライアント詳細設定を作成します。

- 警告メッセージ:
    
    - キー: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - 値: **Warn**

- 理由の入力メッセージ:
    
    - キー: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - 値:**均等**配置

- ブロック メッセージ:
    
    - キー: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - 値:**ブロック**

- これらのメッセージをオフにする:
    
    - キー: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - 値:**オフ**

このクライアント設定を指定しない場合は、OutlookUnlabeledCollaborationAction に指定した値が、添付ファイルのない電子メールメッセージと、添付ファイルを含むラベルなしの電子メールメッセージに使用されます。

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior="Warn"}

## <a name="disable-sending-audit-data-to-azure-information-protection-analytics"></a>Azure Information Protection analytics への監査データの送信を無効にする

この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるポリシーの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

Azure Information Protection 統合されたラベル付けクライアントは、中央レポートをサポートします。既定では、は監査データを[Azure Information Protection analytics](../reports-aip.md)に送信します。 送信および保存される情報の詳細については、中央レポートのドキュメントの「[収集して Microsoft に送信する](../reports-aip.md#information-collected-and-sent-to-microsoft)情報」セクションを参照してください。

この動作を変更して、この情報が統合ラベルクライアントによって送信されないようにするには、選択したラベルポリシーに対して次の文字列を入力します。

- キー: **Enableaudit**

- 値: **False**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableAudit="False"}


## <a name="disable-sending-discovered-sensitive-information-in-documents-to-azure-information-protection-analytics"></a>ドキュメント内の検出された機密情報の Azure Information Protection analytics への送信を無効にする

この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるポリシーの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

Azure Information Protection 統合されたラベル付けクライアントが Office アプリで使用されると、ドキュメントが最初に保存されたときに、その情報を検索します。 [Enableaudit](#disable-sending-audit-data-to-azure-information-protection-analytics)詳細設定を**False**に設定していない場合、定義済みのカスタムの機密情報の種類がすべて[Azure Information Protection analytics](../reports-aip.md)に送信されます。

この動作を変更して、統一されたラベル付けクライアントによって検出された機密情報の種類が送信されないようにするには、選択したラベルポリシーに対して次の文字列を入力します。

- キー: **Runauditinformationタイプ検出**

- 値: **False**

この高度なクライアント設定を設定した場合でも、クライアントから監査情報を送信できますが、ユーザーがラベル付きコンテンツにアクセスした場合、情報はレポートに限定されます。

たとえば次のようになります。

- この設定を使用すると、**社外秘 \ Sales**というラベルが付けられたユーザーによってアクセスされたことを確認できます。

- この設定を行わないと、".docx" に6個のクレジットカード番号が含まれていることがわかります。
    
    - [詳細な分析のためのコンテンツ一致](../reports-aip.md#content-matches-for-deeper-analysis)も有効にすると、これらのクレジット カードの番号も追加で確認できます。

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{RunAuditInformationTypesDiscovery="False"}

## <a name="send-information-type-matches-to-azure-information-protection-analytics"></a>情報の種類の一致を Azure Information Protection analytics に送信する
 
この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるポリシーの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

既定では、統一されたラベル付けクライアントは、機密情報の種類のコンテンツの一致を[Azure Information Protection analytics](../reports-aip.md)に送信しません。 送信できるこの追加情報の詳細については、中央レポートのドキュメントの「詳細な[分析のためのコンテンツの一致](../reports-aip.md#content-matches-for-deeper-analysis)」を参照してください。

機密情報の種類が送信されたときにコンテンツの一致を送信するには、ラベルポリシーで次のアドバンストクライアント設定を作成します。 

- キー: **Logmatchedcontent**

- 値: **True**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{LogMatchedContent="True"}

## <a name="limit-the-number-of-threads-used-by-the-scanner"></a>スキャナーで使用されるスレッドの数を制限する

この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるポリシーの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

既定では、スキャナー サービスを実行しているコンピューター上の利用可能なプロセッサ リソースのすべてがスキャナーによって使われます。 このサービスのスキャン中に CPU 使用量を制限する必要がある場合は、ラベルポリシーで次の詳細設定を作成します。 

値には、スキャナーが並列で実行できる同時スレッドの数を指定します。 スキャナーでは、それがスキャンするファイルごとに個別のスレッドが使われます。このため、この調整構成によって並列でスキャンできるファイルの数も定義されます。 

最初にテスト用の値を構成するときは、コアごとに 2 を指定してから、その結果を監視することをお勧めします。 たとえば、4 コアのコンピューター上でスキャナーを実行する場合、最初は値を 8 に設定します。 必要な場合は、スキャナー コンピューターとスキャン速度に対してご自身が要求する結果のパフォーマンスに応じて、その数を増減させます。 

- キー: **ScannerConcurrencyLevel**

- 値: **\<同時スレッドの数>**

PowerShell コマンドの例: ラベルポリシーの名前は "Scanner" です。

    Set-LabelPolicy -Identity Scanner -AdvancedSettings @{ScannerConcurrencyLevel="8"}


## <a name="migrate-labels-from-secure-islands-and-other-labeling-solutions"></a>Secure Islands からのラベルの移行と、その他のラベル付けのソリューション

この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるラベルの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

この構成は、ファイル名拡張子が ppdf の保護された PDF ファイルと互換性がありません。 これらのファイルは、エクスプローラーまたは PowerShell を使用してクライアントで開くことはできません。

保護された島々でラベル付けされている Office ドキュメントの場合、定義したマッピングを使用して、これらのドキュメントのラベルを機密ラベルにすることができます。 また、この方法を使用して、他のソリューションからのラベルを、そのラベルが Office ドキュメントにある場合は再利用することができます。 

この構成オプションの結果として、次のように、Azure Information Protection 統合ラベル付けクライアントによって新しい感度ラベルが適用されます。

- Office ドキュメントの場合: デスクトップアプリでドキュメントを開くと、新しい秘密度ラベルが設定済みとして表示され、ドキュメントの保存時に適用されます。

- PowerShell の場合: [set-aipfilelabel](/powershell/module/azureinformationprotection/set-aipfilelabel)と[AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification)で新しい秘密度ラベルを適用できます。

- エクスプローラーの場合: [Azure Information Protection] ダイアログボックスで、新しい秘密度ラベルが表示されますが、設定されていません。

この構成では、古いラベルにマップする各機密ラベルに対して、 **labelByCustomProperties**という名前の高度な設定を指定する必要があります。 次に、各エントリに対して、次の構文を使用して値を設定します。

`[migration rule name],[Secure Islands custom property name],[Secure Islands metadata Regex value]`

任意の移行規則名を指定します。 前のラベル付けソリューションからの1つ以上のラベルを機密ラベルにマップする方法を特定するのに役立つわかりやすい名前を使用します。

この設定では、ドキュメントから元のラベルが削除されたり、元のラベルが適用された可能性がある視覚的マーキングが削除されたりすることはありません。 ヘッダーとフッターを削除するには、前のセクション「[他のラベル付けソリューションからヘッダーとフッターを削除](#remove-headers-and-footers-from-other-labeling-solutions)する」を参照してください。

#### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>例1: 同じラベル名の 1 対 1 のマッピング

要件: "社外秘" というセキュリティ保護された島ラベルを持つドキュメントは、Azure Information Protection によって "社外秘" というラベルが付けられます。

この例では:

- Secure Islands のラベルは、**Confidential** という名前が付けられ、**Classification** という名前のカスタム プロパティに保存されます。

詳細設定:

- キー: **labelByCustomProperties**

- 値:**セキュリティ保護された諸島ラベルは社外秘、分類、社外秘**

たとえば、"Confidential" というラベルが付いた PowerShell コマンドの例を次に示します。

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Confidential,Classification,Confidential"}

#### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>例 2: 異なるラベル名の 1 対 1 のマッピング

要件: セキュリティで保護されたアイランドによって "機微な" というラベルが付けられたドキュメントは、Azure Information Protection によって "機密性の高い" というラベルに再設定する

この例では:

- Secure Islands のラベルは **Sensitive** という名前が付けられ、**Classification** という名前のカスタム プロパティに保存されます。

詳細設定:

- キー: **labelByCustomProperties**

- 値:**セキュリティ保護された諸島ラベルは機密、分類、機密**

PowerShell コマンドの例。ラベルの名前は「非常に機密性の高い」です。

    Set-Label -Identity "Highly Confidential" -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Sensitive,Classification,Sensitive"}

#### <a name="example-3-many-to-one-mapping-of-label-names"></a>例 3: ラベル名の多対一のマッピング

要件: "Internal" という語を含む2つのセキュリティ保護された島々ラベルがあり、これらのセキュリティ保護された島々ラベルのいずれかを持つドキュメントを、Azure Information Protection の統合ラベル付けクライアントによって "全般" というラベルに書き換えます。

この例では:

- Secure Islands のラベルには、**Internal** という単語が含まれ、**Classification** という名前のカスタム プロパティに保存されます。

クライアントの詳細設定:

- キー: **labelByCustomProperties**

- 値:**セキュリティ保護された諸島ラベルに内部、分類、および\*内部\*が含まれ**ます

たとえば、"General" というラベルが付いた PowerShell コマンドの例を次に示します。

    Set-Label -Identity General -AdvancedSettings @{labelByCustomProperties="Secure Islands label contains Internal,Classification,.*Internal.*"}

#### <a name="example-4-multiple-rules-for-the-same-label"></a>例 4: 同じラベルに対して複数のルールを使用する

同じラベルに対して複数のルールが必要な場合は、同じキーに対して複数の文字列値を定義します。 

この例では、"Confidential" と "Secret" という名前のセキュリティで保護された諸島ラベルが "**分類**" という名前のカスタムプロパティに格納されていて、Azure Information Protection 統合ラベル付けクライアントに "confidential" という名前の秘密度ラベルを適用します。

    Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}

### <a name="extend-your-label-migration-rules-to-emails"></a>ラベルの移行ルールを電子メールに拡張する

追加のラベルポリシーの詳細設定を指定することにより、Office ドキュメントに加えて、Outlook 電子メールで labelByCustomProperties の詳細設定を使用できます。 ただし、この設定は Outlook のパフォーマンスには既知の悪影響を与えます。そのため、この追加設定は、ビジネス要件を十分に設定している場合にのみ構成します。また、その他のラベル付けソリューション。

この詳細設定を構成するには、選択したラベルポリシーに対して次の文字列を入力します。

- キー: **EnableLabelByMailHeader**

- 値: **True**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableLabelByMailHeader="True"}

### <a name="extend-your-label-migration-rules-to-sharepoint-properties"></a>ラベルの移行ルールを SharePoint プロパティに拡張する

ユーザーに列として公開される SharePoint プロパティで labelByCustomProperties の詳細設定を使用できます。

この設定は、Word、Excel、PowerPoint を使用する場合にサポートされます。

この詳細設定を構成するには、選択したラベルポリシーに対して次の文字列を入力します。

- キー: **EnableLabelBySharePointProperties**

- 値: **True**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

    Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableLabelBySharePointProperties="True"}

## <a name="apply-a-custom-property-when-a-label-is-applied"></a>ラベルが適用されたときにカスタムプロパティを適用する

この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるラベルの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

機密ラベルによって適用されるメタデータに加えて、1つまたは複数のカスタムプロパティをドキュメントまたは電子メールメッセージに適用する場合は、いくつかのシナリオが考えられます。

たとえば次のようになります。

- セキュリティで保護された島など、[別のラベル付けソリューションから移行](#migrate-labels-from-secure-islands-and-other-labeling-solutions)しています。 移行中の相互運用性を確保するために、機密ラベルを使用して、他のラベル付けソリューションで使用されるカスタムプロパティを適用することもできます。

- コンテンツ管理システム (SharePoint や別のベンダーのドキュメント管理ソリューションなど) の場合は、ラベルの値が異なる一貫したカスタムプロパティ名と、ラベル GUID ではなくユーザーフレンドリ名を使用します。

Azure Information Protection 統合ラベル付けクライアントを使用してユーザーにラベルを付ける Office ドキュメントおよび Outlook 電子メールの場合は、定義した1つまたは複数のカスタムプロパティを追加できます。 また、この方法を使用すると、統合されたラベル付けクライアントに対して、このカスタムプロパティを他のソリューションからラベルとして表示することもできます。

この構成オプションの結果として、次のように、Azure Information Protection 統合ラベル付けクライアントによって追加のカスタムプロパティが適用されます。

- Office ドキュメントの場合: デスクトップアプリでドキュメントにラベルが付けられている場合、ドキュメントの保存時に追加のカスタムプロパティが適用されます。

- Outlook 電子メールの場合: 電子メールメッセージが Outlook でラベル付けされている場合、電子メールが送信されるときに、追加のプロパティが x ヘッダーに適用されます。

- PowerShell の場合: [set-aipfilelabel](/powershell/module/azureinformationprotection/set-aipfilelabel)と[AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification)は、ドキュメントにラベルを付けて保存するときに、追加のカスタムプロパティを適用します。 [-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus)は、秘密度ラベルが適用されていない場合に、マップされたラベルとしてカスタムプロパティを表示します。

- エクスプローラーの場合: ユーザーがファイルを右クリックしてラベルを適用すると、カスタムプロパティが適用されます。

この構成では、追加のカスタムプロパティを適用する各機密ラベルに対して、 **Custompropertiesbylabel**という名前の詳細設定を指定する必要があります。 次に、各エントリに対して、次の構文を使用して値を設定します。

`[custom property name],[custom property value]`

#### <a name="example-1-add-a-single-custom-property-for-a-label"></a>例 1: ラベルに対して1つのカスタムプロパティを追加する

要件: Azure Information Protection の統一されたラベル付けクライアントによって "Confidential" というラベルが付けられているドキュメントには、"Secret" という値を持つ "分類" という名前の追加のカスタムプロパティが必要です。

この例では:

- 秘密度ラベルは**Confidential**という名前で、 **Secret**という値を持つ**分類**という名前のカスタムプロパティを作成します。

詳細設定:

- キー: **Custompropertiesbylabel**

- 値:**分類、シークレット**

たとえば、"Confidential" というラベルが付いた PowerShell コマンドの例を次に示します。

    Set-Label -Identity Confidential -AdvancedSettings @{customPropertiesByLabel="Classification,Secret"}

#### <a name="example-2-add-multiple-custom-properties-for-a-label"></a>例 2: ラベルに対して複数のカスタムプロパティを追加する

同じラベルに複数のカスタムプロパティを追加するには、同じキーに対して複数の文字列値を定義する必要があります。

たとえば、ラベルに "General" という名前が付けられていて、" **general** " と**いう名前の**カスタムプロパティと、" **Internal**" の値が指定さ**れた 2**番目のカスタムプロパティを追加する PowerShell コマンドの例を次に示します。

    Set-Label -Identity General -AdvancedSettings @{customPropertiesByLabel=ConvertTo-Json("Classification,General", "Sensitivity,Internal")}

## <a name="configure-a-label-to-apply-smime-protection-in-outlook"></a>ラベルを構成して Outlook で S/MIME 保護を適用する

この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるラベルの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

これらの設定は、動作中の[S/MIME 展開](https://docs.microsoft.com/microsoft-365/security/office-365-security/s-mime-for-message-signing-and-encryption)があり、Azure Information Protection からの Rights Management 保護ではなく、電子メールに対してこの保護方法を自動的に適用するラベルが必要な場合にのみ使用してください。 結果として得られる保護は、ユーザーが Outlook から手動で S/MIME オプションを選択した場合と同じものです。

S/MIME デジタル署名の詳細設定を構成するには、選択したラベルに次の文字列を入力します。

- キー: **SMimeSign**

- 値: **True**

S/MIME 暗号化の詳細設定を構成するには、選択したラベルに次の文字列を入力します。

- キー: **SMimeEncrypt**

- 値: **True**

指定したラベルが暗号化用に構成されている場合、Azure Information Protection の統合ラベル付けクライアントでは、S/MIME 保護は Outlook でのみ Rights Management の保護を置き換えます。 統一されたラベル付けクライアントの一般公開バージョンでは、管理センターのラベルに指定された暗号化設定が引き続き使用されます。 ラベルが組み込まれている Office アプリでは、S/MIME 保護は適用されませんが、代わりに [転送不可] 保護が適用されます。

Outlook でのみラベルを表示する場合は、 **outlook の電子メールメッセージのみ**に暗号化を適用するようにラベルを構成します。

たとえば、"受信者のみ" というラベルが付いた PowerShell コマンドの例を次に示します。

    Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeSign="True"}

    Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeEncrypt="True"}

## <a name="specify-a-default-sublabel-for-a-parent-label"></a>親ラベルに既定のサブラベルを指定する

この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるラベルの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

ラベルにサブラベルを追加すると、ユーザーはドキュメントまたは電子メールに親ラベルを適用できなくなります。 既定では、ユーザーは親ラベルを選択して、適用できるサブラベルを確認してから、サブラベルのいずれかを選択します。 この詳細設定を構成した場合、ユーザーが親ラベルを選択すると、サブラベルが自動的に選択されて適用されます。 

- キー: **DefaultSubLabelId**

- 値: \<サブラベル GUID >

たとえば、親ラベルの名前が "Confidential" で、"All Employees" サブラベルの GUID が8faca7b8-8d20-48a3-8ea2-0f96310a848e である PowerShell コマンドの例を次に示します。

    Set-Label -Identity "Confidential" -AdvancedSettings @{DefaultSubLabelId="8faca7b8-8d20-48a3-8ea2-0f96310a848e"}


## <a name="specify-a-color-for-the-label"></a>ラベルの色を指定します

この構成では、Office 365 セキュリティ/コンプライアンスセンター PowerShell を使用して構成する必要があるラベルの[詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell)を使用します。

この詳細設定を使用して、ラベルの色を設定します。 色を指定するには、色の赤、緑、および青 (RGB) コンポーネントの16進数の16進コードを入力します。 たとえば、#40e0d0 は水色の RGB 16 進値です。

これらのコードの参照が必要な場合は、MSDN web ドキュメントの[\<色 >](https://developer.mozilla.org/docs/Web/CSS/color_value)のページから役に立つテーブルを見つけることができます。また、これらのコードは、画像を編集できる多くのアプリケーションでも見つかります。 たとえば、Microsoft ペイントでは、パレットからカスタム色を選択できます。RGB 値が自動的に表示されるので、それをコピーできます。

ラベルの色の詳細設定を構成するには、選択したラベルに次の文字列を入力します。

- キー: **color**

- 値: \<RGB の16進値 >

PowerShell コマンドの例: ラベルの名前は "Public" です。

    Set-Label -Identity Public -AdvancedSettings @{color="#40e0d0"}

## <a name="sign-in-as-a-different-user"></a>別のユーザーでのサイン イン

運用環境では、ユーザーが Azure Information Protection 統合されたラベル付けクライアントを使用している場合、通常は別のユーザーとしてサインインする必要はありません。 ただし管理者の場合は、テスト段階のときに別ユーザーとしてサインインする必要がある場合があります。 

現在サインインしているアカウントを確認するには、 **[Microsoft Azure Information Protection]** ダイアログボックスを使用します。 Office アプリケーションを開き、 **[ホーム]** タブで **[秘密度]** ボタンを選択し、 **[ヘルプとフィードバック]** を選択します。 アカウント名が **[クライアント ステータス]** セクションに表示されます。

表示されるサインイン アカウントのドメイン名も必ず確認してください。 正しいアカウントでサインインしていてもドメインが間違っている、という状況は気付きにくいものです。 間違ったアカウントを使用すると、ラベルのダウンロードに失敗したり、予期したラベルや動作が表示されないことがあります。

別のユーザーでサイン インする方法は以下の通りです。

1. **%localappdata%\Microsoft\MSIP** に移動し、**TokenCache** ファイルを削除します。

2. 開いている Office アプリケーションがあれば再起動し、別のユーザー アカウントでサインインします。 Azure Information Protection サービスにサインインするためのプロンプトが Office アプリケーションに表示されない場合は、 **[Microsoft Azure Information Protection]** ダイアログボックスに戻り、更新された **[クライアントステータス]** セクションから **[サインイン]** を選択します。

さらに、本サービスには以下の規定が適用されます。

- これらの手順を完了した後も、Azure Information Protection 統合されたラベル付けクライアントが古いアカウントでサインインしている場合は、Internet Explorer からすべての cookie を削除してから、手順 1. と 2. を繰り返します。

- シングル サインオンを使用する場合は、トークン ファイルを削除した後に Windows からサインアウトし、別のユーザー アカウントでサインインする必要があります。 Azure Information Protection 統合されたラベル付けクライアントは、現在サインインしているユーザーアカウントを使用して自動的に認証します。

- このソリューションでは、同じテナントから別ユーザーとしてサインインする操作がサポートされています。 別のテナントから別のユーザーとしてサインインする操作はサポートされていません。 複数のテナントがある Azure Information Protection をテストするには、異なるコンピューターを使用します。

- **[ヘルプとフィードバック]** の **[設定のリセット]** オプションを使用すると、Office 365 セキュリティ/コンプライアンスセンター、Microsoft 365 セキュリティセンター、または Microsoft 365 コンプライアンスセンターから、現在ダウンロードされているラベルとポリシー設定をサインアウトしたり、削除したりできます。


## <a name="support-for-disconnected-computers"></a>切断されたコンピューターのサポート

> [!IMPORTANT]
> 切断されたコンピューターは、ファイルエクスプローラー、PowerShell、Office アプリ、およびスキャナーのラベル付けシナリオでサポートされています。

既定では、Azure Information Protection の統一されたラベル付けクライアントは、インターネットへの接続を自動的に試みて、ラベル付け管理センターからラベルとラベルポリシー設定をダウンロードします。 Office 365 セキュリティ/コンプライアンスセンター、Microsoft 365 security center、または Microsoft 365 コンプライアンスセンター。 一定期間インターネットに接続できないコンピューターがある場合は、統一されたラベル付けクライアントのポリシーを手動で管理するファイルをエクスポートしてコピーできます。

手順:

1. 切断されたコンピューターで使用するラベルおよびポリシー設定をダウンロードするために使用する Azure AD でユーザーアカウントを選択または作成します。

2. このアカウントの追加のラベルポリシー設定として、 **enableaudit**詳細設定を使用して[Azure Information Protection analytics への監査データの送信を無効](#disable-sending-audit-data-to-azure-information-protection-analytics)にします。
    
    切断されたコンピューターがインターネットに接続している場合は、手順1のユーザー名を含む Azure Information Protection analytics にログ情報を送信するので、この手順をお勧めします。 このユーザーアカウントは、切断されたコンピューターで使用しているローカルアカウントとは異なる場合があります。

3. 統一されたラベル付けクライアントがインストールされ、手順1のユーザーアカウントでサインインしているインターネット接続があるコンピューターから、ラベルとポリシー設定をダウンロードします。

4. このコンピューターから、ログファイルをエクスポートします。
    
    たとえば、 [export-Aiの gs](https://docs.microsoft.com/powershell/module/azureinformationprotection/export-aiplogs)コマンドレットを実行するか、クライアントの [[ヘルプとフィードバック](clientv2-admin-guide.md#installing-and-supporting-the-azure-information-protection-unified-labeling-client)] ダイアログボックスの **[ログのエクスポート]** オプションを使用します。 
    
    ログファイルは、1つの圧縮ファイルとしてエクスポートされます。

5.  圧縮ファイルを開き、MSIP フォルダーから、.xml ファイル名拡張子を持つファイルをコピーします。

6. これらのファイルを、切断されたコンピューターの **%localappdata%\Microsoft\MSIP**フォルダーに貼り付けます。

7. 選択したユーザーアカウントが通常インターネットに接続している場合は、 **enableaudit**値を**True**に設定して、監査データの送信を再度有効にします。

8. 接続が切断されたコンピューターがファイルを保護する、ファイルを再保護する、ファイルから保護を削除する、または保護されたファイルを検査するには、 *DelegatedUser*パラメーターを指定して[Set-aipauthentication](/powershell/module/azureinformationprotection/set-aipauthentication)コマンドレットを実行し、手順 1. のユーザーアカウントを指定してユーザーコンテキストを設定します。 たとえば次のようになります。
    
        Set-AIPAuthentication -TenantId "9c11c87a-ac8b-46a3-8d5c-f4d0b72ee29a" -DelegatedUser offlineuser@contoso.com

このコンピューターのユーザーが [[ヘルプとフィードバック](clientv2-admin-guide.md#help-and-feedback-section)] から **[設定のリセット]** オプションを選択した場合、この操作によってポリシーファイルが削除され、クライアントがファイルを手動で置き換えるか、クライアントがインターネットに接続してファイルをダウンロードするまで、クライアントが動作しなくなります。

切断されたコンピューターが Azure Information Protection スキャナーを実行している場合は、追加の構成手順を実行する必要があります。 詳細については、「制限: スキャナーサーバーがスキャナーの展開手順から[インターネットに接続できない](../deploy-aip-scanner.md#restriction-the-scanner-server-cannot-have-internet-connectivity)」を参照してください。

## <a name="change-the-local-logging-level"></a>ローカルのログ記録レベルを変更する

既定では Azure Information Protection 統合されたラベル付けクライアントは、クライアントログファイルを **%localappdata%\Microsoft\MSIP**フォルダーに書き込みます。 これらのファイルは、Microsoft サポートによるトラブルシューティングを目的としています。
 
これらのファイルのログ記録レベルを変更するには、レジストリで次の値の名前を探し、値のデータを必要なログ記録レベルに設定します。

**HKEY_CURRENT_USER \SOFTWARE\Microsoft\MSIP\LogLevel**

ログ記録レベルに次の値のいずれかを設定します。

- **オフ**: ローカルログはありません。

- **エラー**: エラーのみ。

- **警告**: エラーと警告。

- **Info**: 最小ログ記録。イベント id が含まれません (スキャナーの既定の設定)。

- **デバッグ**: 完全な情報。

- **トレース**: 詳細なログ記録 (クライアントの既定の設定)。

このレジストリ設定では、[中央レポート](../reports-aip.md)の Azure Information Protection に送信される情報は変更されません。

## <a name="next-steps"></a>次の手順
Azure Information Protection 統合されたラベル付けクライアントをカスタマイズしたので、このクライアントのサポートに必要な追加情報については、次のリソースを参照してください。

- [クライアント ファイルおよび使用状況ログの記録](client-admin-guide-files-and-logging.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)
