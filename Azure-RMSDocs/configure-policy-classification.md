---
title: Azure Information Protection ラベルの条件を構成する - AIP
description: ラベルの条件を使うと、ドキュメントや電子メールにラベルを自動的に割り当てることができます。 または、推奨するラベルを選択するようユーザーに求めることができます。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 09/16/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
ROBOTS: NOINDEX
ms.subservice: aiplabels
ms.custom: admin
ms.openlocfilehash: 77dd8f891e99b314d2fa50aada52e1ac8f99f47d
ms.sourcegitcommit: b32c16e41ba36167b5a3058b56a73183bdd4306d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/29/2020
ms.locfileid: "97806840"
---
# <a name="how-to-configure-conditions-for-automatic-and-recommended-classification-for-azure-information-protection"></a>Azure Information Protection 用の自動および推奨分類の条件を構成する方法

>***適用対象**:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*
>
>***関連**: [Windows 用のクラシッククライアント Azure Information Protection](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)ます。 統一されたラベル付けクライアントについては、「秘密度ラベル[の暗号化を使用してコンテンツへのアクセスを制限](/microsoft-365/compliance/encryption-sensitivity-labels)する[」および「](/microsoft-365/compliance/sensitivity-labels) Microsoft 365 のドキュメントから[自動的にコンテンツに機密ラベルを適用](/microsoft-365/compliance/apply-sensitivity-label-automatically)する」を参照してください。

