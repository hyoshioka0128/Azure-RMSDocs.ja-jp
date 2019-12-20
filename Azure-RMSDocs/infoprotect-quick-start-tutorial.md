---
title: チュートリアル - Azure Information Protection ポリシーを編集する - AIP
description: 組織用の Microsoft Azure Information Protection ポリシーを編集するための簡単なチュートリアルです。所要時間は約 15 分です。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/01/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: c425fcc71f8400b945ec684f45f5c1622fedbbef
ms.sourcegitcommit: f5d8cf4440a35afaa1ff1a58b2a022740ed85ffd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73559221"
---
# <a name="tutorial-configure-azure-information-protection-policy-settings-and-create-a-new-label"></a>チュートリアル: Azure Information Protection ポリシーの設定を構成して新しいラベルを作成する

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順:[Windows 用 Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

このチュートリアルで学習する内容は次のとおりです。
> [!div class="checklist"]
> * ポリシー設定を構成する
> * 新しいラベルの作成 
> * 視覚的なマーキング、推奨される分類、および保護用のラベルを構成する
> * 設定とラベルの動作を確認する

この構成を行うと、ユーザーは新しいドキュメントまたは電子メールを作成するときに既定のラベルが適用されることを確認できます。 ただし、クレジット カード情報が検出された場合は、新しいラベルを適用するように求められます。 新しいラベルが適用されると、コンテンツは、対応するフッターと透かしと共に再分類され、保護されます。 

このチュートリアルを完了するための所要時間は約 15 分です。

## <a name="prerequisites"></a>必要条件 

このチュートリアルを完了するための必要条件を次に示します。

1. Azure Information Protection プラン 2 を含むサブスクリプション。
    
    Azure Information Protection プラン 2 を含むサブスクリプションを持っていない場合は、組織用の[無料](https://admin.microsoft.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7)アカウントを作成できます。

2. Azure portal に [Azure Information Protection] ペインが追加され、保護サービスがアクティブ化されており、Azure Information Protection のグローバル ポリシーに 1 つ以上のラベルが公開されている。
    
    これらの手順については、「[クイック スタート:Azure portal で Azure Information Protection の使用を開始する](quickstart-viewpolicy.md)」を参照してください。

3. お使いの Windows コンピューター (Windows 7 Service Pack 1 以降) に Azure Information Protection クライアント (クラシック) がインストールされている。 
    
    クラシック クライアントをインストールするには、[Microsoft ダウンロード センター](https://www.microsoft.com/en-us/download/details.aspx?id=53018)に移動し、Azure Information Protection ページから **AzInfoProtection.exe** をダウンロードします。 クラシック クライアントとは別のラベル付けクライアントを使用している場合は、このチュートリアルと同等の手順について [Office ドキュメント](/microsoft-365/compliance/sensitivity-labels)を参照してください。

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

Azure portal を使用して、最初にいくつかのポリシー設定を変更した後、新しいラベルを作成します。

### <a name="edit-the-policy-settings"></a>ポリシー設定を編集する

1. 新しいブラウザー ウィンドウを開き、全体管理者として [Azure portal](https://portal.azure.com) にサインインします。次に、 **[Azure Information Protection]** に移動します。 
    
    たとえば、リソース、サービス、ドキュメントの検索ボックスで次のようにします: 「**Information**」と入力し、 **[Azure Information Protection]** を選択します。
    
    グローバル管理者でない場合は、次のリンクを使用して別のロールにします:「[Azure portal にサインインする](configure-policy.md#signing-in-to-the-azure-portal)」

2. **[分類]**  >  **[ポリシー]**  >  **[グローバル]** を選択して、 **[ポリシー:グローバル]** ペインを開きます。 

3. **[表示する設定を構成して、Information Protection のエンド ユーザーに適用する]** セクションで、ラベルの後にポリシー設定があるのを見つけます。 
    
    設定が現在どのように構成されているかをメモしておきます。 具体的には、 **[既定のラベルの選択]** 設定と **[分類ラベルを低くする、ラベルを削除する、保護を削除する場合、ユーザーは理由を提供する必要があります]** 設定です。 次に例を示します。
    
    ![Azure Information Protection チュートリアル - 変更するポリシー設定](./media/info-protect-policy-default-settings.png)
    
    チュートリアルの後半でこれらのポリシー設定を使用し、その動作を確認します。

4. **[既定のラベルを選択]** に対して、いずれかのラベル ( **[全般]** など) を選択します。 
    
    **[全般]** ラベルは、Azure Information Protection によって自動的に作成される既定のラベルの 1 つです。 この手順は、Azure portal に Azure Information Protection を追加するクイック スタートの「[ラベルの作成と公開](quickstart-viewpolicy.md#create-and-publish-labels)」セクションで説明されています。

5. **[分類ラベルを低くする、ラベルを削除する、保護を削除する場合、ユーザーは理由を提供する必要があります]** オプションが [オン] になっていない場合は、 **[オン]** に設定します。

6. さらに、 **[Office アプリの Information Protection バーを表示します]** が **[オン]** になっていることを確認します。

7. **[保存]** を選択し (この **[ポリシー:グローバル]** ペイン上)、操作を確認するメッセージが表示されたら **[OK]** を選択します。 このペインを閉じます。

### <a name="create-a-new-label-for-protection-visual-markers-and-a-condition-to-prompt-for-classification"></a>保護用の新しいラベル、視覚的なマーカー、および分類を求めるための条件を作成する

ここでは、**社外秘**に新しいサブラベルを作成します。

1. **[分類]**  >  **[ラベル]** メニュー オプションから: **[社外秘]** ラベルを右クリックし、 **[サブラベルの追加]** を選択します。
    
    **[社外秘]** という名前のラベルがない場合は、代わりに別のラベルを選択するか新しいラベルを作成しても、わずかな違いでチュートリアルを続行することができます。

2. **[サブラベル]** ペインで、 **[財務]** のラベル名を指定し、**従業員のみに制限される財務情報が含まれる機密データ**という説明を追加します。
    
    このテキストは、選択したラベルがどのような使用目的であるかを示しており、ユーザーに対してはツールヒントとして表示され、ユーザーがどのラベルを選択するかを決定するのに役立ちます。

3. **[このラベルを含むドキュメントやメールに対するアクセス許可の設定]** に対して、 **[保護]** を選択します。これにより、 **[保護]** オプションを選択することで自動的に **[保護]** ペインが開きます。
    
    ![保護用の Azure Information Protection ラベルの構成](./media/info-protect-protection-bar-configured.png) 
    
4. **[保護]** ペインで、 **[Azure (クラウド キー)]** が選択されていることを確認します。 このオプションが選択されていると、Azure Rights Management サービスによって文書と電子メールが保護されます。 また、 **[アクセス許可の設定]** オプションが選択されていることを確認します。 次に、 **[アクセス許可の追加]** を選択します。

5. **[アクセス許可の追加]** ペインで、 **[\<組織名> の追加 - すべてのメンバー]** を選択します。 たとえば、組織名が VanArsdel Ltd の場合、次のようなオプションが表示されます。
    
    ![すべてのメンバーに Azure Information Protection ラベルの保護アクセス許可を付与する](./media/info-protect-protection-all-members.png) 
    
    このオプションは、アクセス許可を付与できる組織内のすべてのユーザーを自動的に選択します。 ただし、他のオプションでテナントからグループまたはユーザーを検索して参照することができます。 または、 **[詳細の入力]** オプションを選択すると、個別のメール アドレスや、別の組織のすべてのユーザーも指定することができます。

6. アクセス許可に対し、プリセット オプションから **[レビュー担当者]** を選択します。 このアクセス許可レベルが全部のアクセス許可ではなく一部のアクセス許可を自動的に付与することがわかります。
    
    ![共同作成者に Azure Information Protection ラベルの保護アクセス許可を付与する](./media/info-protect-protection-reviewer.png)
    
    **[カスタム]** オプションを使って、異なるアクセス許可レベルを選択したり、個々の使用権限を指定したりできます。 ただし、このチュートリアルでは、 **[レビュー担当者]** オプションのままにします。 後で別のアクセス許可を調べて、指定したユーザーが保護されたドキュメントまたはメールでできることを制限する方法を確認してください。

7. **[OK]** をクリックして **[アクセス許可の追加]** ペインを閉じると、 **[保護]** ペインが構成を反映するように更新されます。 次に例を示します。
    
     ![Azure Information Protection ラベルのアクセス許可構成を示す [保護] ペイン](./media/info-protect-protection-configured.png)
    
    **[アクセス許可の追加]** を選択すると、このアクションによって **[アクセス許可の追加]** ペインが再び開き、さらにユーザーを追加して、別のアクセス許可を付与できます。 たとえば、特定のグループに表示アクセスだけを付与します。 このチュートリアルでは、すべてのユーザーに 1 つのアクセス許可セットのままにします。

8. コンテンツの有効期限とオフライン アクセスを確認して既定値のままにし、 **[OK]** をクリックして保存して、 **[保護]** ペインを閉じます。

8. **[サブラベル]** ペインに戻り、 **[視覚的なマーキングの設定]** セクションを見つけます。
    
    **[このラベルが付いたドキュメントにはフッターをつける]** 設定で、 **[オン]** をクリックし、 **[テキスト]** ボックスに「**Classified as Confidential**」と入力します。 
    
    **[Documents with this label have a watermark]** (このラベルのあるドキュメントに透かしを付ける) 設定では、 **[On]** (オン) をクリックし、 **[Text]** (テキスト) ボックスに組織の名前を入力します。 たとえば、「**VanArsdel, Ltd**」と入力します。 
    
    これらの視覚的なマーカーの外観を変更できますが、ここでは設定は既定値のままにしておきます。
    
9. **[Configure conditions for automatically applying this label]** (このラベルに自動的に適用する条件を構成する) セクションを見つけます。
    
    **[新しい条件の追加]** をクリックし、 **[条件]** ペインで次のように選択します。
    
    」を参照します。 **[条件のタイプを選択]** :既定値の **[情報の種類]** のままにします。
    
    b. **[業種の選択]** :既定値の **[すべて]** のままにします。
    
    c. **[情報の種類を選択]** 検索ボックス:「**クレジット カード番号**」と入力します。 検索結果から **[クレジット カード番号]** を選択します。
    
    d. **[Minimum number of occurrences]\(最小出現回数\)** :既定値の **1** のままにしておきます。
    
    e. **[Count occurrences with unique values only]\(一意の値のみを持つ出現回数のカウント\)** :既定値の **[Off]** (オフ) のままにしておきます。
    
    ![Azure Information Protection チュートリアル - クレジット カードの条件を構成する](./media/step2-configure-condition.png)
    
    **[保存]** をクリックして **[サブラベル]** ペインに戻ります。

10. **[サブラベル]** ペインでは、以下のように、 **[条件名]** に **[クレジット カード番号]** と表示され、 **[出現回数]** に **1** が設定されています。
    
    ![Azure Information Protection チュートリアル - クレジット カード条件の概要](./media/step2-see-condition.png)

11. **[このラベルの適用方法を選択]** :既定値の **[推奨]** のままにします。既定のポリシー ヒントは変更しないでください。 

12. **[管理者向けのメモを追加します]** ボックスに、「**For testing purposes only**」(テスト目的のみ) と入力します。

13. **[サブラベル]** ペインで **[保存]** をクリックします。 確認するメッセージが表示されたら、 **[OK]** をクリックします。 新しいラベルが作成され、保存されますが、まだポリシーには追加されていません。

14. **[分類]**  >  **[ポリシー]** メニュー オプションから: **[グローバル]** をもう一度選択し、ラベルの横にある **[ラベルの追加または削除]** リンクを選択します。

15. **[ポリシー: ラベルの追加または削除]** ペインから、作成したラベルを選択し、 **[財務]** というサブラベルを選択して **[OK]** をクリックします。

16. **[ポリシー: グローバル]** ペインにグローバル ポリシーの新しいサブラベルが表示されます。このサブラベルは、視覚的なマーキングと保護のために構成されています。 次に例を示します。

    ![Azure Information Protection チュートリアル - 新しいサブラベル](./media/info-protect-policy-configuredv2.png)
    
    設定が既定のラベルと理由に関しても構成されていることが確認できます。
    
    ![Azure Information Protection チュートリアル - 設定の構成](./media/info-protect-settings-configuredv2.png)
    

17. **[保存]** をクリックします (この **[ポリシー:グローバル]** ペイン上)。 この操作を確認するメッセージが表示されたら、 **[OK]** をクリックします。

Azure portal を閉じても、または開いたままでこのチュートリアルを完了した後にその他の構成オプションを試してみてもかまいません。

変更の結果を試す準備が整いました。

## <a name="see-classification-labeling-and-protection-in-action"></a>分類、ラベル付け、保護の動作を確認する 

ポリシーに加えた変更と新しく作成したラベルは、Word、Excel、PowerPoint、および Outlook に適用されます。 ただしこのチュートリアルでは、Word を使用してそれらの動作を確認します。 

Word で新しいドキュメントを開きます。 Azure Information Protection クライアントがインストールされているため、次のように表示されます。

![Azure Information Protection チュートリアル - インストールしたクライアント](./media/word2016-calloutsv2.png)

- **[ホーム]** タブの **[保護]** グループと **[保護]** ボタン。
    
    **[保護]**  >  **[ヘルプとフィードバック]** の順にクリックして、 **[Microsoft Azure Information Protection]** ダイアログ ボックスでクライアントのステータスを確認します。 **[接続ユーザー]** とユーザー名が表示されているはずです。 さらに、最終接続日時と Information Protection ポリシーのダウンロード日時も表示されているはずです。 表示されているユーザー名がテナントの正しいものであることを確認します。

- リボンの下の新しい Information Protection バー。 **[秘密度]** というタイトルと、Azure Portal で確認したラベルが表示されます。

### <a name="to-manually-change-our-default-label"></a>既定のラベルを手動で変更するには

1. Information Protection バーの最後のラベルを選択すると、次のように、表示されるサブラベルが示されます。
    
    ![Azure Information Protection チュートリアル - サブラベルを確認する](./media/info-protect-sub-labelsv2.png)

2. これらのサブラベルのいずれかを選択すると、バーには他のラベルは表示されなくなり、このドキュメントに対して選択したラベルが表示されるようになります。 **[秘密度]** の値が変わってラベル名とサブラベル名が表示され、それに応じて、次のようにラベルの色も変わります。 次に例を示します。
    
    ![Azure Information Protection チュートリアル - サブラベルの選択](./media/info-protect-sub-label-selectedv2.png)

3. Information Protection バーで、現在選択しているラベルの値の横にある **[ラベルの編集]** アイコンをクリックします。
    
    ![Azure Information Protection チュートリアル - ラベル アイコンを編集する](./media/info-protect-edit-label-selectedv2.png)
    
    この操作によって、使用できるラベルが再び表示されます。

4. 最初のラベルの **[個人]** を選択します。 このドキュメントに対して、前に選択したラベルよりも低い分類のラベルを選択したため、次のように分類レベルを下げる理由の入力を求められます。
    
    ![Azure Information Protection チュートリアル - レベルを下げる理由の確認要求](./media/info-protect-lower-justification.png)
    
    **[The previous label no longer applies]** (前のラベルが適合しなくなった) を選択して、 **[確認]** をクリックします。 **[秘密度]** の値が **[個人]** に変わり、他のラベルは再び非表示になります。

### <a name="to-remove-the-classification-completely"></a>分類を完全に削除するには

1. Information Protection バーで、 **[ラベルの編集]** アイコンを再度クリックします。 ここでは、いずれかのラベルを選択するのではなく、 **[ラベルの削除]** アイコンをクリックします。
    
    ![Azure Information Protection チュートリアル - アイコンを削除する](./media/delete-icon-from-personalv2.png)
    
2. プロンプトが表示されたら、"このドキュメントでは分類は不要" などと入力し、 **[確認]** をクリックします。  
    
    **[秘密度]** の値が **[未設定]** に変わります。ポリシー設定として既定のラベルを設定していない場合も、最初は新しいドキュメントでこのように表示されます。

### <a name="to-see-a-recommendation-prompt-for-labeling-and-automatic-protection"></a>ラベル付けの推奨プロンプトと自動保護を確認するには

1. Word 文書で、有効なクレジット カード番号 (例:**4242-4242-4242-4242**) を入力します。 

2. 任意のファイル名でローカルにドキュメントを保存します。 

3. クレジット カード番号が検出されたときの保護用に構成したラベルを適用するためのプロンプトが表示されます。 推奨事項に同意しない場合は、ポリシー設定によって、 **[無視]** を選択して拒否できます。 推奨事項を表示するが、ユーザーが設定をオーバーライドできるようにすることは、自動分類を使用する場合の誤検知を削減するのに役立ちます。 このチュートリアルでは、 **[今すぐ変更]** をクリックします。

    ![Azure Information Protection チュートリアル - 推奨プロンプト](./media/change-nowv2.png)

    構成済みのラベルが文書に適用されていることが表示されるようになった (たとえば、**社外秘\財務**) ことに加えて、ページ全体に組織名の透かしが表示され、**社外秘として分類**というフッターも適用されます。 

    また、文書はこのラベルに指定したアクセス許可で保護されます。 文書が保護されていることは、 **[ファイル]** タブをクリックして **[文書の保護]** の情報を見ると確認できます。 文書が**社外秘\財務**およびラベルの説明によって保護されていることがわかります。 
    
    ラベルの保護構成のため、従業員のみが文書を開くことができ、一部のアクションは従業員に対して制限されます。 たとえば、印刷およびコンテンツのコピーと抽出のアクセス許可がないため、文書を印刷したりコピーしたりすることはできません。 このような制限は、データの損失を防ぐのに役立ちます。 ドキュメントの所有者は、ドキュメントを印刷したりコピーしたりできます。 ただし、組織内の他のユーザーに電子メールでドキュメントを送信しても、他のユーザーはこれらの操作を実行できません。

4. もうこのドキュメントを閉じてもかまいません。

## <a name="clean-up-resources"></a>リソースをクリーンアップする

このチュートリアルで行った変更を保持したくない場合は、次の操作を行います。

1. **[分類]**  >  **[ポリシー]**  >  **[グローバル]** を選択して、 **[ポリシー:グローバル]** ペインを開きます。

2. ポリシー設定をメモしておいた元の値に戻した後、 **[保存]** を選択します。 

3. **[分類]**  >  **[ラベル]** メニュー オプションから: **[Azure Information Protection - ラベル]** ペインで、作成した **[財務]** ラベルのコンテキスト メニュー **[...]** を選択します。

4. **[このラベルを削除]** を選択し、確認を求められたら **[OK]** を選択します。

Word を再起動してこれらの変更をダウンロードします。

## <a name="next-steps"></a>次の手順

Azure Information Protection ポリシーの編集について詳しくは、「[Azure Information Protection ポリシーの構成](configure-policy.md)」をご覧ください。

ラベル付けアクティビティのログが記録されている場所について詳しくは、「[Azure Information Protection クライアントの使用状況ログ](./rms-client/client-admin-guide-files-and-logging.md#usage-logging-for-the-azure-information-protection-client)」をご覧ください。

