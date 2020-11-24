---
title: Azure Information Protection の使用権限を構成する
description: Azure Information Protection の Rights Management 保護を使用してファイルまたは電子メールを保護するときに使用される特定の権限について説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 08/04/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
ms.reviewer: esaggese
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 74f141054d177ccabea88f6521ebb2ba6a930be5
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "95570575"
---
# <a name="configuring-usage-rights-for-azure-information-protection"></a>Azure Information Protection の使用権限を構成する

>*適用対象:[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

暗号化のために感度ラベルまたは保護テンプレートを構成する場合は、ユーザー、管理者、または構成済みのサービスによってラベルまたはテンプレートが選択されたときに自動的に適用される使用権限を選択します。 たとえば、Azure Portal では、使用権限の論理的なグループを構成するロールを選択することも、個別の権限を構成することもできます。 または、ユーザーが使用権限を選択して適用することもできます。

この記事では、使用しているアプリケーションに必要な使用権限を構成し、これらの権限がアプリケーションによって解釈されるように設計された方法を理解するのに役立ちます。 ただし、アプリケーションが権限を実装する方法によって異なる場合があるため、運用環境にデプロイする前に、ユーザーが動作を確認するために使用するアプリケーションについて、常にドキュメントを参照し、独自のテストを実行します。

> [!NOTE] 
> 完全を期すため、この記事には 2018 年 1 月 8 日に廃止された Azure クラシック ポータルの値も含まれています。

## <a name="usage-rights-and-descriptions"></a>使用権限と説明
次の表は、Rights Management でサポートされている使用権限と説明の一覧です。それらの使用方法と解釈方法も示します。 一覧では **共通名** を示しています。これは、通常、使用権限が表示されたり参照されたりするときに使われる名前であり、コード内で使用される単一ワード値 (**ポリシーでのエンコード** 値) よりもわかりやすい名前です。 

次の表に示します。

- **Api の定数または値** は、MSIPC api 呼び出しの SDK 名であり、使用権限を確認するアプリケーションを作成するとき、またはポリシーに使用権限を追加するときに使用されます。

- **ラベル管理センター** では、機密ラベルを構成する場所を示します。 Microsoft 365 コンプライアンスセンター、Microsoft 365 セキュリティセンター、または Office 365 セキュリティ & コンプライアンスセンターのいずれかになります。


|使用権限|説明|実装|
|-------------------------------|---------------------------|-----------------|
|共通名: **コンテンツの編集、編集** <br /><br />ポリシーでのエンコード: **DOCEDIT**|アプリケーション内のコンテンツの変更、再配置、書式設定、または並べ替えをユーザーに許可します。 編集済みのコピーを保存する権限は付与されません。<br /><br />Word では、バージョン [1807](/officeupdates/monthly-channel-2018#version-1807-july-25) 以降の Office 365 ProPlus を持っていない限り、**[変更の追跡]** をオンまたはオフにしたり、レビュー担当者として変更の追跡機能をすべて使用したりするには、この権限は十分ではありません。 代わりに、変更の追跡オプションをすべて使用するには、次の権限が必要です: **フル コントロール**。 |Office カスタム権限: **変更** と **フル コントロール** オプションの一部。 <br /><br />Azure クラシック ポータルでの名前: **コンテンツの編集**<br /><br />ラベル管理センターの名前と Azure portal: **コンテンツの編集、編集 (docedit)**<br /><br />AD RMS テンプレートでの名前: **編集** <br /><br />API の定数または値: 該当なし。|
|共通名: **保存** <br /><br />ポリシーでのエンコード: **EDIT**|ドキュメントを現在の場所に保存することをユーザーに許可します。<br /><br />Office アプリケーションでは、この権限により、ユーザーがドキュメントを変更してそれを新しい場所に保存することもできます。選択したファイル形式が Rights Management 保護をネイティブにサポートしている場合は、新しい名前でドキュメントが保存されます。 ファイル形式の制限により、ファイルから元の保護を削除することはできません。|Office カスタム権限: **変更** と **フル コントロール** オプションの一部。 <br /><br />Azure クラシック ポータルでの名前: **ファイルの保存**<br /><br />ラベル管理センターの名前と Azure portal: **保存 (編集)**<br /><br />AD RMS テンプレートでの名前: **保存** <br /><br />API の定数または値: `IPC_GENERIC_WRITE L"EDIT"`|
|共通名: **コメント** <br /><br />ポリシーでのエンコード: **COMMENT**|コンテンツに注釈やコメントを追加するオプションを有効にします。<br /><br />この権限は SDK で使用でき、Azure Information Protection と Windows PowerShell の RMS 保護モジュールでアドホック ポリシーとして使用できます。また、いくつかのソフトウェア ベンダーのアプリケーションに実装されています。 ただし、これは広く使用されておらず、Office アプリケーションではサポートされていません。|Office カスタム権限: 実装されていません。 <br /><br />Azure クラシック ポータルでの名前: 実装されていません。<br /><br />ラベル管理センターの名前と Azure portal: 実装されていません。<br /><br />AD RMS テンプレートでの名前: 実装されていません。 <br /><br />API の定数または値: `IPC_GENERIC_COMMENT L"COMMENT`|
|共通名: **名前を付けて保存、エクスポート** <br /><br />ポリシーでのエンコード: **EXPORT**|別のファイル名でコンテンツを保存するオプション (名前を付けて保存) を有効にします。 <br /><br />Azure Information Protection クライアントについては、ファイルを保護なしで保存し、新しい設定とアクセス許可で再保護することができます。 許可されているこれらの操作は、この権限を持つユーザーが保護されたドキュメントまたは電子メールから Azure Information Protection ラベルを変更または削除できることを意味します。 <br /><br />この権限は、アプリケーションでその他のエクスポート オプション (**[OneNote に送る]** など) を実行することもユーザーに許可します。|Office カスタム権限: **フル コントロール** オプションの一部。 <br /><br />Azure クラシック ポータルでの名前: **コンテンツのエクスポート (名前を付けて保存)** <br /><br />ラベル管理センターの名前と Azure portal: 名前を付け **て保存、エクスポート (エクスポート)**<br /><br />AD RMS テンプレートでの名前: **エクスポート (名前を付けて保存)** <br /><br />API の定数または値: `IPC_GENERIC_EXPORT L"EXPORT"`|
|共通名: **転送** <br /><br />ポリシーでのエンコード: **FORWARD**|電子メール メッセージの転送、**[宛先]**、**[CC]** 行への受信者の追加を行うオプションを有効にします。 この権限は、ドキュメントには適用されません。メール メッセージだけに適用されます。<br /><br />転送操作の一部として転送者が他のユーザーに権限を付与することは許可しません。 <br /><br />この権限を付与するときは、保護されたメール メッセージが添付ファイルとして転送されないように、**コンテンツの編集、編集** 権限 (共通名) と、さらに **保存** 権限 (共通名) も付与します。 これらの権限は、Outlook クライアントまたは Outlook Web アプリを利用する別の組織に電子メールを送信するときにも指定します。 または、 [オンボードコントロール](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy)を実装しているため Rights Management 保護の使用を除外している組織内のユーザーの場合。|Office カスタム権限: **転送不可** 標準ポリシーを使用すると拒否されます。<br /><br />Azure クラシック ポータルでの名前: **転送**<br /><br />ラベル管理センターに名前を付け、Azure portal: **転送 (転送)**<br /><br />AD RMS テンプレートでの名前: **転送** <br /><br />API の定数または値: `IPC_EMAIL_FORWARD L"FORWARD"`|
|共通名: **フル コントロール** <br /><br />ポリシーでのエンコード: **OWNER**|ドキュメントに対するすべての権限を付与します。利用可能なすべての操作を実行できます。<br /><br />ドキュメントの保護解除と再保護の能力も含まれます。 <br /><br />この使用権限は、[Rights Management 所有者](#rights-management-issuer-and-rights-management-owner)と同じではないことに注意してください。|Office カスタム権限: **フル コントロール** カスタム オプション。<br /><br />Azure クラシック ポータルでの名前: **フル コントロール**<br /><br />ラベル管理センターと Azure portal の名前: **フルコントロール (所有者)**<br /><br />AD RMS テンプレートでの名前: **フル コントロール** <br /><br />API の定数または値: `IPC_GENERIC_ALL L"OWNER"`|
|共通名: **印刷** <br /><br />ポリシーでのエンコード: **PRINT**|コンテンツを印刷するオプションを有効にします。|Office カスタム権限: カスタム アクセス許可の **コンテンツの印刷** オプション。 受信者単位の設定ではありません。<br /><br />Azure クラシック ポータルでの名前: **印刷**<br /><br />ラベル管理センターの名前と Azure portal: **印刷 (印刷)**<br /><br />AD RMS テンプレートでの名前: **印刷** <br /><br />API の定数または値: `IPC_GENERIC_PRINT L"PRINT"`|
|共通名: **返信** <br /><br />ポリシーでのエンコード: **REPLY**|メール クライアントの **[返信]** オプションを有効にします。ただし、**[宛先]** または **[CC]** 行に対する変更は許可しません。<br /><br />この権限を付与するときは、保護されたメール メッセージが添付ファイルとして転送されないように、**コンテンツの編集、編集** 権限 (共通名) と、さらに **保存** 権限 (共通名) も付与します。 これらの権限は、Outlook クライアントまたは Outlook Web アプリを利用する別の組織に電子メールを送信するときにも指定します。 または、 [オンボードコントロール](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy)を実装しているため Rights Management 保護の使用を除外している組織内のユーザーの場合。|Office カスタム権限: 該当なし。<br /><br />Azure クラシック ポータルでの名前: **返信**<br /><br />Azure Portal での名前: **返信 (REPLY)**<br /><br />AD RMS テンプレートでの名前: **返信** <br /><br />API の定数または値: `IPC_EMAIL_REPLY`|
|共通名: **全員に返信** <br /><br />ポリシーでのエンコード: **REPLYALL**|メール クライアントの **[全員に返信]** オプションを有効にします。ただし、**[宛先]** または **[CC]** 行への受信者の追加はユーザーに許可しません。<br /><br />この権限を付与するときは、保護されたメール メッセージが添付ファイルとして転送されないように、**コンテンツの編集、編集** 権限 (共通名) と、さらに **保存** 権限 (共通名) も付与します。 これらの権限は、Outlook クライアントまたは Outlook Web アプリを利用する別の組織に電子メールを送信するときにも指定します。 または、 [オンボードコントロール](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy)を実装しているため Rights Management 保護の使用を除外している組織内のユーザーの場合。|Office カスタム権限: 該当なし。<br /><br />Azure クラシック ポータルでの名前: **全員に返信**<br /><br />ラベル管理センターの名前と Azure portal: 全員に **返信 (全員に返信)**<br /><br />AD RMS テンプレートでの名前: **全員に返信** <br /><br />API の定数または値: `IPC_EMAIL_REPLYALL L"REPLYALL"`|
|共通名: **表示、開く、読み取り** <br /><br />ポリシーでのエンコード: **VIEW**|ドキュメントを開き、内容を表示することをユーザーに許可します。<br /><br /> Excel の場合、データを並べ替えるには、この権限は十分ではありません。次の権限が必要です: **コンテンツの編集、編集**。 Excel でデータをフィルター処理するには、次の 2 つの権限が必要です: **コンテンツの編集、編集** および **コピー**。|Office カスタム権限: **読み取り** カスタム ポリシー、**表示** オプション。<br /><br />Azure クラシック ポータルでの名前: **表示**<br /><br />ラベル管理センターの名前と Azure portal: **表示、開く、読み取り (ビュー)**<br /><br />AD RMS テンプレートでの名前: **読み取り** <br /><br />API の定数または値: `IPC_GENERIC_READ L"VIEW"`|
|共通名: **コピー** <br /><br />ポリシーでのエンコード: **EXTRACT**|ドキュメントのデータを同じドキュメントまたは別のドキュメントにコピーする (画面キャプチャを含む) オプションを有効にします。<br /><br />一部のアプリケーションでは、ドキュメント全体を保護されていない形式で保存することも許可されます。<br /><br />Skype for Business のような画面共有アプリケーションでは、プレゼンターは、保護されたドキュメントを正常に発表するために、この権限を持っている必要があります。 プレゼンターがこの権限を持っていない場合は、参加者はドキュメントを表示することができず、黒塗りで表示されます。|Office カスタム権限: **[閲覧の権限を持つユーザーが、コンテンツをコピーすることを許可する]** カスタム ポリシー オプション。<br /><br />Azure クラシック ポータルでの名前: **コンテンツのコピーと抽出**<br /><br />ラベル管理センターの名前と Azure portal: **コピー (EXTRACT)**<br /><br />AD RMS テンプレートでの名前: **抽出** <br /><br />API の定数または値: `IPC_GENERIC_EXTRACT L"EXTRACT"`|
|共通名: **権利の表示** <br /><br />ポリシーでのエンコード: **VIEWRIGHTSDATA**|ドキュメントに適用されるポリシーの表示をユーザーに許可します。 <br /><br /> Office アプリまたは Azure Information Protection クライアントではサポートされていません。|Office カスタム権限: 実装されていません。<br /><br />Azure クラシック ポータルでの名前: **割り当てられた権利の表示**<br /><br />ラベル管理センターに名前を付け、Azure portal: 権限を表示します **(VIEWRIGHTSDATA)**。<br /><br />AD RMS テンプレートでの名前: **権利の表示** <br /><br />API の定数または値: `IPC_READ_RIGHTS L"VIEWRIGHTSDATA"`|
|共通名: **権利の変更** <br /><br />ポリシーでのエンコード: **EDITRIGHTSDATA**|ドキュメントに適用されるポリシーの変更をユーザーに許可します。 保護の解除が含まれます。 <br /><br /> Office アプリまたは Azure Information Protection クライアントではサポートされていません。|Office カスタム権限: 実装されていません。<br /><br />Azure クラシック ポータルでの名前: **権利の変更**<br /><br />ラベル管理センターに名前を付け、Azure portal: **権利の編集 (EDITRIGHTSDATA)** します。<br /><br />AD RMS テンプレートでの名前: **権利の編集** <br /><br />API の定数または値: `PC_WRITE_RIGHTS L"EDITRIGHTSDATA"`|
|共通名: **マクロの許可** <br /><br />ポリシーでのエンコード: **OBJMODEL**|マクロを実行したり、その他のプログラムまたはリモートからドキュメントのコンテンツにアクセスしたりするオプションを有効にします。|Office カスタム権限: **[プログラムによるアクセスを許可]** カスタム ポリシー オプション。 受信者単位の設定ではありません。<br /><br />Azure クラシック ポータルでの名前: **マクロの許可**<br /><br />ラベル管理センターでの名前と Azure portal: **マクロの許可 (OBJMODEL)**<br /><br />AD RMS テンプレートでの名前: **マクロの許可** <br /><br />API の定数または値: 実装されていません。|

## <a name="rights-included-in-permissions-levels"></a>アクセス許可レベルに含まれる権限

一部のアプリケーションは、通常は一緒に使用される使用権限を選択しやすくするために、使用権限をまとめてアクセス許可レベルにグループ化します。 これらのアクセス許可レベルによって、複雑なレベルがユーザーからは見えなくなるため、役割ベースでオプションを選択できるようになります。  たとえば、**レビュー担当者** や **共同作成者** などがあります。 多くの場合、これらのオプションではユーザーに対して権限の概要が表示されますが、前の表に記載されているすべての権限が含まれるとは限りません。

これらのアクセス許可レベルの一覧、および含まれる使用権限の完全な一覧については、次の表を参照してください。 使用権限は、[共通名](#usage-rights-and-descriptions)で表示されています。

|アクセス許可レベル|アプリケーション|含まれる使用権限|
|---------------------|----------------|---------------------------------|
|Viewer|Azure クラシック ポータル <br /><br />Azure portal<br /><br />Windows 用 Azure Information Protection クライアント|表示、開く、読み取り、権利の表示、返信 [[1]](#footnote-1)、全員に返信 [[1]](#footnote-1)、マクロの許可 [[2]](#footnote-2)<br /><br />注: 電子メールの場合、電子メールの返信が添付ファイルではなく電子メール メッセージとして受信されるように、このアクセス許可レベルではなく、レビュー担当者を利用します。 レビュー担当者は、Outlook クライアントまたは Outlook Web アプリを利用する別の組織に電子メールを送信するときにも必要になります。 または、[オンボーディング コントロール](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy)を実装したために、Azure Rights Management サービスの使用対象から除外されている組織内のユーザーにも必要です。|
|レビュー担当者|Azure クラシック ポータル <br /><br />Azure portal<br /><br />Windows 用 Azure Information Protection クライアント|表示、開く、読み取り、保存、コンテンツの編集、編集、権利の表示、返信、全員に返信 [[3]](#footnote-3)、転送 [[3]](#footnote-3)、マクロの許可 [[2]](#footnote-2)|
|共同作成者|Azure クラシック ポータル <br /><br />Azure portal<br /><br />Windows 用 Azure Information Protection クライアント|表示、開く、読み取り、保存、コンテンツの編集、編集、コピー、権利の表示、マクロの許可、名前を付けて保存、エクスポート [[4]](#footnote-4)、印刷、返信 [[3]](#footnote-3)、全員に返信 [[3]](#footnote-3)、転送 [[3]](#footnote-3)|
|共同所有者|Azure クラシック ポータル <br /><br />Azure portal<br /><br />Windows 用 Azure Information Protection クライアント|表示、開く、読み取り、保存、コンテンツの編集、編集、コピー、権利の表示、権利の変更、マクロの許可、名前を付けて保存、エクスポート、印刷、返信 [[3]](#footnote-3)、全員に返信 [[3]](#footnote-3)、転送 [[3]](#footnote-3)、フル コントロール|

----

###### <a name="footnote-1"></a>脚注 1

ラベル管理センターまたは Azure portal には含まれません。

###### <a name="footnote-2"></a>脚注 2

Windows 用の Azure Information Protection クライアントの場合、この権限は Office アプリの Information Protection バーに必要です。

###### <a name="footnote-3"></a>脚注 3
Windows 用 Azure Information Protection クライアントには適用されません。

###### <a name="footnote-4"></a>脚注 4
ラベル管理センター、Azure portal、または Windows 用の Azure Information Protection クライアントには含まれません。

## <a name="rights-included-in-the-default-templates"></a>既定のテンプレートに含まれる権限
次の表は、既定のテンプレートを作成したときに含まれる使用権限の一覧です。 使用権限は、[共通名](#usage-rights-and-descriptions)で表示されています。

これらの既定のテンプレートは、サブスクリプションを購入したときに作成されます。名前と使用権限は、Azure portal と[PowerShell](/powershell/module/aipservice/set-aipservicetemplateproperty)を使用して[変更](configure-policy-templates.md)できます。 

|テンプレートの表示名|使用権限 (2017 年 10 月 6 日から現在)|使用権限 (2017 年 10 月 6 日より前)|
|----------------|--------------------|----------|
|\<*organization name> -社外秘、表示のみ * <br /><br />または<br /><br /> *非常に機密性の高い社外秘 \ すべての従業員*|表示、開く、読み取り、コピー、権利の表示、マクロの許可、印刷、転送、返信、全員に返信、保存、コンテンツの編集、編集|表示、開く、読み取り|
|\<*organization name>部外 <br /><br />または <br /><br />*社外秘 \ すべての従業員*|表示、開く、読み取り、名前を付けて保存、エクスポート、コピー、権利の表示、権利の変更、マクロの許可、印刷、転送、返信、全員に返信、保存、コンテンツの編集、編集、フル コントロール|表示、開く、読み取り、名前を付けて保存、エクスポート、コンテンツの編集、編集、権利の表示、マクロの許可、転送、返信、全員に返信|

## <a name="do-not-forward-option-for-emails"></a>電子メールの [転送不可] オプション

Exchange のクライアントとサービス (Outlook クライアント、Outlook on the web、Exchange メール フロー ルール、Exchange の DLP アクションなど) には、**[転送不可]** というメール用の追加の情報権限保護オプションがあります。 

このオプションは、ユーザー (および Exchange 管理者) には選択可能な既定の Rights Management テンプレートのように見えますが、**[転送不可]** はテンプレートではありません。 そのため、保護テンプレートを参照および管理するとき、Azure Portal には表示されません。 **[転送不可]** オプションは、ユーザーが電子メール受信者に動的に適用する使用権限の集合です。

**[転送不可]** オプションが電子メールに適用される場合、電子メールが暗号化され、受信者は認証される必要があります。 その結果、受信者はメールの転送、印刷、またはコピーを実行できなくなります。 たとえば、Outlook クライアントでは、[転送] ボタンが利用できなくなり、**[名前を付けて保存]** および **[印刷]** メニュー オプションが利用できなくなり、**[宛先]**、**[Cc]**、**[Bcc]** ボックスの受信者を追加したり、変更したりすることができなくなります。

メールに添付されている保護されていない [Office ドキュメント](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM)は、自動的に同じ制限を継承します。 これらのドキュメントに適用される使用権限は、**コンテンツの編集、編集**、**保存**、**表示、開く、読み取り** と **マクロの許可** です。 添付ファイルに別の使用権限を使用する場合または添付ファイルがこの継承された保護をサポートする Office ドキュメントでない場合、電子メールに添付する前に、ファイルを保護する必要があります。 それからファイルに必要な特定の使用権限を割り当てることができます。 

### <a name="difference-between-do-not-forward-and-not-granting-the-forward-usage-right"></a>転送不可と転送の使用権限を付与しないことの違い

**[転送不可]** オプションの適用と電子メールに **転送** 使用権限を与えないテンプレートの適用には重要な違いがあります。**[転送不可]** オプションの場合、元の電子メールでユーザーが選択した受信者に基づく、許可されたユーザーの動的なリストが使用されます。テンプレートの権限の場合、管理者が前もって指定した許可されたユーザーの静的なリストが使用されます。 違いは何でしょうか。 例を見てみましょう。 

あるユーザーがいくつかの情報をマーケティング部署の一部の人たちに電子メールで送信します。それ以外の人とこの情報を共有することは許されません。 権限 (表示、返信、保存) をマーケティング部署に限定するテンプレートで電子メールを保護するべきでしょうか。  それとも、**[転送不可]** オプションを選択するべきでしょうか。 いずれの場合でも、受信者は電子メールを転送できません。 

- テンプレートを適用した場合、受信者はマーケティング部署の他の人と情報を共有できる可能性があります。 たとえば、エクスプローラーを利用し、電子メールを共有の場所や USB ドライブにドラッグ アンド ドロップできます。 マーケティング部署の人で共有の場所や USB ドライブにアクセスできる人であれば、だれでも電子メールの情報を見ることができます。
 
- **[転送不可]** オプションを適用した場合、受信者は電子メールを別の場所に移すことができず、マーケティング部署の他の人と情報を共有することができません。 この場合、元の受信者 (と電子メールの作成者) だけが電子メールの情報を見ることができます。

> [!NOTE] 
> 送信者が選択した受信者だけに電子メールの情報の閲覧を許可することが重要である場合は、**[転送不可]** を使用してください。 送信者が選択した受信者に関係なく、管理者が前もって指定したユーザー グループに権限を制限する場合は、電子メールのテンプレートを使用します。

## <a name="encrypt-only-option-for-emails"></a>電子メールの暗号化のみオプション

Exchange Online で Office 365 Message Encryption の新機能を使用する場合、新しい電子メール オプション (**暗号化のみ**) を利用できます。

このオプションは、Exchange Online を使用するテナントに対して使用できます。また、web 上の Outlook で選択できます。また、メールフロールールの別の権利保護オプションとして、Office 365 の DLP Microsoft 365 [1804](/officeupdates/monthly-channel-2018#outlook-feature-updates-4) アクションとして、また [Azure RMS をサポートする Microsoft 365 アプリ](requirements-applications.md#windows-computers-for-information-rights-management-irm)を使用している場合は、1805の最小バージョンを選択できます。 Encrypt-Only オプションの詳細については、Office チームの次のブログ投稿のお知らせを参照してください。 [office 365 Message Encryption でのロールアウトのみを暗号化](https://aka.ms/omefeb2018)します。

このオプションが選択されると、電子メールが暗号化され、受信者は認証される必要があります。 すると、受信者には **名前を付けて保存、エクスポート** と **フル コントロール** を除くすべての使用権限が割り当てられます。 この使用権限の組み合わせは、保護を削除できないこと以外は、受信者には制限がないということです。 たとえば、受信者は電子メールをコピー、印刷、および転送することができます。 

同様に、既定では、メールに添付されている保護されていない [Office ドキュメント](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM)も同じアクセス許可を継承します。 これらのドキュメントは自動的に保護されます。これらをダウンロードしたら、受信者は Office アプリケーションから保存、編集、コピーおよび印刷することができます。 受信者が文書を保存する場合、新しい名前で保存できます。このとき、別の形式で保存することも可能です。 ただし、元の保護でドキュメントを保存できるよう、保護をサポートするファイル形式のみを使用できます。 添付ファイルに別の使用権限を使用する場合または添付ファイルがこの継承された保護をサポートする Office ドキュメントでない場合、電子メールに添付する前に、ファイルを保護する必要があります。 それからファイルに必要な特定の使用権限を割り当てることができます。

または、[Exchange Online PowerShell](/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/connect-to-exchange-online-powershell) で `Set-IRMConfiguration -DecryptAttachmentForEncryptOnly $true` を指定して、このドキュメントの保護継承を変更することができます。 ユーザーの認証後にドキュメントの元の保護を保持する必要がない場合は、この構成を使用します。 受信者が電子メール メッセージを開く際に、ドキュメントは保護されません。

元の保護を保持するために添付されたドキュメントが必要な場合は、「[Azure Information Protection を使用したセキュアなドキュメント コラボレーション](secure-collaboration-documents.md)」をご覧ください。

注: **DecryptAttachmentFromPortal** への参照が表示されている場合、このパラメーターは、 [Set irmconfiguration](/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration)では非推奨となりました。 このパラメーターを以前に設定したことがない場合は使用できません。

## <a name="automatically-encrypt-pdf-documents-with-exchange-online"></a>PDF ドキュメントを Exchange Online で自動的に暗号化する

Exchange Online で Office 365 Message Encryption の新機能を使用すると、暗号化された電子メールに添付されている場合、保護されていない PDF ドキュメントを自動的に暗号化することができます。 ドキュメントは、電子メールメッセージと同じ権限を継承します。 この構成を有効にするには、 [set-IRMConfiguration](/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration)を使用して **EnablePdfEncryption $True** を設定します。

ISO 規格の PDF 暗号化をサポートするリーダーがまだインストールされていない受信者は、 [Microsoft Information Protection をサポートする pdf リーダー](./rms-client/protected-pdf-readers.md)に記載されているいずれかのリーダーをインストールできます。 または、OME ポータルで、保護された PDF ドキュメントを受信者が読み取ることができます。

## <a name="rights-management-issuer-and-rights-management-owner"></a>Rights Management 発行者と Rights Management 所有者

ドキュメントまたは電子メールが Azure Rights Management サービスを使用して保護されている場合、そのコンテンツを保護するアカウントは自動的にそのコンテンツの Rights Management 発行者になります。 このアカウントは、[利用状況ログ](log-analyze-usage.md#how-to-interpret-your-usage-logs)の **発行者** フィールドに記録されます。 

Rights Management 発行者には、常にドキュメントまたは電子メールのフル コントロール使用権限が与えられます。さらに、次の操作が可能です。

- 保護設定に有効期限が含まれる場合、Rights Management 発行者はその日付の後でもドキュメントまたは電子メールを開き、編集できます。

- Rights Management 発行者は常にドキュメントまたは電子メールにオフラインでアクセスできます。

- Rights Management 発行者は取り消されたドキュメントも開くことができます。 

既定では、このアカウントはそのコンテンツの **Rights Management 所有者** でもあります。これは、ドキュメントまたは電子メールを作成したユーザーが保護を開始した場合です。 ただし、管理者またはサービスがユーザーの代わりにコンテンツを保護できるシナリオもあります。 例:

- 管理者がファイル共有のファイルを一括保護する: Azure AD の管理者アカウントがユーザーのためにドキュメントを保護します。

- Rights Management コネクタが Windows Server フォルダーの Office ドキュメントを保護する: RMS コネクタ用に作成された Azure AD のサービス プリンシパル アカウントがユーザーのためにドキュメントを保護します。

以上のシナリオでは、Rights Management 発行者は Azure Information Protection SDK または PowerShell を利用して Rights Management 所有者を別のアカウントに割り当てることができます。 たとえば、Azure Information Protection クライアントで [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) PowerShell コマンドレットを使用するとき、**OwnerEmail** パラメーターを指定し、Rights Management 所有者を別のアカウントに割り当てることができます。 

ユーザーの代わりに Rights Management 発行者が保護を行う場合、元のドキュメントまたは電子メールの所有者に Rights Management 所有者を割り当てることで、保護コンテンツに対し、保護を自分で開始した場合と同じレベルのコントロールを与えることができます。 

たとえば、印刷使用権限が含まれていないテンプレートで保護されていても、ドキュメントを作成したユーザーはそのドキュメントを印刷できます。 そのテンプレートで構成されているオフライン アクセス設定や有効期限に関係なく、このユーザーは常に自分のドキュメントにアクセスできます。 さらに、Rights Management 所有者にはフル コントロール使用権限が与えられるため、このユーザーはドキュメントを再保護し、追加のユーザー アクセスを付与することもできます (その時点で、ユーザーは Rights Management 発行者と Rights Management 所有者になります)。このユーザーは保護を解除することもできます。 ただし、ドキュメントを追跡し、取り消すことができるのは、Rights Management 発行者だけです。

ドキュメントまたは電子メールの Rights Management 所有者は、[利用状況ログ](log-analyze-usage.md#how-to-interpret-your-usage-logs)で **owner-email** フィールドに記録されます。

Rights Management 所有者と Windows ファイル システム所有者に依存関係はありません。 この 2 つは多くの場合は同じですが、別々にすることもできます (SDK または PowerShell を使用しなくても)。

## <a name="rights-management-use-license"></a>Rights Management の使用ライセンス

Azure Rights Management によって保護されたドキュメントまたは電子メールをユーザーが開くと、そのコンテンツに対する Rights Management の使用ライセンスがユーザーに付与されます。 この使用ライセンスは証明書であり、ドキュメントまたは電子メール メッセージに対するユーザーの使用権限、およびコンテンツを暗号化するために使用された暗号化キーが含まれています。 また、使用ライセンスには有効期日 (設定されている場合) および使用ライセンスの有効期間も含まれます。

ユーザーはコンテンツを開くために、有効な使用ライセンスと権利アカウント証明書 (RAC) 持つ必要があります。この証明書は、[ユーザー環境が初期化され](how-does-it-work.md#initializing-the-user-environment)て 31 日ごとに更新されたときに付与されます。

使用ライセンスの期間中、ユーザーはコンテンツについて再認証も再承認も行われません。 これにより、ユーザーはインターネットに接続しなくても、保護されたドキュメントまたは電子メールを引き続き開くことができます。 使用ライセンスの有効期限を過ぎると、次に保護されたドキュメントまたは電子メールにアクセスしたときに、ユーザーは再認証および再承認される必要があります。 

保護設定を定義したラベルまたはテンプレートによってドキュメントおよび電子メール メッセージが保護されている場合は、ラベルまたはテンプレート内でこれらの設定を変更することができ、コンテンツを再保護する必要はありません。 ユーザーが既にコンテンツにアクセスしている場合は、使用ライセンスの有効期限が過ぎた後で変更が有効になります。 ただし、ユーザーがカスタム アクセス許可 (ad hoc 権利ポリシーとも呼ばれる) を適用した場合、ドキュメントまたは電子メールが保護された後でこれらのアクセス許可を変更する必要があるときは、そのコンテンツを新しいアクセス許可で再度保護する必要があります。 電子メール メッセージのカスタム アクセス許可は、[転送不可] オプションで実装されます。

テナントの既定の使用ライセンス有効期間は30日です。この値を構成するには、PowerShell コマンドレット [AipServiceMaxUseLicenseValidityTime](/powershell/module/aipservice/set-aipservicemaxuselicensevaliditytime)を使用します。 ラベルまたはテンプレートを使用して保護を適用する場合は、より制限の厳しい設定を構成できます。

- Azure Portal で、ラベルまたはテンプレートを構成する場合は、使用ライセンスの有効期間として、**[オフライン アクセスの許可]** 設定の値が使用されます。 
    
    Azure Portal でこの設定を構成するための詳細とガイダンスについては、Rights Management の保護用にラベルを構成する方法について説明した記事の、「[保護の設定に関する情報](configure-policy-protection.md#information-about-the-protection-settings)」の表をご覧ください。

- PowerShell を使用してテンプレートを構成する場合、使用ライセンスの有効期間は、 *LicenseValidityDuration* パラメーターの値を設定します。これは、 [Set AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty) および [Add-aipservicetemplate](/powershell/module/aipservice/add-aipservicetemplate) コマンドレットです。
    
    PowerShell を使用してこの設定を構成するための詳細とガイダンスについては、各コマンドレットのヘルプを参照してください。

## <a name="see-also"></a>参照
[Azure Information Protection のテンプレートを構成して管理する](configure-policy-templates.md)

[Azure Information Protection と、検出サービスまたはデータ復旧用のスーパー ユーザーの構成](configure-super-users.md)