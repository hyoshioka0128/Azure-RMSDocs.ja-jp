---
title: Azure Information Protection のポリシー設定を構成する - AIP
description: すべてのユーザーとデバイスに適用される Azure Information Protection ポリシーを設定します。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/16/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 8a04682a796ceb4305a98bfcbce2266a5fbd834b
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "95570455"
---
# <a name="how-to-configure-the-policy-settings-for-azure-information-protection"></a>Azure Information Protection のポリシー設定を構成する方法

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
> *手順:[Windows 用 Azure Information Protection クライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と **ラベル管理** は、**2021 年 3 月 31 日** で **非推奨** になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

> [!NOTE]
> これらの手順は、Azure Information Protection の統合ラベル付けクライアントではなく、Azure Information Protection クライアント (クラシック) に適用されます。 これらのクライアントの違いがわからない場合は、 こちらの [FAQ](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients) を参照してください。
> 
> 統一されたラベル付けクライアントのポリシー設定を構成するための情報を探している場合は、Microsoft 365 の準拠に関するドキュメントを参照してください。 たとえば、「[機密ラベルについて](/microsoft-365/compliance/sensitivity-labels)」です。

Information Protection バーに表示されるタイトルとヒントのほかに、ラベルから個別に構成できる Azure Information Protection ポリシーにはいくつかの設定があります。

![Azure Information Protection ポリシーのグローバル設定](./media/defaultsettings-aip.png)

Azure Information Protection のサブスクリプションを購入した時期に応じて、ポリシー設定の既定の値が異なることに注意してください。 一部の設定は、[カスタム クライアント設定](./rms-client/client-admin-guide-customizations.md)から設定することもできます。

## <a name="to-configure-the-policy-settings"></a>ポリシー設定を構成するには

1. まだ実行していない場合は、新しいブラウザー ウィンドウを開いて、[Azure Portal にサインインします](configure-policy.md#signing-in-to-the-azure-portal)。 次に、 **[Azure Information Protection]** ペインに移動します。
    
    たとえば、リソース、サービス、ドキュメントの検索ボックスで次のようにします: 「**Information**」と入力し、 **[Azure Information Protection]** を選択します。

2. [**分類**  >  **ポリシー** ] メニューオプションから: [ **Azure Information Protection-ポリシー** ] ウィンドウで、構成する設定がすべてのユーザーに適用される場合は [**グローバル**] を選択します。
    
    構成する設定が[スコープ ポリシー](configure-policy-scope.md)にあり、選択したユーザーだけに適用される場合は、代わりにスコープ ポリシーを選びます。

3. [ **ポリシー** ] ウィンドウで、次の設定を構成します。
    
   - **Select the default label** (既定のラベルを選択します): このオプションを設定した場合、ラベルを持たないドキュメントや電子メールに割り当てるラベルを選択します。 サブラベルがあるラベルは、既定値として設定することはできません。
        
        この設定は、Office アプリとスキャナーに適用されます。 これはエクスプローラーや PowerShell には適用されません。
    
    - **Azure Information Protection analytics に監査データを送信** する: azure [Information Analytics](reports-aip.md)用の azure Log Analytics ワークスペースを作成する前に、この設定の値は [ **オフ** ] になっており、構成されて **いません**。 ワークスペースを作成すると、値が **[オフ]** および **[オン]** に変わります。
        
        この設定を **オン** にすると、中央レポートをサポートするクライアントは、Azure Information Protection サービスにデータを送信します。 この情報には、どのラベルが適用されるか、ユーザーが下位の分類でラベルを選択したとき、またはラベルを削除したときの情報が含まれます。 送信および格納される情報の詳細については、中央レポートのドキュメントの「 [収集して Microsoft に送信する](reports-aip.md#information-collected-and-sent-to-microsoft) 情報」セクションを参照してください。 このデータが送信されないようにするには、このポリシー設定を **Off** に設定します。
    
    - **All documents and emails must have a label** (すべてのドキュメントと電子メールにラベルを設定する必要があります): このオプションを **[オン]** に設定した場合は、すべての保存されるドキュメントと送信される電子メールにラベルを適用する必要があります。 ラベル付けは、ユーザーが手動で割り当てる、[条件](configure-policy-classification.md)の結果として自動的に割り当てる、または (**[Select the default label]** (既定のラベルを選択) オプションを設定することで) 既定で割り当てることができます。
        
       ユーザーがドキュメントを保存または電子メールを送信するときにラベルが割り当てられなかった場合は、ラベルの選択を求めるメッセージが表示されます。 例:
        
       ![ラベル付けが必須である場合の Azure Information Protection のプロンプト](./media/info-protect-enforce-labelv2.png)
        
       [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel)PowerShell コマンドレットと *RemoveLabel* パラメーターを使用してラベルを削除する場合、このオプションは適用されません。
        
   - **分類ラベルを低くする、ラベルを削除する、保護を削除する場合、ユーザーは理由を提供する必要があります**: このオプションが **[オン]** に設定されているときは、ユーザーがこれらの操作を行うと (たとえば **[Public (パブリック)]** ラベルを **[Personal (個人用)]** に変更)、その操作の理由を入力する画面が表示されます。 たとえば、ユーザーは、「このドキュメントにはもう秘密情報が含まれていない」という説明を入力します。 アクションとその理由は、ローカルの Windows イベントログの [**アプリケーションとサービスログ**] Azure Information Protection に記録され  >  **Azure Information Protection** ます。  
        
       ![新しい分類が下位の場合の Azure Information Protection のプロンプト](./media/info-protect-lower-justification.png)
        
       このオプションは、同じ親ラベル下のサブラベルの分類を低くするためには使用できません。
        
   - **For email messages with attachments, apply a label that matches the highest classification of those attachments (添付ファイル付きの電子メール メッセージの場合、添付ファイルの最上位の分類に一致するラベルを適用します)**: このオプションを **[推奨]** に設定すると、ユーザーは自分の電子メール メッセージにラベルを適用するよう求められます。 ラベルは、添付ファイルに適用されている分類のラベルに基づいて動的に選択され、最上位の分類のラベルが選択されます。 添付ファイルは物理ファイルである必要があり、ファイルへのリンク (たとえば、Microsoft SharePoint または OneDrive 上のファイルへのリンク) を指定することはできません。 ユーザーは、推奨設定を受け入れるか、通知を閉じます。 このオプションを **[自動]** に設定すると、ラベルが自動的に適用されますが、ユーザーは電子メールを送信する前に、ラベルを削除することも、別のラベルを選択することもできます。
        
        このポリシー設定を使う際にサブラベルの順序を考慮する場合は、[クライアントの詳細設定を構成する](./rms-client/client-admin-guide-customizations.md#enable-order-support-for-sublabels-on-attachments)必要があります。
        
        最上位の分類ラベルを持つ添付ファイルが、ユーザー定義のアクセス許可のプレビュー設定を使用して保護するように構成されている場合:-ラベルのユーザー定義のアクセス許可に Outlook (転送不可) が含まれている場合、そのラベルが適用され、電子メールに転送防止が適用されません。 ラベルのユーザー定義のアクセス許可が Word、Excel、PowerPoint、およびファイル エクスプローラーのみを対象とする場合、そのラベルは電子メールに適用されず、保護も適用されません。
    
   - **Display the Information Protection bar in Office apps (Office アプリで Information Protection バーを表示する)**: この設定をオフにすると、ユーザーは Word、Excel、PowerPoint、Outlook のバーからラベルを選択できません。 代わりに、リボンの **[保護]** ボタンからラベルを選択する必要があります。 この設定をオンにすると、ユーザーはバーまたはボタンのいずれかからラベルを選択できます。
        
       この設定をオンにしているときに、ユーザーがバーを表示しないことを選択する場合、[Azure Information Protection バーを永久に非表示](./rms-client/client-admin-guide-customizations.md#permanently-hide-the-azure-information-protection-bar)にできるように、この設定をクライアントの詳細設定と共に使用できます。 **[保護]** ボタンから **[バーの表示]** オプションをクリアして、この操作を行うことができます。
    
   - **Add the Do Not Forward button to the Outlook ribbon (Outlook リボンに [転送不可] ボタンを追加する)**: この設定をオンにすると、ユーザーは Outlook メニューから **[転送不可]** オプションを選択できるほか、Outlook リボンの **[保護]** グループからもこのボタンを選択できます。 ユーザーが電子メールを分類して保護できるようにするには、このボタンを追加するのではなく、 [保護用にラベルを構成](configure-policy-protection.md) し、ユーザーに Outlook のアクセス許可を定義することをお勧めします。 この保護設定は、**[転送不可]** ボタンの選択と同様に機能しますが、この機能にラベルが含まれる場合は、メールは分類され、保護されます。
    
       このポリシー設定は、[クライアントのカスタマイズ](./rms-client/client-admin-guide-customizations.md#hide-or-show-the-do-not-forward-button-in-outlook)としてクライアントの詳細設定を使って構成することもできます。
    
   - **Make the custom permissions option available to users \(ユーザーがカスタム アクセス許可オプションを使用できるようにする\)**: この設定をオンにすると、ラベルの構成で指定している可能性がある保護設定をオーバーライドできる、独自の保護設定を設定するオプションがユーザーに表示されます。 ユーザーには、保護を削除するオプションも表示されます。 この設定がオフの場合、これらのオプションはユーザーに表示されません。
        
       このポリシー設定は、ユーザーが Office メニュー オプションから構成できるカスタムのアクセス許可には影響しないことに注意してください。 ただし、[クライアントのカスタマイズ](./rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users)としてクライアントの詳細設定を使用し、構成することもできます。
        
       カスタムのアクセス許可オプションは、次の場所に配置されています。
        
       - Office アプリケーション: リボンから **[ホーム]** タブ > **[保護]** グループ > **[保護]** > **[カスタムのアクセス許可]**
        
       - エクスプローラーから: > 右クリックし **て、**  >  **カスタムアクセス許可** を分類して保護する
    
   - **Provide a custom URL for the Azure Information Protection client "Tell me more" web page (Azure Information Protection クライアントの "詳細情報を表示する" Web ページのカスタム URL を入力する)**: このリンクは、**[Microsoft Azure Information Protection]** ダイアログ ボックスの **[ヘルプとフィードバック]** セクションにあり、ユーザーが Office アプリケーションの **[ホーム]** タブで **[保護]** > **[ヘルプとフィードバック]** を選択したときに表示されます。 このリンクの既定のリンク先は [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) Web サイトです。 このリンクをクリックしたときに別の Web ページが表示されるようにするには、HTTP または HTTPS (推奨) の URL を入力します。 入力されたカスタム URL がどのデバイスでもアクセス可能で正しく表示できるかどうかの確認は行われません。
        
       たとえば、ヘルプデスクの場合、クライアントのインストールと使用に関する情報が記載された Microsoft のドキュメントページを参照してください `https://docs.microsoft.com/information-protection/rms-client/info-protect-client` 。 またはリリースバージョン情報: `https://docs.microsoft.com/information-protection/rms-client/client-version-release-history` 。 あるいは、ユーザー向けの Web ページを独自に作成して、ヘルプ デスクへの連絡方法を掲載したり、ラベルを使用する手順をユーザーに説明するビデオを公開したりすることが考えられます。

4. 変更を保存し、ユーザーが利用できるようにするには、**[保存]** をクリックします。

**[保存]** をクリックすると、変更内容がユーザーとサービスに対して自動的に利用可能になります。 独立した公開オプションはなくなりました。

## <a name="next-steps"></a>次のステップ

このような一部のポリシー設定を連携させる方法を確認するには、チュートリアル「[Configure Azure Information Protection policy settings that work together (連携させる Azure Information Protection のポリシー設定を構成する)](infoprotect-settings-tutorial.md)」をご覧ください。

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。