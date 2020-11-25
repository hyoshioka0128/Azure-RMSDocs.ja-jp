---
title: カスタム構成-Azure Information Protection 統合されたラベル付けクライアント
description: Windows 用に Azure Information Protection 統合ラベルクライアントをカスタマイズする方法について説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 5eb3a8a4-3392-4a50-a2d2-e112c9e72a78
ms.subservice: v2client
ms.reviewer: maayan
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: cd640f1fd60f1ca9872bb3741bfa5d1f0426b18e
ms.sourcegitcommit: 1c12edc8ca4bfac9eb4e87516908cafe6e5dd42a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96034389"
---
# <a name="admin-guide-custom-configurations-for-the-azure-information-protection-unified-labeling-client"></a>管理者ガイド: Azure Information Protection 統合ラベル付けクライアントのカスタム構成

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8、windows server 2019、windows server 2016、windows Server 2012 R2、windows server 2012*
>
>*Windows 7 または Office 2010 を使用している場合は、「 [AIP For windows And office versions in extended support](../known-issues.md#aip-for-windows-and-office-versions-in-extended-support)」を参照してください。*
>
> *手順: [Windows 用の Azure Information Protection 統合ラベル付けクライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

AIP の統一されたラベル付けクライアントを管理する際に、特定のシナリオまたはユーザーに必要な詳細な構成については、次の情報を参照してください。

> [!NOTE]
> これらの設定を行うには、レジストリを編集するか、詳細設定を指定する必要があります。 詳細設定では、 [Office 365 セキュリティ & コンプライアンスセンターの PowerShell](/powershell/exchange/office-365-scc/office-365-scc-powershell)を使用します。
> 

### <a name="how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell"></a>Office 365 セキュリティ & コンプライアンスセンター PowerShell を使用してクライアントの詳細設定を構成する方法

Office 365 Security & コンプライアンスセンターの PowerShell を使用すると、ラベルポリシーとラベルのカスタマイズをサポートする詳細設定を構成できます。 次に例を示します。

- Office アプリの Information Protection バーを表示する設定は、***ラベルポリシーの詳細設定** _ です。
- ラベルの色を指定する設定は、 _*_ラベルの詳細設定_*_ です。

どちらの場合も、 [Office 365 Security & コンプライアンスセンターの PowerShell に接続](/powershell/exchange/office-365-scc/connect-to-scc-powershell/connect-to-scc-powershell)した後、ポリシーまたはラベルの id (名前または GUID) を持つ _AdvancedSettings * パラメーターを指定し、 [ハッシュテーブル](/powershell/module/microsoft.powershell.core/about/about_hash_tables)でキーと値のペアを指定します。 使用する構文は以下のとおりです。

ラベルポリシー設定の場合、単一の文字列値:

```PowerShell
Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key="value1,value2"}
```

ラベルポリシー設定の場合は、同じキーに対して複数の文字列値を指定します。

```PowerShell
Set-LabelPolicy -Identity <PolicyName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}
```

ラベル設定の場合、単一の文字列値:

```PowerShell
Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key="value1,value2"}
```

ラベル設定の場合は、同じキーに対して複数の文字列値を指定します。

```PowerShell
Set-Label -Identity <LabelGUIDorName> -AdvancedSettings @{Key=ConvertTo-Json("value1", "value2")}
```

詳細設定を削除するには、同じ構文を使用しますが、null 文字列値を指定します。

> [!IMPORTANT]
> 文字列に空白を使用すると、ラベルの適用ができなくなります。 

#### <a name="examples-for-setting-advanced-settings"></a>詳細設定の設定例

例 1: 1 つの文字列値のラベルポリシーの詳細設定を設定します。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}
```

例 2: 1 つの文字列値に対して、ラベルの詳細設定を設定します。

```PowerShell
Set-Label -Identity Internal -AdvancedSettings @{smimesign="true"}
```

例 3: 複数の文字列値に対して、ラベルの詳細設定を設定します。

```PowerShell
Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}
```

例 4: null 文字列値を指定して、ラベルポリシーの詳細設定を削除します。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions=""}
```

#### <a name="specifying-the-identity-for-the-label-policy-or-label"></a>ラベルポリシーまたはラベルの id の指定

ラベルポリシーを管理する管理センターには、ポリシー名が1つだけ表示されるため、PowerShell *id* パラメーターにラベルポリシー名を指定するのは簡単です。 ただし、ラベルの場合、管理センターには **名前** と **表示名** の両方が表示されます。 場合によっては、両方の値が同じになりますが、異なっていてもかまいません。

- **Name** はラベルの元の名前であり、すべてのラベルで一意です。 作成したラベルの名前を変更しても、この値は変わりません。 Azure Information Protection から移行されたラベルの場合、Azure portal のラベルのラベル ID が表示されることがあります。

- [**表示名**] はユーザーに表示されるラベルの名前であり、すべてのラベルで一意である必要はありません。 たとえば、"**社外** 秘" と表示され **ている****すべて** の従業員をサブラベル、他の **すべての従業員** にサブラベルを持つユーザーがいるとします。 これらのサブラベルの両方に同じ名前が表示されますが、ラベルは同じではなく、設定も異なります。

ラベルの詳細設定を構成するには、[ **名前** ] の値を使用します。 たとえば、次の図でラベルを識別するには、次のように指定し `-Identity "All Company"` ます。

![秘密度ラベルを識別するには、' 表示名 ' ではなく ' Name ' を使用してください](../media/labelname_scc.png)

ラベル GUID を指定する場合、ラベルを管理する管理センターにはこの値が表示されません。 ただし、次の Office 365 セキュリティ & コンプライアンスセンターの PowerShell コマンドを使用して、この値を見つけることができます。

```PowerShell
Get-Label | Format-Table -Property DisplayName, Name, Guid
```

#### <a name="order-of-precedence---how-conflicting-settings-are-resolved"></a>優先順位-競合する設定の解決方法

機密ラベルを管理する管理センターの1つを使用して、次のラベルポリシー設定を構成できます。

- **このラベルを既定でドキュメントと電子メールに適用する**

- **ユーザーはラベルまたは下位分類ラベルを削除する理由を指定する必要があります**

- **ユーザーに電子メールまたはドキュメントへのラベルの適用を要求する**

- **カスタムヘルプページへのリンクをユーザーに提供する**

