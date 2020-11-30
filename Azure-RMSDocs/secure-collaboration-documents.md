---
title: Azure Information Protection を使用したセキュアなドキュメント コラボレーションの構成
description: Azure Information Protection によって保護されたドキュメントで共同作業を行うための、全体的なワークフローについて説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/19/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 4895c429-959f-47c7-9007-b8f032f6df6f
ms.subservice: aiplabels
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: fcdfc020061428959e2137a46347b49b150ad73a
ms.sourcegitcommit: d31cb53de64bafa2097e682550645cadc612ec3e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96316706"
---
# <a name="configuring-secure-document-collaboration-by-using-azure-information-protection"></a>Azure Information Protection を使用したセキュアなドキュメント コラボレーションの構成

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

>[!NOTE] 
> 統一された効率的なカスタマー エクスペリエンスを提供するため、Azure portal の **Azure Information Protection クライアント (クラシック)** と **ラベル管理** は、**2021 年 3 月 31 日** で **非推奨** になります。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

Azure Information Protection では、承認済みユーザーのコラボレーション機能を損なうことなく、ドキュメントを保護できます。 1 人のユーザーが作成し、表示や編集の権限を他のユーザーと共有するドキュメントの多くは、Word、Excel、PowerPoint の Office ドキュメントになります。 これらのドキュメントでは、保護機能がネイティブにサポートされます。つまり、認証と暗号化の機能だけでなく、より詳細に制御するための制限付き権限もサポートされます。 

これらの権限は使用権限と呼ばれ、表示、編集、印刷などの権限があります。 ドキュメントを保護する際に使用権限を個別に定義することもできますし、使用権限のグループ (権限レベル) を定義することもできます。 権限レベルを使用すると、よく使われる使用権限を簡単に選択することができます (たとえば、レビュー担当者や共同作成者など)。 使用権限とアクセス許可レベルの詳細については、「 [Azure Information Protection の使用権限の構成](configure-usage-rights.md)」を参照してください。

これらの権限を構成する際には、その対象となるユーザーを指定できます。

- **お客様の組織か、Azure Active Directory を使用している別の組織内のユーザーの場合**: で Azure AD ユーザー アカウント、Azure AD グループ、またはその組織内のすべてのユーザーを指定できます。 

- **Azure Active Directory アカウントを持っていないユーザーの場合**: Microsoft アカウントで使用される電子メール アドレスを指定します。 既存のアカウントを使用することもできますし、保護されたドキュメントを開くときにアカウントを作成することもできます。 
    
    Microsoft アカウントでドキュメントを開くには、ユーザーが Microsoft 365 アプリを使用する必要があります (クリックして実行)。 他のエディションやバージョンの Office では、Office の保護されたドキュメントを Microsoft アカウントで開く機能は、まだサポートされていません。

- **認証されたユーザーの場合**: 認証されたユーザーであれば保護されたドキュメントへのアクセスを制御する必要がない場合、このオプションが適しています。 認証は、Azure AD、Microsoft アカウントの使用、コンテンツが Office 365 メッセージの暗号化の新機能で保護されている場合はフェデレーション ソーシャル プロバイダーやワンタイム パスコードなど、さまざまな方法で行われます。 

管理者は、Azure Information Protection ラベルを構成して、権限と承認済みユーザーを適用できます。 この構成により、ユーザーや他の管理者は詳細を指定することなく、ラベルを適用するだけで正しい保護設定を簡単に適用できるようになります。 次のセクションでは、内部および外部ユーザーとの安全なコラボレーションをサポートするドキュメントを保護するためのチュートリアルの例を示します。


## <a name="example-configuration-for-a-label-to-apply-protection-to-support-internal-and-external-collaboration"></a>ラベルの構成例: 保護を適用して内部や外部とのコラボレーションを可能にする


この例では、保護を適用する既存のラベルを構成して、組織のユーザーが、Microsoft 365 または Azure AD を持つ別の組織のユーザー、Microsoft 365 または Azure AD を持つ別の組織のグループ、および Azure AD にアカウントを持たず、代わりに Gmail のメールアドレスを使用するユーザーを持つドキュメントで共同作業できるようにします。

