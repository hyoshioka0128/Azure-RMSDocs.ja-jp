---
title: 分類とラベル付けに関してよく寄せられる質問 - AIP
description: Azure Information Protection の使用について、特に分類とラベル付けに関して質問はございますか。 ここで回答を探してみてください。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 06/21/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.openlocfilehash: db5b1b06f198db0795876e71749b1d220c7c2694
ms.sourcegitcommit: 599306e271392afa4bc05c87982549785ce1860e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/21/2019
ms.locfileid: "67305706"
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Azure Information Protection の分類とラベル付けに関してよく寄せられる質問

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection に関して、特に分類とラベル付けに関して質問はございますか。  ここで回答を探してみてください。 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>Azure Information Protection の分類機能はどのように使用しますか。

[ポリシーの編集と新しいラベルの作成](infoprotect-quick-start-tutorial.md)に関するチュートリアルに従えば、わずか数分でこの動作を確認できます。

追加の分類機能が利用可能になる時期については、[Enterprise Mobility + Security のブログ](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity/label-name/Azure%20Information%20Protection)および [Yammer サイト](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)での案内をご確認ください。 現在のリリースには、次のような制限がいくつかあります。

- Office Web アプリ (Office Online) にはラベル付け機能はありません。

- 分類およびラベル付けは Exchange Online や SharePoint Online とは統合されません。

