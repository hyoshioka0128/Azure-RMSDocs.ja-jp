---
title: 分類とラベル付けに関してよく寄せられる質問 - AIP
description: Azure Information Protection の使用について、特に分類とラベル付けに関して質問はございますか。 ここで回答を探してみてください。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: fc4c86c020427066d519fec4ae6363f131ce64c2
ms.sourcegitcommit: 0f10998e9623f59c36edf89e4661c9c953787aed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88810263"
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Azure Information Protection の分類とラベル付けに関してよく寄せられる質問

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と**ラベル管理**は、**2021 年 3 月 31 日**で**非推奨**になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Azure Information Protection に関して、特に分類とラベル付けに関して質問はございますか。  ここで回答を探してみてください。 

## <a name="which-client-do-i-install-for-testing-new-functionality"></a>新しい機能をテストするためにどのクライアントをインストールしますか?

現時点では、Windows 用に2つの Azure Information Protection クライアントがあります。 

- Azure Information Protection、次のいずれかの管理センターからラベルとポリシー設定をダウンロードする、統一されたラベル **付けクライアント** : Office 365 セキュリティ & コンプライアンスセンター、Microsoft 365 Security Center、Microsoft 365 コンプライアンスセンター。 このクライアントは現在一般公開されており、将来のリリースで追加機能をテストするためのプレビューバージョンがある可能性があります。

- Azure portal からラベルとポリシー設定をダウンロードする **Azure Information Protection クライアント (クラシック)** 。 このクライアントは、以前の一般公開バージョンのクライアント上に構築されます。

現在の機能セットと機能がビジネス要件を満たしている場合は、統一されたラベル付けクライアントでテストすることをお勧めします。 それ以外の場合、または [統合ラベルストアにまだ移行](configure-policy-migrate-labels.md)していない Azure portal でラベルを構成した場合は、クラシッククライアントを使用します。 機能の比較表など、詳細については「[使用する Azure Information Protection クライアントを選択する](./rms-client/use-client.md#choose-which-labeling-client-to-use-for-windows-computers)」をご覧ください。

Azure Information Protection クライアントは、Windows でのみサポートされています。 IOS、Android、macOS、および web でドキュメントや電子メールを分類して保護するには、 [組み込みのラベル付けをサポートする Office アプリ](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps)を使用します。 

## <a name="where-can-i-find-information-about-using-sensitivity-labels-for-office-apps"></a>Office アプリの秘密度ラベルの使用に関する情報はどこで入手できますか。

次のドキュメントリソースを参照してください。

- [秘密度ラベルについて](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels) 

- [Office アプリ内での機密ラベルの使用](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-office-apps)

- [SharePoint と OneDrive で Office ファイルの機密ラベルを有効にする](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files)

- [Office 内のドキュメントと電子メールに機密ラベルを適用する](https://support.office.com/article/Apply-sensitivity-labels-to-your-documents-and-email-within-Office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9#ID0EBFAAA=Office_365)

機密ラベルをサポートするその他のシナリオについては、「 [秘密度ラベルの一般的なシナリオ](https://docs.microsoft.com/microsoft-365/compliance/get-started-with-sensitivity-labels#common-scenarios-for-sensitivity-labels)」を参照してください。

## <a name="can-a-file-have-more-than-one-classification"></a>1 つのファイルに複数の分類を適用することはできますか?

ユーザーが一度に選択できるのはドキュメントまたは電子メールごとに 1 つのラベルのみです。したがって、多くの場合、適用できる分類は 1 つのみとなります。 ただし、ユーザーがサブラベルを選択した場合、実際は同時に 2 つのラベル (プライマリ ラベルとセカンダリ ラベル) が適用されます。 サブラベルを使用すれば、1 つのファイルで 2 つの分類 (制御の追加レベルの親\子関係を示す) を適用することができます。

たとえば、**Confidential** というラベルに、**Legal** や **Finance** などのサブラベルを含めることができます。 これらのサブラベルには、異なる分類の視覚的なマーキングと異なる Rights Management テンプレートをそれぞれ適用することができます。 ユーザーは **Confidential** ラベル自体を選択することはできません。選択できるのは、**Legal** などのそのサブラベルのいずれか 1 つのみです。 したがって、表示されるラベル セットは **Confidential \ Legal** のようになります。 そのファイルのメタデータには、**Confidential** のカスタム テキスト プロパティが 1 つ、**Legal** のカスタム テキスト プロパティが 1 つ、さらに両方の値 (**Confidential Legal**) を含むものが含まれます。 

サブラベルを使用する場合は、プライマリ ラベルで視覚的なマーキング、保護、および条件を構成しないでください。 サブレベルを使用する場合は、サブラベルのみにこれらの設定を構成します。 プライマリ ラベルとそのサブラベルでこれらの設定を構成した場合は、サブラベルの設定が優先されます。

## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>他のユーザーがラベルを削除または変更しないようにするには、どうすればいいですか?

分類ラベルを下げたり、ラベルを削除したり、保護を解除したりする理由をユーザーに示す [ポリシー設定](configure-policy-settings.md) がありますが、この設定によってこれらの操作が妨げられることはありません。 ユーザーによるラベルの削除または変更を防ぐには、コンテンツが既に保護されている必要があります。保護のアクセス許可ではユーザーにエクスポートまたはフル コントロールの[使用権限](configure-usage-rights.md)が付与されません。 

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>電子メールにラベルが付けられた場合、添付ファイルにも同じラベルが自動的に付けられますか?

いいえ。 添付ファイルのある電子メール メッセージにラベルを付ける場合、これらの添付ファイルは同じラベルを継承しません。 添付ファイルは、ラベルがないか、個別に適用されたラベルが付けられた状態で保持されます。 ただし、電子メールのラベルが保護を適用する場合、その保護は Office の添付ファイルに適用されます。

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>DLP ソリューションや他のアプリケーションは Azure Information Protection とどのように統合できますか?

Azure Information Protection は分類に永続的メタデータを使用し、これにはクリア テキストのラベルが含まれるので、DLP ソリューションや他のアプリケーションはこの情報を読み取ることができます。 

このメタデータの詳細については、「[メールやドキュメントに格納されるラベル情報](configure-policy.md#label-information-stored-in-emails-and-documents)」を参照してください。

Exchange Online のメール フロー ルールで、このメタデータを使用する例については、「[Azure Information Protection ラベルの Exchange Online メール フロー ルールの構成](configure-exo-rules.md)」をご覧ください。

## <a name="can-i-create-a-document-template-that-automatically-includes-the-classification"></a>分類が自動的に含まれるドキュメント テンプレートを作成できますか?

はい。 ラベルを構成して、[ラベル名を含むヘッダーまたはフッターを適用する](configure-policy-markings.md)ことができます。 ただし、それが要件を満たしていない場合は、Azure Information Protection クライアント (クラシック) のみに対して、必要な書式を持つドキュメントテンプレートを作成し、フィールドコードとして分類を追加することができます。 

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
