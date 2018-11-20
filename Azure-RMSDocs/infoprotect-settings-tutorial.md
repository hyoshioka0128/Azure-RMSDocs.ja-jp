---
title: チュートリアル - Azure Information Protection のポリシー設定を構成してドキュメントや電子メールを分類する
description: Azure Information Protection のポリシー設定を構成して、組織のドキュメントや電子メールを分類する手順について説明した簡単なチュートリアルです。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/14/2018
ms.topic: tutorial
ms.service: information-protection
ms.openlocfilehash: b9f60d0e8cc61a1d38b2992c0d430507bf494d18
ms.sourcegitcommit: ad37950f6a747c86f6496c6de859e18446f9b03f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2018
ms.locfileid: "51644653"
---
# <a name="tutorial-configure-azure-information-protection-policy-settings-that-work-together"></a>チュートリアル: 連携させる Azure Information Protection のポリシー設定を構成する

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

このチュートリアルで学習する内容は次のとおりです。
> [!div class="checklist"]
> * 連携されるポリシー設定を構成する
> * 設定の動作を確認する

各自のドキュメントや電子メールを手動でラベル付けするようユーザーに任せる代わりに、ポリシー設定を使用して次の操作を実行できます。

- 新しいコンテンツと編集されたコンテンツに対して基本レベルの分類を保証する

- ラベルについてユーザーを教育し、適切なラベルを適用しやすくする

このチュートリアルを完了するための所要時間は約 15 分です。

## <a name="prerequisites"></a>必要条件 

このチュートリアルを完了するための必要条件を次に示します。

1. Azure Information Protection プラン 2 を含むサブスクリプション。
    
    このプランを含むサブスクリプションを持っていない場合は、組織用の[無料](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)アカウントを作成できます。

2. Azure portal に [Azure Information Protection] ブレードを追加し、保護サービスがアクティブになっていることを確認した。

    これらの操作に関するサポートが必要な場合は、[Azure portal に Azure Information Protection を追加し、ポリシーを表示するためのクイック スタート](quickstart-viewpolicy.md)をご覧ください。

3. Azure Information Protection クライアントがコンピューターにインストールされている。 
    
    クライアントをインストールするには、[Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)に移動し、Azure Information Protection ページから **AzInfoProtection.exe** をダウンロードします。

4. Windows (Windows 7 Service Pack 1 以降) を搭載しているコンピューター。また、このコンピューターで、次のいずれかのカテゴリから Office アプリにサインインしている必要があります。
    
    - Office 365 と Office 2016 アプリ (バージョン 1805、ビルド 9330.2078 以降)。 このオプションを使用するには、Azure Rights Management のライセンスがアカウントに割り当てられている必要があります。 このライセンスは、Azure Information Protection サブスクリプションに含まれています。
    
    - Office 365 ProPlus と 2016 アプリまたは 2013 アプリ (クリック実行または Windows インストーラー ベースのインストール)。
    
    - Office Professional Plus 2016。
    
    - Office Professional Plus 2013 Service Pack 1。
    
    - Office Professional Plus 2010 Service Pack 2。

Azure Information Protection を使用するための必要条件の完全な一覧については、「[Azure Information Protection の要件](requirements.md)」をご覧ください。

では、始めましょう。

## <a name="edit-the-azure-information-protection-policy"></a>Azure Information Protection ポリシーを編集する

各自のドキュメントや電子メールを手動でラベル付けするようユーザーに任せる代わりに、いくつかのポリシー設定を使用して基本レベルの分類を保証することができます。 

Azure portal を使用してグローバル ポリシーを編集し、すべてのユーザーに向けたポリシー設定を変更します。

