---
title: Azure Information Protection のポリシー設定を構成する
description: すべてのユーザーとデバイスに適用される Azure Information Protection ポリシーを設定します。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/22/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 629815c0-457d-4697-a4cc-df0e6cc0c1a6
ms.openlocfilehash: f4b79f66bc3f747285b2811327ea158bb83af03d
ms.sourcegitcommit: 94d1c7c795e305444e9fde17ad73e46f242bcfa9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2018
---
# <a name="how-to-configure-the-policy-settings-for-azure-information-protection"></a>Azure Information Protection のポリシー設定を構成する方法

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

>[!NOTE]
> この記事は、グローバル ポリシーまたはスコープ ポリシーからラベルを個別に作成できる、Azure Portal に対する最新の更新を反映しています。 また、ポリシーを公開するオプションは削除されます。 これらの変更に対してテナントがまだ更新されていない場合、たとえば Azure Information Protection に対して **[公開]** オプションがまだ表示され、**[分類]** メニュー オプションが表示されない場合は、数日待ってから以下の手順に戻ってください。

Information Protection バーに表示されるタイトルとヒントのほかに、ラベルから個別に構成できる Azure Information Protection ポリシーにはいくつかの設定があります。

![Azure Information Protection ポリシーのグローバル設定](../media/info-protect-policy-default-settingsv3.png)

Azure Information Protection のサブスクリプションを購入した時期に応じて、ポリシー設定の既定の値が異なることに注意してください。 一部の設定は、[カスタム クライアント設定](../rms-client/client-admin-guide-customizations.md)から設定することもできます。

設定を構成するには:

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、**[Azure Information Protection]** ブレードに移動します。
    
    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. **[分類]** > **[ポリシー]** メニュー オプションから: 構成する設定がすべてのユーザーに適用される場合は、**[Azure Information Protection - ポリシー]** ブレードで **[グローバル]** を選択します。
    
    構成する設定が[スコープ ポリシー](configure-policy-scope.md)にあり、選択したユーザーだけに適用される場合は、代わりにスコープ ポリシーを選びます。

