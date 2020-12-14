---
title: 分類とラベル付けに関してよく寄せられる質問 - AIP
description: Azure Information Protection の使用について、特に分類とラベル付けに関して質問はございますか。 ここで回答を探してみてください。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/12/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: d4bfec07900404c39a17a90468a726f6632078fe
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97382277"
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Azure Information Protection の分類とラベル付けに関してよく寄せられる質問

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連**: [AIP のラベル付けクライアントと従来のクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)です。 詳細については、「 [クラシッククライアントの faq](faqs-classic.md)」も参照してください。 *

>[!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Azure Information Protection に関して、特に分類とラベル付けに関して質問はございますか。  ここで回答を探してみてください。 

## <a name="which-client-do-i-install-for-testing-new-functionality"></a>新しい機能をテストするためにどのクライアントをインストールしますか?

Azure Information Protection 統合された **ラベル付けクライアント** をインストールすることをお勧めします。 統一されたラベル付けクライアントは、次のいずれかの管理センターからラベルとポリシー設定をダウンロードします。 

- Office 365 セキュリティ/コンプアライアンス センター
- Microsoft 365 セキュリティ センター
- Microsoft 365 コンプライアンスセンター。

このクライアントは現在一般公開されており、将来のリリースで追加機能をテストするためのプレビューバージョンがある可能性があります。

まだ [統合ラベルストアに移行](configure-policy-migrate-labels.md)していない Azure portal でラベルを構成した場合は、代わりに **Azure Information Protection クラシッククライアント** を使用します。

機能と機能の比較表を含む詳細については、「 [Windows のラベル付けソリューションを選択](rms-client/use-client.md#choose-your-windows-labeling-solution)する」を参照してください。

> [!TIP]
> Azure Information Protection クライアントは、Windows でのみサポートされています。 
>
> IOS、Android、macOS、および web でドキュメントや電子メールを分類して保護するには、 [組み込みのラベル付けをサポートする Office アプリ](/microsoft-365/compliance/sensitivity-labels-office-apps#support-for-sensitivity-label-capabilities-in-apps)を使用します。 
> 

## <a name="where-can-i-find-information-about-using-sensitivity-labels-for-office-apps"></a>Office アプリの秘密度ラベルの使用に関する情報はどこで入手できますか。

次のドキュメントリソースを参照してください。

- [秘密度ラベルについて](/microsoft-365/compliance/sensitivity-labels) 

- [Office アプリ内での機密ラベルの使用](/microsoft-365/compliance/sensitivity-labels-office-apps)

- [SharePoint と OneDrive で Office ファイルの機密ラベルを有効にする](/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files)

- [Office 内のドキュメントと電子メールに機密ラベルを適用する](https://support.office.com/article/Apply-sensitivity-labels-to-your-documents-and-email-within-Office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9#ID0EBFAAA=Office_365)

機密ラベルをサポートするその他のシナリオについては、「 [秘密度ラベルの一般的なシナリオ](/microsoft-365/compliance/get-started-with-sensitivity-labels#common-scenarios-for-sensitivity-labels)」を参照してください。

## <a name="can-a-file-have-more-than-one-classification"></a>1 つのファイルに複数の分類を適用することはできますか?

ユーザーが一度に選択できるのはドキュメントまたは電子メールごとに 1 つのラベルのみです。したがって、多くの場合、適用できる分類は 1 つのみとなります。 ただし、ユーザーがサブラベルを選択した場合、実際は同時に 2 つのラベル (プライマリ ラベルとセカンダリ ラベル) が適用されます。 サブラベルを使用すれば、1 つのファイルで 2 つの分類 (制御の追加レベルの親\子関係を示す) を適用することができます。

たとえば、**Confidential** というラベルに、**Legal** や **Finance** などのサブラベルを含めることができます。 これらのサブラベルには、異なる分類の視覚的なマーキングと異なる Rights Management テンプレートをそれぞれ適用することができます。 ユーザーは **Confidential** ラベル自体を選択することはできません。選択できるのは、**Legal** などのそのサブラベルのいずれか 1 つのみです。 したがって、表示されるラベル セットは **Confidential \ Legal** のようになります。 そのファイルのメタデータには、**Confidential** のカスタム テキスト プロパティが 1 つ、**Legal** のカスタム テキスト プロパティが 1 つ、さらに両方の値 (**Confidential Legal**) を含むものが含まれます。 

サブラベルを使用する場合は、プライマリ ラベルで視覚的なマーキング、保護、および条件を構成しないでください。 サブレベルを使用する場合は、サブラベルのみにこれらの設定を構成します。 プライマリ ラベルとそのサブラベルでこれらの設定を構成した場合は、サブラベルの設定が優先されます。

## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>他のユーザーがラベルを削除または変更しないようにするには、どうすればいいですか?

ユーザーによるラベルの削除または変更を防ぐには、コンテンツが既に保護されている必要があります。保護のアクセス許可ではユーザーにエクスポートまたはフル コントロールの[使用権限](configure-usage-rights.md)が付与されません。 

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>電子メールにラベルが付けられた場合、添付ファイルにも同じラベルが自動的に付けられますか?

いいえ。 添付ファイルのある電子メール メッセージにラベルを付ける場合、これらの添付ファイルは同じラベルを継承しません。 添付ファイルは、ラベルがないか、個別に適用されたラベルが付けられた状態で保持されます。 ただし、電子メールのラベルが保護を適用する場合、その保護は Office の添付ファイルに適用されます。

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>DLP ソリューションや他のアプリケーションは Azure Information Protection とどのように統合できますか?

Azure Information Protection は分類に永続的メタデータを使用し、これにはクリア テキストのラベルが含まれるので、DLP ソリューションや他のアプリケーションはこの情報を読み取ることができます。 

Exchange Online のメール フロー ルールで、このメタデータを使用する例については、「[Azure Information Protection ラベルの Exchange Online メール フロー ルールの構成](configure-exo-rules.md)」をご覧ください。