---
title: RMS 共有アプリケーションを使用したインプレースの保護 - AIP
description: コンピューター、サーバー、または別のストレージ デバイスにファイルを安全に格納する方法についての手順です。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 33920329-5247-4f6c-8651-6227afb4a1fa
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 0d819fd242e57402a790e9acb40ffa48eeb701b4
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
ms.locfileid: "30206062"
---
# <a name="protect-a-file-on-a-device-protect-in-place-by-using-the-rights-management-sharing-application"></a>Rights Management 共有アプリケーションを使用して、デバイス上のファイルを保護する (インプレースの保護)

>*適用対象: Active Directory Rights Management サービス[、Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*

インプレースのファイルを保護する場合は、元の保護されていないファイルを置き換えます。 次に、その場所にファイルを残したまま別のフォルダーやデバイスにコピーするか、ファイルのあるフォルダーを共有すると、ファイルは保護されたままになります。 エクスプローラーまたは Office アプリケーションから直接、電子メールで保護されたファイルを共有することをお勧めしますが、保護されたファイルを電子メール メッセージに添付することもできます (「[Rights Management 共有アプリケーションを使用して、電子メールで共有するファイルを保護する](sharing-app-protect-by-email.md)」を参照してください)。

> [!TIP]
> ファイルを保護しようとするとエラーが表示される場合は、「 [Windows 用 Microsoft Rights Management 共有アプリケーションの FAQ](http://go.microsoft.com/fwlink/?LinkId=303971)」をご覧ください。

## <a name="to-protect-a-file-on-a-device-protect-in-place"></a>デバイス上のファイルを保護するには (インプレースの保護)

1.  エクスプ ローラーで、保護するファイルを選びます。 右クリックして **[RMS による保護]** を選択し、**[Protect in-place]** (保護済み) をクリックします。 次に例を示します。

    ![[保護済み] メニュー オプション](../media/ADRMS_MSRMSApp_SP_CompanyDefined.png)

    > [!NOTE]
    > **[RMS による保護]** オプションが表示されない場合は、RMS 共有アプリケーションがコンピューターにインストールされていないか、コンピューターを再起動してインストールを完了させる必要がある場合があります。 RMS 共有アプリケーションをインストールする方法の詳細については、「[Rights Management 共有アプリケーションをダウンロードしてインストールする](install-sharing-app.md)」を参照してください。

2.  以下のいずれかを実行します。

    -   ポリシー テンプレートを選びます。これらは定義済みのアクセス許可で、通常、組織のユーザーに対してアクセスと使用を制限します。 たとえば、組織名が "Contoso, Ltd" の場合、"**Contoso, Ltd - 社外秘、表示のみ**" となります。 初めてこのコンピューターでファイルを保護する場合は、まず **[会社定義の保護]** を選び、テンプレートをダウンロードする必要があります。

        次回 **[Protect in-place]** (保護済み) オプションをクリックすると、最大 10 個のテンプレートが表示されて選択できます。 使用可能なテンプレートが 10 個よりも多く、その中に使用したいテンプレートが表示されていない場合は、**[会社定義の保護]** をクリックして、すべてのテンプレートをダウンロードして表示します。

        ポリシー テンプレートを選ぶと、複数のファイルとフォルダーも保護できます。 1 つのフォルダーを選ぶと、そのフォルダー内のすべてのファイルが自動的に選択されて保護されますが、そのフォルダー内に新たに作成したファイルは自動的に保護されません。

    -   **[カスタム アクセス許可]** を選びます。テンプレートで必要なレベルの保護を指定できない場合や、保護オプションを自分で明示的に設定する場合は、このオプションを選びます。 [[保護の追加] ダイアログ ボックス](sharing-app-dialog-box.md)で、このファイルに必要なオプションを指定し、**[適用]** をクリックします。

3.  ファイルが保護されていることを確認するダイアログ ボックスがすぐに表示されると、エクスプローラーにフォーカスが戻ります。 選んだファイルやファイルが保護されるようになりました。 場合によっては (保護の追加によってファイル名の拡張子が変更される場合)、エクスプローラーの元のファイルが Rights Management の保護のロック アイコンの付いた新しいファイルに置き換えられます。 次に例を示します。

    ![RMS 共有アプリケーションのロック アイコン付き保護ファイル](../media/ADRMS_MSRMSApp_Pfile.png)

アクセス許可を変更する場合は、単にファイルを再び保護します。

後でファイルから保護を削除する必要がある場合は、「[Rights Management 共有アプリケーションの使用によるファイルからの保護の削除](sharing-app-remove-protection.md)」を参照してください。

## <a name="examples-and-other-instructions"></a>例とその他の説明
Rights Management 共有アプリケーションの使用方法の例と操作手順については、Rights Management 共有アプリケーション ユーザー ガイドの次のセクションをご覧ください。

-   [RMS 共有アプリケーションの使用例](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [作業内容](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>参照
[Rights Management 共有アプリケーション ユーザー ガイド](sharing-app-user-guide.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]