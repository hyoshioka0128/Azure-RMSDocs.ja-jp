---
title: チュートリアル - Azure Information Protection ポリシー設定を使ってデータを分類する
description: Azure Information Protection のポリシー設定を構成して、組織のドキュメントや電子メールを分類する手順について説明した簡単なチュートリアルです。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/04/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 292d7f00aeeb4f13b9d8e2f88b746d6ef967dda9
ms.sourcegitcommit: dec5df81b569283a72f0a983d3f53b82cbbc562c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2020
ms.locfileid: "87802251"
---
# <a name="tutorial-configure-azure-information-protection-policy-settings-that-work-together"></a>チュートリアル:連携させる Azure Information Protection のポリシー設定を構成する

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順:[Windows 用 Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と**ラベル管理**は、**2021 年 3 月 31 日**で**非推奨**になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

このチュートリアルでは、以下を実行する方法について説明します。
> [!div class="checklist"]
> * 連携されるポリシー設定を構成する
> * 設定の動作を確認する


各自のドキュメントや電子メールを手動でラベル付けするようユーザーに任せる代わりに、Azure Information Protection のポリシー設定を使用して次のことを行えます。

- 新しいコンテンツと編集されたコンテンツに対して基本レベルの分類を保証する

- ラベルについてユーザーを教育し、適切なラベルを適用しやすくする

このチュートリアルを完了するための所要時間は約 15 分です。

## <a name="prerequisites"></a>[前提条件] 

このチュートリアルを完了するための必要条件を次に示します。

1. Azure Information Protection プラン 1 またはプラン 2 を含むサブスクリプション。
    
    このプランを含むサブスクリプションを持っていない場合は、組織用の[無料](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)アカウントを作成できます。

2. Azure portal に [Azure Information Protection] ペインが追加されていて、Azure Information Protection のグローバル ポリシーに 1 つ以上のラベルが公開されている。
    
    これらの手順については、「[クイック スタート:Azure portal で Azure Information Protection の使用を開始する](quickstart-viewpolicy.md)」を参照してください。

3. お使いの Windows コンピューター (Windows 7 Service Pack 1 以降) に Azure Information Protection クライアント (クラシック) がインストールされている。 
    
    クラシック クライアントをインストールするには、[Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=53018)に移動し、Azure Information Protection ページから **AzInfoProtection.exe** をダウンロードします。 
    
    クラシック クライアントとは別のラベル付けクライアントを使用している場合は、Microsoft 365 のコンプライアンス ドキュメントで機密ラベルのポリシー設定の詳細を確認してください。 たとえば、「[機密ラベルについて](/microsoft-365/compliance/sensitivity-labels)」です。

4. 次のいずれかのカテゴリから Office アプリにサインインしている。
    
    - Azure Rights Management (別名: Azure Information Protection for Office 365) のライセンスが割り当てられている場合は、Office 365 Business または Microsoft 365 Business の最小バージョン 1805、ビルド 9330.2078 の Office アプリ。
    
    - Office 365 ProPlus
    
    - Office Professional Plus 2019
    
    - Office Professional Plus 2016
    
    - Office Professional Plus 2013 Service Pack 1
    
    - Office Professional Plus 2010 Service Pack 2

Azure Information Protection を使用するための必要条件の完全な一覧については、「[Azure Information Protection の要件](requirements.md)」をご覧ください。

では、始めましょう。

## <a name="edit-the-azure-information-protection-policy"></a>Azure Information Protection ポリシーを編集する

各自のドキュメントや電子メールを手動でラベル付けするようユーザーに任せる代わりに、いくつかのポリシー設定を使用して基本レベルの分類を保証することができます。 

Azure portal を使用してグローバル ポリシーを編集し、すべてのユーザーに向けたポリシー設定を変更します。

1. 新しいブラウザー ウィンドウを開き、全体管理者として [Azure portal](https://portal.azure.com) にサインインします。次に、 **[Azure Information Protection]** に移動します。 
    
    たとえば、リソース、サービス、ドキュメントの検索ボックスで次のようにします: 「**Information**」と入力し、 **[Azure Information Protection]** を選択します。
    
    グローバル管理者でない場合は、次のリンクを使用して別のロールにします:「[Azure portal にサインインする](configure-policy.md#signing-in-to-the-azure-portal)」

2. **[分類]**  >  **[ポリシー]**  >  **[グローバル]** を選択して、 **[ポリシー:グローバル]** ペインを開きます。 

3. **[表示する設定を構成して、Information Protection のエンド ユーザーに適用する]** セクションで、ラベルの後にポリシー設定があるのを見つけます。 設定の値は次に表示する値とは異なる場合があります。
    
    ![Azure Information Protection チュートリアル - 既定の設定](./media/defaultsettings-aip.png)

4. 設定を変更して、次の表の値に合わせます。 このチュートリアルの完了時に設定を元に戻す必要がある場合は、変更する設定をメモしておきます。 

    |設定|値|説明|
    |-------|-----|-----|
    |**既定のラベルの選択**|**全般**|**[全般]** ラベルは、Azure Information Protection によって自動的に作成される既定のラベルの 1 つです。 その手順は「[ラベルの作成と公開](quickstart-viewpolicy.md#create-and-publish-labels)」のクイック スタートで説明されています。 **[全般]** という名前のラベルがない場合は、ドロップダウン リストから別のラベルを選択します。 ラベル付けされていないドキュメントや電子メールは、基本の分類として自動的にこのラベルを適用されます。 ただし、ユーザーは選択したラベルを別のラベルに変更できます。|
    |**すべてのドキュメントとメールにラベルを付ける**|**オン**|この設定は必須のラベル付けとも呼ばれます。ユーザーがラベルを付けずにドキュメントを保存したり電子メールを送信したりできないようにするためです。 既定のラベルと合わせると、ドキュメントと電子メールには、設定した既定のラベルか各自が選択したラベルのいずれかが付けられます。
    |**添付ファイルのある電子メール メッセージの場合、その添付ファイルの最上位の分類と一致するラベルを適用します**|**推奨**|この設定では、自分が選択した既定のラベルよりも上位の分類を持つドキュメントをユーザーが添付した場合に、その電子メール用の上位の分類のラベルを選択するようユーザーに求めます。
    |**Office アプリの Information Protection バーを表示します**|**オン**|Information Protection バーを表示させると、ユーザーが既定のラベルを確認および変更しやすくなります。
    
    設定は次のように表示されます。
    
    ![Azure Information Protection チュートリアル - 既定の設定の変更](./media/defaultsettings-aip-changed.png)

5. **[保存]** を選択し (この **[ポリシー:グローバル]** ペイン上)、操作を確認するメッセージが表示されたら **[OK]** を選択します。 

## <a name="see-your-policy-settings-in-action"></a>ポリシー設定の動作を確認する 

このチュートリアルでは、Word と Outlook を使用してポリシーの変更の動作を確認します。 ポリシー設定を変更する前にこれらのアプリを既に読み込んでいた場合は、アプリを再起動して変更をダウンロードさせます。

### <a name="default-label-and-the-information-protection-bar"></a>既定のラベルと Information Protection バー

Word で新しいドキュメントを開きます。 ドキュメントのラベルの選択がユーザーに任されるのではなく、自動的に **[全般]** ラベルが付けられていることを確認します。 

使用可能なラベルを示す Information Protection バーが表示されていると、ユーザーは現在選択しているラベルを確認したり、既定のラベルが適切でない場合はそれを変更したりしやすくなります。

![Azure Information Protection チュートリアル - 既定のラベルを持つ新しいドキュメント](./media/defaultlabel-word.png)

ラベルを変更する代わりに、Information Protection バーを閉じて、バーが表示されない場合のエクスペリエンスと比較します。

![Azure Information Protection チュートリアル - バーを閉じる](./media/infoprotect-bar-close.png)

**[全般]** ラベルが選択されたままですが、非常にわかりにくくなります。 また、別のラベルを選択する方法もわかりにくくなります。 そのためには、ユーザーは **[保護]** ボタンを選択する必要があります。

![Azure Information Protection チュートリアル - [保護] ボタンの選択](./media/infoprotect-protectbutton-pulldown.png)

これで、プルダウン メニューから、横にチェック マークが付いている **[全般]** ラベルが選択されていることがわかります。 現在選択されているラベルを変更するために、ユーザーは一覧から別のラベルを選択できます。 ユーザーが初めてラベル付けを使用する場合、おそらく毎回 **[保護]** ボタンを選択することを覚えられないでしょう。 また、別のラベルを選択できるということに気付かない可能性もあります。

もう一度 Information Protection バーを表示するには、プルダウン メニューから **[バーの表示]** を選択します。

> [!TIP]
> [クライアントの詳細設定](./rms-client/client-admin-guide-customizations.md#set-a-different-default-label-for-outlook)を構成すると、Outlook に対して別の既定のラベルを選択できます。

### <a name="mandatory-labeling"></a>必須のラベル付け

現在選択されている **[全般]** ラベルを別のラベルに変更することはできますが、それを削除することはできません。 **[すべてのドキュメントとメールにラベルを付ける]** 設定を **[オン]** に変更したため、Information Protection バー上で **[ラベルの削除]** アイコンを使用することはできません。 

その設定を変更していなかった場合は、Information Protection バーに次のアイコンが表示されます。

![Azure Information Protection チュートリアル - バーを閉じる](./media/infoprotect-deletelabel-icon.png)

既定のラベルと共に必須のラベル付けを使用すると、新規のまたは編集したドキュメント (および電子メール) に対して任意の基本の分類が適用されるよう保証することができます。 

必須のラベル付け設定と共に既定のラベルを設定していなかった場合、ユーザーは、ラベル付けされていないドキュメントを保存したりラベル付けされていない電子メールを送信したりするたびにラベルを選択するよう求められます。 これらの継続的なプロンプトに対して、多くのユーザーがストレスを感じる可能性があります。また、精度の低いラベル付けの原因となる可能性もあります。 ドキュメントや電子メールの作業を終えたユーザーにラベルを選択するよう求めると、各ユーザーのワークフローが中断されます。そして、やらなければならない次の作業に移行するために、ユーザーは適当なラベルをランダムに選択しようとします。

### <a name="recommendations-for-emails-with-attachments"></a>添付ファイル付きの電子メールの推奨事項

開いた Word 文書に対して、 **[全般]** よりも上位の分類を持つラベルを選択します。 たとえば、 **[社外秘]** の下にあるいずれかのサブラベル ( **[Confidential - Anyone (not protected)]\(社外秘 - すべてのユーザー (未保護)\)** など) です。 ドキュメントをローカルに保存し、任意の名前を付けます。 

Outlook を起動し、新しい電子メール メッセージを作成します。 Word の場合と同様に、新しい電子メール メッセージには自動的に **[全般]** ラベルが付けられ、Information Protection バーが表示されます。

ラベル付けした Word ドキュメントを、添付ファイルとして電子メール メッセージに追加します。 電子メールのラベルを、Word の添付ファイルと一致する **[社外秘]** ラベルに変更するよう求めるプロンプトが表示されます。 推奨事項を受け入れるか、破棄することができます。

![Azure Information Protection チュートリアル - ラベル付けされた添付ファイルと一致するよう電子メールをラベル付けし直すよう求めるプロンプト](./media/infoprotect-matchemail-label.png)

**[破棄]** をクリックすると、新しいラベルは適用されず、構成した既定のラベル **[全般]** が電子メールに適用されたままになります。 使用可能なラベルは引き続き表示されており、代替として選択できます。

**[今すぐ変更]** を選択すると、電子メールに **[社外秘]** サブラベルがラベル付けし直されます。 ただし、電子メールを送信する前でも、[ラベルの編集] アイコンを選択すれば、ユーザーがラベルを変更することは可能です。

![Azure Information Protection チュートリアル - ラベル アイコンを編集する](./media/infoprotect-editlabel-icon.png)

そうすると、Information Protection バーが再度表示され、ユーザーは代わりのラベルを選択できます。

電子メールを送信する前にラベルの選択を行うので、このポリシー設定の動作を確認するために電子メールを実際に送信する必要はありません。 送信または保存せずに電子メールを閉じてかまいません。

ただし、上位の分類 ( **[非常に機密性の高い社外秘]** ラベルのサブラベル) を持つ別のドキュメントを添付して、この手順を繰り返すこともできます。 その場合、上位の分類ラベルを適用するよう求めるプロンプトがどのように変更されるのかを確認できます。 同じ親ラベルを持つサブラベルを使って複数の添付ファイルをテストする場合、その順序をサポートするには Azure portal で[クライアントの詳細設定](./rms-client/client-admin-guide-customizations.md#enable-order-support-for-sublabels-on-attachments)を構成する必要があります。

## <a name="clean-up-resources"></a>リソースをクリーンアップする

このチュートリアルで行った変更を保持したくない場合は、次の操作を行います。

1. **[分類]**  >  **[ポリシー]**  >  **[グローバル]** を選択して、 **[ポリシー:グローバル]** ペインを開きます。

2. ポリシー設定をメモしておいた元の値に戻した後、 **[保存]** を選択します。

Word アプリと Outlook アプリを再起動して、これらの変更をダウンロードします。

## <a name="next-steps"></a>次のステップ

Azure Information Protection のポリシー設定の編集について詳しくは、「[Azure Information Protection のポリシー設定を構成する方法](configure-policy-settings.md)」をご覧ください。

変更したポリシー設定は、適切なラベルを選択するようユーザーに推奨することに加えて、基本レベルの分類を保証することにも役立ちました。 次の手順では、ドキュメントおよび電子メールの内容を調べてから、適切なラベルを推奨または自動的に適用することによって、この戦略を補強します。 これを行うには、条件のラベルを構成します。 詳細については、「[Azure Information Protection 用の自動および推奨分類の条件を構成する方法](configure-policy-classification.md)」をご覧ください。
