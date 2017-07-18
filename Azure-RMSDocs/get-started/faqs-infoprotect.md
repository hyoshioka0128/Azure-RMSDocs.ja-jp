---
title: "分類とラベル付けに関してよく寄せられる質問 - AIP"
description: "Azure Information Protection の使用について、特に分類とラベル付けに関して質問はございますか。 ここで回答を探してみてください。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/12/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4b595b6a-7eb0-4438-b49a-686431f95ddd
ms.reviewer: adhall
ms.suite: ems
ms.openlocfilehash: 80efd633bc814af1ac28e4b6bf2d0b3062b27d01
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2017
---
# <a name="frequently-asked-questions-about-classification-and-labeling-in-azure-information-protection"></a>Azure Information Protection の分類とラベル付けに関してよく寄せられる質問

>*適用対象: Azure Information Protection、Office 365*

Azure Information Protection に関して、特に分類とラベル付けに関して質問はございますか。  ここで回答を探してみてください。 

## <a name="what-can-i-do-with-the-classification-capabilities-in-azure-information-protection"></a>Azure Information Protection の分類機能はどのように使用しますか。

「[Azure Information Protection のクイック スタート チュートリアル](infoprotect-quick-start-tutorial.md)」に従えば、わずか数分でこの動作を確認できます。

追加の分類機能が利用可能になる時期については、[Enterprise Mobility and Security ブログ](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection)および [Yammer サイト](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all)での案内をご確認ください。 現在のリリースには、次のような制限がいくつかあります。

- ラベル名とツール ヒントは 1 言語でのみサポートされます。 ただし、複数言語サポートは現在プレビュー段階です。 詳細については、[他の言語用ラベルを構成する方法](../deploy-use/configure-policy-languages.md)に関するページをご覧ください。

- 分類とラベル付けには集中的なログはありません。

- 自動分類の条件は、語句またはパターンでなければなりません。

- モバイル デバイス (iOS および Android) および Mac コンピューター用の Office アプリや Office Web アプリ (Office Online) ではラベル付けできません。

- 分類およびラベル付けは Exchange Online や SharePoint Online とは統合されません。

- パートナーおよび開発者用の SDK にはまだ分類とラベル付け機能は含まれていません。

