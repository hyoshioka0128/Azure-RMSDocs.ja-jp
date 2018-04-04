---
title: RMS で保護されたファイルを RMS 共有アプリケーションで開く - AIP
description: 保護されたファイルを表示して使用する手順です。Rights Management (RMS) 共有アプリケーションがインストールされている必要があります。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/18/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e5fa4666-6906-405a-9e0c-2c52d4cd27c8
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 393db5da6f2a563b073b071e873a8c5d555a76e6
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="view-and-use-files-that-have-been-protected-by-rights-management"></a>Rights Management によって保護されたファイルを表示して使用する

>*適用対象: Active Directory Rights Management サービス[、Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、Windows 10、Windows 7 SP1、Windows 8、Windows 8.1*

[Rights Management (RMS) 共有アプリケーションがコンピューターにインストールされている場合は](install-sharing-app.md)、ダブルクリックするだけで保護されたファイルを表示できます。 ファイルは電子メール メッセージの添付ファイルの場合もあれば、ファイル エクスプローラーで表示されるファイルの場合もあります。

> [!NOTE]
> 保護されたファイルを表示するには、先にユーザーがファイルを表示する権限を持つことを Rights Management サービスが確認する必要があります。それには、ユーザー名とパスワードを調べます。 場合によっては、ユーザー名とパスワードがキャッシュに格納されていて、資格情報の入力を求められないことがあります。 それ以外の場合は、資格情報を指定するように求められます。
>
> 組織が Azure Information Protection または AD RMS を使用していない場合は、RMS で保護されたファイルを開けるように資格情報を受け付ける無料のアカウントを要求できます。
>
> -   このアカウントを要求するには、リンクをクリックして、 [個人用 RMS](http://go.microsoft.com/fwlink/?LinkId=309469)を要求します。
>
>     サインアップするときは、個人の電子メール アドレスではなく会社の電子メール アドレスを使用してください。 電子メールで保護された添付ファイルを受け取ったためにサインアップする場合は、その電子メール メッセージの送信に使用されたものと同じ電子メール アドレスを使用します。
> -   詳細については、「[個人用 RMS と Microsoft Azure Rights Management](../understand-explore/rms-for-individuals.md)」を参照してください。

## <a name="to-view-a-protected-file"></a>保護されたファイルを表示するには
ファイル エクスプローラーまたは添付ファイルを含む電子メール メッセージを使用して、保護されたファイルをダブルクリックし、要求された場合は資格情報を入力します。

ファイル名拡張子が異なる 2 つのバージョンのファイルが表示される場合、拡張子が .ppdf のファイルは、他のファイルが開かない場合にのみ開いてください。 .ppdf バージョンを開くことができない場合は、最初に [RMS 共有アプリケーション](install-sharing-app.md)をインストールします。このアプリケーションは、.ppdf ファイル名拡張子を持つファイルを開く方法を認識しています。

> [!NOTE]
> 詳細については、「[自動的に作成される .ppdf ファイルとは](sharing-app-dialog-box.md#whats-the-ppdf-file-thats-automatically-created)」を参照してください。

ファイルを開く方法はファイルが保護された方法によって異なり、ファイルが保護された方法はファイル名拡張子を見るとわかります。 いずれの場合も、ファイルを開くと監査される場合があり、保護されている限り監査された状態のままになります。 さらに、ファイルが電子メールの添付ファイルとして送信された場合、ファイルを開くたびに送信者に電子メールで通知される可能性があります。

- **ファイル名拡張子*が .pfile*である**

    このファイルは一般的に保護されています。

    ファイルを開くと、共有アプリケーションから **[保護されたファイル]** ダイアログ ボックスが表示され、そのファイルを保護したユーザー、および共同所有者のアクセス許可に従うことを期待されていることが示されます。 **[開く]** をクリックしてファイルを読み取ります。

    ![RMS 共有アプリケーションの使用時に電子メールで共有される pfile のダイアログ ボックス](../media/ADRMS_MSRMSApp_PfilePermission.png)

- **ファイル名拡張子が *.ppdf* か、ファイルが保護されたテキストまたは画像ファイル (*.ptxt*、*.pjpg* など) である**

    ファイルは、読み取り専用コピーとしてネイティブに保護されています。

    ファイルは、RMS 共有アプリケーションとともにインストールされるビューアーを使用して開きます。 このファイルは、別の場所に保存したり、名前を変更した場合でも、読み取り専用です。

- **その他のファイル名拡張子を持つファイル**

    ファイルは、ネイティブに保護されています。

    ファイルは元のファイル名拡張子に関連付けられているアプリケーションを使用して開き、ファイルの先頭に制限バナーが表示されます。 バナーには、ファイルに適用されるアクセス許可またはファイルを表示するためのリンクが表示される可能性があります。 たとえば、次が表示される可能性があります。ファイルとそのファイルにアクセスできるユーザーに適用されている実際のアクセス許可を確認するには、ここで **[現在、アクセスが制限されています]** をクリックします。

    ![ファイル保護時に制限されるアクセス バナー](../media/ADRMS_MSRMSApp_RestrictedAccess.png)



Rights Management サービスでサポートされるファイル名拡張子の完全な一覧については、「[Rights Management 共有アプリケーション管理者ガイド](sharing-app-admin-guide.md)」の「[サポートされているファイルの種類とファイル名拡張子](sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions)」セクションを参照してください。 ファイル名拡張子が一覧にない場合は、Web 検索を使用して、別のアプリケーションでサポートされているファイル名拡張子であるかどうかを確認します。

## <a name="to-use-files-that-have-been-protected-for-example-edit-and-print-the-file"></a>保護されているファイルを使用するには (ファイルを編集して印刷する場合など)
保護されたファイルを開いた後、読み取り以外にも編集、コピー、印刷などを行う場合は、ファイル名拡張子に応じて次の手順に従います。

- **ファイル名拡張子*が .pfile*である**

    開いているファイルを保存し、使用するアプリケーションに関連付けられている新しいファイル名拡張子を付けます。

    たとえば、ファイルがファイル名 document.vsdx.pfile を使用して保護された場合、ファイルを表示し、ファイル エクスプローラーで document.vsdx としてファイルを保存します。

    新しいファイルは保護されていません。 ファイルを保護する場合は、手動で行う必要があります。 手順については、「[Rights Management 共有アプリケーションを使用して、デバイス上のファイルを保護する (インプレースの保護)](sharing-app-protect-in-place.md)」を参照してください。

- **ファイル名拡張子が *.ppdf* か、ファイルが保護されたテキストまたは画像ファイル (*.ptxt*、*.pjpg* など) である**

    ファイルを表示することだけができ、ファイルの名前変更または移動を行っても、ファイルの保護は維持されます。

- **その他のファイル名拡張子を持つファイル**

    これらのファイルを使用するには、Rights Management 保護を認識するアプリケーションがデバイスに必要です。 これらのアプリケーションは RMS 対応アプリケーションと呼ばれます。 Office 2016、Office 2013、および Office 2010 のアプリケーション (Word、Excel、PowerPoint、Outlook など) は、Rights Management 対応アプリケーションの例です。 ただし、他のソフトウェア会社のアプリケーションやユーザー独自の基幹業務アプリケーションなど、Microsoft 以外のアプリケーションも、Rights Management 対応である場合があります。

    Rights Management 対応のアプリケーションは、他の Rights Management 対応アプリケーションによって保護されているファイルを開く方法を認識しています。 また、Rights Management 対応アプリケーションは、ユーザーがファイルを編集したり、別のファイル名や別の場所に保存したりしても、ファイルに適用された保護を維持します。 Rights Management 対応アプリケーションを使用すると、ユーザーはファイルに現在適用されているアクセス許可に従ってファイルを使用できます。ユーザーがファイルを使用するためのアクセス許可を持っている場合、ファイルを使用できます。 たとえば、ファイルを編集できても印刷はできません。


## <a name="examples-and-other-instructions"></a>例とその他の説明
Rights Management 共有アプリケーションの使用方法の例と操作手順については、Rights Management 共有アプリケーション ユーザー ガイドの次のセクションをご覧ください。

-   [RMS 共有アプリケーションの使用例](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [作業内容](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>参照
[Rights Management 共有アプリケーション ユーザー ガイド](sharing-app-user-guide.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]