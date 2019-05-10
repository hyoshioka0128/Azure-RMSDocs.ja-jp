---
title: 分類し、保護 - Azure Information Protection クライアントのラベル付けを統合します。
description: 分類して、Azure Information Protection を使用すると、ドキュメントや電子メールを保護する方法は、Windows 用のラベル付けのクライアントを統合する手順です。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 04/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.suite: ems
ms.openlocfilehash: 1b05cf8f5194c8491a2aa7bb687622e821e770cb
ms.sourcegitcommit: 2fe9333c3e6c98e7dd9003c5f4cd7c1e7a48b297
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2019
ms.locfileid: "64880119"
---
# <a name="user-guide-classify-and-protect-with-the-azure-information-protection-unified-labeling-client"></a>ユーザー ガイド: 分類および Azure Information Protection の統合されたラベル付けクライアントと保護

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*
>
> *手順:[Azure Information Protection unified Windows 用のラベル付けのクライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

> [!NOTE]
> 次の手順に従って、ドキュメントや電子メールを分類して保護します。 ドキュメントや電子メールを分類するだけで保護する必要がない場合は、[分類のみの手順](clientv2-classify.md)を参照してください。 どちらの手順を使用するかわからない場合は、管理者またはヘルプ デスクに確認してください。

ドキュメントや電子メールを分類して保護する最も簡単な方法は、Office デスクトップ アプリ (**Word**、**Excel**、**PowerPoint**、**Outlook**) 内から作成または編集することです。 

ただし、**エクスプローラー**を利用してファイルを分類し、保護することもできます。 この方法では対応しているファイルの種類が増えます。また、複数のファイルを一度に分類し、保護できるので便利です。 この方法は、Office ドキュメント、PDF ファイル、テキスト ファイル、画像ファイルなどさまざまなファイルの保護をサポートしています。 

ラベルによりドキュメントに保護が適用される場合、保護されたドキュメントは SharePoint または OneDrive に保存するには適しません。 これらの場所では、保護されたファイルに対する共同作成、Office Online、検索、ドキュメント プレビュー、サムネイル、電子情報開示がサポートされていません。

### <a name="safely-share-a-file-with-people-outside-your-organization"></a>組織外の相手と安全にファイルを共有する

保護されているファイルは、他のユーザーと安全に共有できます。 たとえば、保護されたドキュメントを電子メールに添付することもできます。

組織外のユーザーとファイルを共有する場合は、外部ユーザーからファイルを保護する方法について、事前にヘルプ デスクや管理者に確認をとってください。

たとえば、別の組織内のユーザーと定期的に情報をやりとりをする場合は、それらのユーザーが保護されたドキュメントを読み取って使用できるように、管理者が保護を設定するラベルを構成している可能性があります。 その後、それらのラベルを選択し、共有するドキュメントを分類して保護します。

また、外部のユーザーがいる場合[企業間取引 (B2B) アカウント](/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)使用できますに作成、[カスタム アクセス許可を設定するファイル エクスプ ローラー](#using-file-explorer-to-classify-and-protect-files)共有する前に、ドキュメントの。 カスタム アクセス許可を設定し、内部利用向けにドキュメントが既に保護されている場合、まずそのファイルのコピーを作成して、元のアクセス許可を保持します。 次に、そのコピーを使用してカスタム アクセス許可を設定します。


## <a name="using-office-apps-to-classify-and-protect-your-documents-and-emails"></a>Office アプリを使用してドキュメントや電子メールを分類して保護する

**ホーム**] タブで、[、**感度**リボンのボタンをクリックし、いずれかが構成されているラベルを選択します。 以下に例を示します。

![感度ボタンの例](../media/sensitivity-not-set-callout.png)

または、選択した場合に**バーを表示する**から、**感度**ボタン、Azure Information Protection バーからラベルを選択することができます。 以下に例を示します。

![Azure Information Protection バーの例](../media/info-protect-barv2-not-set-callout.png)

などのラベルを設定する"**社外秘** \ **すべての従業員**"を選択します**社外秘**し**すべての従業員**します。 現在のドキュメントや電子メールに適用するラベルがわからない場合は、ラベルのツールヒントで、各ラベルの詳細と適用する場合を参照してください。 ラベルがドキュメントに既に適用され、ラベルを変更する場合は、別のラベルを選択できます。 Azure Information Protection バーを表示して、ラベルが、バーを選択して、最初に表示されていない場合、**ラベルの編集**アイコンは、現在のラベル値の横にあります。

ラベルの手動選択に加え、次の方法でラベルを適用することもできます。

- 管理者が既定のラベルを構成済み。そのまま使用するか、変更することができます。

- 管理者は、機密情報が検出されたときに自動的に設定するラベルを構成します。

- 管理者が構成済みの機密情報が検出されると、および推奨事項に同意するように求められます (とラベルが適用されるキーを押す)、ラベルが推奨されるか、拒否 (推奨されたラベルは適用されません)。

### <a name="exceptions-for-the-sensitivity-button"></a>感度ボタンの例外

##### <a name="dont-see-the-sensitivity-button-in-your-office-apps"></a>Office アプリでの感度ボタンが表示されない場合

- Azure Information Protection の統合されたラベル付けクライアントがない[インストール](install-unifiedlabelingclient-app.md)します。

- 表示されない場合、**感度**リボンのボタンしますが、表示、**保護**代わりにラベルが付いたボタンをクリックする必要があります、Azure Information Protection クライアントのインストールと Azure Information Protection ではありません統一されたラベル付けクライアント。 [詳細情報](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)
 
##### <a name="is-the-label-that-you-expect-to-see-not-displayed"></a>表示されるはずのラベルが表示されない場合 

考えられる理由:

- 管理者が新しいラベルを構成したばかりの場合は、すべてのインスタンスの Office アプリを終了してから、開き直します。 この操作で、ラベルの変更が確認されます。

- 存在しないラベルで保護を適用すると、Rights Management 保護の適用をサポートしていない Office のエディションになる可能性があります。 確認するには、**[保護]** > **[ヘルプとフィードバック]** の順にクリックします。 ダイアログ ボックスで、**[クライアント ステータス]** セクションに **[このクライアントには Office Professional Plus のライセンスがありません]** というメッセージが表示されているかどうかを確認します。 
    
    ユーザーに Azure Rights Management (別名: Azure Information Protection for Office 365) のライセンスが割り当てられている場合は、Office 365 Business または Microsoft 365 Business の Office アプリがあれば、Office Professional Plus は必要ありません。

- 自分のアカウントを含まない範囲のポリシーのラベルである可能性があります。 ヘルプ デスクまたは管理者に問い合わせてください。


### <a name="safely-sharing-by-email"></a>電子メールで安全に共有する

電子メールで Office ドキュメントを共有するとき、保護しているメールにドキュメントを添付できます。メールに適用されているものと同じ制約でドキュメントが自動的に保護されます。 

ただし、最初に、ドキュメントを保護するため、電子メールに添付したい場合があります。 メール メッセージに機密情報が含まれている場合、メールも保護します。 電子メールに添付する前に文書の保護の利点:

- メール メッセージとは異なるアクセス許可をドキュメントに適用できます。

## <a name="using-file-explorer-to-classify-and-protect-files"></a>エクスプローラーを使用してファイルを分類および保護する

エクスプローラーを使用すると、1 つのファイル、複数のファイル、またはフォルダーをすばやく分類して保護することができます。 

フォルダーを選択すると、そのフォルダー内のすべてのファイルとサブフォルダーが設定された分類および保護のオプションで自動的に選択されます。 ただし、そのフォルダーまたはサブフォルダー内に作成した新しいファイルは、設定されたオプションで自動的に構成されません。

エクスプローラーを使用してファイルの分類と保護を行う場合、1 つまたは複数のラベルが淡色表示の場合、選択したファイルは分類をサポートしていません。 このようなファイルについては、管理者によってラベルが保護を適用するように構成された場合にのみ、ラベルを選択できます。 または、独自の保護設定を指定することができます。 

一部のファイルは、変更すると PC が動作しなくなる可能性があるため、分類と保護の対象から自動的に除外されます。 これらのファイルを選択することはできますが、除外されるフォルダーまたはファイルとしてスキップされます。 たとえば、実行可能ファイルや Windows フォルダーが含まれます。

管理者ガイドには、サポートされるファイルの種類と自動的に除外されるファイルとフォルダーの詳細な一覧が記載されています。[ファイルの種類の Azure Information Protection の統合されたラベル付けクライアントでサポートされている](clientv2-admin-guide-file-types.md)します。


### <a name="to-classify-and-protect-a-file-by-using-file-explorer"></a>エクスプローラーを使用してファイルを分類および保護するには

1. エクスプローラーで、1 つのファイル、複数のファイル、またはフォルダーを選択します。 右クリックして **[分類して保護する]** を選択します。 以下に例を示します。
    
    ![Azure Information Protection を使用する場合のファイル エクスプローラーの右クリック オプション [分類して保護する]](../media/right-click-classify-protect-folder.png)

2. **[分類と保護 - Azure Information Protection]** ダイアログ ボックスで、Office アプリケーションでの操作と同様にラベルを使用し、管理者によって定義されたとおりに分類と保護を設定します。 

   - 選択できるラベルがない場合 (すべてのラベルが淡色表示されている場合): 選択したファイルでは分類がサポートされていませんが、カスタム アクセス許可で保護できます (手順 3)。 以下に例を示します。

     ![[分類と保護 - Azure Information Protection]** ダイアログ ボックスで使用できるラベルがない](../media/v2info-protect-dialog-labels-dimmed.png)

3. ことができます独自の保護設定を指定ではなく、管理者が含まれている保護設定を使用して、選択したラベル。 この操作を行うには、**[カスタム アクセス許可で保護する]** 選択します。
    
    指定したカスタムのアクセス許可は、選択したラベルに対して管理者から定義されている保護設定を補足するのではなく、この設定に置き換わります。  

4. カスタムのアクセス許可オプションを選択した場合は、次の項目を指定します。

   - **アクセス許可の選択**: 選択したファイルを保護する場合のユーザーのアクセス レベルを選びます。
    
   - **ユーザー、グループ、および組織の選択**: ファイルに対して選択したアクセス許可を持つユーザーを指定します。 組織内のユーザー全員について、組織で使用する完全なメール アドレス、グループ メール アドレス、ドメイン名を入力します。 
    
     あるいは、アドレス帳アイコンを使用して、Outlook のアドレス帳からユーザーまたはグループを選択できます。
        
    - **アクセスの有効期限**: 指定されたユーザーが日付を設定した後、選択したファイルまたはファイルを開くことができませんように時間を区別するファイルに対してのみこのオプションを選択します。 自分は元のファイルを引き続き開くことができますが、(現在のタイム ゾーンで) 設定した日の深夜を過ぎた後は、他のユーザーはファイルを開くことができなくなります。
    
     この設定を Office 2010 アプリのカスタム アクセス許可を使用して構成していた場合、指定した有効期限の日付はこのダイアログ ボックスには表示されませんが、有効期限は依然として有効です。 これは Office 2010 で有効期限を構成していた場合にのみ発生する表示上の問題です。

5. **[適用]** をクリックし、**"作業が終了しました"** というメッセージで結果が示されるまで待ちます。 次に、 **[閉じる]** をクリックします。

選択されたファイルは、指定した設定に従って分類および保護されます。 場合によっては (保護の追加によってファイル名の拡張子が変更される場合)、エクスプローラーの元のファイルが Azure Information Protection のロック アイコンの付いた新しいファイルに置き換えられます。 以下に例を示します。

![Azure Information Protection のロック アイコンが付いた保護されたファイル](../media/Pfile.png)

分類と保護について考えが変わったり、後で設定を変更する必要がある場合は、新しい設定でこのプロセスを繰り返すだけです。

ファイルを電子メールで送信したり、別の場所に保存した場合にも、指定した分類と保護はファイルに設定されたままです。 

## <a name="other-instructions"></a>その他の手順
Azure Information Protection の統合されたラベル付けクライアントのユーザーからの複数の操作手順を紹介します。

-   [目的に合ったトピックをクリックしてください](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>管理者向け追加情報    

参照してください[機密ラベルの概要](/Office365/SecurityCompliance/sensitivity-labels)します。