3. **[ポリシー]** ブレードで、設定を構成します。
    
    - **Select the default label** (既定のラベルを選択します): このオプションを設定した場合、ラベルを持たないドキュメントや電子メールに割り当てるラベルを選択します。 サブラベルがあるラベルは、既定値として設定することはできません。 
    
    - **All documents and emails must have a label** (すべてのドキュメントと電子メールにラベルを設定する必要があります): このオプションを **[オン]** に設定した場合は、すべての保存されるドキュメントと送信される電子メールにラベルを適用する必要があります。 ラベル付けは、ユーザーが手動で割り当てる、[条件](configure-policy-classification.md)の結果として自動的に割り当てる、または (**[Select the default label]** (既定のラベルを選択) オプションを設定することで) 既定で割り当てることができます。
        
        ユーザーがドキュメントを保存または電子メールを送信するときにラベルが割り当てられなかった場合は、ラベルの選択を求めるメッセージが表示されます。 次に例を示します。
        
        ![ラベル付けが必須である場合の Azure Information Protection のプロンプト](../media/info-protect-enforce-labelv2.png)
        
    - **分類ラベルを低くする、ラベルを削除する、保護を削除する場合、ユーザーは理由を提供する必要があります**: このオプションが **[オン]** に設定されているときは、ユーザーがこれらの操作を行うと (たとえば **[Public (パブリック)]** ラベルを **[Personal (個人用)]** に変更)、その操作の理由を入力する画面が表示されます。 たとえば、ユーザーは、「このドキュメントにはもう秘密情報が含まれていない」という説明を入力します。 この操作と妥当性の理由は、次のローカルの Windows イベント ログの **[アプリケーションとサービス ログ]**  >  **[Azure Information Protection]** に記録されます。  
        
        ![新しい分類が下位の場合の Azure Information Protection のプロンプト](../media/info-protect-lower-justification.png)
        
        このオプションは、サブラベルには適用されません。
        
    - **For email messages with attachments, apply a label that matches the highest classification of those attachments (添付ファイル付きの電子メール メッセージの場合、添付ファイルの最上位の分類に一致するラベルを適用します)**: このオプションを **[推奨]** に設定すると、ユーザーは自分の電子メール メッセージにラベルを適用するよう求められます。 ラベルは、添付ファイルに適用されている分類のラベルに基づいて動的に選択され、最上位の分類のラベルが選択されます。 添付ファイルは物理ファイルである必要があり、ファイルへのリンク (たとえば、SharePoint または OneDrive for Business 上のファイルへのリンク) はできません。 ユーザーは、推奨設定を受け入れるか、通知を閉じます。 このオプションを **[オン]** に設定すると、ラベルが自動的に適用されますが、ユーザーは電子メールを送信する前に、ラベルを削除することも、別のラベルを選択することもできます。  
    
    - **Display the Information Protection bar in Office apps (Office アプリで Information Protection バーを表示する)**: この設定をオフにすると、ユーザーは Word、Excel、PowerPoint、Outlook のバーからラベルを選択できません。 代わりに、リボンの **[保護]** ボタンからラベルを選択する必要があります。 この設定をオンにすると、ユーザーはバーまたはボタンのいずれかからラベルを選択できます。
        
        この設定をオンにしているときに、ユーザーがバーを表示しないことを選択する場合、[Azure Information Protection バーを永久に非表示](../rms-client/client-admin-guide-customizations.md#permanently-hide-the-azure-information-protection-bar)にできるように、この設定をクライアントの詳細設定と共に使用できます。 **[保護]** ボタンから **[バーの表示]** オプションをクリアして、この操作を行うことができます。
    
    - **Add the Do Not Forward button to the Outlook ribbon (Outlook リボンに [転送不可] ボタンを追加する)**: この設定をオンにすると、ユーザーは Outlook メニューから **[転送不可]** オプションを選択できるほか、Outlook リボンの **[保護]** グループからもこのボタンを選択できます。 ユーザーがメールを分類および保護できるようにするには、このボタンを追加しないことをお勧めします。ただし、代わりに Outlook に[保護のラベル](configure-policy-protection.md)とユーザー定義のアクセス許可を構成できます。 この保護設定は、**[転送不可]** ボタンの選択と同様に機能しますが、この機能にラベルが含まれる場合は、メールは分類され、保護されます。
    
        このポリシー設定は、[クライアントのカスタマイズ](../rms-client/client-admin-guide-customizations.md#hide-or-show-the-do-not-forward-button-in-outlook)としてクライアントの詳細設定を使って構成することもできます。
    
    - **Make the custom permissions option available to users (ユーザーがカスタム アクセス許可オプションを使用できるようにする)**: この設定をオンにすると、ユーザーは独自の保護設定を設定したり、ラベルの構成で指定している可能性がある保護設定を上書きしたりすることができます。 この設定をオフにすると、カスタムのアクセス許可オプションをユーザーが選択することはできません。
        
        このポリシー設定は、ユーザーが Office メニュー オプションから構成できるカスタムのアクセス許可には影響しないことに注意してください。 ただし、[クライアントのカスタマイズ](../rms-client/client-admin-guide-customizations.md#make-the-custom-permissions-options-available-or-unavailable-to-users)としてクライアントの詳細設定を使用し、構成することもできます。
        
        カスタムのアクセス許可オプションは、次の場所に配置されています。
        
        - Office アプリケーション: リボンから **[ホーム]** タブ > **[保護]** グループ > **[保護]**  >  **[カスタムのアクセス許可]**
        
        - エクスプローラー: 右クリック > **[分類して保護する]** > **[カスタムのアクセス許可]**
    
    - **Provide a custom URL for the Azure Information Protection client "Tell me more" web page (Azure Information Protection クライアントの "詳細情報を表示する" Web ページのカスタム URL を入力する)**: このリンクは、**[Microsoft Azure Information Protection]** ダイアログ ボックスの **[ヘルプとフィードバック]** セクションにあり、ユーザーが Office アプリケーションの **[ホーム]** タブで **[保護]**  >  **[ヘルプとフィードバック]** を選択したときに表示されます。 このリンクの既定のリンク先は [Azure Information Protection](https://www.microsoft.com/cloud-platform/azure-information-protection) Web サイトです。 このリンクをクリックしたときに別の Web ページが表示されるようにするには、HTTP または HTTPS (推奨) の URL を入力します。 入力されたカスタム URL がどのデバイスでもアクセス可能で正しく表示できるかどうかの確認は行われません。
        
        たとえば、ヘルプ デスクの場合、クライアントのインストールおよび使用に関する情報 (**https://docs.microsoft.com/information-protection/rms-client/info-protect-client**)、またはリリース バージョン情報 (**https://docs.microsoft.com/information-protection/rms-client/client-version-release-history**) が含まれる Microsoft ドキュメント ページを入力することが考えられます。 あるいは、ユーザー向けの Web ページを独自に作成して、ヘルプ デスクへの連絡方法を掲載したり、ラベルを使用する手順をユーザーに説明するビデオを公開したりすることが考えられます。

3. 変更を保存し、ユーザーが利用できるようにするには、**[保存]** をクリックします。

**[保存]** をクリックすると、変更内容がユーザーとサービスに対して自動的に利用可能になります。 独立した公開オプションはなくなりました。

## <a name="next-steps"></a>次の手順

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
