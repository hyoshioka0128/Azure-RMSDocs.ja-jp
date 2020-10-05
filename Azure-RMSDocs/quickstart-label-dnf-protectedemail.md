---
title: クイック スタート - Azure Information Protection (AIP) でラベルを構成し、ユーザーがメールを簡単に保護できるようにする
description: 転送不可の保護を自動的に適用することで、ユーザーの電子メールを保護するラベルを構成します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/04/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 4d81f1406f1894acf6c820693e80d00dca1662f4
ms.sourcegitcommit: 24c97b58849af4322d3211b8d3165734d5ad6c88
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/29/2020
ms.locfileid: "91428454"
---
# <a name="quickstart-configure-a-label-for-users-to-easily-protect-emails-that-contain-sensitive-information"></a>クイック スタート:ラベルを構成して、ユーザーが機密情報を含む電子メールを簡単に保護できるようにする

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順:[Windows 用 Azure Information Protection クラシック クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE]
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と**ラベル管理**は、**2021 年 3 月 31 日**で**非推奨**になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

このクイック スタートでは、 **[転送不可]** の保護設定を自動的に適用するように、既存の Azure Information Protection ラベルを構成します。

現在の Azure Information Protection ポリシーには、この構成を持つ次の 2 つのラベルが既に含まれています。

- **社外秘 \ 受信者のみ**

- **非常に機密性の高い社外秘 \ 受信者のみ**

ただし、ポリシーが古い場合や、組織のポリシーの作成時に保護がアクティブ化されなかった場合、これらのラベルは含まれません。

**必要な時間:** この構成は 5 分で完了します。

## <a name="prerequisites"></a>[前提条件]

このクイック スタートを完了するには、次の要件があります。

