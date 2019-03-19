---
title: Azure Information Protection ラベルの条件を構成する - AIP
description: ラベルの条件を使うと、ドキュメントや電子メールにラベルを自動的に割り当てることができます。 または、推奨するラベルを選択するようユーザーに求めることができます。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 03/14/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
ms.openlocfilehash: f8545491a527b8e502150cd83802b2868dd3a1da
ms.sourcegitcommit: d716d3345a6a5adc63814dee28f7c01b55b96770
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2019
ms.locfileid: "57829044"
---
# <a name="how-to-configure-conditions-for-automatic-and-recommended-classification-for-azure-information-protection"></a>Azure Information Protection 用の自動および推奨分類の条件を構成する方法

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

ラベルの条件を構成するときに、ドキュメントまたは電子メールにラベルを自動的に割り当てることができます。 または、自分が推奨するラベルを選択するようにユーザーに求めることもできます。 

これらの条件を構成するときには、**クレジット カード番号**や**米国社会保障番号 (SSN)** などの定義済みのパターンを使用できます。 または、自動分類の条件として、ユーザー指定の文字列またはパターンを定義することもできます。 これらの条件は、ドキュメントや電子メールの本文とヘッダーおよびフッターに適用されます。 条件の詳細については、[次の手順](#to-configure-recommended-or-automatic-classification-for-a-label)の手順 5 をご覧ください。

最良のユーザー エクスペリエンスとビジネスの継続性を確保するために、自動分類ではなく、ユーザーが推奨する分類から始めることをお勧めします。 この構成の場合、ユーザーは、分類や関連付けられている保護を受け入れるか、それらの提案が自分のドキュメントまたは電子メール メッセージに適していない場合はオーバーライドすることを選択できます。

ラベルを推奨される操作として適用するように条件を構成したときのプロンプトの例を、カスタム ポリシー ヒントと共に示します。

![Azure Information Protection の検出と推奨事項](./media/info-protect-recommend-calloutsv2.png)

この例では、ユーザーは **[今すぐ変更]** をクリックして推奨されたラベルを適用するか、**[閉じる]** を選択することでその推奨をオーバーライドできます。 ユーザーが推奨を無視することを選択しても、ドキュメントを次に開いたときに条件がまだ適用される場合は、ラベルの推奨がもう一度表示されます。

推奨されている分類ではなく自動分類を構成した場合、ラベルは自動的に適用され、ユーザーには Word、Excel、PowerPoint 内に引き続き通知が表示されます。 ただし、**[今すぐ変更]** および **[閉じる]** ボタンは **[OK]** で置き換えられます。 Outlook では、自動分類の場合に通知は表示されず、電子メールの送信時にラベルが適用されます。

> [!IMPORTANT]
>自動分類とユーザー定義のアクセス許可にはラベルを構成しないでください。 ユーザー定義のアクセス許可オプションは、アクセス許可を与える人をユーザーが指定できるという[保護設定](configure-policy-protection.md)となります。
>
>自動分類とユーザー定義のアクセス許可にラベルを構成すると、条件に対してコンテンツがチェックされ、ユーザー定義のアクセス許可設定は適用されません。 推奨されている分類とユーザー定義のアクセス許可を使用できます。

## <a name="how-automatic-or-recommended-labels-are-applied"></a>自動ラベルと推奨ラベルが適用されるしくみ

- 自動分類は、Word、Excel、PowerPoint でドキュメントが保存されるときと、Outlook で電子メールが送信されるときに適用されます。 
    
    以前に手動でラベルが付けられているか、以前に上位の分類で自動的にラベルが付けられているドキュメントと電子メールには自動分類を使用できません。 

- 推奨分類は、Word、Excel、および PowerPoint でドキュメントが保存されるときに適用されます。 現在プレビュー段階にある[高度なクライアント設定](./rms-client/client-admin-guide-customizations.md#enable-recommended-classification-in-outlook)を構成しない限り、推奨分類を Outlook に使用することはできません。
    
    以前に上位の分類でラベルが付けられているドキュメントには推奨分類を使用できません。 

ドキュメントに指定された条件規則が Azure Information Protection クライアントによって定期的にチェックされるように、この動作を変更できます。 この構成には、現在プレビュー版の[高度なクライアント設定](./rms-client/client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background)が必要です。

### <a name="how-multiple-conditions-are-evaluated-when-they-apply-to-more-than-one-label"></a>複数のラベルに適用するときの複数の条件の評価方法

1. ラベルは、ポリシー内で指定した位置に従って評価の順序を決められます。先頭に配置したラベルが最下位 (秘密度が最も低い) になり、最後に配置したラベルが最上位 (秘密度が最も高い) になります。

2. 最も秘密度の高いラベルが適用されます。
 
3. 最後のサブラベルが適用されます。


## <a name="to-configure-recommended-or-automatic-classification-for-a-label"></a>ラベルの推奨または自動分類を構成するには

1. まだサインインしていない場合は、新しいブラウザー ウィンドウを開き、[Azure Portal にサインイン](configure-policy.md#signing-in-to-the-azure-portal)します。 次に、**[Azure Information Protection]** ブレードに移動します。 
    
    たとえば、ハブ メニューで **[すべてのサービス]** をクリックし、[フィルター] ボックスに「**Information**」と入力します。 "**Azure Information Protection**" を選択します。

2. **[分類]** > **[ラベル]** メニュー オプションから: **[Azure Information Protection - ラベル]** ブレードで、構成するラベルを選択します。

3. **[ラベル]** ブレードで、**[Configure conditions for automatically applying this label]** (このラベルに自動的に適用する条件を構成する) セクションの **[新しい条件の追加]** をクリックします。

4. **[条件]** ブレードで、定義済みの条件を使用する場合は **[情報の種類]** を、独自の条件を指定する場合は **[カスタム]** を選択します。
    - **[情報の種類]** を選択した場合:使用可能な条件の一覧から選択し、最小出現回数と、出現で出現回数に一意の値を含めるかどうかを選択します。
        
        情報の種類では、Office 365 データ損失防止 (DLP) の機密情報の種類とパターン検出が使われます。 多くの共通の機密情報の種類から選ぶことができ、これらの一部は異なるリージョンに固有です。 詳しくは、Office 365 ドキュメントの「[What the sensitive information types look for](/office365/securitycompliance/what-the-sensitive-information-types-look-for)」(検索される機密情報の種類) をご覧ください。
        
        Azure Portal から選択できる情報の種類の一覧は、定期的に更新され、Office DLP の新しいデータが追加されます。 ただし、ルール パッケージとして定義され、Office 365 セキュリティ/コンプライアンス センターにアップロードされたユーザー設定の機密情報の種類は、一覧から除外されます。
        
        > [!IMPORTANT]
        > 一部の情報には、クライアントの最小バージョンが必要な情報もあります。 [詳細情報](#sensitive-information-types-that-require-a-minimum-version-of-the-client) 
        
        Azure Information Protection は、選択された情報の種類を評価するとき、Office DLP 信頼レベルの設定を使わず、最も低い信頼度に従って一致させます。
    
    - **[カスタム]** を選択した場合:一致させる名前とフレーズを指定します。引用符と特殊文字は除外する必要があります。 次に、正規表現として一致させるかどうか、大文字と小文字を区別するかどうか、最小出現回数、出現で出現回数に一意の値を含めるどうかを選択します。
        
        正規表現では、Office 365 の正規表現パターンが使用されます。 カスタム条件に正規表現を指定するために、次の Boost から参照できる「[Perl Regular Expression Syntax](https://www.boost.org/doc/libs/1_37_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html)」 (Perl 正規表現構文) の特定のバージョンをご覧ください。
        
5. **[最小出現回数]** と **[一意の値のみを含む出現回数をカウント]** を変更する必要があるかどうかを決定し、**[保存]** を選択します。 
    
    出現オプションの例:社会保障番号の情報の種類を選択し、最小出現回数として 2 を設定したときに、ドキュメントに同じ社会保障番号が 2 回記載されていたとします。**[一意の値のみを含む出現回数をカウント]** を **[オン]** に設定した場合、条件は満たされません。 このオプションを **[オフ]** に設定した場合、条件は満たされます。

6. **[ラベル]** ブレードで、次のように構成し、**[保存]** をクリックします。
    
    - 自動分類または推奨分類を選択します。**[このラベルの適用方法を選択: 自動またはユーザーへの推奨]** に対して、**[自動]** または **[推奨]** を選択します。
    
    - ユーザー プロンプトまたはポリシー ヒント用のテキストを指定します。既定のテキストを維持するか、独自の文字列を指定します。

**[保存]** をクリックすると、変更内容がユーザーとサービスに対して自動的に利用可能になります。 独立した公開オプションはなくなりました。

### <a name="sensitive-information-types-that-require-a-minimum-version-of-the-client"></a>クライアントの最小バージョンが必要な機密情報の種類

次の機密情報の種類には、Azure Information Protection クライアントのバージョン 1.37.19.0 以降が必要です。

- **EU の携帯電話番号**
- **EU のパスポート番号**
- **EU の運転免許証番号**
- **EU の国民識別番号**
- **EU の社会保障番号 (SSN) または同等の ID**
- **EU の納税者識別番号 (TIN)**
- **タイの人口識別コード**
- **トルコの国民識別番号**
- **日本の住民基本台帳カード番号**


次の機密情報の種類を使用するには、Azure Information Protection クライアントの最新プレビュー バージョンが必要です。

- **Azure Service Bus の接続文字列**
- **Azure IoT の接続文字列**
- **Azure ストレージ アカウント**
- **Azure IAAS データベースの接続文字列および Azure SQL の接続文字列**
- **Azure Redis Cache の接続文字列**
- **Azure SAS**
- **SQL Server の接続文字列**
- **Azure DocumentDB の認証キー**
- **Azure 発行設定のパスワード**
- **Azure Storage のアカウント キー (汎用)**

また、次の機密情報の種類は Azure Information Protection クライアントの最新プレビュー バージョンでサポートされておらず、Azure portal に表示されなくなりました。

- **EU の電話番号**
- **EU の GPS 座標**

## <a name="next-steps"></a>次の手順

[Azure Information Protection スキャナー](deploy-aip-scanner.md)のデプロイについて検討します。このスキャナーは自動分類規則を利用し、ネットワーク共有やオンプレミス ファイル ストアのファイルを検出、分類、保護できます。  

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。


