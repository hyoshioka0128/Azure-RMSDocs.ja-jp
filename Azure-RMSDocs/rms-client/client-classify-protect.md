---
title: '& 保護-Azure Information Protection クライアントの分類'
description: Windows 用 Azure Information Protection クライアントを使用するときに、ドキュメントと電子メールを分類して保護する方法について説明します。
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/04/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 75268245-6f14-4218-b904-202f63fb3ce6
ms.subservice: v1client
ms.reviewer: eymanor
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 506d4aebd479dbbbb64011380befac48909a1922
ms.sourcegitcommit: 2917e822a5d1b21bf465f2cb93cfe46937b1faa7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2020
ms.locfileid: "79403979"
---
# <a name="user-guide-classify-and-protect-with-the-azure-information-protection-client"></a>ユーザーガイド: Azure Information Protection クライアントを使用した分類と保護

>*適用対象: Active Directory Rights Management サービス、 [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、windows 10、Windows 8.1、windows 8*
>
> *手順: [Windows 用の Azure Information Protection クライアント](../faqs.md#whats-the-difference-between-the-azure-information-protection-client-and-the-azure-information-protection-unified-labeling-client)*

> [!NOTE]
> 次の手順に従って、ドキュメントや電子メールを分類して保護します。 ドキュメントや電子メールを分類するだけで保護する必要がない場合は、[分類のみの手順](client-classify.md)を参照してください。 どちらの手順を使用するかわからない場合は、管理者またはヘルプ デスクに確認してください。

Office のデスクトップ アプリ (**Word**、**Excel**、**PowerPoint**、**Outlook**) でドキュメントや電子メールを作成したり編集すると、分類と保護が簡単になります。 

ただし、**エクスプローラー**を利用してファイルを分類し、保護することもできます。 この方法では対応しているファイルの種類が増えます。また、複数のファイルを一度に分類し、保護できるので便利です。 この方法は、Office ドキュメント、PDF ファイル、テキスト ファイル、画像ファイルなどさまざまなファイルの保護をサポートしています。 

ラベルによりドキュメントに保護が適用される場合、保護されたドキュメントは SharePoint または OneDrive に保存するには適しません。 これらの場所では、保護されたファイルの共同作成、web 用 Office、検索、ドキュメントプレビュー、サムネイル、および電子情報開示はサポートされていません。

> [!TIP]
> [SharePoint で機密ラベルが有効になっ](https://docs.microsoft.com/microsoft-365/compliance/sensitivity-labels-sharepoint-onedrive-files)ている場合、これらの場所でサポートされている統合秘密度ラベルへのラベルの移行については、管理者にお問い合わせください。

### <a name="safely-share-a-file-with-people-outside-your-organization"></a>組織外の相手と安全にファイルを共有する

保護されているファイルは、他のユーザーと安全に共有できます。 たとえば、保護されたドキュメントを電子メールに添付することもできます。

組織外のユーザーとファイルを共有する場合は、外部ユーザーからファイルを保護する方法について、事前にヘルプ デスクや管理者に確認をとってください。

たとえば、組織が別の組織のユーザーと定期的に通信する場合、管理者は、保護されたドキュメントを読み取り、使用できるようにラベルを構成している可能性があります。 その場合は、これらのラベルを選択して、共有するドキュメントを分類して保護します。

なお、外部ユーザーに対して[企業間取引 (B2B) アカウント](/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)が作成されている場合は、ドキュメントを共有する前に、[Office アプリを使用してカスタム アクセス許可を設定する](#set-custom-permissions-for-a-document)か、[ファイル エクスプ ローラーを使用してカスタム アクセス許可を設定する](#using-file-explorer-to-classify-and-protect-files)ことができます。 カスタム アクセス許可を設定し、内部利用向けにドキュメントが既に保護されている場合、まずそのファイルのコピーを作成して、元のアクセス許可を保持します。 次に、そのコピーを使用してカスタム アクセス許可を設定します。


## <a name="using-office-apps-to-classify-and-protect-your-documents-and-emails"></a>Office アプリを使用してドキュメントや電子メールを分類して保護する

Azure Information Protection バーまたはリボンの **[保護]** ボタンを使用して、構成されているラベルを 1 つ選択します。 

たとえば、次の図は、Azure Information Protection バーの **[秘密度]** が **[未設定]** のため、ドキュメントにまだラベルが設定されていないことを示します。 "General" など、ラベルを設定するには、 **[全般]** をクリックします。 現在のドキュメントや電子メールに適用するラベルがわからない場合は、ラベルのツールヒントで、各ラベルの詳細と適用する場合を参照してください。 

![Azure Information Protection バーの例](../media/info-protect-bar-not-set-callout.png)

ラベルがドキュメントに既に適用され、ラベルを変更する場合は、別のラベルを選択できます。 ラベルがバーに表示されない場合は、現在のラベル値の横にある **[ラベルの編集]** アイコンをクリックします。

ラベルの手動選択に加え、次の方法でラベルを適用することもできます。

- 管理者が既定のラベルを構成済み。そのまま使用するか、変更することができます。

- 機密データが検出された場合に特定のラベルを選択するように推奨するプロンプトを管理者が構成済み。 推奨を受け入れる (ラベルが適用される) か、拒否することができます (推奨されたラベルが適用されない)。

### <a name="exceptions-for-the-azure-information-protection-bar"></a>Azure Information Protection バーの例外 

##### <a name="dont-see-this-information-protection-bar-in-your-office-apps"></a>お使いの Office アプリでこの Information Protection バーが表示されない場合

考えられる理由:

- Azure Information Protection クライアントが[インストール](install-client-app.md)されていません。

- お客様はクライアントをインストールしていますが、管理者がバーを表示しないように設定を構成しています。 代わりに、Office リボンの **[ファイル]** タブで、 **[保護]** ボタンからラベルを選択します。 

- クライアントが[保護のみモード](client-protection-only-mode.md)で実行されています。
 
##### <a name="is-the-label-that-you-expect-to-see-not-displayed"></a>表示されるはずのラベルが表示されない場合 

考えられる理由:

- 管理者が新しいラベルを構成したばかりの場合は、すべてのインスタンスの Office アプリを終了してから、開き直します。 この操作で、ラベルの変更が確認されます。

- 存在しないラベルで保護を適用すると、Rights Management 保護の適用をサポートしていない Office のエディションになる可能性があります。 確認するには、 **[保護]**  >  **[ヘルプとフィードバック]** の順にクリックします。 ダイアログ ボックスで、 **[クライアント ステータス]** セクションに **[このクライアントには Office Professional Plus のライセンスがありません]** というメッセージが表示されているかどうかを確認します。 
    
    ユーザーに Azure Rights Management (別名: Azure Information Protection for Office 365) のライセンスが割り当てられている場合は、Office 365 Business または Microsoft 365 Business の Office アプリがあれば、Office Professional Plus は必要ありません。

- 自分のアカウントを含まない範囲のポリシーのラベルである可能性があります。 ヘルプ デスクまたは管理者に問い合わせてください。

### <a name="set-custom-permissions-for-a-document"></a>ドキュメントのカスタム アクセス許可を設定する

管理者から許可されている場合は、選択したラベルに対して管理者から指定されている保護設定を使用するのではなく、独自のドキュメントの保護設定を指定することができます。 このオプションはドキュメントに固有で、Outlook では使用できません。

1. **[ホーム]** タブの **[保護]** グループで、 **[保護]**  >  **[カスタム アクセス許可]** をクリックします。

    ![カスタムアクセス許可オプション](../media/custom-permissions-callout.png)
    
    **[カスタム アクセス許可]** が表示されない場合、管理者はお客様がこのオプションを使用することを許可していません。
    
    指定したカスタムのアクセス許可は、選択したラベルに対して管理者から定義されている保護設定を補足するのではなく、この設定に置き換わることに注意してください。  

2. **[Microsoft Azure Information Protection]** ダイアログ ボックスで、以下を指定します。

    - **カスタム アクセス許可で保護する**: こちらが選択されていて、カスタム アクセス許可を指定して適用できることを確認します。 このオプションをクリアしてカスタム アクセス許可を削除します。
    
    - **アクセス許可の選択**: 自分だけがファイルにアクセスできるようにファイルを保護するには、 **[Only for me (自分のみ)]** を選択します。 それ以外の場合は、ユーザーに付与するアクセス レベルを選択します。
    
    - **ユーザー、グループ、および組織の選択**: ファイルに対して選択したアクセス許可を持つユーザーを指定します。 組織内のユーザー全員について、組織で使用する完全なメール アドレス、グループ メール アドレス、ドメイン名を入力します。 
        
        アドレス帳アイコンを使用して、Outlook のアドレス帳からユーザーまたはグループを選択することもできます。
    
    - **[アクセスの有効期限]** : 指定したユーザーが、設定した日付の後に選択したファイルを開くことができないように、時間を区別するファイルに対してのみこのオプションを選択します。 自分は元のファイルを引き続き開くことができますが、(現在のタイム ゾーンで) 設定した日の深夜を過ぎた後は、他のユーザーはファイルを開くことができなくなります。

5. **[適用]** をクリックして、 **"カスタム アクセス許可が適用されました"** というメッセージが表示されるまで待ちます。 次に、 **[閉じる]** をクリックします。

### <a name="safely-sharing-by-email"></a>電子メールで安全に共有する

電子メールで Office ドキュメントを共有するとき、保護しているメールにドキュメントを添付できます。メールに適用されているものと同じ制約でドキュメントが自動的に保護されます。 

ただし、先にドキュメントを保護し、それからドキュメントをメールに添付することを推奨しています。 メール メッセージに機密情報が含まれている場合、メールも保護します。 メールに添付する前にドキュメントを保護することには、2 つの利点があります。

- メールで送信した後、ドキュメントを追跡し、必要であれば取り消すことができます。

- メール メッセージとは異なるアクセス許可をドキュメントに適用できます。

## <a name="using-file-explorer-to-classify-and-protect-files"></a>エクスプローラーを使用してファイルを分類および保護する

エクスプローラーを使用すると、1 つのファイル、複数のファイル、またはフォルダーをすばやく分類して保護することができます。 

フォルダーを選択すると、そのフォルダー内のすべてのファイルとサブフォルダーが設定された分類および保護のオプションで自動的に選択されます。 ただし、そのフォルダーまたはサブフォルダー内に作成した新しいファイルは、設定されたオプションで自動的に構成されません。

エクスプローラーを使用してファイルの分類と保護を行う場合、1 つまたは複数のラベルが淡色表示の場合、選択したファイルは分類をサポートしていません。 このようなファイルについては、管理者によってラベルが保護を適用するように構成された場合にのみ、ラベルを選択できます。 または、独自の保護設定を指定することができます。 

一部のファイルは、変更すると PC が動作しなくなる可能性があるため、分類と保護の対象から自動的に除外されます。 これらのファイルを選択することはできますが、除外されるフォルダーまたはファイルとしてスキップされます。 たとえば、実行可能ファイルや Windows フォルダーが含まれます。

管理者ガイドには、サポートされるファイルの種類と自動的に除外されるファイルとフォルダーの詳細な一覧が記載されています。「[File types supported by the Azure Information Protection client](client-admin-guide-file-types.md)」(Azure Information Protection クライアントでサポートされるファイルの種類) を参照してください。


### <a name="to-classify-and-protect-a-file-by-using-file-explorer"></a>エクスプローラーを使用してファイルを分類および保護するには

1. エクスプローラーで、1 つのファイル、複数のファイル、またはフォルダーを選択します。 右クリックして **[分類して保護する]** を選択します。 例 :
    
    ![Azure Information Protection を使用する場合のファイル エクスプローラーの右クリック オプション [分類して保護する]](../media/right-click-classify-protect-folder.png)

2. **[分類と保護 - Azure Information Protection]** ダイアログ ボックスで、Office アプリケーションでの操作と同様にラベルを使用し、管理者によって定義されたとおりに分類と保護を設定します。 

   - 選択できるラベルがない場合 (すべてのラベルが淡色表示されている場合): 選択したファイルは分類をサポートしていませんが、カスタム アクセス許可で保護できます (手順 3)。 例 :

     ![[分類と保護 - Azure Information Protection]** ダイアログ ボックスで使用できるラベルがない](../media/info-protect-dialog-labels-dimmed.png)
    
   - ラベルが表示されず、このダイアログ ボックスで **[Company pre-defined protection]** (会社の定義済み保護) のオプションは表示される場合、クライアントは[保護のみモード](client-protection-only-mode.md)で実行されています。 管理者が構成した保護を適用するには、テンプレートを選択します。独自の保護設定を指定するには **[カスタム アクセス許可]** を選択して手順 4 に進みます。
    
     ![[分類と保護 - Azure Information Protection]** ダイアログ ボックスにラベルがない](../media/info-protect-dialog-labels-protection-only.png)
    
3. 管理者から許可されている場合は、選択したラベルに対して管理者が含めた保護設定を使用するのではなく、独自の保護設定を指定することができます。 この操作を行うには、 **[カスタム アクセス許可で保護する]** 選択します。
    
    **[カスタム アクセス許可で保護する]** が表示されない場合、管理者はお客様がこのオプションを使用することを許可していません。
    
    指定したカスタムのアクセス許可は、選択したラベルに対して管理者から定義されている保護設定を補足するのではなく、この設定に置き換わります。  

4. カスタムのアクセス許可オプションを選択した場合は、次の項目を指定します。

   - **アクセス許可の選択**: 選択したファイルを保護する場合のユーザーのアクセス レベルを選択します。
    
   - **ユーザー、グループ、および組織の選択**: ファイルに対して選択したアクセス許可を持つユーザーを指定します。 組織内のユーザー全員について、組織で使用する完全なメール アドレス、グループ メール アドレス、ドメイン名を入力します。 
    
     あるいは、アドレス帳アイコンを使用して、Outlook のアドレス帳からユーザーまたはグループを選択できます。
        
   - **アクセスの有効期限**: ファイルの期間が限定されていて、設定した日付を過ぎた後は指定したユーザーがファイルを開けないようにする場合にのみ、このオプションを選択します。自分は元のファイルを引き続き開くことができますが、(使用中のタイム ゾーンで) 設定した日付の深夜を過ぎた後は、指定したユーザーはファイルを開くことができなくなります。
    
     この設定を Office 2010 アプリのカスタム アクセス許可を使用して構成していた場合、指定した有効期限の日付はこのダイアログ ボックスには表示されませんが、有効期限は依然として有効です。 これは Office 2010 で有効期限を構成していた場合にのみ発生する表示上の問題です。

5. **[適用]** をクリックし、 **"作業が終了しました"** というメッセージで結果が示されるまで待ちます。 次に、 **[閉じる]** をクリックします。

選択されたファイルは、指定した設定に従って分類および保護されます。 場合によっては (保護の追加によってファイル名の拡張子が変更される場合)、エクスプローラーの元のファイルが Azure Information Protection のロック アイコンの付いた新しいファイルに置き換えられます。 例 :

![Azure Information Protection のロック アイコンが付いた保護されたファイル](../media/Pfile.png)

分類と保護について考えが変わったり、後で設定を変更する必要がある場合は、新しい設定でこのプロセスを繰り返すだけです。

ファイルを電子メールで送信したり、別の場所に保存した場合にも、指定した分類と保護はファイルに設定されたままです。 ファイルを保護した場合は、ユーザーによる保護されたファイルの使用状況を追跡し、必要に応じてファイルへのアクセスを取り消すことができます。 詳細については、「[Azure Information Protection を使用して保護されたドキュメントを追跡および取り消す](client-track-revoke.md)」を参照してください。 


## <a name="other-instructions"></a>その他の手順
他の操作手順については、Azure Information Protection ユーザー ガイドを参照してください。

-   [作業内容](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>管理者向け追加情報    
**[Make the custom permissions option available to users]\(ユーザーがカスタム アクセス許可オプションを使用できるようにする\)** のポリシー設定を有効にする構成手順については、「[Azure Information Protection のポリシー設定を構成する](../configure-policy-settings.md)」を参照してください。

その他の構成手順: [Azure Information Protection ポリシーの構成](../configure-policy.md)

