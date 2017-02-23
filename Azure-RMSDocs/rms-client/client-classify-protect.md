---
title: "Azure Information Protection を使用してファイルや電子メールを分類して保護する | Azure Information Protection"
description: "ドキュメントや電子メールを分類して保護する方法の手順です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 75268245-6f14-4218-b904-202f63fb3ce6
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 335da7ca2fd37140cb1a52ca354b571ec822ff49
ms.openlocfilehash: ab9105b7d83b0cddee80b7c60e78ef18d54992d7


---

# <a name="classify-and-protect-a-file-or-email-by-using-azure-information-protection"></a>Azure Information Protection を使用してファイルや電子メールを分類して保護する

>*適用対象: Active Directory Rights Management サービス、Azure Information Protection、Windows 10、Windows 8.1、Windows 8、Windows 7 SP1*

Office のデスクトップ アプリ (**Word**、**Excel**、**PowerPoint**、**Outlook**) でドキュメントや電子メールを作成したり編集すると、分類と保護が簡単になります。 

ただし、**エクスプローラー**を使用してファイルの分類と保護を行うこともできます。エクスプローラーは、その他のファイルの種類をサポートし、複数のファイルを一度に分類して保護するための便利な方法です。 この方法は、Office ドキュメント、PDF ファイル、テキスト ファイル、画像ファイルなどさまざまなファイルの保護をサポートしています。 

### <a name="safely-share-a-file-with-people-outside-your-organization"></a>組織外の相手と安全にファイルを共有する

保護されているファイルは、他のユーザーと安全に共有できます。 たとえば、ファイルを電子メールに添付したり、SharePoint サイトから招待状を送信したりすることができます。