|要件  |説明  |
|---------|---------|
|**サポート サブスクリプション**     |  [**Azure Information Protection プラン 1 またはプラン 2**](https://azure.microsoft.com/pricing/details/information-protection/) を含むサブスクリプションが必要です。 </br></br>このようないずれかのサブスクリプションがない場合は、組織用の[無料](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)アカウントを作成できます。       |
|**Azure portal に AIP が追加されている**    |  Azure portal に [Azure Information Protection] ペインを追加し、保護サービスがアクティブになっていることを確認した。 </br></br>詳細については、「[クイック スタート: 作業の開始](quickstart-viewpolicy.md)に関するページをご覧ください。       |
|**構成する既存の Azure Information Protection ラベル**     | 既定のいずれかのラベルまたは作成済みのラベルを使用できます。 詳細については、「[クイック スタート: 特定のユーザー向けの新しい Azure Information Protection ラベルを作成する](quickstart-label-specificusers.md)」をご覧ください。 |
|**クラシック クライアントがインストールされている**    |   新しいラベルをテストするには、使用するコンピューターにクラシック クライアントをインストールする必要があります。 </br></br>Azure Information Protection クラシック クライアントは、2021 年 3 月に非推奨となる予定です。 AIP クラシック クライアントをデプロイするには、サポート チケットを作成してダウンロード アクセスを取得します。  |
|**Office アプリにサインインしている Windows コンピューター** |新しいラベルをテストするには、Windows (Windows 7 Service Pack 1 以降) を実行しているコンピューターが必要です。 </br></br>このコンピューターで、次のいずれかのバージョンに該当する Office アプリにサインインします。 </br>- Azure Rights Management のライセンスが割り当てられている場合は Office アプリの最小バージョン 1805、Microsoft 365 Apps for Business のビルド 9330.2078、または Microsoft 365 Business Premium。 </br>- Microsoft 365 Apps for Enterprise。 </br>- Office Professional Plus 2019。 </br>- Office Professional Plus 2016。</br>- Office Professional Plus 2013 Service Pack 1。 </br>- Office Professional Plus 2010 Service Pack 2。|
| | |

Azure Information Protection を使用するための必要条件の完全な一覧については、「[Azure Information Protection の要件](requirements.md)」をご覧ください。

## <a name="configure-an-existing-label-to-apply-the-do-not-forward-protection"></a>転送不可の保護を適用するように既存のラベルを構成する

1. 新しいブラウザー ウィンドウを開き、全体管理者として [Azure portal](https://portal.azure.com) にサインインします。次に、 **[Azure Information Protection]** に移動します。

    たとえば、リソース、サービス、ドキュメントの検索ボックスで次のようにします: 「**Information**」と入力し、 **[Azure Information Protection]** を選択します。

    グローバル管理者でない場合は、次のリンクを使用して別のロールにします:「[Azure portal にサインインする](configure-policy.md#signing-in-to-the-azure-portal)」

1. **[分類]**  >  **[ラベル]** メニュー オプションから: **[Azure Information Protection - ラベル]** ペインで、保護を適用するように構成するラベルを選択します。

1. **[ラベル]** ペインで、 **[このラベルを含むドキュメントやメールに対するアクセス許可の設定]** を見つけます。 **[保護]** を選択すると、 **[未構成]** または **[保護の削除]** が以前に選択されていた場合に **[保護]** ペインが自動的に開きます。

    **[保護]** ペインが自動的に開かない場合は、 **[保護]** を選択します。

    :::image type="content" source="media/info-protect-protection-bar-configured.png" alt-text="Azure Information Protection ラベルの保護を構成する":::

1. **[保護]** ペインで、 **[Azure (クラウド キー)]** が選択されていることを確認します。

1. **[ユーザー定義のアクセス許可の設定 (プレビュー)]** を選択します。

1. 次のオプションが選択されていることを確認します。 **[Outlook で [転送不可] を適用する]** 。

1. 選択されている場合は、次のオプションをオフにします。 **[Word、Excel、PowerPoint、エクスプローラーでは、カスタム アクセス許可を指定するようユーザーに促す]** 。

1. **[保護]** ペインで **[OK]** をクリックしてから、 **[ラベル]** ペインで **[保存]** をクリックします。

これで、Outlook でのみ表示され、メールに **[転送不可]** の保護が適用されるようにラベルが構成されました。

## <a name="test-your-new-label"></a>新しいラベルをテストする

[Office 365 Message Encryption の新機能](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e)向けに Exchange Online が構成されている場合、構成済みのラベルは Outlook でのみ表示され、組織外の受信者に送信される電子メールに適しています。

1. コンピューターで Outlook を開き、新しい電子メール メッセージを作成します。 Outlook が既に開いている場合は再起動して、ポリシーの更新を適用します。

2. 受信者、電子メール メッセージのテキストを指定し、作成したラベルを適用します。

    電子メール メッセージはラベル名に従って分類され、転送不可の制限を使用して保護されます。

3. 電子メールを送信します。

これにより、受信者はその電子メールを転送したり印刷することができなくなり、メールからコピーしたり、添付ファイルを保存したり、電子メールを別の名前で保存することもできなくなります。 任意のユーザーが任意のデバイスで、保護された電子メール メッセージを読むことができます。

## <a name="clean-up-resources"></a>リソースをクリーンアップする

この構成を保持しない場合や、保護を適用しないようなラベルを返さない場合は、次の手順を実行します。

1. **[分類]**  >  **[ラベル]** メニュー オプションから: **[Azure Information Protection - ラベル]** ペインで、構成したラベルを選択します。

1. **[ラベル]** ペインで、 **[このラベルを含むドキュメントやメールに対するアクセス許可の設定]** を見つけ、 **[未構成]** を選択して **[保存]** を選択します。

## <a name="next-steps"></a>次のステップ

このクイック スタートには、ラベルをすばやく構成するための最低限のオプションが含まれています。ラベルを使用すると、ユーザーは電子メールを簡単に保護できます。 ただし、構成の制限が厳しすぎる場合や、制限が不十分な場合は、以下に示す他の構成例をご覧ください。

- [[転送不可] よりも制限の緩いアクセス許可をサポートする保護された電子メールのラベル](configure-policy-protection.md#example-4-label-for-protected-email-that-supports-less-restrictive-permissions-than-do-not-forward)

- [コンテンツを暗号化するが、アクセスできるユーザーは制限しないラベル](configure-policy-protection.md#example-5-label-that-encrypts-content-but-doesnt-restrict-who-can-access-it)

保護を適用するラベルを構成するための詳しい手順については、「[Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)」をご覧ください。