> [!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure Portal の **Azure Information Protection のクラシック クライアント** と **ラベル管理** は、**2021 年 3 月 31 日** をもって **非推奨** になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。
>

ラベルの条件を構成するときに、ドキュメントまたは電子メールにラベルを自動的に割り当てることができます。 または、自分が推奨するラベルを選択するようにユーザーに求めることもできます。 

これらの条件を構成するときには、**クレジット カード番号** や **米国社会保障番号 (SSN)** などの定義済みのパターンを使用できます。 または、自動分類の条件として、ユーザー指定の文字列またはパターンを定義することもできます。 これらの条件は、ドキュメントや電子メールの本文とヘッダーおよびフッターに適用されます。 条件の詳細については、[次の手順](#to-configure-recommended-or-automatic-classification-for-a-label)の手順 5 をご覧ください。

最良のユーザー エクスペリエンスとビジネスの継続性を確保するために、自動分類ではなく、ユーザーが推奨する分類から始めることをお勧めします。 この構成の場合、ユーザーは、分類や関連付けられている保護を受け入れるか、それらの提案が自分のドキュメントまたは電子メール メッセージに適していない場合はオーバーライドすることを選択できます。

ラベルを推奨される操作として適用するように条件を構成したときのプロンプトの例を、カスタム ポリシー ヒントと共に示します。

![Azure Information Protection の検出と推奨事項](./media/info-protect-recommend-calloutsv2.png)

この例では、ユーザーは **[今すぐ変更]** をクリックして推奨されたラベルを適用するか、**[閉じる]** を選択することでその推奨をオーバーライドできます。 ユーザーが推奨を無視することを選択しても、ドキュメントを次に開いたときに条件がまだ適用される場合は、ラベルの推奨がもう一度表示されます。

推奨されている分類ではなく自動分類を構成した場合、ラベルは自動的に適用され、ユーザーには Word、Excel、PowerPoint 内に引き続き通知が表示されます。 ただし、[ **今すぐ変更** ] と [ **無視** ] ボタンは **[OK]** に置き換えられます。 Outlook では、自動分類の場合に通知は表示されず、電子メールの送信時にラベルが適用されます。

> [!IMPORTANT]
>自動分類とユーザー定義のアクセス許可にはラベルを構成しないでください。 ユーザー定義のアクセス許可オプションは、アクセス許可を与える人をユーザーが指定できるという[保護設定](configure-policy-protection.md)となります。
>
>自動分類とユーザー定義のアクセス許可にラベルを構成すると、条件に対してコンテンツがチェックされ、ユーザー定義のアクセス許可設定は適用されません。 推奨されている分類とユーザー定義のアクセス許可を使用できます。

## <a name="how-automatic-or-recommended-labels-are-applied"></a>自動ラベルと推奨ラベルが適用されるしくみ

- 自動分類は、ドキュメントを保存するときに Word、Excel、PowerPoint に適用され、電子メールの送信時に Outlook に適用されます。 
    
    以前に手動でラベル付けされていた、またはより高度な分類で自動的にラベル付けされていたドキュメントやメールに対しては、自動分類を使用することはできません。 

- 推奨分類は、ドキュメントを保存するときに Word、Excel、および PowerPoint に適用されます。 現在プレビュー段階にある[高度なクライアント設定](./rms-client/client-admin-guide-customizations.md#enable-recommended-classification-in-outlook)を構成しない限り、推奨分類を Outlook に使用することはできません。
    
    以前に上位の分類でラベルが付けられているドキュメントには推奨分類を使用できません。 

ドキュメントに指定された条件規則が Azure Information Protection クライアントによって定期的にチェックされるように、この動作を変更できます。 たとえば、Microsoft SharePoint、OneDrive for work または学校に自動的に保存される Office アプリで [自動](https://support.office.com/article/what-is-autosave-6d6bd723-ebfd-4e40-b5f6-ae6e8088f7a5) 保存を使用する場合、または onedrive for home を使用する場合に適しています。 このシナリオをサポートするには、現在プレビューの段階にある [アドバンストクライアント設定](./rms-client/client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background) を構成できます。 この設定により、分類がバックグラウンドで継続的に実行されるようになります。

### <a name="how-multiple-conditions-are-evaluated-when-they-apply-to-more-than-one-label"></a>複数のラベルに適用するときの複数の条件の評価方法

1. ラベルは、ポリシーに指定した位置に従って評価の順序が決まります。先頭に配置されたラベルが最下位 (秘密度が最も低い) になり、最後に配置されたラベルが最上位 (秘密度が最も高い) ものになります。

2. 最も秘密度の高いラベルが適用されます。
 
3. 最後のサブラベルが適用されます。


## <a name="to-configure-recommended-or-automatic-classification-for-a-label"></a>ラベルの推奨または自動分類を構成するには

1. まだ実行していない場合は、新しいブラウザー ウィンドウを開いて、[Azure Portal にサインインします](configure-policy.md#signing-in-to-the-azure-portal)。 次に、 **[Azure Information Protection]** ペインに移動します。 
    
    たとえば、リソース、サービス、ドキュメントの検索ボックスで次のようにします: 「**Information**」と入力し、 **[Azure Information Protection]** を選択します。

2. [**分類**  >  **ラベル**] メニューオプションから: [ **Azure Information Protection ラベル**] ウィンドウで、構成するラベルを選択します。

3. [ **ラベル** ] ウィンドウの [ **このラベルを自動的に適用するための条件を構成** します] セクションで、[ **新しい条件の追加**] をクリックします。

4. [ **条件** ] ペインで、定義済みの条件を使用する場合は [ **情報の種類** ] を、独自の条件を指定する場合は [ **カスタム** ] を選択します。
    - **[情報の種類]** を選択した場合: 使用可能な条件の一覧から選択し、最小出現回数と、出現で出現回数に一意の値を含めるかどうかを選択します。
        
        この情報の種類は、Microsoft 365 データ損失防止 (DLP) の機密情報の種類とパターンの検出を使用します。 多くの共通の機密情報の種類から選ぶことができ、これらの一部は異なるリージョンに固有です。 詳細については、Microsoft 365 のドキュメントを参照してください。 [機密情報の種類](/microsoft-365/compliance/what-the-sensitive-information-types-look-for) については、「」を参照してください。
        
        Azure Portal から選択できる情報の種類の一覧は、定期的に更新され、Office DLP の新しいデータが追加されます。 ただし、ルール パッケージとして定義され、Office 365 セキュリティ/コンプライアンス センターにアップロードされたユーザー設定の機密情報の種類は、一覧から除外されます。
        
        > [!IMPORTANT]
        > 一部の情報には、クライアントの最小バージョンが必要な情報もあります。 [詳細情報](#sensitive-information-types-that-require-a-minimum-version-of-the-client) 
        
        Azure Information Protection は、選択された情報の種類を評価するとき、Office DLP 信頼レベルの設定を使わず、最も低い信頼度に従って一致させます。
    
    - **[カスタム]** を選択した場合: 一致させる名前とフレーズを指定します。引用符と特殊文字は除外する必要があります。 次に、正規表現として一致させるかどうか、大文字と小文字を区別するかどうか、最小出現回数、出現で出現回数に一意の値を含めるどうかを選択します。
        
        正規表現では、Office 365 の正規表現パターンが使用されます。 カスタム条件に正規表現を指定するために、次の Boost から参照できる「[Perl Regular Expression Syntax](https://www.boost.org/doc/libs/1_37_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html)」 (Perl 正規表現構文) の特定のバージョンをご覧ください。 カスタム正規表現は [.net ドキュメント](/dotnet/standard/base-types/character-escapes-in-regular-expressions#character-escapes-in-net)に準拠している必要があります。 さらに、Unicode (\x{# # # #...} という形式の Unicode を指定するために使用される Perl 5 の文字エスケープ。ここで、# # # #... は一連の16進数字) はサポートされて **いません** 。
        
5. **[最小出現回数]** と **[一意の値のみを含む出現回数をカウント]** を変更する必要があるかどうかを決定し、**[保存]** を選択します。 
    
    出現オプションの例: 社会保障番号の情報タイプを選択し、最小出現回数として 2 を設定したときに、ドキュメントに同じ社会保障番号が 2 回記載されていたとします。**[一意の値のみを含む出現回数をカウント]** を **[オン]** に設定した場合、条件は満たされません。 このオプションを **[オフ]** に設定した場合、条件は満たされます。

6. **ラベル** ウィンドウに戻り、次のように構成して、[**保存**] をクリックします。
    
    - 自動分類または推奨分類を選択します。**[Select how this label is applied: automatically or recommended to user]** (ラベルの適用方法を選択してください: 自動またはユーザーに推奨) で、**[自動]** または **[推奨]** を選択します。
    
    - ユーザー プロンプトまたはポリシー ヒント用のテキストを指定します。既定のテキストを維持するか、独自の文字列を指定します。

**[保存]** をクリックすると、変更内容がユーザーとサービスに対して自動的に利用可能になります。 独立した公開オプションはなくなりました。

### <a name="sensitive-information-types-that-require-a-minimum-version-of-the-client"></a>クライアントの最小バージョンが必要な機密情報の種類

次の機密情報の種類には、Azure Information Protection クライアントの1.48.204.0 の最小バージョンが必要です。

- **Azure Service Bus 接続文字列**
- **Azure IoT 接続文字列**
- **Azure Storage アカウント**
- **Azure IAAS データベース接続文字列および Azure SQL 接続文字列**
- **Azure Redis Cache 接続文字列**
- **Azure SAS**
- **SQL Server 接続文字列**
- **Azure DocumentDB 認証キー**
- **Azure 発行設定パスワード**
- **Azure Storage アカウント キー (汎用)**

これらの機密情報の種類の詳細については、次のブログ投稿を参照してください。資格情報を[自動的に検出することで、セキュリティを強化する](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Azure-Information-Protection-helps-you-to-be-more-secure-by/ba-p/360181)ための Azure Information Protection です。

さらに、Azure Information Protection クライアントの1.48.204.0 以降では、次の機密情報の種類はサポートされておらず、Azure portal に表示されなくなりました。 これらの機密情報の種類を使用するラベルがある場合は、これらを削除することをお勧めします。正しく検出されないようにし、スキャナーレポートでそれらへの参照を無視する必要があるためです。

- **EU 電話番号**
- **EU の GPS 座標**

## <a name="next-steps"></a>次のステップ

[Azure Information Protection スキャナー](deploy-aip-scanner.md)のデプロイについて検討します。このスキャナーは自動分類規則を利用し、ネットワーク共有やオンプレミス ファイル ストアのファイルを検出、分類、保護できます。  

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。