---
title: 分類とラベル付けに関してよく寄せられる質問 - AIP
description: Azure Information Protection の使用について、特に分類とラベル付けに関して質問はございますか。 ここで回答を探してみてください。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/14/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.openlocfilehash: 2c0d391e2d00ec7d0bc09d98de3fe6f502f999a4
ms.sourcegitcommit: 4c4af9766342272eaa18df720ba3738d44ba99c8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/15/2018
ms.locfileid: "51707744"
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Azure Information Protection の分類とラベル付けに関してよく寄せられる質問

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection に関して、特に分類とラベル付けに関して質問はございますか。  ここで回答を探してみてください。 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>Azure Information Protection の分類機能はどのように使用しますか。

[ポリシーの編集と新しいラベルの作成](infoprotect-quick-start-tutorial.md)に関するチュートリアルに従えば、わずか数分でこの動作を確認できます。

追加の分類機能が利用可能になる時期については、[Enterprise Mobility + Security のブログ](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity/label-name/Azure%20Information%20Protection)および [Yammer サイト](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)での案内をご確認ください。 現在のリリースには、次のような制限がいくつかあります。

- Office Web アプリ (Office Online) にはラベル付け機能はありません。

- 分類およびラベル付けは Exchange Online や SharePoint Online とは統合されません。

> [!NOTE]
> **プレビュー段階**:
> - 分類とラベル付け用の中央レポート。 詳細については、「[Central reporting for Azure Information Protection](reports-aip.md)」 (Azure Information Protection の中央レポート機能) を参照してください。
> - [Office Insider プログラム](https://support.office.com/article/what-is-office-insider-f4208185-b63a-4b68-9c7a-9a32d2411c16)にオプトインしているお客様のための、モバイル デバイス (iOS および Android) および Mac コンピューター用の Office アプリでのラベル付け機能。 詳細については、「[Office 内の文書やメールに機密ラベルを適用する](https://aka.ms/officemipdocs)」を参照してください。


Azure Information Protection の [UserVoice サイト](https://msip.uservoice.com/)にアクセスし、新機能のご要望をお知らせください。また、リクエストへの投票も受け付けています。

## <a name="do-i-need-to-be-a-global-admin-to-configure-classification-and-labels"></a>分類とラベルを構成するにはグローバル管理者である必要がありますか?

新しく導入された Information Protection 管理者ロールと共に、この質問は主要な FAQ ページ「[Azure Information Protection を構成するにはグローバル管理者である必要がありますか、または他の管理者に委任できますか?](faqs.md#do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators)」で回答されています。

[Azure Information Protection クライアント](https://www.microsoft.com/en-us/download/details.aspx?id=53018)をインストールするときにデモ ポリシーをインストールするオプションを選択した場合は、ポータルにサインインしなくてもラベル機能を試すことができます。 デモ ポリシーでは Azure Information Protection 用の既定のポリシーがローカルにインストールされるので、ドキュメントと電子メールへのラベル付けを試すことができますが、ラベルの変更または新規追加には Azure Portal にサインインする必要があります。 

## <a name="can-a-file-have-more-than-one-classification"></a>1 つのファイルに複数の分類を適用することはできますか?

ユーザーが一度に選択できるのはドキュメントまたは電子メールごとに 1 つのラベルのみです。したがって、多くの場合、適用できる分類は 1 つのみとなります。 ただし、ユーザーがサブラベルを選択した場合、実際は同時に 2 つのラベル (プライマリ ラベルとセカンダリ ラベル) が適用されます。 サブラベルを使用すれば、1 つのファイルで 2 つの分類 (制御の追加レベルの親\子関係を示す) を適用することができます。

たとえば、**Confidential** というラベルに、**Legal** や **Finance** などのサブラベルを含めることができます。 これらのサブラベルには、異なる分類の視覚的なマーキングと異なる Rights Management テンプレートをそれぞれ適用することができます。 ユーザーは **Confidential** ラベル自体を選択することはできません。選択できるのは、**Legal** などのそのサブラベルのいずれか 1 つのみです。 したがって、表示されるラベル セットは **Confidential \ Legal** のようになります。 そのファイルのメタデータには、**Confidential** のカスタム テキスト プロパティが 1 つ、**Legal** のカスタム テキスト プロパティが 1 つ、さらに両方の値 (**Confidential Legal**) を含むものが含まれます。 

サブラベルを使用する場合は、プライマリ ラベルで視覚的なマーキング、保護、および条件を構成しないでください。 サブレベルを使用する場合は、サブラベルのみにこれらの設定を構成します。 プライマリ ラベルとそのサブラベルでこれらの設定を構成した場合は、サブラベルの設定が優先されます。

## <a name="how-do-i-prevent-somebody-from-removing-or-changing-a-label"></a>他のユーザーがラベルを削除または変更しないようにするには、どうすればいいですか?

分類ラベルを下げる場合、ラベルを削除する場合、保護を解除する場合にその理由をユーザーが説明しなければならない[ポリシー設定](configure-policy-settings.md)がありますが、この設定ではこれらの操作を回避しません。 ユーザーによるラベルの削除または変更を防ぐには、コンテンツが既に保護されている必要があります。保護のアクセス許可ではユーザーにエクスポートまたはフル コントロールの[使用権限](configure-usage-rights.md)が付与されません。 

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>電子メールにラベルが付けられた場合、添付ファイルにも同じラベルが自動的に付けられますか?

いいえ。 添付ファイルのある電子メール メッセージにラベルを付ける場合、これらの添付ファイルは同じラベルを継承しません。 添付ファイルは、ラベルがないか、個別に適用されたラベルが付けられた状態で保持されます。 ただし、電子メールのラベルが保護を適用する場合、その保護は Office の添付ファイルに適用されます。

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>DLP ソリューションや他のアプリケーションは Azure Information Protection とどのように統合できますか?

Azure Information Protection は分類に永続的メタデータを使用し、これにはクリア テキストのラベルが含まれるので、DLP ソリューションや他のアプリケーションはこの情報を読み取ることができます。 

Exchange Online のメール フロー ルールでのこのメタデータの使用に関する詳細と例については、「[Configuring Exchange Online mail flow rules for Azure Information Protection labels](configure-exo-rules.md)」(Azure Information Protection ラベル用に Exchange Online のメール フロー ルールを構成する) をご覧ください。

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>Azure Information Protection の電子メールの分類は、Exchange のメッセージ分類とどのように違いますか?

Exchange のメッセージ分類は電子メールを分類する古い機能で、Azure Information Protection の分類機能とは別に実装されます。 

ただし、ユーザーが Outlook on the web や一部のモバイル用メール アプリケーションを使用して電子メールを分類する場合に、これら 2 つのソリューションを統合し、Azure Information Protection の分類および対応するラベル マーキングが自動的に追加されるようにすることができます。 

同じ手法を使用して、Outlook on the web とこれらのモバイル用メール アプリケーションで独自のラベルを使用できます。

構成手順については、「[Integrate Exchange message classification with Azure Information Protection for a mobile device labeling solution (Exchange のメッセージ分類と Azure Information Protection を統合したモバイル デバイス用ラベル付けソリューション)](./rms-client/client-admin-guide-customizations.md#integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution)」をご覧ください。 