組織外の相手とファイルをよく共有する場合、ユーザーがその相手に読み取りを許可する保護を設定できるように、管理者がラベルを構成することができます。 また、ファイルを共有する前に、[エクスプローラーを使用してファイルにカスタム アクセス許可を設定する](#using-file-explorer-to-classify-and-protect-files)こともできます。 

カスタム アクセス許可を設定し、内部利用向けにファイルが既に保護されている場合、まずそのファイルのコピーを作成します。 このコピーを使用してカスタム アクセス許可を設定します。  

カスタム アクセス許可でファイルを保護する場合は、標準の共有メカニズムを使用してファイルを共有します。 保護されたファイルを初めて受け取る共有相手の場合は、必要に応じて相手に表示手順を説明します。 このような相手には、「**このファイルは Microsoft Azure Information Protection で保護されています。初めて利用する場合は、[こちらの手順](https://aka.ms/rms-signup)を参照してください**」というメッセージをコピーして貼り付けることをお勧めします。


## <a name="using-office-apps-to-classify-and-protect-your-documents-and-emails"></a>Office アプリを使用してドキュメントや電子メールを分類して保護する

Azure Information Protection バーを使用して、構成されているラベルを&1; つ選択します。 

たとえば、次の図は、**[秘密度]** が **[未設定]** のため、ドキュメントにまだラベルが設定されていないことを示します。 [内部] などのラベルを設定するには、**[内部]** をクリックします。 現在のドキュメントや電子メールに適用するラベルがわからない場合は、ラベルのツールヒントで、各ラベルの詳細と適用する場合を参照してください。

![Azure Information Protection バーの例](../media/info-protect-bar-not-set-callout.png)

ラベルがドキュメントに既に適用され、ラベルを変更する場合は、別のラベルを選択できます。 ラベルがバーに表示されない場合は、現在のラベル値の横にある **[ラベルの編集]** アイコンをクリックします。

ラベルの手動選択に加え、次の方法でラベルを適用することもできます。

- 管理者が既定のラベルを構成済み。そのまま使用するか、変更することができます。

- 機密データが検出された場合に特定のラベルを選択するように推奨するプロンプトを管理者が構成済み。 推奨を受け入れる (ラベルが適用される) か、拒否することができます (推奨されたラベルが適用されない)。

### <a name="exceptions-for-the-azure-information-protection-bar"></a>Azure Information Protection バーの例外 

##### <a name="dont-see-this-information-protection-bar-in-your-office-apps"></a>お使いの Office アプリでこの Information Protection バーが表示されない場合

- Azure Information Protection クライアントが[インストール](install-client-app.md)されていないか、クライアントが[保護のみモード](client-protection-only-mode.md)で実行されている可能性があります。
 
##### <a name="is-the-label-that-you-expect-to-see-not-displayed-on-the-bar"></a>表示されるはずのラベルがバーに表示されない場合 

- 管理者が新しいラベルを構成したばかりの場合は、すべてのインスタンスの Office アプリを終了してから、開き直します。 この操作で、ラベルの変更が確認されます。

- 存在しないラベルで保護を適用すると、Rights Management 保護の適用をサポートしていない Office のエディションになる可能性があります。 これを確認するには、**[保護]** > **[ヘルプとフィードバック]** をクリックし、**[クライアント ステータス]** セクションに **"This client is not licensed for Office Professional Plus"** (このクライアントには Office Professional Plus のライセンスがありません) というメッセージが表示されているかどうかを確認します。 

- 自分のアカウントを含まない範囲のポリシーのラベルである可能性があります。 ヘルプ デスクまたは管理者に問い合わせてください。

### <a name="keyboard-shortcuts-for-the-azure-information-protection-bar"></a>Azure Information Protection バーのショートカット キー

キーボード ショートカットを使用して、Azure Information Protection バーにアクセスするには、次のキーの組み合わせを使用します:

- **Ctrl** + **Shift** + **~** キーを押します。 

次に、Tab キーを使用してバーのラベルと他のコントロール (**[ラベルの非表示]** アイコンと **[ラベルの削除]** アイコン) を選択し、Enter キーで選択します。

## <a name="using-file-explorer-to-classify-and-protect-files"></a>エクスプローラーを使用してファイルを分類および保護する

エクスプローラーを使用すると、1 つのファイル、複数のファイル、またはフォルダーをすばやく分類して保護することができます。 

フォルダーを選択すると、そのフォルダー内のすべてのファイルとサブフォルダーが設定された分類および保護のオプションで自動的に選択されます。 ただし、そのフォルダーまたはサブフォルダー内に作成した新しいファイルは、設定されたオプションで自動的に構成されません。

エクスプローラーを使用してファイルの分類と保護を行う場合、1 つまたは複数のラベルが淡色表示の場合、選択したファイルは分類をサポートしていません。 このようなファイルについては、管理者によってラベルが保護を適用するように構成された場合にのみ、ラベルを選択できます。 または、独自の保護設定を指定することができます。 

一部のファイルは、変更すると PC が動作しなくなる可能性があるため、分類と保護の対象から自動的に除外されます。 これらのファイルを選択することはできますが、除外されるフォルダーまたはファイルとしてスキップされます。 たとえば、実行可能ファイルや Windows フォルダーが含まれます。

管理者ガイドには、サポートされるファイルの種類と自動的に除外されるファイルとフォルダーの詳細な一覧が記載されています。「[File types supported by the Azure Information Protection client](client-admin-guide-file-types.md)」(Azure Information Protection クライアントでサポートされるファイルの種類) を参照してください。


### <a name="to-classify-and-protect-a-file-by-using-file-explorer"></a>エクスプローラーを使用してファイルを分類および保護するには

1. エクスプローラーで、1 つのファイル、複数のファイル、またはフォルダーを選択します。 右クリックして **[分類して保護する]** を選択します。 たとえば、
    
    ![Azure Information Protection を使用する場合のファイル エクスプローラーの右クリック オプション [分類して保護する]](../media/right-click-classify-protect-folder.png)

2. **[分類と保護 - Azure Information Protection]** ダイアログ ボックスで、Office アプリケーションでの操作と同様にラベルを使用し、管理者によって定義されたとおりに分類と保護を設定します。 

    - 選択できるラベルがない場合 (すべてのラベルが淡色表示されている場合): 選択したファイルは分類をサポートしていませんが、カスタム アクセス許可で保護できます (手順 3)。 たとえば、

    ![[分類と保護 - Azure Information Protection]** ダイアログ ボックスで使用できるラベルがない](../media/info-protect-dialog-labels-dimmed.png)
    
    - ラベルが表示されず、このダイアログ ボックスで **[Company pre-defined protection]** (会社の定義済み保護) のオプションは表示される場合、クライアントは[保護のみモード](client-protection-only-mode.md)で実行されています。 管理者が構成した保護を適用するには、テンプレートを選択します。独自の保護設定を指定するには **[カスタム アクセス許可]** を選択して手順 4 に進みます。
    
    ![[分類と保護 - Azure Information Protection]** ダイアログ ボックスにラベルがない](../media/info-protect-dialog-labels-protection-only.png)
    
3. 選択したラベルに対し管理者から指定されている保護設定を使用するのではなく、独自の保護設定を指定する場合は、**[Protect with custom permissions] (カスタムのアクセス許可による保護)** を選択します。
    
    指定したカスタムのアクセス許可は、選択したラベルに対して管理者から定義されている保護設定を補足するのではなく、この設定に置き換わります。  

4. カスタムのアクセス許可オプションを選択した場合は、次の項目を指定します。

    - **アクセス許可の選択**: 選択したファイルを保護する場合のユーザーのアクセス レベルを選択します。
    
    - **ユーザーの選択**: ファイルに対して選択したアクセス許可を持つユーザーを指定します。 組織内のユーザーやグループについては、アドレス帳を使用して検索と選択ができます。 別の組織のユーザーについては、完全なメール アドレスを指定する必要があります。 個人用のメールアドレスは現在サポートされていないため、仕事用のメール アドレスを使用してください。
        
    - **アクセスの有効期限**: ファイルの期間が限定されていて、指定された日付を過ぎた後は指定されたユーザーがファイルを開けないようにする場合にのみ、このオプションを選択します。 自分は元のファイルを引き続き開くことができますが、(使用中のタイム ゾーンで) 選択した日付の深夜を過ぎた後は、他のユーザーはファイルを開くことができなくなります。

5. **[適用]** をクリックし、**"作業が終了しました"** というメッセージで結果が示されるまで待ちます。 次に、 **[閉じる]**をクリックします。

選択されたファイルは、指定した設定に従って分類および保護されます。 場合によっては (保護の追加によってファイル名の拡張子が変更される場合)、エクスプローラーの元のファイルが Azure Information Protection のロック アイコンの付いた新しいファイルに置き換えられます。 たとえば、

![Azure Information Protection のロック アイコンが付いた保護されたファイル](../media/Pfile.png)

分類と保護について考えが変わったり、後で設定を変更する必要がある場合は、新しい設定でこのプロセスを繰り返すだけです。

ファイルを電子メールで送信したり、別の場所に保存した場合にも、指定した分類と保護はファイルに設定されたままです。 ファイルを保護した場合は、ユーザーによる保護されたファイルの使用状況を追跡し、必要に応じてファイルへのアクセスを取り消すことができます。 詳細については、「[Azure Information Protection を使用して保護されたドキュメントを追跡および取り消す](client-track-revoke.md)」を参照してください。 


## <a name="other-instructions"></a>その他の手順
他の操作手順については、Azure Information Protection ユーザー ガイドを参照してください。

-   [作業内容](client-user-guide.md#what-do-you-want-to-do)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]



<!--HONumber=Feb17_HO2-->


