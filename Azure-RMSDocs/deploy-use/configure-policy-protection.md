---
title: "Azure Information Protection ラベルを保護するように構成する"
description: "Rights Management 保護を使用するようにラベルを構成すると、最も機密性の高いドキュメントや電子メールを保護できます。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/05/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
ms.openlocfilehash: f5c4e2f7513832a884820ec0c57c7da2dec5f04e
ms.sourcegitcommit: 8b768e7e249e124f24acdf630d165eaf743f9c21
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/05/2017
---
# Rights Management による保護でラベルを構成する方法
<a id="how-to-configure-a-label-for-rights-management-protection" class="xliff"></a>

>*適用対象: Azure Information Protection*

暗号化ポリシー、ID ポリシー、および承認ポリシーによってデータ損失を防止する Rights Management サービスを使用することで、最も機密性の高いドキュメントや電子メールを保護することができます。 この保護は、ドキュメントおよび電子メールの Rights Management テンプレートを使用するようにラベルを構成した場合、または Outlook の電子メール メッセージの **[転送不可]** オプションに適用されます。 

テンプレートは、Azure Rights Management をアクティブ化したときに自動的に作成される既定のいずれかのテンプレート、またはカスタム テンプレートのどちらも使用できます。 Azure Rights Management の部門別テンプレートはサポートされていますが、保護は、ドキュメントまたは電子メールの作成者がテンプレートの構成範囲内にある場合にのみ適用されます。 ユーザーがその範囲外である場合は、Azure Information Protection でラベルを適用できないことを示すメッセージが表示されます。

## 保護のしくみ
<a id="how-the-protection-works" class="xliff"></a>

Rights Management によって保護されるドキュメントまたは電子メールは、保存時および送信時に暗号化され、権限のあるユーザーのみが暗号化を解除できます。 この暗号化は、ドキュメントまたは電子メールの名前が変更された場合でも維持されます。 さらに、次の例のように、使用権限と制限を構成できます。

- 組織内のユーザーのみが社外秘のドキュメントまたは電子メールを開くことができます。

- マーケティング部門のユーザーのみが宣伝の通知ドキュメントまたは電子メールの編集と印刷を実行でき、組織内の他のすべてのユーザーはそれらの閲覧のみを実行できます。

- ユーザーは、社内の再編成に関するニュースを含む電子メールを転送したり、電子メールの情報をコピーしたりすることはできません。

- ビジネス パートナーに送信される現在の価格表は、指定日以降は開くことができません。

Azure Rights Management テンプレートとこのテンプレートを Azure クラシック ポータルで構成する方法の詳細については、「[Azure Rights Management サービスのカスタム テンプレートを構成する](../deploy-use/configure-custom-templates.md)」をご覧ください。

Azure Rights Management とそのしくみの詳細については、[Azure Rights Management の概要に関するページ](../understand-explore/what-is-azure-rms.md)を参照してください。

> [!IMPORTANT]
> Azure Rights Management による保護を適用するようにラベルを構成するには、組織に対して Azure Rights Management サービスをアクティブにする必要があります。 この手順をまだ行っていない場合は、「[Rights Management をアクティブにする](../deploy-use/activate-service.md)」を参照してください。

ユーザーが電子メールを保護するラベルを Outlook で適用するために、Information Rights Management (IRM) 用に Exchange を構成する必要はありません。 ただし、Exchange が IRM 用に構成されるまで、Exchange で Azure Rights Management による保護を使用するすべての機能を利用できません。 たとえば、ユーザーは保護された電子メールを携帯電話や Web 上の Outlook で表示できなくなります。また、保護された電子メールには検索のインデックスを作成できません。権限管理の保護のために Exchange Online DLP も構成できなくなります。 このような追加のシナリオをサポートするように Exchange を構成するには、以下のリソースを参照してください。