1. 新しいブラウザー ウィンドウを開き、全体管理者として [Azure portal](https://portal.azure.com) にサインインします。次に、**[Azure Information Protection]** に移動します。 
    
    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。
    
    グローバル管理者でない場合は、別のロールのためにリンク「[Azure Portal にサインインする](configure-policy.md#signing-in-to-the-azure-portal)」を使用します。

2. **[分類]** > **[ポリシー]** > **[グローバル]** を選択して、**[ポリシー: グローバル]** ブレードを開きます。 

3. **[表示する設定を構成して、Information Protection のエンド ユーザーに適用する]** セクションで、ラベルの後にポリシー設定があるのを見つけます。 設定の値は次に表示する値とは異なる場合があります。
    
    ![Azure Information Protection チュートリアル - 既定の設定](./media/defaultsettings-aip.png)

4. 設定を変更して、次の表の値に合わせます。 このチュートリアルの完了時に設定を元に戻す必要がある場合は、変更する設定をメモしておきます。 

    |Setting|値|説明|
    |-------|-----|-----|
    |**既定のラベルの選択**|**全般**|**[全般]** という名前のラベルがない場合は、ドロップダウン リストから別のラベルを選択します。 ラベル付けされていないドキュメントや電子メールは、基本の分類として自動的にこのラベルを適用されます。 ただし、ユーザーは選択したラベルを別のラベルに変更できます。|
    |**すべてのドキュメントとメールにラベルを付ける**|**オン**|この設定は必須のラベル付けとも呼ばれます。ユーザーがラベルを付けずにドキュメントを保存したり電子メールを送信したりできないようにするためです。 既定のラベルと合わせると、ドキュメントと電子メールには、設定した既定のラベルか各自が選択したラベルのいずれかが付けられます。
    |**添付ファイルのある電子メール メッセージの場合、その添付ファイルの最上位の分類と一致するラベルを適用します**|**推奨**|この設定では、自分が選択した既定のラベルよりも上位の分類を持つドキュメントをユーザーが添付した場合に、その電子メール用の上位の分類のラベルを選択するようユーザーに求めます。
    |**Office アプリの Information Protection バーを表示します**|**オン**|Information Protection バーを表示させると、ユーザーが既定のラベルを確認および変更しやすくなります。
    
    設定は次のように表示されます。
    
    ![Azure Information Protection チュートリアル - 既定の設定の変更](./media/defaultsettings-aip-changed.png)

5. この **[ポリシー: グローバル]** ブレードで **[保存]** を選択します。操作を確認するメッセージが表示されたら **[OK]** を選択します。 

## <a name="see-your-policy-settings-in-action"></a>ポリシー設定の動作を確認する 

このチュートリアルでは、Word と Outlook を使用してポリシーの変更の動作を確認します。 ポリシー設定を変更する前にこれらのアプリを既に読み込んでいた場合は、アプリを再起動して変更をダウンロードさせます。

### <a name="default-label-and-the-information-protection-bar"></a>既定のラベルと Information Protection バー

Word で新しいドキュメントを開きます。 ドキュメントのラベルの選択がユーザーに任されるのではなく、自動的に **[全般]** ラベルが付けられていることを確認します。 

使用可能なラベルを示す Information Protection バーが表示されていると、ユーザーは現在選択しているラベルを確認したり、既定のラベルが適切でない場合はそれを変更したりしやすくなります。

![Azure Information Protection チュートリアル - 既定のラベルを持つ新しいドキュメント](./media/defaultlabel-word.png)

ラベルを変更する代わりに、Information Protection バーを閉じて、バーが表示されない場合のエクスペリエンスと比較します。

![Azure Information Protection チュートリアル - 既定のラベルを持つ新しいドキュメント](./media/infoprotect-bar-close.png)

**[全般]** ラベルが選択されたままですが、非常にわかりにくくなります。 また、別のラベルを選択する方法もわかりにくくなります。 そのためには、ユーザーは **[保護]** ボタンを選択する必要があります。

![Azure Information Protection チュートリアル - [保護] ボタンの選択](./media/infoprotect-protectbutton-pulldown.png)

これで、プルダウン メニューから、横にチェック マークが付いている **[全般]** ラベルが選択されていることがわかります。 現在選択されているラベルを変更するために、ユーザーは一覧から別のラベルを選択できます。 ユーザーが初めてラベル付けを使用する場合、おそらく毎回 **[保護]** ボタンを選択することを覚えられないでしょう。 また、別のラベルを選択できるということに気付かない可能性もあります。

もう一度 Information Protection バーを表示するには、プルダウン メニューから **[バーの表示]** を選択します。

> [!TIP]
> [クライアントの詳細設定](./rms-client/client-admin-guide-customizations.md#set-a-different-default-label-for-outlook)を構成すると、Outlook に対して別の既定のラベルを選択できます。

### <a name="mandatory-labeling"></a>必須のラベル付け

現在選択されている **[全般]** ラベルを別のラベルに変更することはできますが、それを削除することはできません。 **[すべてのドキュメントとメールにラベルを付ける]** 設定を **[オン]** に変更したため、Information Protection バー上で **[ラベルの削除]** アイコンを使用することはできません。 

その設定を変更していなかった場合は、Information Protection バーに次のアイコンが表示されます。

![Azure Information Protection チュートリアル - [保護] ボタンの選択](./media/infoprotect-deletelabel-icon.png)

既定のラベルと共に必須のラベル付けを使用すると、新規のまたは編集したドキュメント (および電子メール) に対して任意の基本の分類が適用されるよう保証することができます。 

必須のラベル付け設定と共に既定のラベルを設定していなかった場合、ユーザーは、ラベル付けされていないドキュメントを保存したりラベル付けされていない電子メールを送信したりするたびにラベルを選択するよう求められます。 これらの継続的なプロンプトに対して、多くのユーザーがストレスを感じる可能性があります。また、精度の低いラベル付けの原因となる可能性もあります。 ドキュメントや電子メールの作業を終えたユーザーにラベルを選択するよう求めると、各ユーザーのワークフローが中断されます。そして、やらなければならない次の作業に移行するために、ユーザーは適当なラベルをランダムに選択しようとします。

### <a name="recommendations-for-emails-with-attachments"></a>添付ファイル付きの電子メールの推奨事項

開いた Word 文書に対して、**[全般]** よりも上位の分類を持つラベルを選択します。 たとえば、**[社外秘]** の下にあるいずれかのサブラベル (**[Confidential - Anyone (not protected)]\(社外秘 - すべてのユーザー (未保護)\)** など) です。 ドキュメントをローカルに保存し、任意の名前を付けます。 

Outlook を起動し、新しい電子メール メッセージを作成します。 Word の場合と同様に、新しい電子メール メッセージには自動的に **[全般]** ラベルが付けられ、Information Protection バーが表示されます。

ラベル付けした Word ドキュメントを、添付ファイルとして電子メール メッセージに追加します。 電子メールのラベルを、Word の添付ファイルと一致する **[社外秘]** ラベルに変更するよう求めるプロンプトが表示されます。 推奨事項を受け入れるか、破棄することができます。

![Azure Information Protection チュートリアル - ラベル付けされた添付ファイルと一致するよう電子メールをラベル付けし直すよう求めるプロンプト](./media/infoprotect-matchemail-label.png)

**[破棄]** をクリックすると、新しいラベルは適用されず、構成した既定のラベル **[全般]** が電子メールに適用されたままになります。 使用可能なラベルは引き続き表示されており、代替として選択できます。

**[今すぐ変更]** を選択すると、電子メールに **[社外秘]** サブラベルがラベル付けし直されます。 ただし、ユーザーは、電子メールを送信する前に [ラベルの編集] を選択して、まだラベルを変更することができます。

![Azure Information Protection チュートリアル - ラベル付けされた添付ファイルと一致するよう電子メールをラベル付けし直すよう求めるプロンプト](./media/infoprotect-editlabel-icon.png)

そうすると、Information Protection バーが再度表示され、ユーザーは代わりのラベルを選択できます。

電子メールを送信する前にラベルの選択を行うので、このポリシー設定の動作を確認するために電子メールを実際に送信する必要はありません。 送信または保存せずに電子メールを閉じてかまいません。

ただし、上位の分類 (**[非常に機密性の高い社外秘]** ラベルのサブラベル) を持つ別のドキュメントを添付して、この手順を繰り返すこともできます。 その場合、上位の分類ラベルを適用するよう求めるプロンプトがどのように変更されるのかを確認できます。

## <a name="clean-up-resources"></a>リソースをクリーンアップする

このチュートリアルで行った変更を保持したくない場合は、次の操作を行います。

1. **[分類]** > **[ポリシー]** > **[グローバル]** を選択して、**[ポリシー: グローバル]** ブレードを開きます。

2. ポリシー設定をメモしておいた元の値に戻した後、**[保存]** を選択します。

Word アプリと Outlook アプリを再起動して、これらの変更をダウンロードします。

## <a name="next-steps"></a>次の手順

Azure Information Protection のポリシー設定の編集について詳しくは、「[Azure Information Protection のポリシー設定を構成する方法](configure-policy-settings.md)」をご覧ください。

変更したポリシー設定は、適切なラベルを選択するようユーザーに推奨することに加えて、基本レベルの分類を保証することにも役立ちました。 次の手順では、ドキュメントおよび電子メールの内容を調べてから、適切なラベルを推奨または自動的に適用することによって、この戦略を補強します。 これを行うには、条件のラベルを構成します。 詳細については、「[Azure Information Protection 用の自動および推奨分類の条件を構成する方法](configure-policy-classification.md)」をご覧ください。