> [!NOTE]
> **プレビュー段階**:
> - 分類とラベル付け用の中央レポート。 詳細については、「[Central reporting for Azure Information Protection](reports-aip.md)」 (Azure Information Protection の中央レポート機能) を参照してください。
>
>**最近リリースされた機能**:
> - モバイル デバイス (iOS および Android) および Mac コンピューター用の Office アプリに組み込まれたラベル付け機能。 詳細については、「[Office 内の文書やメールに機密ラベルを適用する](https://aka.ms/officemipdocs)」を参照してください。

Azure Information Protection の [UserVoice サイト](https://msip.uservoice.com/)にアクセスし、新機能のご要望をお知らせください。また、リクエストへの投票も受け付けています。

## <a name="which-client-do-i-install-for-testing-new-functionality"></a>新しい機能をテスト用クライアントをインストールします。

現時点では、Windows の 2 つのクライアントがあります。 

- **Azure Information Protection クライアントのラベル付けを統合する**管理センターでは、次のいずれかからラベルとポリシー設定をダウンロードします。Office 365 セキュリティ/コンプライアンス センター、Microsoft 365 セキュリティ センター, Microsoft 365 コンプライアンス センター。 このクライアントは現在一般提供であり、将来のリリースの他の機能をテストするためのプレビュー バージョンを使います。

- **Azure Information Protection クライアント (クラシック)** Azure portal からラベルとポリシー設定をダウンロードします。 このクライアントは、クライアントの以前の一般公開バージョンに基づいています。

その現在の機能セットと機能は、ビジネス要件を満たしている場合、統一されたラベル付けクライアントでテストすることをお勧めします。 そうでない場合、またはまだしていない Azure portal でラベルを構成している場合[統合のラベル付けのストアに移行](configure-policy-migrate-labels.md)、従来のクライアントを使用します。

機能の比較表など、詳細については「[使用する Azure Information Protection クライアントを選択する](./rms-client/use-client.md#choose-which-azure-information-protection-client-to-use)」をご覧ください。

## <a name="can-a-file-have-more-than-one-classification"></a>1 つのファイルに複数の分類を適用することはできますか?

ユーザーが一度に選択できるのはドキュメントまたは電子メールごとに 1 つのラベルのみです。したがって、多くの場合、適用できる分類は 1 つのみとなります。 ただし、ユーザーがサブラベルを選択した場合、実際は同時に 2 つのラベル (プライマリ ラベルとセカンダリ ラベル) が適用されます。 サブラベルを使用すれば、1 つのファイルで 2 つの分類 (制御の追加レベルの親\子関係を示す) を適用することができます。

たとえば、**Confidential** というラベルに、**Legal** や **Finance** などのサブラベルを含めることができます。 これらのサブラベルには、異なる分類の視覚的なマーキングと異なる Rights Management テンプレートをそれぞれ適用することができます。 ユーザーは **Confidential** ラベル自体を選択することはできません。選択できるのは、**Legal** などのそのサブラベルのいずれか 1 つのみです。 したがって、表示されるラベル セットは **Confidential \ Legal** のようになります。 そのファイルのメタデータには、**Confidential** のカスタム テキスト プロパティが 1 つ、**Legal** のカスタム テキスト プロパティが 1 つ、さらに両方の値 (**Confidential Legal**) を含むものが含まれます。 

サブラベルを使用する場合は、プライマリ ラベルで視覚的なマーキング、保護、および条件を構成しないでください。 サブレベルを使用する場合は、サブラベルのみにこれらの設定を構成します。 プライマリ ラベルとそのサブラベルでこれらの設定を構成した場合は、サブラベルの設定が優先されます。

## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>他のユーザーがラベルを削除または変更しないようにするには、どうすればいいですか?

分類ラベルを下げる場合、ラベルを削除する場合、保護を解除する場合にその理由をユーザーが説明しなければならない[ポリシー設定](configure-policy-settings.md)がありますが、この設定ではこれらの操作を回避しません。 ユーザーによるラベルの削除または変更を防ぐには、コンテンツが既に保護されている必要があります。保護のアクセス許可ではユーザーにエクスポートまたはフル コントロールの[使用権限](configure-usage-rights.md)が付与されません。 

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>電子メールにラベルが付けられた場合、添付ファイルにも同じラベルが自動的に付けられますか?

No. 添付ファイルのある電子メール メッセージにラベルを付ける場合、これらの添付ファイルは同じラベルを継承しません。 添付ファイルは、ラベルがないか、個別に適用されたラベルが付けられた状態で保持されます。 ただし、電子メールのラベルが保護を適用する場合、その保護は Office の添付ファイルに適用されます。

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>DLP ソリューションや他のアプリケーションは Azure Information Protection とどのように統合できますか?

Azure Information Protection は分類に永続的メタデータを使用し、これにはクリア テキストのラベルが含まれるので、DLP ソリューションや他のアプリケーションはこの情報を読み取ることができます。 

このメタデータの詳細については、「[メールやドキュメントに格納されるラベル情報](configure-policy.md#label-information-stored-in-emails-and-documents)」を参照してください。

Exchange Online のメール フロー ルールで、このメタデータを使用する例については、「[Azure Information Protection ラベルの Exchange Online メール フロー ルールの構成](configure-exo-rules.md)」をご覧ください。

## <a name="can-i-create-a-document-template-that-automatically-includes-the-classification"></a>分類が自動的に含まれるドキュメント テンプレートを作成できますか?

可能。 ラベルを構成して、[ラベル名を含むヘッダーまたはフッターを適用する](configure-policy-markings.md)ことができます。 ただし、それがご自身の要件を満たしていない場合は、好みの書式設定を持つドキュメント テンプレートを作成し、フィールド コードとして分類を追加することができます。 

例として、ドキュメントのヘッダーに分類を表示するテーブルがあるとします。 または、概要向けにドキュメントの分類を参照する具体的な表現を使用します。

このフィールド コードをドキュメントに追加するには:

1. ドキュメントにラベルを付けて保存します。 このアクションにより新しいメタデータ フィールドが作成され、これをフィールド コード用に使用できます。

2. ドキュメント内で、ラベルの分類を追加したい位置にカーソルを合わせた後、 **[挿入]** タブから **[テキスト]**  >  **[クイック パーツ]**  >  **[フィールド]** を選択します。

3. **[フィールド]** ダイアログ ボックスの **[カテゴリ]** ドロップダウンから、 **[ドキュメント情報]** を選択します。 次に、 **[フィールド名]** ドロップダウンから **[DocProperty (文書プロパティ)]** を選択します。

4. **[プロパティ]** ドロップダウンから **[秘密度]** を選択し、 **[OK]** を選択します。

現在のラベルの分類がドキュメントに表示され、この値はドキュメントを開くかテンプレートを使用するたびに自動的に更新されます。 このため、ラベルが変更されると、このフィールド コードに対して表示される分類がドキュメント内で自動的に更新されます。

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>Azure Information Protection の電子メールの分類は、Exchange のメッセージ分類とどのように違いますか?

Exchange のメッセージ分類は電子メールを分類する古い機能で、Azure Information Protection の分類機能とは別に実装されます。 

ただし、ユーザーが Outlook on the web や一部のモバイル用メール アプリケーションを使用して電子メールを分類する場合に、これら 2 つのソリューションを統合し、Azure Information Protection の分類および対応するラベル マーキングが自動的に追加されるようにすることができます。 

同じ手法を使用して、Outlook on the web とこれらのモバイル用メール アプリケーションで独自のラベルを使用できます。

構成手順については、「[Integrate Exchange message classification with Azure Information Protection for a mobile device labeling solution (Exchange のメッセージ分類と Azure Information Protection を統合したモバイル デバイス用ラベル付けソリューション)](./rms-client/client-admin-guide-customizations.md#integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution)」をご覧ください。