- Exchange Online の場合: 「[Exchange Online: IRM 構成](../deploy-use/configure-office365.md#exchange-online-irm-configuration)」の手順を参照してください。

- オンプレミスの Exchange の場合: [RMS コネクタを展開し、Exchange サーバーを構成する](../deploy-use/deploy-rms-connector.md)必要があります。 


## Rights Management による保護にラベルを構成するには
<a id="to-configure-a-label-for-rights-management-protection" class="xliff"></a>

1. [Azure Portal](https://portal.azure.com) にサインインしていない場合は新しいブラウザーのウィンドウを開き、セキュリティ管理者または全体管理者としてサインインし、**[Azure Information Protection]** ブレードに移動します。 

    たとえば、ハブ メニューで **[その他のサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. 構成するラベルがすべてのユーザーに適用される場合は、**[Azure Information Protection]** ブレードから **[Global]** (全体) を選択します。 ただし、構成するラベルが[スコープ ポリシー](configure-policy-scope.md)内にあり、選択したユーザーだけに適用される場合は、代わりにそのスコープ ポリシーを選択します。

3. **[ポリシー]** ブレードで、構成するラベルを選択すると、**[ラベル]** ブレードが開きます。 

4. **[ラベル]** ブレードで、**[Set permissions for documents and emails containing this label]** (このラベルを含むドキュメントと電子メールにアクセス許可を設定する) を見つけ、下記オプションから 1 つ選択します。
    
    - **[未構成]**: 現在、ラベルが保護を適用するように構成されており、選択したラベルにこれ以上保護を適用しない場合は、このオプションを選択します。 次に手順 11 に進みます。
    
    - **[保護]**: 保護を適用するには、このオプションを選択し、手順 5. に進みます。
    
    - **[保護の削除]**: ドキュメントまたは電子メールに構成されている保護を削除するには、このオプションを選択します。 次に手順 11 に進みます。
        
        このオプションを持つラベルを適用するには、ユーザーは Rights Management による保護を削除する権限を持っている必要があるので、注意してください。 このオプションを使用するには、ユーザーは **[エクスポート]** または **[フル コントロール]** [usage right (使用権限)](../deploy-use/configure-usage-rights.md)を持っている、Rights Management の所有者 (自動的にフル コントロール使用権限が付与されています) である、または [super user for Azure Rights Management (Azure Rights Management のスーパー ユーザー)](../deploy-use/configure-super-users.md) である必要があります。 既定の Azure Rights Management テンプレートには、ユーザーに保護を削除させる使用権限は含まれません。 
        
        ユーザーが Rights Management による保護を削除する権限を持たずに **[保護の削除]** オプションを持つラベルを選択する場合、次のメッセージが表示されます: **Azure Information Protection ではこのラベルを適用できません。この問題が引き続き発生する場合は、管理者に問い合わせてください。**

5. **[保護]** を選択した場合、次のように **[保護]** を選択して **[保護]** ブレードを開きます。
    
    ![Azure Information Protection ラベルの保護を構成する](../media/info-protect-protection-bar.png)

6. **[保護]** ブレードで、**[Azure RMS]** または **[HYOK (AD RMS)]** を選択します。 
    
    ほとんどの場合、アクセス許可の設定には **[Azure RMS]** を選択します。 この "*Hold Your Own Key*" (HYOK) 構成に付随する前提条件と制限事項を読み、理解するまでは **[HYOK (AD RMS)]** を選択しないでください。 詳細については、「[AD RMS 保護の Hold Your Own Key (HYOK) の要件と制限事項](configure-adrms-restrictions.md)」を参照してください。 HYOK (AD RMS) の構成を続行するには、手順 10 に進みます。
    
7. 次のいずれかのオプションを選択します。
    
    - **[転送不可]**: 電子メールの場合はこの Outlook オプションを設定します。
    
    - **[定義済みのテンプレートを選択する]**: 既定のテンプレートのいずれかまたは構成したカスタム テンプレートを使用します。
    
    - **[Set permissions (Preview)]\(アクセス許可を設定 (プレビュー)\)**: このポータルで新しい保護設定を定義します。

8. **[Azure RMS]** で **[Select a predefined template (定義済みテンプレートの選択)]** を選択した場合、ドロップ ダウン ボックスをクリックし、このラベルでドキュメントと電子メールを保護するために使用する[テンプレート](../deploy-use/configure-custom-templates.md)を選択します。
    
    **[部門別テンプレート]**を選択する場合、または[オンボーディング コントロール](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment)を構成済みの場合:
    
    - 構成されたテンプレート範囲の外にいるユーザー、または Azure Rights Management 保護の適用から除外されているユーザーは、引き続きラベルを確認できますが、適用することはできません。 それらのユーザーがラベルを選択した場合、次のメッセージが表示されます: **Azure Information Protection はこのラベルを適用できません。この問題が引き続き発生する場合は、管理者に問い合わせてください。**
    
        スコープ ポリシーを構成する場合でも、すべてのテンプレートが常に表示されることに注意してください。 たとえば、マーケティング グループのスコープ ポリシーを構成しているとします。 選択可能な Azure RMS テンプレートは、マーケティング グループにスコープされたテンプレートに制限されることはなく、選択されたユーザーが使用できない部門別のテンプレートを選択することが可能です。 構成を簡単にしてトラブルシューティングを最小限に抑えるために、部門別テンプレートの名前がスコープ ポリシーのラベルに一致するように名前を付けることを考慮してください。 
            
9. **[Azure RMS]** で **[Set permissions (Preview)]\(アクセス許可を設定 (プレビュー)\)** を選択した場合、このオプションには Azure クラシック ポータルで構成できる[カスタム テンプレート](configure-custom-templates.md)の構成オプションのほとんどが含まれています。 さらに、組織からあらゆるユーザーを簡単に追加したり、個々のユーザーまたはグループに、あるいはドメイン名を指定するときは別の組織のすべてのユーザーに、外部メール アドレスを指定したりできます。 
    
    このプレビュー構成の詳細については、「[Azure Information Protection unified administration now in Preview](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/26/azure-information-protection-unified-administration-now-in-preview/)」 (Azure 情報保護統合管理のプレビューが公開されました) というブログ投稿を参照してください。 
    
    選択できるアクセス許可の詳細については、「[Azure Rights Management の使用権限を構成する](configure-usage-rights.md)」を参照してください。
    
    **[Set permissions (Preview)]\(アクセス許可を設定 (プレビュー)\)** オプションに含まれる、次の設定を変更するかどうかを確認します。 アクセス許可と同様に、これらの設定は、[Rights Management の発行者や Rights Management の所有者](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner)、管理者によって割り当てられた[スーパー ユーザー](configure-super-users.md)には適用されません。
    
    |Setting|詳細情報|推奨される設定
    |-----------|--------------------|--------------------|
    |**[コンテンツの有効期限]**|このテンプレートによって保護されているドキュメントまたは電子メールを、選択したユーザーが開けなくなる日付またはそれまでの日数を定義します。 日付を指定するか、保護がコンテンツに適用された時点からの日数を指定できます。<br /><br />日付を指定する場合は、現在のタイム ゾーンの午前 0 時から有効になります。|**[コンテンツには有効期限がありません]** (コンテンツに期限付きの特定の要件が含まれる場合を除く)。|
    |**[オフライン アクセスの許可]**|この設定を使用すると、選択されたユーザーはインターネットに接続していないときに保護されたコンテンツを開くことができるため、セキュリティ要件 (失効後のアクセスを含む) のバランスを取ることができます。<br /><br />インターネットに接続されていないときにコンテンツを使用できないように指定するか、コンテンツが指定された日数のみ利用できるように指定した場合、そのしきい値に達すると、ユーザーは再認証される必要があり、アクセスがログに記録されます。 この場合、ユーザーの資格情報がキャッシュされていない場合、ユーザーはドキュメントまたは電子メールを開く前にサインインするように要求されます。<br /><br />再認証に加えて、ポリシーおよびユーザー グループのメンバーシップが再評価されます。 つまり、ユーザーが最後にコンテンツにアクセスした後にポリシーまたはグループ メンバーシップが変更された場合、ユーザーが同じドキュメントまたは電子メールにアクセスしたときに異なる結果になる可能性があります。 これには、ドキュメントが[失効](../rms-client/client-track-revoke.md)された場合にアクセスできないことも含まれます。|コンテンツの重要度に応じて次のように設定します。<br /><br />- **[インターネットに接続せずにコンテンツを利用できる日数]** = **7** (不正ユーザーの手に渡った場合にビジネス上の損失を招く可能性がある機密性の高いビジネス データ)。 この推奨設定では、柔軟性とセキュリティのバランスを取ることができます。 例としては、契約書、セキュリティ レポート、予測の概要、および販売取引データなどがあります。<br /><br />- **[Never\(常に不可\)]** (承認されていない人と共有した場合、ビジネスに損害を与える可能性のある非常に機密性の高いビジネス データ)。 この推奨では柔軟性よりもセキュリティが優先され、ドキュメントが失効されると、承認されたすべてのユーザーが直ちにそのドキュメントを開けなくなります。 例としては、従業員と顧客の情報、パスワード、ソース コード、および発表前の財務レポートなどがあります。|
    
    この設定のグループ化により、Azure Rights Management サービスのカスタム テンプレートが作成されます。 これらのテンプレートは、Azure Rights Management に統合されたアプリケーションとサービスで使用できます。 コンピューターとサービスがテンプレートをダウンロードおよび更新する方法の詳細については、「[ユーザー用のテンプレートの更新](refresh-templates.md)」をご覧ください。

10. **[HYOK (AD RMS)]** で **[テンプレートの選択]** を選択した場合: AD RMS クラスターのテンプレート GUID とライセンス URL を指定します。 [詳細情報](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label)

11. **[OK]** をクリックして **[保護]** ブレードを閉じ、選択した **[転送不可]** または選択したテンプレートが **[ラベル]** ブレードの **[保護]** オプションに表示されていることを確認します。

12. **[ラベル]** ブレードで、**[保存]** をクリックします。

13. ユーザーが変更を使用できるようにするには、**[Azure Information Protection]** ブレードで **[公開]** をクリックします。

## 次のステップ
<a id="next-steps" class="xliff"></a>

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]