2 月のリリースでは以前の多くの制限がなくなりました。 詳細については、[ブログの投稿のお知らせ](https://blogs.technet.microsoft.com/enterprisemobility/2017/02/08/azure-information-protection-december-update-moves-to-general-availability/)を参照してください。

## <a name="do-i-need-to-be-a-global-admin-to-configure-classification-and-labels"></a>分類とラベルを構成するにはグローバル管理者である必要がありますか?

Azure Information Protection ポリシーを構成するとき、Azure Active Directory のグローバル管理者として Azure Portal にサインインする必要がなくなりました。 また、セキュリティ管理者の役割が与えられたアカウントを利用できるようになりました。

[Azure Information Protection クライアント](https://www.microsoft.com/en-us/download/details.aspx?id=53018)をインストールするときにデモ ポリシーをインストールするオプションを選択した場合は、ポータルにサインインしなくてもラベル機能を試すことができます。 デモ ポリシーでは Azure Information Protection 用の既定のポリシーがローカルにインストールされるので、ドキュメントと電子メールへのラベル付けを試用できますが、ラベルの変更または新規追加には Azure Portal にサインインする必要があります。 

## <a name="which-options-in-the-azure-portal-are-p2"></a>Azure Portal のオプションが P2 かどうかを確認するにはどうすればよいですか?

**Azure Information Protection Premium 2** (P2) のサブスクリプションを必要とする Azure Portal のオプションでは、そのことを示す情報ポップアップ メッセージが表示されるようになりました。 P1 および P2 のサブスクリプションに含まれる機能について詳しくは、Azure Information Protection のサイトの[機能一覧](https://www.microsoft.com/cloud-platform/azure-information-protection-features)をご覧ください。

## <a name="can-a-file-have-more-than-one-classification"></a>1 つのファイルに複数の分類を適用することはできますか?

ユーザーが一度に選択できるのはドキュメントまたは電子メールごとに 1 つのラベルのみです。したがって、多くの場合、適用できる分類は 1 つのみとなります。 ただし、ユーザーがサブラベルを選択した場合、実際は同時に 2 つのラベル (プライマリ ラベルとセカンダリ ラベル) が適用されます。 サブラベルを使用すれば、1 つのファイルで 2 つの分類 (制御の追加レベルの親\子関係を示す) を適用することができます。

たとえば、**Confidential** というラベルに、**Legal** や **Finance** などのサブラベルを含めることができます。 これらのサブラベルには、異なる分類ビジュアル マーキングと異なる Rights Management テンプレートをそれぞれ適用することができます。 ユーザーは **Confidential** ラベル自体を選択することはできません。選択できるのは、**Legal** などのそのサブラベルのいずれか 1 つのみです。 したがって、表示されるラベル セットは **Confidential \ Legal** のようになります。 そのファイルのメタデータには、**Confidential** のカスタム テキスト プロパティが 1 つ、**Legal** のカスタム テキスト プロパティが 1 つ、さらに両方の値 (**Confidential Legal**) を含むものが含まれます。 

サブラベルを使用する場合は、プライマリ ラベルでビジュアル マーキング、保護、および条件を構成しないでください。 サブレベルを使用する場合は、サブラベルのみにこれらの設定を構成してください。 プライマリ ラベルとそのサブラベルでこれらの設定を構成した場合は、サブラベルの設定が優先されます。

## <a name="when-an-email-is-labeled-do-any-attachments-automatically-get-the-same-labeling"></a>電子メールにラベルが付けられた場合、添付ファイルにも同じラベルが自動的に付けられますか?

いいえ。 添付ファイルのある電子メール メッセージにラベルを付ける場合、これらの添付ファイルは同じラベルを継承しません。 添付ファイルは、ラベルがないか、個別に適用されたラベルが付けられた状態で保持されます。 ただし、電子メールのラベルが保護を適用する場合、その保護は添付ファイルに適用されます。

## <a name="how-can-dlp-solutions-and-other-applications-integrate-with-azure-information-protection"></a>DLP ソリューションや他のアプリケーションは Azure Information Protection とどのように統合できますか?

Azure Information Protection は分類に永続的メタデータを使用し、これにはクリア テキストのラベルが含まれるので、DLP ソリューションや他のアプリケーションはこの情報を読み取ることができます。 ファイルでは、このメタデータはカスタム プロパティに格納されます。 電子メールでは、この情報は電子メールのヘッダーにあります。

## <a name="how-is-azure-information-protection-classification-for-emails-different-from-exchange-message-classification"></a>Azure Information Protection の電子メールの分類は、Exchange のメッセージ分類とどのように違いますか?

Exchange のメッセージ分類は電子メールを分類する古い機能で、Azure Information Protection の分類機能とは別に実装されます。 

ただし、ユーザーが Outlook on the web や一部のモバイル用メール アプリケーションを使用して電子メールを分類する場合に、これら 2 つのソリューションを統合し、Azure Information Protection の分類および対応するラベル マーキングが自動的に追加されるようにすることができます。 

同じ手法を使用して、Outlook on the web とこれらのモバイル用メール アプリケーションで独自のラベルを使用できます。

構成手順については、「[Integrate Exchange message classification with Azure Information Protection for a mobile device labeling solution (Exchange のメッセージ分類と Azure Information Protection を統合したモバイル デバイス用ラベル付けソリューション)](../rms-client/client-admin-guide-customizations.md#integration-with-exchange-message-classification-for-a-mobile-device-labeling-solution)」をご覧ください。 



[!INCLUDE[Commenting house rules](../includes/houserules.md)]