シナリオによって特定の相手に対するアクセスが制限されるため、認証されたユーザーの設定は含まれません。 この設定でラベルを構成する方法の例としては、「[例 5: コンテンツを暗号化するがアクセスを制限しないラベル](configure-policy-protection.md#example-5-label-that-encrypts-content-but-doesnt-restrict-who-can-access-it)」をご覧ください。  

1. グローバル ポリシーまたはスコープ付きポリシーに含まれている既存のラベルを選択します。 **[保護]** ペインで、**[Azure (クラウド キー)]** が選択されていることを確認します。
    
2. **[アクセス許可を設定する]** が選択されていることを確認し、**[アクセス許可を追加]** を選択します。

3. **[アクセス許可の追加]** ペインで、次の操作を行います。 
    
   - 内部グループ: **[ディレクトリを参照]** を選択し、グループを選択します (電子メールが有効になっている必要があります)。
    
   - 第 1 外部組織内の全ユーザー: **[詳細を入力]** を選択し、組織のテナント内のドメイン名を入力します (たとえば、fabrikam.com)。
    
   - 第 2 外部組織内のグループ: **[詳細を入力]** タブで、組織のテナント内のグループの電子メール アドレスを入力します。 たとえば、「 sales@contoso.com 」のように入力します。
    
   - Azure AD アカウントを持っていないユーザー: **[詳細を入力]** タブで、ユーザーの電子メール アドレスを入力します。 たとえば、「 bengi.turan@gmail.com 」のように入力します。 

4. これらすべてのユーザーに同じ権限を付与するには、**[事前設定されたものの中からアクセス許可を選択する]** で、**[共同所有者]**、**[共同作成者]**、**[レビュー担当者]**、または **[カスタム]** を選択し、付与する権限を選択します。
    
    たとえば、構成後の権限は次のようになります。
        
    ![セキュアなコラボレーションのための権限の構成](./media/collaboration-permissions.png)

5. **[アクセス許可の追加]** ペインで **[OK]** をクリックします。

6. [ **保護** ] ウィンドウで、[ **OK]** をクリックします。

7. **[ラベル]** ペインで、**[保存]** を選択します。 

## <a name="applying-the-label-that-supports-secure-collaboration"></a>セキュアなコラボレーションをサポートするラベルの適用

ラベルを構成したら、次に示す各種の方法でラベルをドキュメントに適用できます。

|ラベルの適用方法|詳細情報|
|---------------|----------|
|Office アプリケーションでのドキュメント作成時に、手動でラベルを選択する。|Office リボンの **[保護]** ボタンか、Azure Information Protection バーからラベルを選択します。|
|新規ドキュメントの保存時に、ラベルを選択するように求められる。|**[すべてのドキュメントとメールにラベルを付ける]** という Azure Information Protection [ポリシー設定](configure-policy-settings.md)を構成した場合です。|
|電子メールによってドキュメントを共有し、Outlook でラベルを手動で選択する。|Office リボンの **[保護]** ボタン (または Azure Information Protection バー) からラベルを選択すると、添付されたドキュメントが同じ設定で自動的に保護されます。|
|管理者が PowerShell を使用してドキュメントにラベルを適用する。|[Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) コマンドレットを使用して、特定のドキュメントや、フォルダー内のすべてのドキュメントにラベルを適用します。|
|自動分類を適用するようにラベルを構成する (これは、Azure Information Protection スキャナーまたは PowerShell を使用して適用できるようになりました)。|「[Azure Information Protection 用の自動および推奨分類の条件を構成する方法](configure-policy-classification.md)」をご覧ください。|

このチュートリアルを完了するには、Office アプリケーションでドキュメントを作成する際に手動でラベルを適用します。 

1. クライアント コンピューターで、Office アプリケーションが既に開いている場合は、まずアプリケーションを終了し、再度起動して、新たに構成されたラベルを含む最新のポリシー変更を取得します。 

2. ドキュメントにラベルを適用し、保存します。

保護されたドキュメントを電子メールに添付して共有し、ドキュメントの編集を許可する相手にそれを送信します。

## <a name="opening-and-editing-the-protected-document"></a>保護されたドキュメントを開いて編集する

承認済みのユーザーがドキュメントを編集用に開くと、ドキュメントが開く際、権限が制限されていることを知らせる情報バナーが表示されます。 次に例を示します。

![Azure Information Protection の権限に関する情報バナーの例](./media/example-restricted-access-banner.png)

**[アクセス許可​​の表示]** ボタン選択すると、 自分の持っている権限が表示されます。 次の例の場合、ユーザーはドキュメントの表示と編集を行うことができます。

![Azure Information Protection の権限に関するダイアログ ボックスの例](./media/example-permisisons-popup.png)

注: Azure Information Protection を使用している外部ユーザーによってドキュメントが開かれた場合、Office アプリケーションでは、そのドキュメントの分類ラベルの視覚的なマーキングは残りますが、ラベルは表示されません。 代わりに、外部ユーザーはそれぞれの組織の分類法に沿って各自のラベルを適用できます。 外部ユーザーが編集したドキュメントを送り返してきた場合、Office でドキュメントを再び開くと元の分類ラベルが表示されます。

保護されたドキュメントが開く前に、次のいずれかの認証フローが発生します。

- Azure AD アカウントを持っているユーザーの場合は、Azure AD の資格情報を使用して Azure AD から認証されると、ドキュメントが開きます。 

- Azure AD アカウントを持っていないユーザーの場合、ドキュメントを開く権限があるアカウントで Office にサインインしていない場合は、**[アカウント]** ページが表示されます。 
    
   **[アカウント]** ページで、**[アカウントを追加]** をクリックします。
   
    ![Microsoft アカウントを追加して保護されたドキュメント開く](./media/add-account-msa.png)

   **[サインイン]** ページで、**[アカウントを作成しましょう]** を選択し、 プロンプトに従って、権限の付与に使用された電子メール アドレスで新しい Microsoft アカウントを作成します。
    
    ![Microsoft アカウントを作成して保護されたドキュメント開く](./media/create-account-msa.png)
    
    新しい Microsoft アカウントが作成されると、ローカル アカウントがその新しい Microsoft アカウントに切り替わり、ユーザーがドキュメントを開けるようになります。


### <a name="supported-scenarios-for-opening-protected-documents"></a>保護されたドキュメントを開く際のサポートされているシナリオ

次の表は、保護されたドキュメントの表示と編集のためにサポートされている認証方法をまとめたものです。

さらに、次のシナリオではドキュメントの表示がサポートされます。

- Windows、iOS、Android 用の Azure Information Protection ビューアーでは、Microsoft アカウントを使用することでファイルを表示用に開くことができます。 

- Exchange Online と Office 365 メッセージの暗号化の新機能を使用した認証のためにソーシャル プロバイダーとワンタイム パスコードが使用されている場合、ブラウザーで保護された添付ファイルを開くことができます。 

|ドキュメントの表示と編集のためのプラットフォーム: <br />Word、Excel、PowerPoint|認証方法:<br />Azure AD|認証方法:<br />Microsoft アカウント|
|---------------|----------|-----------|-----------|
|Windows|はい [[1]](#footnote-1)|はい (Microsoft 365 アプリのみ)|
|iOS|はい [[1]](#footnote-1)|はい (バージョン2.42 以降) |
|Android|はい [[1]](#footnote-1)|はい (バージョン16.0.13029 以降)|
|MacOS|はい [[1]](#footnote-1)|はい (バージョン16.42 以降)|

###### <a name="footnote-1"></a>脚注 1
ユーザー アカウント、電子メールが有効なグループ、すべてのメンバーがサポートされています。 ユーザー アカウント、および電子メールが有効なグループには、ゲスト アカウントが含まれる場合があります。 すべてのメンバーには、ゲスト アカウントは含まれません。

## <a name="next-steps"></a>次のステップ

一般的なシナリオで保護を適用するためのラベルについては、他の[構成例](configure-policy-protection.md#example-configurations)をご覧ください。 この記事には、保護設定に関する詳細も含まれています。

ラベルについて構成できるその他のオプションや設定について詳しくは、[Azure Information Protection ポリシーの構成](configure-policy.md)に関する記事をご覧ください。 

この記事で構成されているラベルでは、同じ名前の保護テンプレートも作成されます。 ご使用のアプリケーションやサービスが Azure Information Protection の保護テンプレートと統合されている場合は、このテンプレートを適用できます (たとえば、DLP ソリューションやメール フロー ルール)。 Web 上の Outlook では、Azure Information Protection のグローバル ポリシーからの保護テンプレートが自動的に表示されます。 