1人のユーザーに対して複数のラベルポリシーが構成されており、それぞれが異なるポリシー設定を持っている場合は、管理センターのポリシーの順序に従って、最後のポリシー設定が適用されます。 詳細については、「[ラベルポリシーの優先度 (順序](/microsoft-365/compliance/sensitivity-labels#label-policy-priority-order-matters)の問題)」を参照してください。

ラベルポリシーの詳細設定は、最後のポリシー設定を使用して同じロジックを使用して適用されます。 

> [!NOTE]
> Outlook に別の既定のラベルを設定できるようにするために、 [Outlookdefaultlabel](#set-a-different-default-label-for-outlook) の [詳細ラベル] ポリシー設定には、例外が現在存在しています。
> 
> OutlookDefaultLabel 設定が競合している場合は、管理センターのポリシーの順序に従って、 *最初* のポリシー設定から構成が取得されます。

#### <a name="available-advanced-settings-for-label-policies"></a>ラベルポリシーの使用可能な詳細設定

[新しい-labelpolicy](/powershell/module/exchange/policy-and-compliance/new-labelpolicy)と [設定-labelpolicy](/powershell/module/exchange/policy-and-compliance/set-labelpolicy)を指定して、 *advanced settings* パラメーターを使用します。

|設定|シナリオと手順|
|----------------|---------------|
|AdditionalPPrefixExtensions|[変更のサポート \<EXT> 。\<EXT> この詳細プロパティを使用して PFILE を P に](#additionalpprefixextensions)
|AttachmentAction|[添付ファイルのある電子メール メッセージの場合、その添付ファイルの最上位の分類と一致するラベルを適用します](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments)
|AttachmentActionTip|[添付ファイルのある電子メール メッセージの場合、その添付ファイルの最上位の分類と一致するラベルを適用します](#for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments) 
|DisableMandatoryInOutlook|[必須ラベルから Outlook メッセージを除外する](#exempt-outlook-messages-from-mandatory-labeling)
|EnableAudit|[Azure Information Protection analytics への監査データの送信を無効にする](#disable-sending-audit-data-to-azure-information-protection-analytics)|
|EnableContainerSupport|[PST、rar、7zip、および MSG ファイルからの保護の削除を有効にする](#enable-removal-of-protection-from-compressed-files)
|EnableCustomPermissions|[エクスプローラーでカスタムアクセス許可を無効にする](#disable-custom-permissions-in-file-explorer)|
|EnableCustomPermissionsForCustomProtectedFiles|[カスタム アクセス許可で保護されているファイルについて、ファイル エクスプローラーでカスタム アクセス許可を常にユーザーに表示する](#for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer) |
|EnableLabelByMailHeader|[Secure Islands からのラベルの移行と、その他のラベル付けのソリューション](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|EnableLabelBySharePointProperties|[Secure Islands からのラベルの移行と、その他のラベル付けのソリューション](#migrate-labels-from-secure-islands-and-other-labeling-solutions)
|HideBarByDefault デフォルト)|[Office アプリの Information Protection バーを表示します](#display-the-information-protection-bar-in-office-apps)|
|JustificationTextForUserText | [変更されたラベルの理由プロンプトテキストをカスタマイズする](#customize-justification-prompt-texts-for-modified-labels) |
|LogMatchedContent|[情報の種類の一致を Azure Information Protection analytics に送信する](#send-information-type-matches-to-azure-information-protection-analytics)|
|OutlookBlockTrustedDomains|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookBlockUntrustedCollaborationLabel|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookCollaborationRule| [Outlook ポップアップメッセージをカスタマイズする](#customize-outlook-popup-messages)|
|OutlookDefaultLabel|[Outlook に別の既定ラベルを設定する](#set-a-different-default-label-for-outlook)|
|Outlookジャスト Ifytrusteddomains|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookJustifyUntrustedCollaborationLabel|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookRecommendationEnabled|[Outlook で推奨分類を有効にする](#enable-recommended-classification-in-outlook)|
|OutlookOverrideUnlabeledCollaborationExtensions|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookSkipSmimeOnReadingPaneEnabled | [S/MIME メールで Outlook のパフォーマンスの問題を回避する](#prevent-outlook-performance-issues-with-smime-emails)|
|OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnTrustedDomains|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|OutlookWarnUntrustedCollaborationLabel|[Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する](#implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent)|
|PFileSupportedExtensions|[保護するファイルの種類を変更する](#change-which-file-types-to-protect)|
|PostponeMandatoryBeforeSave|[必須のラベル付けを使用するときにドキュメントの "後で" を削除する](#remove-not-now-for-documents-when-you-use-mandatory-labeling)|
|RemoveExternalContentMarkingInApp|[他のラベル付けソリューションからヘッダーとフッターを削除する](#remove-headers-and-footers-from-other-labeling-solutions)|
|RemoveExternalMarkingFromCustomLayouts | [PowerPoint でカスタムレイアウトから外部コンテンツマークを削除する](#remove-external-content-marking-from-custom-layouts-in-powerpoint)|
|ReportAnIssueLink|[ユーザー向けの "問題の報告" を追加する](#add-report-an-issue-for-users)|
|RunPolicyInBackground|[バックグラウンドでの分類の継続的実行をオンにする](#turn-on-classification-to-run-continuously-in-the-background)
|ScannerConcurrencyLevel|[スキャナーで使用されるスレッドの数を制限する](#limit-the-number-of-threads-used-by-the-scanner)|
|Scantaskattributeattributeskip | [ファイル属性に応じてスキャン中にファイルをスキップまたは無視する](#skip-or-ignore-files-during-scans-depending-on-file-attributes)
|SharepointWebRequestTimeout| [SharePoint のタイムアウトを構成する](#configure-sharepoint-timeouts)|
|SharepointFileWebRequestTimeout |[SharePoint のタイムアウトを構成する](#configure-sharepoint-timeouts)|
|UseCopyAndPreserveNTFSOwner | [ラベル付け中に NTFS 所有者を保持する](#preserve-ntfs-owners-during-labeling-public-preview)

"Global" という名前のラベルポリシーに対してラベルポリシー設定が有効であることを確認する PowerShell コマンドの例を次に示します。

```PowerShell
(Get-LabelPolicy -Identity Global).settings
```

#### <a name="available-advanced-settings-for-labels"></a>ラベルに使用できる詳細設定

[新しいラベル](/powershell/module/exchange/policy-and-compliance/new-label)と [セットラベル](/powershell/module/exchange/policy-and-compliance/set-label)を使用して、 *advanced settings* パラメーターを使用します。

|設定|シナリオと手順|
|----------------|---------------|
|color|[ラベルの色を指定する](#specify-a-color-for-the-label)|
|customPropertiesByLabel|[ラベルが適用されたときにカスタムプロパティを適用する](#apply-a-custom-property-when-a-label-is-applied)|
|DefaultSubLabelId|[親ラベルに既定のサブラベルを指定する](#specify-a-default-sublabel-for-a-parent-label) 
|labelByCustomProperties|[Secure Islands からのラベルの移行と、その他のラベル付けのソリューション](#migrate-labels-from-secure-islands-and-other-labeling-solutions)|
|SMimeEncrypt|[ラベルを構成して Outlook で S/MIME 保護を適用する](#configure-a-label-to-apply-smime-protection-in-outlook)|
|SMimeSign|[ラベルを構成して Outlook で S/MIME 保護を適用する](#configure-a-label-to-apply-smime-protection-in-outlook)|

"Public" という名前のラベルに対して有効なラベル設定を確認する PowerShell コマンドの例を次に示します。

```PowerShell
(Get-Label -Identity Public).settings
```

## <a name="display-the-information-protection-bar-in-office-apps"></a>Display the Information Protection bar in Office apps\(Office アプリの Information Protection バーを表示する\)

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるポリシーの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

既定では、ユーザーは、[**秘密度**] ボタンから [**バーの表示**] オプションを選択して、Office アプリの Information Protection バーを表示する必要があります。 **Hidebarbydefault デフォルト** キーを使用して、値を **False** に設定すると、ユーザーがバーまたはボタンからラベルを選択できるように、このバーが自動的に表示されます。 

選択したラベルポリシーについて、次の文字列を指定します。

- キー: **Hidebarbydefault デフォルト**

- 値: **False**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{HideBarByDefault="False"}
```

## <a name="exempt-outlook-messages-from-mandatory-labeling"></a>必須ラベルから Outlook メッセージを除外する

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるポリシーの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

既定では、すべてのドキュメントのラベルポリシー設定を有効にし、 **電子メールにラベルを付ける必要** がある場合、保存されているすべてのドキュメントと送信された電子メールにラベルが適用されている必要があります。 次の詳細設定を構成すると、ポリシー設定は Office ドキュメントにのみ適用され、Outlook メッセージには適用されません。

選択したラベルポリシーについて、次の文字列を指定します。

- キー: **DisableMandatoryInOutlook**

- 値: **True**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{DisableMandatoryInOutlook="True"}
```

## <a name="enable-recommended-classification-in-outlook"></a>Outlook で推奨分類を有効にする

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるポリシーの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

推奨分類のラベルを設定すると、Word、Excel、PowerPoint では、推奨ラベルを受け入れるか、却下するように求められます。 また、このラベル推奨が Outlook でも表示されます。

選択したラベルポリシーについて、次の文字列を指定します。

- キー: **OutlookRecommendationEnabled**

- 値: **True**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookRecommendationEnabled="True"}
```

## <a name="enable-removal-of-protection-from-compressed-files"></a>圧縮ファイルからの保護の削除を有効にする

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるポリシーの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

この設定を構成すると、  [PowerShell](./clientv2-admin-guide-powershell.md) コマンドレット **set-aipfilelabel** が有効になり、PST、rar、7ZIP、および MSG ファイルからの保護の削除が可能になります。

- キー: **EnableContainerSupport**

- 値: **True**

ポリシーが有効になっている PowerShell コマンドの例:

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableContainerSupport="True"}
```

## <a name="set-a-different-default-label-for-outlook"></a>Outlook に別の既定ラベルを設定します

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるポリシーの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

この設定を構成すると、Outlook では、[ **既定でドキュメントと電子メールにこのラベルを適用する**] オプションのポリシー設定として構成されている既定のラベルが適用されません。 別の既定のラベルを適用できるか、ラベルがありません。

選択したラベルポリシーについて、次の文字列を指定します。

- キー: **OutlookDefaultLabel**

- 値: \<**label GUID**> または **None**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookDefaultLabel="None"}
```

## <a name="change-which-file-types-to-protect"></a>保護するファイルの種類を変更する

これらの構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるポリシーの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

既定では、Azure Information Protection の統一されたラベル付けクライアントは、すべてのファイルの種類を保護します。クライアントのスキャナーは、Office のファイルの種類と PDF ファイルのみを保護します。

次のいずれかを指定することで、選択したラベルポリシーのこの既定の動作を変更できます。

### <a name="pfilesupportedextension"></a>PFileSupportedExtension

- キー: **PFileSupportedExtensions**

- 数値 **\<string value>** 

次の表を使用して、指定する文字列値を指定します。

| 文字列値| Client| スキャナー|
|-------------|-------|--------|
|\*|既定値: すべてのファイルの種類に保護を適用します。|すべてのファイルの種類に保護を適用する|
|Convertto-html (".jpg", ".png")|Office のファイルの種類と PDF ファイルに加えて、指定したファイル名拡張子に保護を適用します。 | Office のファイルの種類と PDF ファイルに加えて、指定したファイル名拡張子に保護を適用します。
| | | |

例 1: すべてのファイルの種類を保護するためのスキャナーの PowerShell コマンド: ラベルポリシーの名前は "Scanner" です。

```PowerShell
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions="*"}
```

例 2: スキャナーの PowerShell コマンドを使用して、Office ファイルと PDF ファイルに加え、.txt ファイルと .csv ファイルを保護します。ここで、ラベルポリシーには "Scanner" という名前を付けます。

```PowerShell
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{PFileSupportedExtensions=ConvertTo-Json(".txt", ".csv")}
```

この設定では、保護するファイルの種類を変更できますが、既定の保護レベルをネイティブから汎用に変更することはできません。 たとえば、統一されたラベル付けクライアントを実行しているユーザーに対しては、既定の設定を変更して、Office ファイルと PDF ファイルのみをすべてのファイルの種類ではなく保護するようにすることができます。 ただし、これらのファイルの種類は、pfile ファイル名拡張子で汎用的に保護されるように変更することはできません。

### <a name="additionalpprefixextensions"></a>AdditionalPPrefixExtensions

統一されたラベル付けクライアントは、変更をサポート \<EXT> します。詳細プロパティの AdditionalPPrefixExtensions を使用して、PFILE を P にし \<EXT> ます。 **AdditionalPPrefixExtensions** この詳細プロパティは、右クリック、PowerShell、およびスキャナーでサポートされています。 すべてのアプリの動作は似ています。   

- キー: **AdditionalPPrefixExtensions**

- 数値 **\<string value>** 

次の表を使用して、指定する文字列値を指定します。

| 文字列値| クライアントとスキャナー|
|-------------|---------------|
|\*|すべての PFile 拡張機能は P になります\<EXT>|
|\<null value>| 既定値は、既定の保護値のように動作します。|
|Convertto-html (".dwg", ".zip")|前の一覧に加えて、".dwg" と ".zip" は P になります。\<EXT>| 

例 1: 保護 ".dwg" が "pfile" になる既定の動作と同じように動作する PowerShell コマンド。

```PowerShell
Set-LabelPolicy -AdvancedSettings @{ AdditionalPPrefixExtensions =""}
```

例 2: ファイルが保護されている場合に、すべての PFile 拡張機能を汎用保護 (PFile) からネイティブ保護 (. pdwg) に変更する PowerShell コマンド:

```PowerShell
Set-LabelPolicy -AdvancedSettings @{ AdditionalPPrefixExtensions ="*"}
```

例 3: このサービスを使用するときに ".dwg" を ". pdwg" に変更する PowerShell コマンドを次のように保護します。

```PowerShell
Set-LabelPolicy -AdvancedSettings @{ AdditionalPPrefixExtensions =ConvertTo-Json(".dwg")}
```

この設定では、次の拡張機能 (「」を使用します。 txt "、" .xml "、" .bmp "、" jfif "、" .jpg "、" .jpeg "、" jpe "、". .png "、" "、". jpe "、" .png "、" .tif "、" tiff "、" .gif ") は常に P になり \<EXT> ます。注目すべき除外とは、"ptxt" が "pfile" にならないことです。 
**AdditionalPPrefixExtensions** は、advanced プロパティ- [**Pfilesupportedexテンション**](#pfilesupportedextension) が有効になっている場合にのみ機能します。 

## <a name="remove-not-now-for-documents-when-you-use-mandatory-labeling"></a>必須のラベル付けを使用するときにドキュメントの "後で" を削除する

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるポリシーの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

すべてのドキュメントにラベルポリシー設定を使用し、 **電子メールにラベルを付ける必要が** ある場合、ユーザーは Office ドキュメントを最初に保存するときにラベルを選択し、Outlook から電子メールを送信するように求められます。

ドキュメントの場合、ユーザーは **[後で]** を選択して一時的にメッセージを無視し、ラベルを選んで、ドキュメントに戻ることができます。 ただし、ラベルを付けないと、保したドキュメントを閉じることはできません。 

**PostponeMandatoryBeforeSave** 設定を構成すると、[ **Not now** ] オプションが削除され、ユーザーはドキュメントが最初に保存されたときにラベルを選択する必要があります。

> [!TIP]
> また、 **PostponeMandatoryBeforeSave** 設定によって、電子メールで送信される前に共有ドキュメントにラベルが付けられるようにもなります。 
>
>既定では、 **すべてのドキュメントと電子メール** がポリシーで有効になっている必要がある場合でも、ユーザーは Outlook 内から電子メールに添付されたラベルファイルにのみ昇格されます。  
> 
選択したラベルポリシーについて、次の文字列を指定します。

- キー: **PostponeMandatoryBeforeSave**

- 値: **False**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{PostponeMandatoryBeforeSave="False"}
```

## <a name="remove-headers-and-footers-from-other-labeling-solutions"></a>他のラベル付けソリューションからヘッダーとフッターを削除する

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるポリシーの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

他のラベル付けソリューションから分類を削除するには、2つの方法があります。 最初のメソッドは、図形名が詳細プロパティ **WordShapeNameToRemove** で定義されている名前と一致する word 文書から図形を削除します。2番目の方法では、 **Removeexternalcontentmarkinginapp** 詳細プロパティで定義されている、word、Excel、および PowerPoint ドキュメントからテキストベースのヘッダーまたはフッターを削除または置換できます。 

### <a name="use-the-wordshapenametoremove-advanced-property"></a>WordShapeNameToRemove advanced プロパティを使用する

***WordShapeNameToRemove** advanced プロパティは、バージョン2.6.101.0 以降でサポートされています。*

この設定を使用すると、別のラベル付けソリューションによって視覚的なマーキングが適用されている場合に、Word 文書から図形ベースのラベルを削除または置換できます。 たとえば、図形には、新しいラベル名と独自の図形を使用するために、機密ラベルに移行した古いラベルの名前が含まれています。

この詳細プロパティを使用するには、Word 文書で図形名を検索し、図形の **WordShapeNameToRemove** 詳細プロパティリストで定義する必要があります。 この詳細プロパティの図形の一覧で定義されている名前で始まる Word の図形は、サービスによって削除されます。

削除するすべての図形の名前を定義し、リソースを集中的に使用するプロセスであるすべての図形のテキストをチェックしないようにすることで、無視するテキストを含む図形を削除しないようにします。

この追加の詳細プロパティ設定で Word 図形を指定せず、 **Removeexternalcontentmarkinginapp** キー値に word が含まれている場合は、 **Externalcontentmarkingtorclean** 値で指定したテキストのすべての図形がチェックされます。 

使用していて除外する図形の名前を検索するには、次のようにします。

1. Word で、**選択** ウィンドウを表示します。 [**ホーム**] タブ >**編集** グループ > 選択] ウィンドウの [オプション > 選択 **] ウィンドウ****を選択** します。

2. 削除対象としてマークするページ上の図形を選択します。 マークした図形の名前が **選択** ウィンドウで強調表示されるようになりました。

図形の名前を使用して、* * * * WordShapeNameToRemove * * * キーの文字列値を指定します。 

例: シェイプ名は **dc** です。 この名前の図形を削除するには、値 `dc` を指定します。

- キー: **WordShapeNameToRemove**

- 値: \<**Word shape name**> 

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{WordShapeNameToRemove="dc"}
```

複数の単語図形を削除する場合は、削除する図形の数を指定します。

### <a name="use-the-removeexternalcontentmarkinginapp-advanced-property"></a>RemoveExternalContentMarkingInApp 詳細設定プロパティの使用

この設定を使用すると、別のラベル付けソリューションによって視覚的なマーキングが適用されている場合に、テキストベースのヘッダーまたはフッターをドキュメントから削除したり置き換えることができます。 たとえば、古いフッターには、新しいラベル名とその独自のフッターを使用するために、機密ラベルに移行した古いラベルの名前が含まれています。

統一されたラベル付けクライアントがポリシーでこの構成を取得すると、Office アプリでドキュメントを開いたときに古いヘッダーとフッターが削除されるか、またはドキュメントに機密ラベルが適用されます。

この構成は Outlook ではサポートされていません。そのため、この構成を Word、Excel、PowerPoint で使用すると、ユーザーのこれらのアプリのパフォーマンスに悪影響が生じる場合があります。 この構成ではアプリケーションごとの設定を定義することができます。たとえば、Word 文書のヘッダーとフッターのテキストは検索し、Excel のスプレッドシートや PowerPoint のプレゼンテーションのテキストは検索しないようにできます。

パターンマッチングはユーザーのパフォーマンスに影響するため、Office アプリケーションの種類 (**W** Ord、E **X** セル、 **P** owerpoint) は、検索する必要があるものだけに制限することをお勧めします。
選択したラベルポリシーについて、次の文字列を指定します。
- キー: **RemoveExternalContentMarkingInApp**

- 値: \<**Office application types WXP**> 

次に例を示します。

- Word 文書のみを検索するには、**W** を指定します。

- Word 文書と PowerPoint プレゼンテーションを検索するには、**WP** を指定します。

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInApp="WX"}
```

この後、ヘッダーまたはフッターの内容と、その削除または置換方法を指定したりするために、少なくとも 1 つのより詳細なクライアント設定 **ExternalContentMarkingToRemove** が必要です。

### <a name="how-to-configure-externalcontentmarkingtoremove"></a>ExternalContentMarkingToRemove を構成する方法

**Externalcontentmarkingtoremove** キー] に文字列値を指定すると、正規表現を使用する3つのオプションが表示されます。 これらの各シナリオについて、次の表の「 **値の例** 」の列に示されている構文を使用します。

|オプション  |説明の例 |値の例|
|---------|---------|---------|
|**ヘッダーまたはフッター内のすべてを削除する部分的な一致**     | ヘッダーまたはフッターには、 **削除する文字列テキスト** が含まれており、これらのヘッダーまたはフッターを完全に削除する必要があります。   |`*TEXT*`  | 
|**ヘッダーまたはフッター内の特定の単語だけを削除するには、[一致する文字列を入力します。**     |    ヘッダーまたはフッターには **削除する文字列テキスト** が含まれており、 **テキスト** のみを削除して、ヘッダーまたはフッター文字列を **削除** する場合は削除します。      |`TEXT ` |
|**ヘッダーまたはフッター内のすべてを削除するための完全一致**     |ヘッダーまたはフッターには、 **削除する文字列テキスト** が含まれています。 正確にこの文字列が含まれているヘッダーまたはフッターを削除したいとします。         |`^TEXT TO REMOVE$`|
|     |         | |


指定した文字列のパターン マッチングでは大文字と小文字が区別されます。 文字列の最大長は255文字で、空白を含めることはできません。 

一部のドキュメントには非表示の文字やさまざまな種類のスペースやタブが含まれているため、語句や文に指定した文字列が検出されない可能性があります。 値には、できるだけ単独の特徴的な単語を指定し、運用環境に展開する前に結果をテストしてください。

同じラベルポリシーについて、次の文字列を指定します。

- キー: **ExternalContentMarkingToRemove**

- 値: \<**string to match, defined as regular expression**> 

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*TEXT*"}
```

#### <a name="multiline-headers-or-footers"></a>複数行のヘッダーまたはフッター

ヘッダーまたはフッターのテキストが複数行にわたる場合は、行ごとにキーと値を作成します。 たとえば、次の2行のフッターがあるとします。

**ファイルは社外秘として分類**

**ラベルは手動で適用**

この複数行のフッターを削除するには、同じラベルポリシーに対して次の2つのエントリを作成します。

- キー: **ExternalContentMarkingToRemove**

- キー値 1: **\* 社外秘***

- キー値 2: **\* ラベルが適用され** ました* 

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{ExternalContentMarkingToRemove="*Confidential*,*Label applied*"}
```

#### <a name="optimization-for-powerpoint"></a>PowerPoint 用の最適化

PowerPoint のヘッダーとフッターは、図形として実装されます。 

ヘッダーまたはフッターでは *なく* 、指定したテキストを含む図形を削除しないようにするには、 **PowerPointShapeNameToRemove** という名前の追加のアドバンストクライアント設定を使用します。 また、すべての図形のテキストのチェックはリソースを消費するプロセスであるため、この設定を使用して回避することをお勧めします。

- この追加のクライアントの詳細設定を指定せず、PowerPoint が **RemoveExternalContentMarkingInApp** キーの値に含まれている場合、**ExternalContentMarkingToRemove** で指定したテキストがすべての図形でチェックされます。 

- この値が指定されている場合は、図形名の条件を満たす図形だけでなく、 **Externalcontentmarkingtoremove** によって提供された文字列と一致するテキストも削除されます。

また、PowerPoint でカスタムレイアウトが構成されている場合、既定の動作では、カスタムレイアウト内で見つかった図形は無視されます。 カスタムレイアウト内から外部コンテンツマーキングを明示的に削除するには、 **Removeexternalmarkingfromcustomlayouts** 詳細プロパティを true に設定し **ます。**

> [!NOTE]
> このセクションで説明するクライアントの詳細設定でサポートされている PowerPoint 図形の種類は、 **Msotextbox、** **MsoTextEffect、** および **msotextbox** です。
>
##### <a name="find-the-name-of-the-shape-that-youre-using-as-a-header-or-footer"></a>ヘッダーまたはフッターとして使用している図形の名前を検索する

1. PowerPoint の **選択** ウィンドウを表示し、**[書式]** タブ > **[配置]** グループ > **[選択ウィンドウ]** の順に選択します。

2. ヘッダーまたはフッターを含むスライド上の図形を選択します。 選択した図形の名前が、**選択** ウィンドウで強調表示されます。

図形の名前を使用して、**PowerPointShapeNameToRemove** キーの文字列値を指定します。 

**例:** 図形名は **fc** です。 この名前の図形を削除するには、値 `fc` を指定します。

- キー: **PowerPointShapeNameToRemove**

- 値: \<**PowerPoint shape name**> 

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{PowerPointShapeNameToRemove="fc"}
```

複数の PowerPoint 図形を削除する場合は、削除する図形の数を指定します。

既定では、マスター スライドのヘッダーとフッターのみがチェックされます。 この検索の対象をすべてのスライドに広げるには、**RemoveExternalContentMarkingInAllSlides** という名前の、追加のクライアントの詳細設定を使用します。ただし、このプロセスはリソースをより多く消費します。

- キー: **RemoveExternalContentMarkingInAllSlides**

- 値: **True**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalContentMarkingInAllSlides="True"}
```

##### <a name="remove-external-content-marking-from-custom-layouts-in-powerpoint"></a>PowerPoint でカスタムレイアウトから外部コンテンツマークを削除する

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるポリシーの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

既定では、外部コンテンツマーキングを削除するために使用されるロジックは、PowerPoint で構成されたカスタムレイアウトを無視します。 このロジックをカスタムレイアウトに拡張するには、 **Removeexternalmarkingfromcustomlayouts** 詳細プロパティを **True** に設定します。

- キー: **Removeexternalmarkingfromcustomlayouts**

- 値: **True**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{RemoveExternalMarkingFromCustomLayouts="True"}
```

## <a name="disable-custom-permissions-in-file-explorer"></a>エクスプローラーでカスタムアクセス許可を無効にする

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるポリシーの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

既定では、ユーザーはエクスプローラーで右クリックして [**分類と保護**] を選択すると、[**カスタムアクセス許可で保護** する] というオプションが表示されます。 このオプションを使用すると、ラベルの構成に含まれている可能性のある保護設定を上書きできる、独自の保護設定を設定できます。 ユーザーには、保護を削除するオプションも表示されます。 この設定を構成すると、ユーザーにはこれらのオプションが表示されません。

この詳細設定を構成するには、選択したラベルポリシーに対して次の文字列を入力します。

- キー: **EnableCustomPermissions**

- 値: **False**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissions="False"}
```

## <a name="for-files-protected-with-custom-permissions-always-display-custom-permissions-to-users-in-file-explorer"></a>カスタム アクセス許可で保護されているファイルについて、ファイル エクスプローラーでカスタム アクセス許可を常にユーザーに表示する

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるポリシーの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

[エクスプローラーでカスタムアクセス許可を無効](#disable-custom-permissions-in-file-explorer)にするように [高度なクライアント] 設定を構成した場合、既定では、ユーザーは保護されたドキュメントで既に設定されているカスタムアクセス許可を表示または変更できません。

ただし、このシナリオでは、ユーザーがエクスプローラーを使用してファイルを右クリックして、保護されたドキュメントのカスタムアクセス許可を表示および変更できるように、さらに詳細なクライアント設定を指定することもできます。

この詳細設定を構成するには、選択したラベルポリシーに対して次の文字列を入力します。

- キー: **EnableCustomPermissionsForCustomProtectedFiles**

- 値: **True**

PowerShell コマンドの例:

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableCustomPermissionsForCustomProtectedFiles="True"}
```

## <a name="for-email-messages-with-attachments-apply-a-label-that-matches-the-highest-classification-of-those-attachments"></a>添付ファイル付きの電子メール メッセージの場合、添付ファイルの最上位の分類に一致するラベルを適用します

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるポリシーの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

この設定は、ユーザーがラベル付きドキュメントを電子メールに添付するときに、電子メールメッセージ自体にラベルを付けない場合に使用します。 このシナリオでは、添付ファイルに適用される分類ラベルに基づいて、ラベルが自動的に選択されます。 最高の分類ラベルが選択されます。

添付ファイルは物理ファイルである必要があり、ファイルへのリンク (たとえば、Microsoft SharePoint または OneDrive 上のファイルへのリンク) を指定することはできません。

この設定を [ **推奨**] に構成すると、ユーザーは、カスタマイズ可能なツールヒントを使用して、選択したラベルを電子メールメッセージに適用するように求められます。 ユーザーは、推奨設定を受け入れるか、通知を閉じます。 または、この設定を [ **自動**] に構成できます。選択したラベルは自動的に適用されますが、ユーザーは電子メールを送信する前に、ラベルを削除したり、別のラベルを選択したりできます。

> [!NOTE]
> 最高の分類ラベルを持つ添付ファイルが、ユーザー定義のアクセス許可の設定を使用して保護するように構成されている場合は、次のようになります。
> 
> - ラベルのユーザー定義のアクセス許可に Outlook ([転送不可]) が含まれている場合、そのラベルが選択され、電子メールに [転送防止] が適用されません。
> - ラベルのユーザー定義アクセス許可が Word、Excel、PowerPoint、およびエクスプローラー専用の場合、そのラベルは電子メールメッセージには適用されず、保護もされません。
> 

この詳細設定を構成するには、選択したラベルポリシーに対して次の文字列を入力します。

- キー 1: **Attachmentaction**

- キー値 1: **推奨** または **自動**

- キー 2: **Attachmentactiontip**

- キー値 2: " \<customized tooltip> "

カスタマイズしたツールヒントでは、単一の言語のみがサポートされます。

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{AttachmentAction="Automatic"}
```

## <a name="add-report-an-issue-for-users"></a>ユーザー向けの "問題の報告" を追加する

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるポリシーの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

次のクライアントの詳細設定を指定すると、ユーザーに、**[ヘルプとフィードバック]** クライアント ダイアログ ボックスから選択できる **[問題の報告]** オプションが表示されます。 リンクの HTTP 文字列を指定します。 たとえば、ユーザーが問題を報告するための、カスタマイズされた独自の Web ページや、ヘルプ デスクに送信される電子メール アドレスです。 

この詳細設定を構成するには、選択したラベルポリシーに対して次の文字列を入力します。

- キー: **ReportAnIssueLink**

- 数値 **\<HTTP string>**

Web サイトの値の例: `https://support.contoso.com`

メール アドレスの値の例: `mailto:helpdesk@contoso.com`

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{ReportAnIssueLink="mailto:helpdesk@contoso.com"}
```

## <a name="implement-pop-up-messages-in-outlook-that-warn-justify-or-block-emails-being-sent"></a>Outlook で、送信される電子メールに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装する

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるポリシーの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

次のクライアント詳細設定を作成して構成すると、Outlook でユーザーに対してポップアップ メッセージが表示されます。これにより、次のどちらかのシナリオで、電子メールを送信する前に警告したり、電子メールの送信理由の入力を求めたり、電子メールの送信を妨げることができます。

- **電子メール、または電子メールの添付ファイルに特定のラベルが含まれる**:
    - 添付ファイルはあらゆる種類のファイルである可能性がある

- **電子メール、または電子メールの添付ファイルにラベルがない**:
    - 添付ファイルは Office ドキュメントまたは PDF ドキュメントである可能性がある

これらの条件が満たされると、ユーザーには、次のいずれかの操作を含むポップアップメッセージが表示されます。

- **警告**: ユーザーは、確認して送信するか、キャンセルすることができます。

- [**ジャスティファイ**]: ユーザーに対して理由 (定義済みオプションまたは自由形式) の入力を求められます。  その後、ユーザーは電子メールを送信またはキャンセルできます。 理由のテキストは、他のシステムで読み取ることができるように電子メールの X ヘッダーに書き込まれます。 たとえば、データ損失防止 (DLP) サービスです。

- **ブロック**: 条件が残っている間、ユーザーは電子メールを送信できません。 メッセージには、ユーザーが問題に対処できるように、電子メールをブロックする理由が含まれます。 たとえば、特定の受信者を削除する、電子メールにラベルを付けるなどです。 

ポップアップメッセージが特定のラベルに対して実行されている場合は、ドメイン名を使用して受信者の例外を構成できます。

これらの設定を構成する方法のチュートリアルの例については、ビデオ [Azure Information Protection Outlook のポップアップ構成](https://azure.microsoft.com/resources/videos/how-to-configure-azure-information-protection-popup-for-outlook/) を参照してください。

> [!TIP]
> ドキュメントが Outlook の外部から共有されている場合でもポップアップが表示されるようにするには **(ファイル > 共有 > コピーを添付します)、** [PostponeMandatoryBeforeSave](#remove-not-now-for-documents-when-you-use-mandatory-labeling) の詳細設定を構成することもできます。

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-specific-labels"></a>特定のラベルに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装するには:

選択したポリシーについて、次のキーを使用して次の詳細設定を1つ以上作成します。 値には、1つまたは複数のラベルを Guid で指定し、それぞれをコンマで区切って指定します。

複数のラベル Guid の値の例 (コンマ区切り文字列): 

```sh
dcf781ba-727f-4860-b3c1-73479e31912b,1ace2cc3-14bc-4142-9125-bf946a70542c,3e9df74d-3168-48af-8b11-037e3021813f
```

- 警告メッセージ: 
    
    - キー: **OutlookWarnUntrustedCollaborationLabel**
    
    - 値: \<**label GUIDs, comma-separated**>

- 理由の入力メッセージ: 
    
    - キー: **OutlookJustifyUntrustedCollaborationLabel**
    
    - 値: \<**label GUIDs, comma-separated**>

- ブロック メッセージ: 
    
    - キー: **OutlookBlockUntrustedCollaborationLabel**
    
    - 値: \<**label GUIDs, comma-separated**>


PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookWarnUntrustedCollaborationLabel="8faca7b8-8d20-48a3-8ea2-0f96310a848e,b6d21387-5d34-4dc8-90ae-049453cec5cf,bb48a6cb-44a8-49c3-9102-2d2b017dcead,74591a94-1e0e-4b5d-b947-62b70fc0f53a,6c375a97-2b9b-4ccd-9c5b-e24e4fd67f73"}

Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyUntrustedCollaborationLabel="dc284177-b2ac-4c96-8d78-e3e1e960318f,d8bb73c3-399d-41c2-a08a-6f0642766e31,750e87d4-0e91-4367-be44-c9c24c9103b4,32133e19-ccbd-4ff1-9254-3a6464bf89fd,74348570-5f32-4df9-8a6b-e6259b74085b,3e8d34df-e004-45b5-ae3d-efdc4731df24"}

Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockUntrustedCollaborationLabel="0eb351a6-0c2d-4c1d-a5f6-caa80c9bdeec,40e82af6-5dad-45ea-9c6a-6fe6d4f1626b"}
```

#### <a name="to-exempt-domain-names-for-pop-up-messages-configured-for-specific-labels"></a>特定のラベル用に構成されたポップアップメッセージのドメイン名を除外するには

これらのポップアップメッセージで指定したラベルについては、特定のドメイン名を除外して、そのドメイン名が電子メールアドレスに含まれている受信者のメッセージがユーザーに表示されないようにすることができます。 この場合、電子メールは中断なく送信されます。 複数のドメインを指定するには、ドメインをコンマで区切って 1 つの文字列として追加します。

一般的な構成では、組織の外部の受信者、または組織の承認済みのパートナーではない受信者についてのみ、ポップアップ メッセージが表示されます。 この場合は、お客様の組織およびパートナーによって使用されるすべての電子メール ドメインを指定します。

同じラベルポリシーについて、次の高度なクライアント設定を作成し、値として1つ以上のドメインをコンマで区切って指定します。

コンマ区切り文字列としての複数のドメインの値の例: `contoso.com,fabrikam.com,litware.com`

- 警告メッセージ: 
    
    - キー: **OutlookWarnTrustedDomains**
    
    - 数値 **\<**domain names, comma separated**>**

- 理由の入力メッセージ: 
    
    - キー: **Outlookジャスト Ifytrusteddomains**
    
    - 数値 **\<**domain names, comma separated**>**

- ブロック メッセージ: 
    
    - キー: **Outlookblocktrusteddomains**
    
    - 数値 **\<**domain names, comma separated**>**

たとえば、[**社外秘 \ すべての従業員**] ラベルに対して **OutlookBlockUntrustedCollaborationLabel** アドバンストクライアント設定を指定したとします。 ここで、 **Outlookジャスト Ifytrusteddomains** と **contoso.com** の追加のアドバンストクライアント設定を指定します。 その結果、ユーザーは、" john@sales.contoso.com **社外秘 \ すべての従業員** " というラベルが付いたときに電子メールをに送信できますが、Gmail アカウントに同じラベルの電子メールを送信することは禁止されます。

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookBlockTrustedDomains="gmail.com"}

Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookJustifyTrustedDomains="contoso.com,fabrikam.com,litware.com"}
```

### <a name="to-implement-the-warn-justify-or-block-pop-up-messages-for-emails-or-attachments-that-dont-have-a-label"></a>ラベルのない電子メールまたは添付ファイルに対する警告、理由の入力、またはブロックのためのポップアップ メッセージを実装するには:

同じラベルポリシーについて、次のいずれかの値を使用して次のアドバンストクライアント設定を作成します。

- 警告メッセージ: 
    
    - キー: **OutlookUnlabeledCollaborationAction**
    
    - 値: **Warn**

- 理由の入力メッセージ: 
    
    - キー: **OutlookUnlabeledCollaborationAction**
    
    - 値:**均等** 配置

- ブロック メッセージ: 
    
    - キー: **OutlookUnlabeledCollaborationAction**
    
    - 値: **ブロック**

- これらのメッセージをオフにする: 
    
    - キー: **OutlookUnlabeledCollaborationAction**
    
    - 値: **オフ**


PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationAction="Warn"}
```

#### <a name="to-define-specific-file-name-extensions-for-the-warn-justify-or-block-pop-up-messages-for-email-attachments-that-dont-have-a-label"></a>ラベルのない電子メールの添付ファイルのポップアップメッセージに対して、警告、配置、またはブロックを行うための特定のファイル名拡張子を定義するには

既定では、すべての Office ドキュメントおよび PDF ドキュメントに対して、ポップアップメッセージの警告、位置揃え、またはブロックが適用されます。 この一覧を調整するには、[警告]、[メッセージを表示する]、または [ブロックするメッセージ] に、追加の詳細設定とファイル名拡張子のコンマ区切りの一覧を表示するファイル名拡張子を指定します。

コンマ区切りの文字列として定義する複数のファイル名拡張子の値の例を次に示します。 `.XLSX,.XLSM,.XLS,.XLTX,.XLTM,.DOCX,.DOCM,.DOC,.DOCX,.DOCM,.PPTX,.PPTM,.PPT,.PPTX,.PPTM`

この例では、ラベル付けされていない PDF ドキュメントは、ポップアップメッセージの警告、配置、またはブロックにはなりません。

同じラベルポリシーについて、次の文字列を入力します。 


- キー: **OutlookOverrideUnlabeledCollaborationExtensions**

- 数値 **\<**file name extensions to display messages, comma separated**>**


PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookOverrideUnlabeledCollaborationExtensions=".PPTX,.PPTM,.PPT,.PPTX,.PPTM"}
```

#### <a name="to-specify-a-different-action-for-email-messages-without-attachments"></a>添付ファイルのない電子メールメッセージに対して別のアクションを指定するには

既定では、ポップアップメッセージを表示するために OutlookUnlabeledCollaborationAction に指定する値は、ラベルのない電子メールまたは添付ファイルに適用されます。 添付ファイルのない電子メールメッセージに対して、別の詳細設定を指定することで、この構成を調整できます。

次のいずれかの値を使用して、次のクライアント詳細設定を作成します。

- 警告メッセージ: 
    
    - キー: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - 値: **Warn**

- 理由の入力メッセージ: 
    
    - キー: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - 値:**均等** 配置

- ブロック メッセージ: 
    
    - キー: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - 値: **ブロック**

- これらのメッセージをオフにする: 
    
    - キー: **OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior**
    
    - 値: **オフ**

このクライアント設定を指定しない場合は、OutlookUnlabeledCollaborationAction に指定した値が、添付ファイルのない電子メールメッセージと、添付ファイルを含むラベルなしの電子メールメッセージに使用されます。

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookUnlabeledCollaborationActionOverrideMailBodyBehavior="Warn"}
```

## <a name="disable-sending-audit-data-to-azure-information-protection-analytics"></a>Azure Information Protection analytics への監査データの送信を無効にする

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるポリシーの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

Azure Information Protection 統合されたラベル付けクライアントは、中央レポートをサポートします。既定では、は監査データを [Azure Information Protection analytics](../reports-aip.md)に送信します。 送信および保存される情報の詳細については、中央レポートのドキュメントの「 [収集して Microsoft に送信する](../reports-aip.md#information-collected-and-sent-to-microsoft) 情報」セクションを参照してください。

この動作を変更して、この情報が統合ラベルクライアントによって送信されないようにするには、選択したラベルポリシーに対して次の文字列を入力します。

- キー: **Enableaudit**

- 値: **False**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableAudit="False"}
```

## <a name="send-information-type-matches-to-azure-information-protection-analytics"></a>情報の種類の一致を Azure Information Protection analytics に送信する
 
この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるポリシーの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

既定では、統一されたラベル付けクライアントは、機密情報の種類のコンテンツの一致を [Azure Information Protection analytics](../reports-aip.md)に送信しません。 送信できるこの追加情報の詳細については、中央レポートのドキュメントの「詳細な [分析のためのコンテンツの一致](../reports-aip.md#content-matches-for-deeper-analysis) 」を参照してください。

機密情報の種類が送信されたときにコンテンツの一致を送信するには、ラベルポリシーで次のアドバンストクライアント設定を作成します。 

- キー: **Logmatchedcontent**

- 値: **True**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{LogMatchedContent="True"}
```

## <a name="limit-cpu-consumption"></a>CPU 消費量の制限

スキャナーは、全体的なコンピューターの CPU が85% を超えることがないように、リソースの消費を制限します。 

スキャナーバージョン 2.7. x. x から、CPU の使用量を制限することをお勧めします。この場合 **、cpu の詳細設定** 方法として、次の **スキャン** を行います。 

> [!IMPORTANT]
> 次のスレッド制限ポリシーが使用されている場合、 **Scanare maxcpu** および **Scanare mincpu** の詳細設定は無視されます。 **スキャン** を使用して cpu 消費を制限し、cpu の詳細設定を **スキャン** するには、スレッドの数を制限するポリシーの使用を取り消します。 

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるポリシーの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

スキャナーコンピューターの CPU 使用量を制限するために、 **Scanmachines maxcpu** と **Scanmachines mincpu** の2つの詳細設定を作成することにより、管理が容易になります。 

既定では、 **Scanで maxcpu** は100に設定されています。つまり、cpu の最大消費量に制限はありません。 この場合、スキャナープロセスは、使用可能なすべての CPU 時間を使用してスキャンレートを最大化しようとします。

**Scan@ Maxcpu** を100未満に設定すると、スキャナーは過去30分間の cpu 使用量を監視し、最大 cpu が設定した制限を超えた場合は、新しいファイルに割り当てられたスレッドの数を減らし始めます。 スレッド数の制限は、CPU 消費量が、 **scanで** 設定されている値よりも大きい場合に限り、続行します。

Scanに **cpu** がチェックされるのは、 **scan@ cpu** が100と等しくない場合のみです。 **Scanに cpu** を設定することはできません、 **scanている cpu** の数。 Scanの **cpu** を少なくとも15点以上に設定する  **ことをお** 勧めします。   

この設定の既定値は50です。つまり、過去30分間の CPU 使用量がこの値を下回ると、スキャナーは新しいスレッドを追加して、より多くのファイルを同時にスキャンするようにします。これにより、CPU 使用量がスキャンに **よって設定** されたレベルに達します。 

## <a name="limit-the-number-of-threads-used-by-the-scanner"></a>スキャナーで使用されるスレッドの数を制限する

> [!IMPORTANT]
> 次のスレッド制限ポリシーが使用されている場合、 **Scanare maxcpu** および **Scanare mincpu** の詳細設定は無視されます。 **スキャン** を使用して cpu 消費を制限し、cpu の詳細設定を **スキャン** するには、スレッドの数を制限するポリシーの使用を取り消します。 

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるポリシーの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

既定では、スキャナー サービスを実行しているコンピューター上の利用可能なプロセッサ リソースのすべてがスキャナーによって使われます。 このサービスのスキャン中に CPU 使用量を制限する必要がある場合は、ラベルポリシーで次の詳細設定を作成します。 

値には、スキャナーが並列で実行できる同時スレッドの数を指定します。 スキャナーでは、それがスキャンするファイルごとに個別のスレッドが使われます。このため、この調整構成によって並列でスキャンできるファイルの数も定義されます。 

最初にテスト用の値を構成するときは、コアごとに 2 を指定してから、その結果を監視することをお勧めします。 たとえば、4 コアのコンピューター上でスキャナーを実行する場合、最初は値を 8 に設定します。 必要な場合は、スキャナー コンピューターとスキャン速度に対してご自身が要求する結果のパフォーマンスに応じて、その数を増減させます。 

- キー: **ScannerConcurrencyLevel**

- 数値 **\<number of concurrent threads>**

PowerShell コマンドの例: ラベルポリシーの名前は "Scanner" です。

```PowerShell
Set-LabelPolicy -Identity Scanner -AdvancedSettings @{ScannerConcurrencyLevel="8"}
```

## <a name="migrate-labels-from-secure-islands-and-other-labeling-solutions"></a>Secure Islands からのラベルの移行と、その他のラベル付けのソリューション

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要がある、ラベルの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

この構成は、ファイル名拡張子が ppdf の保護された PDF ファイルと互換性がありません。 これらのファイルは、エクスプローラーまたは PowerShell を使用してクライアントで開くことはできません。

保護された島々でラベル付けされている Office ドキュメントの場合、定義したマッピングを使用して、これらのドキュメントのラベルを機密ラベルにすることができます。 また、この方法を使用して、他のソリューションからのラベルを、そのラベルが Office ドキュメントにある場合は再利用することができます。 

この構成オプションの結果として、次のように、Azure Information Protection 統合ラベル付けクライアントによって新しい感度ラベルが適用されます。

- Office ドキュメントの場合: デスクトップアプリでドキュメントを開くと、新しい秘密度ラベルが設定済みとして表示され、ドキュメントの保存時に適用されます。

- PowerShell の場合: [set-aipfilelabel](/powershell/module/azureinformationprotection/set-aipfilelabel) と [AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification) で新しい秘密度ラベルを適用できます。

- エクスプローラーの場合: [Azure Information Protection] ダイアログボックスで、新しい秘密度ラベルが表示されますが、設定されていません。

この構成では、古いラベルにマップする各機密ラベルに対して、 **labelByCustomProperties** という名前の高度な設定を指定する必要があります。 次に、各エントリに対して、次の構文を使用して値を設定します。

`[migration rule name],[Secure Islands custom property name],[Secure Islands metadata Regex value]`

任意の移行規則名を指定します。 前のラベル付けソリューションからの1つ以上のラベルを機密ラベルにマップする方法を特定するのに役立つわかりやすい名前を使用します。

この設定では、ドキュメントから元のラベルが削除されたり、元のラベルが適用された可能性がある視覚的マーキングが削除されたりすることはありません。 ヘッダーとフッターを削除するには、前のセクション「 [他のラベル付けソリューションからヘッダーとフッターを削除](#remove-headers-and-footers-from-other-labeling-solutions)する」を参照してください。

#### <a name="example-1-one-to-one-mapping-of-the-same-label-name"></a>例1: 同じラベル名の 1 対 1 のマッピング

要件: "社外秘" というセキュリティ保護された島ラベルを持つドキュメントは、Azure Information Protection によって "社外秘" というラベルが付けられます。

この例では、次のように記述されています。

- Secure Islands のラベルは、**Confidential** という名前が付けられ、**Classification** という名前のカスタム プロパティに保存されます。

詳細設定:

- キー: **labelByCustomProperties**

- 値: **セキュリティ保護された諸島ラベルは社外秘、分類、社外秘**

たとえば、"Confidential" というラベルが付いた PowerShell コマンドの例を次に示します。

```PowerShell
Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Confidential,Classification,Confidential"}
```

#### <a name="example-2-one-to-one-mapping-for-a-different-label-name"></a>例 2: 異なるラベル名の 1 対 1 のマッピング

要件: セキュリティで保護されたアイランドによって "機微な" というラベルが付けられたドキュメントは、Azure Information Protection によって "機密性の高い" というラベルに再設定する

この例では、次のように記述されています。

- Secure Islands のラベルは **Sensitive** という名前が付けられ、**Classification** という名前のカスタム プロパティに保存されます。

詳細設定:

- キー: **labelByCustomProperties**

- 値: **セキュリティ保護された諸島ラベルは機密、分類、機密**

PowerShell コマンドの例。ラベルの名前は「非常に機密性の高い」です。

```PowerShell
Set-Label -Identity "Highly Confidential" -AdvancedSettings @{labelByCustomProperties="Secure Islands label is Sensitive,Classification,Sensitive"}
```

#### <a name="example-3-many-to-one-mapping-of-label-names"></a>例 3: ラベル名の多対一のマッピング

要件: "Internal" という語を含む2つのセキュリティ保護された島々ラベルがあり、これらのセキュリティ保護された島々ラベルのいずれかを持つドキュメントを、Azure Information Protection の統合ラベル付けクライアントによって "全般" というラベルに書き換えます。

この例では、次のように記述されています。

- Secure Islands のラベルには、**Internal** という単語が含まれ、**Classification** という名前のカスタム プロパティに保存されます。

クライアントの詳細設定:

- キー: **labelByCustomProperties**

- 値:**セキュリティ保護された諸島ラベルには、内部、分類、およびが含まれます。 \*内部。 \***

たとえば、"General" というラベルが付いた PowerShell コマンドの例を次に示します。

```PowerShell
Set-Label -Identity General -AdvancedSettings @{labelByCustomProperties="Secure Islands label contains Internal,Classification,.*Internal.*"}
```

#### <a name="example-4-multiple-rules-for-the-same-label"></a>例 4: 同じラベルに対して複数のルールを使用する

同じラベルに対して複数のルールが必要な場合は、同じキーに対して複数の文字列値を定義します。 

この例では、"Confidential" と "Secret" という名前のセキュリティで保護された諸島ラベルが " **分類**" という名前のカスタムプロパティに格納されていて、Azure Information Protection 統合ラベル付けクライアントに "confidential" という名前の秘密度ラベルを適用します。

```PowerShell
Set-Label -Identity Confidential -AdvancedSettings @{labelByCustomProperties=ConvertTo-Json("Migrate Confidential label,Classification,Confidential", "Migrate Secret label,Classification,Secret")}
```

### <a name="extend-your-label-migration-rules-to-emails"></a>ラベルの移行ルールを電子メールに拡張する

Office ドキュメントに加えて、Outlook 電子メールの [*labelByCustomProperties*](#migrate-labels-from-secure-islands-and-other-labeling-solutions) 詳細設定で定義した構成を、追加のラベルポリシーの詳細設定を指定することによって使用できます。 

ただし、この設定は Outlook のパフォーマンスには既知の悪影響を与えます。そのため、この追加設定は、ビジネス要件が強い場合にのみ構成し、他のラベル付けソリューションからの移行を完了したときには null 文字列値に設定するようにしてください。

この詳細設定を構成するには、選択したラベルポリシーに対して次の文字列を入力します。

- キー: **EnableLabelByMailHeader**

- 値: **True**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableLabelByMailHeader="True"}
```

### <a name="extend-your-label-migration-rules-to-sharepoint-properties"></a>ラベルの移行ルールを SharePoint プロパティに拡張する

定義した構成は、追加のラベルポリシーの詳細設定を指定することによって、ユーザーに列として公開される SharePoint プロパティの [*labelByCustomProperties*](#migrate-labels-from-secure-islands-and-other-labeling-solutions) 詳細設定で使用できます。

この設定は、Word、Excel、PowerPoint を使用する場合にサポートされます。

この詳細設定を構成するには、選択したラベルポリシーに対して次の文字列を入力します。

- キー: **EnableLabelBySharePointProperties**

- 値: **True**

PowerShell コマンドの例: ラベルポリシーの名前は "Global" です。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{EnableLabelBySharePointProperties="True"}
```

## <a name="apply-a-custom-property-when-a-label-is-applied"></a>ラベルが適用されたときにカスタムプロパティを適用する

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要がある、ラベルの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

機密ラベルによって適用されるメタデータに加えて、1つまたは複数のカスタムプロパティをドキュメントまたは電子メールメッセージに適用する場合は、いくつかのシナリオが考えられます。

次に例を示します。

- セキュリティで保護された島など、 [別のラベル付けソリューションから移行](#migrate-labels-from-secure-islands-and-other-labeling-solutions)しています。 移行中の相互運用性を確保するために、機密ラベルを使用して、他のラベル付けソリューションで使用されるカスタムプロパティを適用することもできます。

- コンテンツ管理システム (SharePoint や別のベンダーのドキュメント管理ソリューションなど) の場合は、ラベルの値が異なる一貫したカスタムプロパティ名と、ラベル GUID ではなくユーザーフレンドリ名を使用します。

Azure Information Protection 統合ラベル付けクライアントを使用してユーザーにラベルを付ける Office ドキュメントおよび Outlook 電子メールの場合は、定義した1つまたは複数のカスタムプロパティを追加できます。 また、この方法を使用すると、統合されたラベル付けクライアントに対して、このカスタムプロパティを他のソリューションからラベルとして表示することもできます。

この構成オプションの結果として、次のように、Azure Information Protection 統合ラベル付けクライアントによって追加のカスタムプロパティが適用されます。

- Office ドキュメントの場合: デスクトップアプリでドキュメントにラベルが付けられている場合、ドキュメントの保存時に追加のカスタムプロパティが適用されます。

- Outlook 電子メールの場合: 電子メールメッセージが Outlook でラベル付けされている場合、電子メールが送信されるときに、追加のプロパティが x ヘッダーに適用されます。

- PowerShell の場合: [set-aipfilelabel](/powershell/module/azureinformationprotection/set-aipfilelabel) と [AIPFileClassificiation](/powershell/module/azureinformationprotection/set-aipfileclassification) は、ドキュメントにラベルを付けて保存するときに、追加のカスタムプロパティを適用します。 [-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) は、秘密度ラベルが適用されていない場合に、マップされたラベルとしてカスタムプロパティを表示します。

- エクスプローラーの場合: ユーザーがファイルを右クリックしてラベルを適用すると、カスタムプロパティが適用されます。

この構成では、追加のカスタムプロパティを適用する各機密ラベルに対して、 **Custompropertiesbylabel** という名前の詳細設定を指定する必要があります。 次に、各エントリに対して、次の構文を使用して値を設定します。

```sh
[custom property name],[custom property value]
```

> [!IMPORTANT]
> 文字列に空白を使用すると、ラベルの適用ができなくなります。

#### <a name="example-1-add-a-single-custom-property-for-a-label"></a>例 1: ラベルに対して1つのカスタムプロパティを追加する

要件: Azure Information Protection の統一されたラベル付けクライアントによって "Confidential" というラベルが付けられているドキュメントには、"Secret" という値を持つ "分類" という名前の追加のカスタムプロパティが必要です。

この例では、次のように記述されています。

- 秘密度ラベルは **Confidential** という名前で、 **Secret** という値を持つ **分類** という名前のカスタムプロパティを作成します。

詳細設定:

- キー: **Custompropertiesbylabel**

- 値: **分類、シークレット**

たとえば、"Confidential" というラベルが付いた PowerShell コマンドの例を次に示します。

```PowerShell
    Set-Label -Identity Confidential -AdvancedSettings @{customPropertiesByLabel="Classification,Secret"}
```

#### <a name="example-2-add-multiple-custom-properties-for-a-label"></a>例 2: ラベルに対して複数のカスタムプロパティを追加する

同じラベルに複数のカスタムプロパティを追加するには、同じキーに対して複数の文字列値を定義する必要があります。

たとえば、ラベルに "General" という名前が付けられていて、" **general** " と **いう名前の** カスタムプロパティと、" **Internal**" の値が指定さ **れた 2** 番目のカスタムプロパティを追加する PowerShell コマンドの例を次に示します。

```PowerShell
Set-Label -Identity General -AdvancedSettings @{customPropertiesByLabel=ConvertTo-Json("Classification,General", "Sensitivity,Internal")}
```

## <a name="configure-a-label-to-apply-smime-protection-in-outlook"></a>ラベルを構成して Outlook で S/MIME 保護を適用する

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるラベルの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

これらの設定は、動作中の [S/MIME 展開](/microsoft-365/security/office-365-security/s-mime-for-message-signing-and-encryption) があり、Azure Information Protection からの Rights Management 保護ではなく、電子メールに対してこの保護方法を自動的に適用するラベルが必要な場合にのみ使用してください。 結果として得られる保護は、ユーザーが Outlook から手動で S/MIME オプションを選択した場合と同じものです。

S/MIME デジタル署名の詳細設定を構成するには、選択したラベルに次の文字列を入力します。

- キー: **SMimeSign**

- 値: **True**

S/MIME 暗号化の詳細設定を構成するには、選択したラベルに次の文字列を入力します。

- キー: **SMimeEncrypt**

- 値: **True**

指定したラベルが暗号化用に構成されている場合、Azure Information Protection の統合ラベル付けクライアントでは、S/MIME 保護は Outlook でのみ Rights Management の保護を置き換えます。 統一されたラベル付けクライアントの一般公開バージョンでは、管理センターのラベルに指定された暗号化設定が引き続き使用されます。 ラベルが組み込まれている Office アプリでは、S/MIME 保護は適用されませんが、代わりに [転送不可] 保護が適用されます。

Outlook でのみラベルを表示する場合は、 **outlook の電子メールメッセージのみ** に暗号化を適用するようにラベルを構成します。

たとえば、"受信者のみ" というラベルが付いた PowerShell コマンドの例を次に示します。

```PowerShell
Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeSign="True"}

Set-Label -Identity "Recipients Only" -AdvancedSettings @{SMimeEncrypt="True"}
```

## <a name="specify-a-default-sublabel-for-a-parent-label"></a>親ラベルに既定のサブラベルを指定する

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要がある、ラベルの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

ラベルにサブラベルを追加すると、ユーザーはドキュメントまたは電子メールに親ラベルを適用できなくなります。 既定では、ユーザーは親ラベルを選択して、適用できるサブラベルを確認してから、サブラベルのいずれかを選択します。 この詳細設定を構成した場合、ユーザーが親ラベルを選択すると、サブラベルが自動的に選択されて適用されます。 

- キー: **DefaultSubLabelId**

- 値: \<sublabel GUID>

たとえば、親ラベルの名前が "Confidential" で、"All Employees" サブラベルの GUID が8faca7b8-8d20-48a3-8ea2-0f96310a848e である PowerShell コマンドの例を次に示します。

```PowerShell
Set-Label -Identity "Confidential" -AdvancedSettings @{DefaultSubLabelId="8faca7b8-8d20-48a3-8ea2-0f96310a848e"}
```

## <a name="turn-on-classification-to-run-continuously-in-the-background"></a>バックグラウンドでの分類の継続的実行をオンにする

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要がある、ラベルの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。 

この設定を構成すると、Azure Information Protection 統合されたラベル付けクライアントがドキュメントに自動および推奨のラベルを適用する方法の既定の動作が変更されます。

Word、Excel、PowerPoint に対して、自動分類はバックグラウンドで継続的に実行されます。

この動作は Outlook でも変わりません。
Azure Information Protection 統合されたラベル付けクライアントが指定された条件ルールのドキュメントを定期的にチェックすると、この動作により、SharePoint に格納されているドキュメントの自動および推奨の分類と保護が有効になります。 条件規則が既に実行されているため、大きなファイルもすばやく保存されます。

条件規則がユーザーの入力と同時にリアルタイムで実行されることはありません。 ドキュメントが変更された場合、バックグラウンド タスクとして定期的に実行されます。

この詳細設定を構成するには、次の文字列を入力します。

- キー: **RunPolicyInBackground**
- 値: **True**

PowerShell コマンドの例: 

```PowerShell
Set-LabelPolicy -Identity PolicyName -AdvancedSettings @{RunPolicyInBackground = "true"}
```

> [!NOTE]
> 現在、この機能はプレビュー段階にあります。 [Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)には、ベータ版、プレビュー版、またはまだ一般提供されていない Azure 機能に適用される追加の法律条項が含まれています。 
> 

## <a name="specify-a-color-for-the-label"></a>ラベルの色を指定する

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるラベルの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

この詳細設定を使用して、ラベルの色を設定します。 色を指定するには、色の赤、緑、および青 (RGB) コンポーネントの16進数の16進コードを入力します。 たとえば、#40e0d0 は水色の RGB 16 進値です。

これらのコードの参照が必要な場合は、MSDN web docs のページにある役に立つテーブルを確認でき [\<color>](https://developer.mozilla.org/docs/Web/CSS/color_value) ます。また、これらのコードは、画像を編集できる多くのアプリケーションでも見つかります。 たとえば、Microsoft ペイントでは、パレットからカスタム色を選択できます。RGB 値が自動的に表示されるので、それをコピーできます。

ラベルの色の詳細設定を構成するには、選択したラベルに次の文字列を入力します。

- キー: **color**

- 値: \<RGB hex value>

PowerShell コマンドの例: ラベルの名前は "Public" です。

```PowerShell
Set-Label -Identity Public -AdvancedSettings @{color="#40e0d0"}
```

## <a name="sign-in-as-a-different-user"></a>別のユーザーでのサイン イン

複数のユーザーによるサインインは、運用環境の AIP ではサポートされていません。 この手順では、テスト目的でのみ別のユーザーとしてサインインする方法について説明します。

現在サインインしているアカウントを確認するには、[ **Microsoft Azure Information Protection** ] ダイアログボックスを使用します。 Office アプリケーションを開き、[ **ホーム** ] タブで [ **秘密度** ] ボタンを選択し、[ **ヘルプとフィードバック**] を選択します。 アカウント名が **[クライアント ステータス]** セクションに表示されます。

表示されるサインイン アカウントのドメイン名も必ず確認してください。 正しいアカウントでサインインしていてもドメインが間違っている、という状況は気付きにくいものです。 間違ったアカウントを使用すると、ラベルのダウンロードに失敗したり、予期したラベルや動作が表示されないことがあります。

別のユーザーでサイン インする方法は以下の通りです。

1. **%localappdata%\Microsoft\MSIP** に移動し、**TokenCache** ファイルを削除します。

2. 開いている Office アプリケーションがあれば再起動し、別のユーザー アカウントでサインインします。 Azure Information Protection サービスにサインインするためのプロンプトが Office アプリケーションに表示されない場合は、[ **Microsoft Azure Information Protection** ] ダイアログボックスに戻り、[更新された **クライアントステータス**] セクションから [**サインイン**] を選択します。

追加として:

- これらの手順を完了した後も、Azure Information Protection 統合されたラベル付けクライアントが古いアカウントでサインインしている場合は、Internet Explorer からすべての cookie を削除してから、手順 1. と 2. を繰り返します。

- シングル サインオンを使用する場合は、トークン ファイルを削除した後に Windows からサインアウトし、別のユーザー アカウントでサインインする必要があります。 Azure Information Protection 統合されたラベル付けクライアントは、現在サインインしているユーザーアカウントを使用して自動的に認証します。

- このソリューションでは、同じテナントから別ユーザーとしてサインインする操作がサポートされています。 別のテナントから別のユーザーとしてサインインする操作はサポートされていません。 複数のテナントがある Azure Information Protection をテストするには、異なるコンピューターを使用します。

- **ヘルプとフィードバック** の [**設定のリセット**] オプションを使用すると、Office 365 セキュリティ & コンプライアンスセンター、Microsoft 365 セキュリティセンター、または Microsoft 365 コンプライアンスセンターから、現在ダウンロードされているラベルとポリシー設定をサインアウトしたり、削除したりできます。


## <a name="support-for-disconnected-computers"></a>切断されたコンピューターのサポート

> [!IMPORTANT]
> 切断されたコンピューターは、ファイルエクスプローラー、PowerShell、Office アプリ、およびスキャナーのラベル付けシナリオでサポートされています。

既定では、Azure Information Protection の統一されたラベル付けクライアントは、インターネットへの接続を自動的に試みて、ラベル管理センター (Office 365 セキュリティ & コンプライアンスセンター、Microsoft 365 セキュリティセンター、または Microsoft 365 コンプライアンスセンター) からラベルとラベルのポリシー設定をダウンロードします。 一定期間インターネットに接続できないコンピューターがある場合は、統一されたラベル付けクライアントのポリシーを手動で管理するファイルをエクスポートしてコピーできます。

手順: 

1. 切断されたコンピューターで使用するラベルおよびポリシー設定をダウンロードするために使用する Azure AD でユーザーアカウントを選択または作成します。

2. このアカウントの追加のラベルポリシー設定として、 **enableaudit** 詳細設定を使用して [Azure Information Protection analytics への監査データの送信を無効](#disable-sending-audit-data-to-azure-information-protection-analytics)にします。
    
    切断されたコンピューターがインターネットに接続している場合は、手順1のユーザー名を含む Azure Information Protection analytics にログ情報を送信するので、この手順をお勧めします。 このユーザーアカウントは、切断されたコンピューターで使用しているローカルアカウントとは異なる場合があります。

3. 統一されたラベル付けクライアントがインストールされ、手順1のユーザーアカウントでサインインしているインターネット接続があるコンピューターから、ラベルとポリシー設定をダウンロードします。

4. このコンピューターから、ログファイルをエクスポートします。
    
    たとえば、 [export-Aiの gs](/powershell/module/azureinformationprotection/export-aiplogs)コマンドレットを実行するか、クライアントの [[ヘルプとフィードバック](clientv2-admin-guide.md#installing-and-supporting-the-azure-information-protection-unified-labeling-client)] ダイアログボックスの [**ログのエクスポート**] オプションを使用します。 
    
    ログファイルは、1つの圧縮ファイルとしてエクスポートされます。

5.  圧縮ファイルを開き、MSIP フォルダーから、.xml ファイル名拡張子を持つファイルをコピーします。

6. これらのファイルを、切断されたコンピューターの **%localappdata%\Microsoft\MSIP** フォルダーに貼り付けます。

7. 選択したユーザーアカウントが通常インターネットに接続している場合は、 **enableaudit** 値を **True** に設定して、監査データの送信を再度有効にします。

このコンピューターのユーザーが [[ヘルプとフィードバック](clientv2-admin-guide.md#help-and-feedback-section)] から [**設定のリセット**] オプションを選択した場合、この操作によってポリシーファイルが削除され、クライアントがファイルを手動で置き換えるか、クライアントがインターネットに接続してファイルをダウンロードするまで、クライアントが動作しなくなります。

切断されたコンピューターが Azure Information Protection スキャナーを実行している場合は、追加の構成手順を実行する必要があります。 詳細については、「制限: スキャナーサーバーがスキャナーの展開手順から [インターネットに接続できない](../deploy-aip-scanner-prereqs.md#restriction-the-scanner-server-cannot-have-internet-connectivity) 」を参照してください。

## <a name="change-the-local-logging-level"></a>ローカルのログ記録レベルを変更する

既定では Azure Information Protection 統合されたラベル付けクライアントは、クライアントログファイルを **%localappdata%\Microsoft\MSIP** フォルダーに書き込みます。 これらのファイルは、Microsoft サポートによるトラブルシューティングを目的としています。
 
これらのファイルのログ記録レベルを変更するには、レジストリで次の値の名前を探し、値のデータを必要なログ記録レベルに設定します。

**HKEY_CURRENT_USER\SOFTWARE\Microsoft\MSIP\LogLevel**

ログ記録レベルに次の値のいずれかを設定します。

- **オフ**: ローカルログはありません。

- **エラー**: エラーのみ。

- **警告**: エラーと警告。

- **Info**: 最小ログ記録。イベント id が含まれません (スキャナーの既定の設定)。

- **デバッグ**: 完全な情報。

- **トレース**: 詳細なログ記録 (クライアントの既定の設定)。

このレジストリ設定では、 [中央レポート](../reports-aip.md)の Azure Information Protection に送信される情報は変更されません。

## <a name="skip-or-ignore-files-during-scans-depending-on-file-attributes"></a>ファイル属性に応じてスキャン中にファイルをスキップまたは無視する

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるポリシーの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

既定では、Azure Information Protection 統合されたラベル付けスキャナーは、関連するすべてのファイルをスキャンします。 ただし、アーカイブされたファイルや移動されたファイルなど、スキップする特定のファイルを定義することもできます。 

スキャナーで、 **スキャン** の詳細設定を使用して、ファイル属性に基づいて特定のファイルをスキップできるようにします。 [設定] の値に、ファイルがすべて **true** に設定されている場合にスキップされるファイルの属性を一覧表示します。 このファイル属性の一覧では、ロジックとロジックを使用します。

次のサンプルの PowerShell コマンドは、"Global" という名前のラベルでこの詳細設定を使用する方法を示しています。

**読み取り専用のファイルとアーカイブされたファイルの両方をスキップする**

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{ ScannerFSAttributesToSkip =" FILE_ATTRIBUTE_READONLY, FILE_ATTRIBUTE_ARCHIVE"}
```

**読み取り専用またはアーカイブ済みのファイルをスキップする**

ロジックまたはロジックを使用するには、同じプロパティを複数回実行します。 次に例を示します。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{ ScannerFSAttributesToSkip =" FILE_ATTRIBUTE_READONLY"}
Set-LabelPolicy -Identity Global -AdvancedSettings @{ ScannerFSAttributesToSkip =" FILE_ATTRIBUTE_ARCHIVE"}
```

> [!TIP]
> 次の属性を使用してファイルをスキップするようにスキャナーを有効にすることをお勧めします。
> * FILE_ATTRIBUTE_SYSTEM
> * FILE_ATTRIBUTE_HIDDEN
> * FILE_ATTRIBUTE_DEVICE
> * FILE_ATTRIBUTE_OFFLINE
> * FILE_ATTRIBUTE_RECALL_ON_DATA_ACCESS
> * FILE_ATTRIBUTE_RECALL_ON_OPEN
> * FILE_ATTRIBUTE_TEMPORARY

**Scannerfsattributestoskip** 詳細設定で定義できるすべてのファイル属性の一覧については、「 [Win32 ファイル属性定数](/windows/win32/fileio/file-attribute-constants)」を参照してください。

## <a name="preserve-ntfs-owners-during-labeling-public-preview"></a>ラベル付け中に NTFS 所有者を保持する (パブリックプレビュー)

この構成では、Office 365 セキュリティ & コンプライアンスセンターの PowerShell を使用して構成する必要があるポリシーの [詳細設定](#how-to-configure-advanced-settings-for-the-client-by-using-office-365-security--compliance-center-powershell) を使用します。

既定では、スキャナー、PowerShell、およびエクスプローラーの拡張機能のラベル付けによって、ラベル付けの前に定義された NTFS 所有者が保持されません。 

NTFS 所有者の値が保持されるようにするには、選択したラベルポリシーの **UseCopyAndPreserveNTFSOwner** advanced 設定を **true** に設定します。

> [!CAUTION]
> この詳細設定を定義するのは、スキャナーとスキャンされたリポジトリの間に低待機時間で信頼性の高いネットワーク接続を確保できる場合だけにしてください。 ラベルの自動処理中にネットワークエラーが発生すると、ファイルが失われる可能性があります。

ラベルポリシーの名前が "Global" の場合のサンプルの PowerShell コマンド:

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{ UseCopyAndPreserveNTFSOwner ="true"}
```

> [!NOTE]
> 現在、この機能はプレビュー段階にあります。 [Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)には、ベータ版、プレビュー版、またはまだ一般提供されていない Azure 機能に適用される追加の法律条項が含まれています。 
> 

## <a name="customize-justification-prompt-texts-for-modified-labels"></a>変更されたラベルの理由プロンプトテキストをカスタマイズする

エンドユーザーがドキュメントや電子メールの分類ラベルを変更するときに、Office と AIP クライアントの両方に表示される理由プロンプトをカスタマイズします。

たとえば、管理者は、顧客の識別情報をこのフィールドに追加しないようにユーザーに通知することができます。

:::image type="content" source="../media/justification-office.png" alt-text="カスタマイズされた理由プロンプトのテキスト":::

表示される既定 **の他の** テキストを変更するには、 **JustificationTextForUserText** advanced プロパティを使用して、このコマンドレットを [設定](/powershell/module/exchange/set-labelpolicy) します。 代わりに、使用するテキストに値を設定します。

次に例を示します。

``` PowerShell

[Set-LabelPolicy](/powershell/module/exchange/set-labelpolicy) -Identity Global -AdvancedSettings @{JustificationTextForUserText="Other (please explain) - Do not enter sensitive info"}
```

## <a name="customize-outlook-popup-messages"></a>Outlook ポップアップメッセージをカスタマイズする

AIP 管理者は、次のように、Outlook でエンドユーザーに表示されるポップアップメッセージをカスタマイズできます。

- ブロックされた電子メールのメッセージ
- ユーザーが送信しているコンテンツを確認するように求める警告メッセージ
- ユーザーが送信しているコンテンツを正当化するよう要求する理由メッセージ

> [!IMPORTANT]
> この手順では、 **OutlookUnlabeledCollaborationAction** advanced プロパティを使用して定義済みのすべての設定が上書きされます。
>
> 実稼働環境では、**OutlookUnlabeledCollaborationAction** 詳細プロパティを使用してルールを定義する、"*または*" 下記のように定義した json ファイルを使用して複雑なルールを定義する、の "*いずれか*" により、複雑化させないようにすることをお勧めします。
>

**Outlook ポップアップメッセージをカスタマイズするには、次のようにします。**

1. Json ファイルを作成 **します。** 各ファイルには、Outlook によるユーザーへのポップアップメッセージの表示方法を構成するルールがあります。 詳細については、「 [Rule value. json 構文](#rule-value-json-syntax) 」と「 [Sample popup customization](#sample-popup-customization-json-code)」を参照してください。

1. PowerShell を使用して、構成するポップアップメッセージを制御する詳細設定を定義します。 構成するルールごとに個別のコマンドセットを実行します。

    PowerShell コマンドの各セットには、構成するポリシーの名前と、ルールを定義するキーと値が含まれている必要があります。

    使用する構文は以下のとおりです。

    ```PowerShell
    $filedata = Get-Content "<Path to json file>”
    Set-LabelPolicy -Identity <Policy name> -AdvancedSettings @{<Key> ="$filedata"}
    ```
    各値の説明: 

    - `<Path to json file>` は、作成した json ファイルへのパスです。 例: **C:\Users\msanchez\Desktop\ \dlp\OutlookCollaborationRule_1.json**。
    - `<Policy name>` 構成するポリシーの名前を指定します。 
    - `<Key>` は、ルールの名前です。 次の構文を使用し **<#>** ます。は、ルールのシリアル番号です。 
    
        `OutlookCollaborationRule_<x>` 

    詳細については、「 [Outlook のカスタマイズ規則](#ordering-your-outlook-customization-rules) と [規則の値の Json 構文](#rule-value-json-syntax)の順序付け」を参照してください。

   
> [!TIP]
> 追加の組織の場合は、PowerShell コマンドで使用したキーと同じ文字列でファイルに名前を付けます。 たとえば、ファイルに **OutlookCollaborationRule_1.js** という名前を付け、キーとして **OutlookCollaborationRule_1** を使用します。
>
> ドキュメントが Outlook の外部から共有されている場合でもポップアップが表示されるようにするには **(ファイル > 共有 > コピーを添付します)、** [PostponeMandatoryBeforeSave](#remove-not-now-for-documents-when-you-use-mandatory-labeling) の詳細設定を構成することもできます。
> 

### <a name="ordering-your-outlook-customization-rules"></a>Outlook のカスタマイズ規則の順序付け

AIP は、入力したキーのシリアル番号を使用して、ルールが処理される順序を決定します。 各ルールに使用するキーを定義するときは、より少ない数のより制限の厳しいルールを定義し、その後により多くの数値を持つ制限の少ないルールを定義します。

特定のルールの一致が見つかると、AIP はルールの処理を停止し、照合ルールに関連付けられたアクションを実行します。 (**最初の一致-> 終了** ロジック)
    
**例:**

特定の **警告** メッセージを含むすべての **内部** 電子メールを構成するとしますが、通常はこれらをブロックする必要はありません。 ただし、**社内** の電子メールとしてでも、**シークレット** として分類された添付ファイルをユーザーが送信できないようにする必要があります。 

このシナリオでは、内部ルールキー **に対し** て汎用的な警告を行う前に、より具体的なルールである **ブロックシークレット** ルールキーの順序を指定します。
- **ブロック** メッセージの場合: **OutlookCollaborationRule_1**
- **警告** メッセージの場合: **OutlookCollaborationRule_2**

### <a name="rule-value-json-syntax"></a>Rule 値. json 構文

ルールの json 構文を次のように定義します。

``` JSON
"type" : "And",
"nodes" : []
```

少なくとも2つのノード、最初のノードがルールの条件を表し、最後のノードがルールのアクションを表している必要があります。 詳細については次を参照してください:

- [ルール条件の構文](#rule-condition-syntax)
- [ルールアクションの構文](#rule-action-syntax)

##### <a name="rule-condition-syntax"></a>ルール条件の構文

[ルール条件] ノードには、ノードの種類が含まれている必要があります。 

サポートされているノードの種類は次のとおりです。

|ノード型  |説明  |
|---------|---------|
| **And**   | すべての子ノードで *とを実行し* ます     |
| **Or**    |すべての子ノードで *または* を実行します       |
| **Not**   | 独自の子に対し *ては実行されません*      |
| **除く**    | 独自の子に対して *は not* を返し、 **All** として動作します。        |
| **に** 渡される **ドメイン: listofdomains**    |次のいずれかを確認します。 <br />-親が Except の場合、は、**すべて** の受信者がいずれかのドメインにあるかどうか **を確認し** ます。<br />-親が他 **の任意の** ものである場合 **を除き、** は、いずれかの受信者がいずれかのドメインにあるかどうかを確認します。   |
| **Emaillabel、ラベルの** 続き | 次のいずれかです。  <br />-ラベル ID <br />-null (ラベルが付けられていない場合)             |
| **Attachmentlabel、** **label** 、 **supportedExtensions**    | 次のいずれかです。  <br /><br />**本来** <br />-親が Except の場合、サポートされている拡張子が1つの添付ファイルが **すべて** ラベル内に存在するかどうか **を** 確認します。<br />-親が他の任意のものである場合 **を除き、は、** サポートされている拡張子が1つの添付ファイルがラベル内に存在 **するかどう** かを確認します。 <br />-ラベルが付けられていない場合、 **label = null** <br /><br /> **false:** その他のすべての場合 
| | |

#### <a name="rule-action-syntax"></a>ルールアクションの構文

ルールアクションには、次のいずれかを指定できます。

|アクション  |Syntax  |サンプル メッセージ  |
|---------|---------|---------|
|**ブロック**     |    `Block (List<language, [title, body]>)`     |    **_メールがブロック_* されました _<br /><br />  _You は、**シークレット** として分類されたコンテンツを1つ以上の信頼されていない受信者に送信しようとしています: *<br />* `rsinclair@contoso.com` *<br /><br />* 組織のポリシーでは、この操作が許可されて これらの受信者を削除するか、コンテンツを置き換えることを検討してください。 *|
|**呼びかけ**     | `Warn (List<language,[title,body]>)`        |  **_確認が必要_* _<br /><br />_You は、**一般** に分類されたコンテンツを1つ以上の信頼されていない受信者に送信しようとしています *<br />* `rsinclair@contoso.com` *<br /><br />* 。組織のポリシーでは、このコンテンツの送信を確認する必要があります。 *       |
|**揃え**     | `Justify (numOfOptions, hasFreeTextOption, List<language, [Title, body, options1,options2….]> )` <br /><br />最大3つのオプションを含めることができます。        |  **_理由が必要_* _ <br /><br />_Your 組織ポリシーでは、 **一般** に分類されたコンテンツを信頼されていない受信者に送信する理由が必要です。 *<br /><br />*-受信者がこのコンテンツの共有を承認されていることを確認します。詳細に *<br />* ついては、「マイマネージャーが承認したコンテンツ ( *<br />* その他)」をご確認ください。 |
| | | |

##### <a name="action-parameters"></a>アクションのパラメーター

アクションにパラメーターが指定されていない場合、ポップアップには既定のテキストが表示されます。 

すべてのテキストでは、次の動的パラメーターがサポートされています。 

|パラメーター  |説明  |
|---------|---------|
| `${MatchedRecipientsList}`  | 条件 **に** 対する文字列の最後の一致       |
| `${MatchedLabelName}`      | ポリシーのローカライズされた名前を持つメール/添付ファイルの **ラベル**               |
| `${MatchedAttachmentName}` | **Attachmentlabel** 条件の最後に一致した添付ファイルの名前 |
| | |

> [!NOTE]
> すべてのメッセージには、[ **詳細** を表示する] オプション、および [ **ヘルプ** と **フィードバック** ] ダイアログが含まれます。
>
> 言語は、次のようなロケール名のための **判別** **turename** **です。**  =  `en-us`**スペイン語** = `es-es`
>
> だけでは、のように、親のみの言語名もサポートされ `en` ます。
> 

### <a name="sample-popup-customization-json-code"></a>サンプルのポップアップカスタマイズ. json コード

次の一連の **json** コードは、Outlook がユーザーのポップアップメッセージを表示する方法を制御するさまざまなルールを定義する方法を示しています。

- [**例 1**: 内部電子メールまたは添付ファイルをブロックする](#example-1-block-internal-emails-or-attachments)
- [**例 2**: 未分類の Office 添付ファイルをブロックする](#example-2-block-unclassified-office-attachments)
- [**例 3**: ユーザーが社外秘の電子メールまたは添付ファイルの送信を受け入れるように要求する](#example-3-require-the-user-to-accept-sending-a-confidential-email-or-attachment)
- [**例 4**: ラベルのないメールと、特定のラベルを持つ添付ファイルを警告する](#example-4-warn-on-mail-with-no-label-and-an-attachment-with-a-specific-label)
- [**例 5**: 2 つの定義済みオプションと追加のフリーテキストオプションを使用して、理由を確認する](#example-5-prompt-for-a-justification-with-two-predefined-options-and-an-extra-free-text-option)

#### <a name="example-1-block-internal-emails-or-attachments"></a>例 1: 内部電子メールまたは添付ファイルをブロックする

次の **json** コードは、 **内部** から外部の受信者に設定されている電子メールまたは添付ファイルをブロックします。

この例では、 **89a453df-5df447 9768-8191-259d0cf9560a** が **内部** ラベルの ID であり、内部ドメインに **contoso.com** と **microsoft.com** が含まれています。

```powershell
{   
    "type" : "And",     
    "nodes" : [         
        {           
            "type" : "Except" ,             
            "node" :{               
                "type" : "SentTo",                  
                "Domains" : [                   
                    "contoso.com",                  
              "microsoft.com"
                ]               
            }       
        },
        {           
            "type" : "Or",          
            "nodes" : [                 
                {           
                    "type" : "AttachmentLabel",             
                    "LabelId" : "89a453df-5df4-4976-8191-259d0cf9560a"      
                },{                     
                    "type" : "EmailLabel",                  
                    "LabelId" : "89a453df-5df4-4976-8191-259d0cf9560a"              
                }
            ]
        },      
        {           
            "type" : "Block",           
            "LocalizationData": {               
                "en-us": {                
                    "Title": "Email Blocked",                 
                    "Body": "The email or at least one of the attachments is classified as <Bold>${MatchedLabelName}</Bold>. Documents classified as <Bold> ${MatchedLabelName}</Bold> cannot be sent to external recipients (${MatchedRecipientsList}).<br><br>List of attachments classified as <Bold>${MatchedLabelName}</Bold>:<br><br>${MatchedAttachmentName}<br><br><br>This message will not be sent.<br>You are responsible for ensuring compliance with classification requirements as per Contoso’s policies."               
                },              
                "es-es": {                
                    "Title": "Correo electrónico bloqueado",                  
                    "Body": "El correo electrónico o al menos uno de los archivos adjuntos se clasifica como <Bold> ${MatchedLabelName}</Bold>."                
                }           
            },          
            "DefaultLanguage": "en-us"      
        }   
    ] 
}
```

#### <a name="example-2-block-unclassified-office-attachments"></a>例 2: 未分類の Office 添付ファイルをブロックする

次の **json** コードは、未分類の Office の添付ファイルや電子メールを外部の受信者に送信することをブロックします。

次の例では、ラベル付けが必要な添付ファイルの一覧は、 **.doc、.docm、.docx、ドット、normal.dotm、.dotx、potm、です。 potx、.pps、ppsm、ppsx、.ppt、.vdw、.vsd、. vsdm、.vsdx、.vss、. vssm、.vst、vstm、vssx、.vstx、.xls、.xlsb、.xlt、.xlsm、.xlsx、xltm、xltm のうち、xltm** を、それぞれに対して、、します。

```powershell
{   
    "type" : "And",     
    "nodes" : [         
        {           
            "type" : "Except" ,             
            "node" :{               
                "type" : "SentTo",                  
                "Domains" : [                   
                    "contoso.com",                  
                    "microsoft.com"
                ]               
            }       
        },
        {           
            "type" : "Or",          
            "nodes" : [                 
                {           
                    "type" : "AttachmentLabel",
                     "LabelId" : null,
                    "Extensions": [
                                    ".doc",
                                    ".docm",
                                    ".docx",
                                    ".dot",
                                    ".dotm",
                                    ".dotx",
                                    ".potm",
                                    ".potx",
                                    ".pps",
                                    ".ppsm",
                                    ".ppsx",
                                    ".ppt",
                                    ".pptm",
                                    ".pptx",
                                    ".vdw",
                                    ".vsd",
                                    ".vsdm",
                                    ".vsdx",
                                    ".vss",
                                    ".vssm",
                                    ".vst",
                                    ".vstm",
                                    ".vssx",
                                    ".vstx",
                                    ".xls",
                                    ".xlsb",
                                    ".xlt",
                                    ".xlsm",
                                    ".xlsx",
                                    ".xltm",
                                    ".xltx"
                                 ]
                    
                },{                     
                    "type" : "EmailLabel",
                     "LabelId" : null
                }
            ]
        },      
        {           
            "type" : "Email Block",             
            "LocalizationData": {               
                "en-us": {                
                    "Title": "Emailed Blocked",                   
                    "Body": "Classification is necessary for attachments to be sent to external recipients.<br><br>List of attachments that are not classified:<br><br>${MatchedAttachmentName}<br><br><br>This message will not be sent.<br>You are responsible for ensuring compliance to classification requirement as per Contoso’s policies.<br><br>For MS Office documents, classify and send again.<br><br>For PDF files, classify the document or classify the email (using the most restrictive classification level of any single attachment or the email content) and send again."               
                },              
                "es-es": {                
                    "Title": "Correo electrónico bloqueado",                  
                    "Body": "La clasificación es necesaria para que los archivos adjuntos se envíen a destinatarios externos."              
                }           
            },          
            "DefaultLanguage": "en-us"      
        }   
    ] 
}
```

#### <a name="example-3-require-the-user-to-accept-sending-a-confidential-email-or-attachment"></a>例 3: ユーザーが社外秘の電子メールまたは添付ファイルの送信を受け入れるように要求する

次の例では、Outlook が、 **社外秘** の電子メールまたは添付ファイルを外部の受信者に送信していることをユーザーに警告するメッセージを表示します。また、ユーザーが [ **同意** する] を選択する必要もあります。 

この種の警告メッセージは、ユーザーが **同意** を選択する必要があるため、厳密には理由として考えられます。

``` powershell
{   
    "type" : "And",     
    "nodes" : [         
        {           
            "type" : "Except" ,             
            "node" :{               
                "type" : "SentTo",                  
                "Domains" : [                   
                    "contoso.com",                  
                    "microsoft.com"
                ]               
            }       
        },
        {           
            "type" : "Or",          
            "nodes" : [                 
                {           
                    "type" : "AttachmentLabel",             
                    "LabelId" : "3acd2acc-2072-48b1-80c8-4da23e245613"      
                },{                     
                    "type" : "EmailLabel",                  
                    "LabelId" : "3acd2acc-2072-48b1-80c8-4da23e245613"              
                }
            ]
        },      
        {           
            "type" : "Justify",             
            "LocalizationData": {               
                "en-us": {                
                    "Title": "Warning",                   
                    "Body": "You are sending a document that is classified as <Bold>${MatchedLabelName}</Bold> to at least one external recipient. Please make sure that the content is correctly classified and that the recipients are entitled to receive this document.<br><br>List of attachments classified as <Bold>${MatchedLabelName}</Bold>:<br><br>${MatchedAttachmentName}<br><br><Bold>List of external email addresses:</Bold><br>${MatchedRecipientsList})<br><br>You are responsible for ensuring compliance to classification requirement as per Contoso’s policies.<br><br><Bold>Acknowledgement</Bold><br>By clicking <Bold>I accept<\Bold> below, you confirm that the recipient is entitled to receive the content and the communication complies with CS Policies and Standards",
                    "Options": [                        
                        "I accept"              
                    ] 
                },              
                "es-es": {                
                    "Title": "Advertencia",                   
                    "Body": "Está enviando un documento clasificado como <Bold>${MatchedLabelName}</Bold> a al menos un destinatario externo. Asegúrese de que el contenido esté correctamente clasificado y que los destinatarios tengan derecho a recibir este documento.",
                    "Options": [                        
                        "Acepto"                    
                    ]                   
                }           
            },          
            "HasFreeTextOption":"false",            
            "DefaultLanguage": "en-us"      
        }   
    ] 
}
```

#### <a name="example-4-warn-on-mail-with-no-label-and-an-attachment-with-a-specific-label"></a>例 4: ラベルのないメールと、特定のラベルを持つ添付ファイルを警告する

次の **json コード** は、Outlook が内部電子メールを送信しているときにラベルがなく、特定のラベルを持つ添付ファイルがある場合に、ユーザーに警告します。 

この例では、 **bcbef25a-c4db-446b-9496-1b558d9edd0e** は添付ファイルのラベルの ID です。

既定では、添付ファイルが付いている電子メールは、同じラベルを自動的に受信しません。

```powershell
{   
    "type" : "And",     
    "nodes" : [         
        {           
            "type" : "EmailLabel",
                     "LabelId" : null           
        },
        {
          "type": "AttachmentLabel",
          "LabelId": "bcbef25a-c4db-446b-9496-1b558d9edd0e",
          "Extensions": [
                ".docx",
                ".xlsx",
                ".pptx"
             ]
        },
    {           
            "type" : "SentTo",              
            "Domains" : [               
                "contoso.com",              
            ]           
        },      
        {           
            "type" : "Warn" 
        }   
    ] 
}
```

#### <a name="example-5-prompt-for-a-justification-with-two-predefined-options-and-an-extra-free-text-option"></a>例 5: 2 つの定義済みオプションと追加のフリーテキストオプションを使用して、理由を確認する

次の json コードを使用すると、ユーザーにアクションの理由を求めるメッセージが表示され **ます。** 理由テキストには、3つの自由テキストオプションと共に、2つの定義済みオプションがあります。

```PowerShell
{   
    "type" : "And",     
    "nodes" : [         
        {           
            "type" : "Except" ,             
            "node" :{               
                "type" : "SentTo",                  
                "Domains" : [                   
                    "contoso.com",                                  
                ]               
            }       
        },      
        {           
            "type" : "EmailLabel",          
            "LabelId" : "34b8beec-40df-4219-9dd4-553e1c8904c1"      
        },      
        {           
            "type" : "Justify",             
            "LocalizationData": {               
                "en-us": {                  
                    "Title": "Justification Required",                  
                    "Body": "Your organization policy requires justification for you to send content classified as <Bold> ${MatchedLabelName}</Bold>,to untrusted recipients:<br>Recipients are: ${MatchedRecipientsList}",                     
                    "Options": [                        
                        "I confirm the recipients are approved for sharing this content",                   
                        "My manager approved sharing of this content",                      
                        "Other, as explained"                   
                    ]               
                },              
                "es-es": {                  
                    "Title": "Justificación necesaria",                     
                    "Body": "La política de su organización requiere una justificación para que envíe contenido clasificado como <Bold> ${MatchedLabelName}</Bold> a destinatarios que no sean de confianza.",                  
                    "Options": [                        
                        "Confirmo que los destinatarios están aprobados para compartir este contenido.",
                        "Mi gerente aprobó compartir este contenido",
                        "Otro, como se explicó"                     
                    ]               
                }           
            },          
            "HasFreeTextOption":"true",             
            "DefaultLanguage": "en-us"      
        }   
    ] 
}
```

## <a name="configure-sharepoint-timeouts"></a>SharePoint のタイムアウトを構成する

既定では、SharePoint との相互作用のタイムアウトは2分間です。その後、試行された AIP 操作は失敗します。

[バージョン 2.8.85.0](unifiedlabelingclient-version-release-history.md#version-28850)以降では、AIP 管理者は、 **hh: mm: ss** 構文を使用してタイムアウトを定義し、次の詳細プロパティを使用してこのタイムアウトを制御できます。

- **SharepointWebRequestTimeout**。 SharePoint へのすべての AIP web 要求のタイムアウトを指定します。 既定値は2分です。

    たとえば、ポリシーに **Global** という名前が付けられている場合、次のサンプル PowerShell コマンドを実行すると、web 要求のタイムアウトが5分に更新されます。

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{SharepointWebRequestTimeout="00:05:00"}
    ```

- **SharepointFileWebRequestTimeout**。 AIP web 要求を使用して、SharePoint ファイルのタイムアウトを特定します。 既定値 = 15 分

    たとえば、ポリシーに **Global** という名前が付けられている場合、次のサンプルの PowerShell コマンドでは、ファイルの web 要求タイムアウトを10分に更新します。

    ```PowerShell
    Set-LabelPolicy -Identity Global -AdvancedSettings @{SharepointFileWebRequestTimeout="00:10:00"}
    ```

## <a name="prevent-outlook-performance-issues-with-smime-emails"></a>S/MIME メールで Outlook のパフォーマンスの問題を回避する

S/MIME メールが読み取りウィンドウで開かれると、Outlook でパフォーマンスの問題が発生する可能性があります。 これらの問題を回避するには、 **OutlookSkipSmimeOnReadingPaneEnabled** advanced プロパティを有効にします。 

このプロパティを有効にすると、AIP バーと電子メール分類が閲覧ウィンドウに表示されなくなります。

たとえば、ポリシーに **Global** という名前が付けられている場合、次の PowerShell コマンドの例では、 **OutlookSkipSmimeOnReadingPaneEnabled** プロパティを有効にします。

```PowerShell
Set-LabelPolicy -Identity Global -AdvancedSettings @{OutlookSkipSmimeOnReadingPaneEnabled="true"}
```

## <a name="next-steps"></a>次のステップ

Azure Information Protection 統合されたラベル付けクライアントをカスタマイズしたので、このクライアントのサポートに必要な追加情報については、次のリソースを参照してください。

- [クライアントのファイルと使用状況ログ](client-admin-guide-files-and-logging.md)

- [サポートされるファイルの種類](client-admin-guide-file-types.md)

- [PowerShell コマンド](client-admin-guide-powershell.md)