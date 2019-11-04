---
title: Azure Information Protection の使用権限を構成する
description: Azure Information Protection の Rights Management 保護を使用してファイルまたは電子メールを保護するときに使用される特定の権限について説明します。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/04/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
ms.reviewer: esaggese
ms.subservice: azurerms
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 8df8af6462a1e574186f096c919b070d4c7b6812
ms.sourcegitcommit: fbd1834eaacb17857e59421d7be0942a9a0eefb2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2019
ms.locfileid: "73444929"
---
# <a name="configuring-usage-rights-for-azure-information-protection"></a>Azure Information Protection の使用権限を構成する

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、[Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Azure Information Protection を使用してファイルまたは電子メールに対して Rights Management 保護を設定し、テンプレートを使用しない場合は、使用権限を自分で構成する必要があります。 さらに、保護するテンプレートまたはラベルを構成するときに、ユーザー、管理者、または構成されたサービスによってテンプレートまたはラベルが選択されたときに自動的に適用される使用権限を選択します。 たとえば、Azure Portal では、使用権限の論理的なグループを構成するロールを選ぶことも、個別の権限を構成することもできます。

この記事では、使用しているアプリケーションに対して必要な使用権限を構成する際に役立つ情報を提供すると共に、それらの権限がアプリケーションによってどのように解釈されるのかを説明します。

> [!NOTE] 
> 完全を期すため、この記事には 2018 年 1 月 8 日に廃止された Azure クラシック ポータルの値が含まれています。
>
> 新しいポータルへの移行については「[Azure クラシック ポータルで行っていたタスク](migrate-portal.md)」を参照してください。

## <a name="usage-rights-and-descriptions"></a>使用権限と説明
次の表では、Rights Management がサポートする使用権限を一覧表示して説明します。さらに、これらを使用し、解釈する方法も示します。 これらの権限は、表示または参照される使用権限がどのように表示される可能性があるかを示す**共通名**によって一覧表示されます。通常、コード内で使用される単一ワード値 (**ポリシーでのエンコード**の値) のより親しみやすいバージョンとして表示されます。 

**API の定数または値**は、MSIPC API 呼び出しの SDK 名であり、使用権限があるかどうかを確認したり、ポリシーに使用権限を追加したりする RMS 対応アプリケーションを記述するときに使用されます。


|使用権限|[説明]|実装|
|-------------------------------|---------------------------|-----------------|
|共通名: **コンテンツの編集、編集** <br /><br />ポリシーでのエンコード: **DOCEDIT**|アプリケーション内のコンテンツの変更、再配置、書式設定、または並べ替えをユーザーに許可します。 編集済みのコピーを保存する権限は付与されません。<br /><br />Word では、バージョン [1807](https://docs.microsoft.com/officeupdates/monthly-channel-2018#version-1807-july-25) 以降の Office 365 ProPlus を持っていない限り、 **[変更の追跡]** をオンまたはオフにしたり、レビュー担当者として変更の追跡機能をすべて使用したりするには、この権限は十分ではありません。 代わりに、変更の追跡オプションをすべて使用するには、次の権限が必要です: **フル コントロール**。 |Office カスタム権限: **変更**と**フル コントロール** オプションの一部。 <br /><br />Azure クラシック ポータルでの名前: **コンテンツの編集**<br /><br />Azure Portal での名前: **コンテンツの編集、編集 (DOCEDIT)**<br /><br />AD RMS テンプレートでの名前: **編集** <br /><br />API の定数または値: 該当なし。|
|共通名: **保存** <br /><br />ポリシーでのエンコード: **EDIT**|ドキュメントを現在の場所に保存することをユーザーに許可します。<br /><br />Office アプリケーションでは、この権限により、ユーザーがドキュメントを変更してそれを新しい場所に保存することもできます。選択したファイル形式が Rights Management 保護をネイティブにサポートしている場合は、新しい名前でドキュメントが保存されます。 ファイル形式の制限により、ファイルから元の保護を削除することはできません。|Office カスタム権限: **変更**と**フル コントロール** オプションの一部。 <br /><br />Azure クラシック ポータルでの名前: **ファイルの保存**<br /><br />Azure Portal での名前: **保存 (EDIT)**<br /><br />AD RMS テンプレートでの名前: **保存** <br /><br />API の定数または値: `IPC_GENERIC_WRITE L"EDIT"`|
|共通名: **コメント** <br /><br />ポリシーでのエンコード: **COMMENT**|コンテンツに注釈やコメントを追加するオプションを有効にします。<br /><br />この権限は SDK で使用でき、Azure Information Protection と Windows PowerShell の RMS 保護モジュールでアドホック ポリシーとして使用できます。また、いくつかのソフトウェア ベンダーのアプリケーションに実装されています。 ただし広く使用されてはおらず、Office アプリケーションでは現在のところサポートされていません。|Office カスタム権限: 実装されていません。 <br /><br />Azure クラシック ポータルでの名前: 実装されていません。<br /><br />Azure ポータルでの名前: 実装されていません。<br /><br />AD RMS テンプレートでの名前: 実装されていません。 <br /><br />API の定数または値: `IPC_GENERIC_COMMENT L"COMMENT`|
|共通名: **名前を付けて保存、エクスポート** <br /><br />ポリシーでのエンコード: **EXPORT**|別のファイル名でコンテンツを保存するオプション (名前を付けて保存) を有効にします。 <br /><br />Azure Information Protection クライアントについては、ファイルを保護なしで保存し、新しい設定とアクセス許可で再保護することができます。 許可されているこれらの操作は、この権限を持つユーザーが保護されたドキュメントまたは電子メールから Azure Information Protection ラベルを変更または削除できることを意味します。 <br /><br />この権限は、アプリケーションでその他のエクスポート オプション ( **[OneNote に送る]** など) を実行することもユーザーに許可します。|Office カスタム権限: **フル コントロール** オプションの一部。 <br /><br />Azure クラシック ポータルでの名前: **コンテンツのエクスポート (名前を付けて保存)** <br /><br />Azure Portal での名前: **名前を付けて保存、エクスポート (EXPORT)**<br /><br />AD RMS テンプレートでの名前: **エクスポート (名前を付けて保存)** <br /><br />API の定数または値: `IPC_GENERIC_EXPORT L"EXPORT"`|
|共通名: **転送** <br /><br />ポリシーでのエンコード: **FORWARD**|電子メール メッセージの転送、 **[宛先]** 、 **[CC]** 行への受信者の追加を行うオプションを有効にします。 この権限は、ドキュメントには適用されません。メール メッセージだけに適用されます。<br /><br />転送操作の一部として転送者が他のユーザーに権限を付与することは許可しません。 <br /><br />この権限を付与するときは、保護されたメール メッセージが添付ファイルとして転送されないように、**コンテンツの編集、編集**権限 (共通名) と、さらに**保存**権限 (共通名) も付与します。 これらの権限は、Outlook クライアントまたは Outlook Web アプリを利用する別の組織に電子メールを送信するときにも指定します。 または、[オンボードコントロール](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy)を実装しているため Rights Management 保護の使用を除外している組織内のユーザーの場合。|Office カスタム権限: **転送不可**標準ポリシーを使用すると拒否されます。<br /><br />Azure クラシック ポータルでの名前: **転送**<br /><br />Azure Portal での名前: **転送 (FORWARD)**<br /><br />AD RMS テンプレートでの名前: **転送** <br /><br />API の定数または値: `IPC_EMAIL_FORWARD L"FORWARD"`|
|共通名: **フル コントロール** <br /><br />ポリシーでのエンコード: **OWNER**|ドキュメントに対するすべての権限を付与します。利用可能なすべての操作を実行できます。<br /><br />ドキュメントの保護解除と再保護の能力も含まれます。 <br /><br />この使用権限は [Rights Management 所有者](#rights-management-issuer-and-rights-management-owner)とは同じではありません。|Office カスタム権限: **フル コントロール** カスタム オプション。<br /><br />Azure クラシック ポータルでの名前: **フル コントロール**<br /><br />Azure Portal での名前: **フル コントロール (OWNER)**<br /><br />AD RMS テンプレートでの名前: **フル コントロール** <br /><br />API の定数または値: `IPC_GENERIC_ALL L"OWNER"`|
|共通名: **印刷** <br /><br />ポリシーでのエンコード: **PRINT**|コンテンツを印刷するオプションを有効にします。|Office カスタム権限: カスタム アクセス許可の**コンテンツの印刷**オプション。 受信者単位の設定ではありません。<br /><br />Azure クラシック ポータルでの名前: **印刷**<br /><br />Azure Portal での名前: **印刷 (PRINT)**<br /><br />AD RMS テンプレートでの名前: **印刷** <br /><br />API の定数または値: `IPC_GENERIC_PRINT L"PRINT"`|
|共通名: **返信** <br /><br />ポリシーでのエンコード: **REPLY**|メール クライアントの **[返信]** オプションを有効にします。ただし、 **[宛先]** または **[CC]** 行に対する変更は許可しません。<br /><br />この権限を付与するときは、保護されたメール メッセージが添付ファイルとして転送されないように、**コンテンツの編集、編集**権限 (共通名) と、さらに**保存**権限 (共通名) も付与します。 これらの権限は、Outlook クライアントまたは Outlook Web アプリを利用する別の組織に電子メールを送信するときにも指定します。 または、[オンボードコントロール](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy)を実装しているため Rights Management 保護の使用を除外している組織内のユーザーの場合。|Office カスタム権限: 該当なし。<br /><br />Azure クラシック ポータルでの名前: **返信**<br /><br />Azure クラシック ポータルでの名前: **返信 (REPLY)**<br /><br />AD RMS テンプレートでの名前: **返信** <br /><br />API の定数または値: `IPC_EMAIL_REPLY`|
|共通名: **全員に返信** <br /><br />ポリシーでのエンコード: **REPLYALL**|メール クライアントの **[全員に返信]** オプションを有効にします。ただし、 **[宛先]** または **[CC]** 行への受信者の追加はユーザーに許可しません。<br /><br />この権限を付与するときは、保護されたメール メッセージが添付ファイルとして転送されないように、**コンテンツの編集、編集**権限 (共通名) と、さらに**保存**権限 (共通名) も付与します。 これらの権限は、Outlook クライアントまたは Outlook Web アプリを利用する別の組織に電子メールを送信するときにも指定します。 または、[オンボードコントロール](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy)を実装しているため Rights Management 保護の使用を除外している組織内のユーザーの場合。|Office カスタム権限: 該当なし。<br /><br />Azure クラシック ポータルでの名前: **全員に返信**<br /><br />Azure Portal での名前: **全員に返信 (REPLY ALL)**<br /><br />AD RMS テンプレートでの名前: **全員に返信** <br /><br />API の定数または値: `IPC_EMAIL_REPLYALL L"REPLYALL"`|
|共通名: **表示、開く、読み取り** <br /><br />ポリシーでのエンコード: **VIEW**|ドキュメントを開き、内容を表示することをユーザーに許可します。<br /><br /> Excel の場合、データを並べ替えるには、この権限は十分ではありません。次の権限が必要です: **コンテンツの編集、編集**。 Excel でデータをフィルター処理するには、次の 2 つの権限が必要です: **コンテンツの編集、編集**および**コピー**。|Office カスタム権限: **読み取り**カスタムポリシー、**表示**オプション。<br /><br />Azure クラシック ポータルでの名前: **表示**<br /><br />Azure Portal での名前:**表示、開く、読み取り (VIEW)**<br /><br />AD RMS テンプレートでの名前: **読み取り** <br /><br />API の定数または値: `IPC_GENERIC_READ L"VIEW"`|
|共通名: **コピー** <br /><br />ポリシーでのエンコード: **EXTRACT**|ドキュメントのデータ (画面キャプチャを含む) を同じドキュメントまたは別のドキュメントにコピーするオプションを有効にします。<br /><br />一部のアプリケーションでは、ドキュメント全体を保護されていない形式で保存することも許可されます。<br /><br />Skype for Business のような画面共有アプリケーションでは、プレゼンターは、保護されたドキュメントを正常に表示するために、この権限を持っている必要があります。 プレゼンターがこの権限を持っていない場合は、参加者はドキュメントを表示することができず、黒塗りで表示されます。|Office カスタム権限: **[閲覧の権限を持つユーザーが、コンテンツをコピーすることを許可する]** カスタム ポリシー オプションと同様。<br /><br />Azure クラシック ポータルでの名前: **コンテンツのコピーと抽出**<br /><br />Azure Portal での名前: **コピー (EXTRACT)**<br /><br />AD RMS テンプレートでの名前: **Extract** <br /><br />API の定数または値: `IPC_GENERIC_EXTRACT L"EXTRACT"`|
|共通名: **権限の表示** <br /><br />ポリシーでのエンコード: **VIEWRIGHTSDATA**|ドキュメントに適用されたポリシーを表示することをユーザーに許可します。|Office カスタム権限: 実装されていません。<br /><br />Azure クラシック ポータルでの名前: **割り当てられた権限の表示**<br /><br />Azure Portal での名前: **権限の表示 (VIEWRIGHTSDATA)**<br /><br />AD RMS テンプレートでの名前: **権限の表示** <br /><br />API の定数または値: `IPC_READ_RIGHTS L"VIEWRIGHTSDATA"`|
|共通名: **権限の変更** <br /><br />ポリシーでのエンコード: **EDITRIGHTSDATA**|ドキュメントに適用されたポリシーを変更することをユーザーに許可します。 保護の削除などを含みます。|Office カスタム権限: 実装されていません。<br /><br />Azure クラシック ポータルでの名前: **権限の変更**<br /><br />Azure Portal での名前: **権限の編集 (EDITRIGHTSDATA)**<br /><br />AD RMS テンプレートでの名前: **権限の編集** <br /><br />API の定数または値: `PC_WRITE_RIGHTS L"EDITRIGHTSDATA"`|
|共通名: **マクロの許可** <br /><br />ポリシーでのエンコード: **OBJMODEL**|マクロを実行したり、その他のプログラムまたはリモートからのドキュメント内のコンテンツへのアクセスを実行したりするオプションを有効にします。|Office カスタム権限: **[プログラムによるアクセスを許可]** カスタム ポリシー オプションと同様。 受信者単位の設定ではありません。<br /><br />Azure クラシック ポータルでの名前: **マクロの許可**<br /><br />Azure Portal での名前: **マクロの許可 (OBJMODEL)**<br /><br />AD RMS テンプレートでの名前: **マクロの許可** <br /><br />API の定数または値: 実装されていません。|

## <a name="rights-included-in-permissions-levels"></a>アクセス許可レベルに含まれる権限

一部のアプリケーションは、通常は一緒に使用される使用権限を選択しやすくために、使用権限をまとめてアクセス許可レベルにグループ化します。 これらのアクセス許可レベルは、役割ベースのオプションを選択できるように、ユーザーからの複雑さのレベルを抽象化するのに役立ちます。  たとえば、**レビュー担当者**や**共同作成者**などがあります。 多くの場合、これらのオプションではユーザーに対して権限の概要が表示されますが、前の表に記載されているすべての権限が含まれるとは限りません。

これらのアクセス許可レベルの一覧、および含まれる使用権限の完全な一覧については、次の表を使用してください。 使用権限は、[共通名](#usage-rights-and-descriptions)で一覧表示されています。

|アクセス許可レベル|アプリケーション|含まれる使用権限|
|---------------------|----------------|---------------------------------|
|表示者|Azure クラシック ポータル <br /><br />Azure Portal を比較してデバイス コンプライアンス ポリシーを使用する<br /><br />Windows 用 Azure Information Protection クライアント|表示、開く、読み取り、権限の表示、返信 [[1]](#footnote-1)、全員に返信 [[1]](#footnote-1)、マクロの許可 [[2]](#footnote-2)<br /><br />注: 電子メールの場合、電子メールの返信が添付ファイルではなく電子メール メッセージとして受信されるように、このアクセス許可レベルではなく、レビュー担当者を利用します。 レビュー担当者は、Outlook クライアントまたは Outlook Web アプリを利用する別の組織に電子メールを送信するときにも必要になります。 または、[オンボーディング制御](/powershell/module/aipservice/set-aipserviceonboardingcontrolpolicy)を実装しているため、Azure Rights Management サービスの使用対象から除外されている組織内のユーザーに適用されます。|
|レビュー担当者|Azure クラシック ポータル <br /><br />Azure Portal を比較してデバイス コンプライアンス ポリシーを使用する<br /><br />Windows 用 Azure Information Protection クライアント|表示、開く、読み取り、保存、コンテンツの編集、編集、権限の表示、返信、全員に返信 [[3]](#footnote-3)、転送 [[3]](#footnote-3)、マクロの許可 [[2]](#footnote-2)|
|共同作成者|Azure クラシック ポータル <br /><br />Azure Portal を比較してデバイス コンプライアンス ポリシーを使用する<br /><br />Windows 用 Azure Information Protection クライアント|表示、開く、読み取り、保存、コンテンツの編集、編集、コピー、権限の表示、マクロの許可、名前を付けて保存、エクスポート [[4]](#footnote-4)、印刷、返信 [[3]](#footnote-3)、全員に返信 [[3]](#footnote-3)、転送 [[3]](#footnote-3)|
|共同所有者|Azure クラシック ポータル <br /><br />Azure Portal を比較してデバイス コンプライアンス ポリシーを使用する<br /><br />Windows 用 Azure Information Protection クライアント|表示、開く、読み取り、保存、コンテンツの編集、編集、コピー、権限の表示、権限の変更、マクロの許可、名前を付けて保存、エクスポート、印刷、返信 [[3]](#footnote-3)、全員に返信 [[3]](#footnote-3)、転送 [[3]](#footnote-3)、フル コントロール|

----

###### <a name="footnote-1"></a>脚注 1:

Azure Portal には含まれていません。

###### <a name="footnote-2"></a>脚注 2

Windows 用 Azure Information Protection クライアントの場合、この権限は、Office アプリケーションの Information Protection バーで現在必要です。

###### <a name="footnote-3"></a>脚注 3
Windows 用 Azure Information Protection クライアントには適用されません。

###### <a name="footnote-4"></a>脚注 4
Azure Portal または Windows 用 Azure Information Protection クライアントには含まれていません。

## <a name="rights-included-in-the-default-templates"></a>既定のテンプレートに含まれる権限
次の表は、既定のテンプレートを作成したときに含まれる使用権限を一覧表示しています。 使用権限は、[共通名](#usage-rights-and-descriptions)で一覧表示されています。

これらの既定のテンプレートは、サブスクリプションを購入すると作成されます。Azure Portal で、名前と使用権限を[変更](configure-policy-templates.md)することができます。 

|テンプレートの表示名|使用権限 (2017 年 10 月 6 日から現在)|使用権限 (2017 年 10 月 6 日より前)|
|----------------|--------------------|----------|
|\<*組織名> - 社外秘、表示のみ* <br /><br />または<br /><br /> *非常に機密性の高い社外秘 \ すべての従業員*|表示、開く、読み取り、コピー、権限の表示、マクロの許可、印刷、転送、返信、全員に返信、保存、コンテンツの編集、編集|表示、開く、読み取り|
|\<*組織名> - 社外秘* <br /><br />または <br /><br />*社外秘 \ すべての従業員*|表示、開く、読み取り、名前を付けて保存、エクスポート、コピー、権限の表示、権限の変更、マクロの許可、印刷、転送、返信、全員に返信、保存、コンテンツの編集、編集、フル コントロール|表示、開く、読み取り、名前を付けて保存、エクスポート、コンテンツの編集、編集、権限の表示、マクロの許可、転送、返信、全員に返信|

## <a name="do-not-forward-option-for-emails"></a>電子メールの [転送不可] オプション

Exchange のクライアントとサービス (Outlook クライアント、Outlook on the web、Exchange メール フロー ルール、Exchange の DLP アクションなど) には、 **[転送不可]** というメール用の追加の情報権限保護オプションがあります。 

このオプションは、選択できる既定の Rights Management テンプレートのようにユーザー (と Exchange 管理者) には見えますが、 **[転送不可]** はテンプレートではありません。 そのため、保護テンプレートを参照および管理するとき、Azure Portal には表示されません。 **[転送不可]** オプションは、ユーザーが電子メール受信者に動的に適用する使用権限の集合です。

**[転送不可]** オプションが電子メールに適用される場合、電子メールが暗号化され、受信者は認証される必要があります。 その結果、受信者はメールの転送、印刷、またはコピーを実行できなくなります。 たとえば、Outlook クライアントでは、[転送] ボタンが利用できなくなり、 **[名前を付けて保存]** および **[印刷]** メニュー オプションが利用できなくなり、 **[宛先]** 、 **[Cc]** 、 **[Bcc]** ボックスの受信者を追加したり、変更したりすることができなくなります。

メールに添付されている保護されていない [Office ドキュメント](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM)は、自動的に同じ制限を継承します。 これらのドキュメントに適用される使用権限は、**コンテンツの編集、編集**、**保存**、**表示、開く、読み取り**と**マクロの許可**です。 添付ファイルに別の使用権限を使用する場合または添付ファイルがこの継承された保護をサポートする Office ドキュメントでない場合、電子メールに添付する前に、ファイルを保護する必要があります。 それからファイルに必要な特定の使用権限を割り当てることができます。 

### <a name="difference-between-do-not-forward-and-not-granting-the-forward-usage-right"></a>転送不可と転送の使用権限を付与しないことの違い

**[転送不可]** オプションの適用と電子メールに**転送**使用権限を与えないテンプレートの適用には重要な違いがあります。 **[転送不可]** オプションの場合、元の電子メールでユーザーが選択した受信者に基づく、許可されたユーザーの動的なリストが使用されます。テンプレートの権限の場合、管理者が前もって指定した許可されたユーザーの静的なリストが使用されます。 違いは何ですか。 例を見てみましょう。 

あるユーザーがいくつかの情報をマーケティング部署の一部の人たちに電子メールで送信します。それ以外の人とこの情報を共有することは許されません。 権限 (表示、返信、保存) をマーケティング部署に限定するテンプレートで電子メールを保護するべきでしょうか。  それとも、 **[転送不可]** オプションを選択するべきでしょうか。 いずれの場合でも、受信者は電子メールを転送できません。 

- テンプレートを適用した場合、受信者はマーケティング部署の他の人と情報を共有できる可能性があります。 たとえば、エクスプローラーを利用し、電子メールを共有の場所や USB ドライブにドラッグアンドドロップできます。 マーケティング部署の人 (と電子メールの作成者) でこの場所にアクセスできる人であれば、誰でも電子メールの情報を見ることができます。
 
- **[転送不可]** オプションを適用した場合、受信者は電子メールを別の場所に移すことができず、マーケティング部署の他の人と情報を共有することができません。 この場合、元の受信者 (と電子メールの作成者) だけが電子メールの情報を見ることができます。

> [!NOTE] 
> 送信者が選択した受信者だけに電子メールの情報の閲覧を許可することが重要である場合、 **[転送不可]** を使用してください。 送信者が選択した受信者に関係なく、管理者が前もって指定したユーザー グループに権限を制限するとき、電子メールのテンプレートを使用します。

## <a name="encrypt-only-option-for-emails"></a>電子メールの暗号化のみオプション

Exchange Online で Office 365 Message Encryption の新機能を使用する場合、新しい電子メール オプション (**暗号化のみ**) を利用できます。

このオプションは、Exchange Online を使用するテナントが利用可能であり、Outlook on the web でメール フロー ルールの別の権利保護オプションとして、Office 365 の DLP アクションとして、および Outlook (Office 365 ProPlus の最小バージョン [1804](/officeupdates/monthly-channel-2018#outlook-feature-updates-4)、および [Azure RMS をサポートする Office 365 アプリ](requirements-applications.md#windows-computers-for-information-rights-management-irm)がある場合は、最小バージョン 1805) から選択することができます。 [暗号化のみ] オプションの詳細については、Office チームの次のブログ投稿のお知らせを参照してください。 [office 365 Message Encryption でのロールアウトのみを暗号化](https://aka.ms/omefeb2018)します。

このオプションが選択されると、電子メールが暗号化され、受信者は認証される必要があります。 すると、受信者には**名前を付けて保存、エクスポート**と**フル コントロール**を除くすべての使用権限が割り当てられます。 この使用権限の組み合わせは、保護を削除できないこと以外は、受信者には制限がないということです。 たとえば、受信者は電子メールをコピー、印刷、および転送することができます。 

同様に、既定では、メールに添付されている保護されていない [Office ドキュメント](https://support.office.com/article/bb643d33-4a3f-4ac7-9770-fd50d95f58dc#FileTypesforIRM)も同じアクセス許可を継承します。 これらのドキュメントは自動的に保護されます。これらをダウンロードしたら、受信者は Office アプリケーションから保存、編集、コピーおよび印刷することができます。 受信者が文書を保存する場合、新しい名前で保存できます。このとき、別の形式で保存することも可能です。 ただし、元の保護でドキュメントを保存できるよう、保護をサポートするファイル形式のみを使用できます。 添付ファイルに別の使用権限を使用する場合または添付ファイルがこの継承された保護をサポートする Office ドキュメントでない場合、電子メールに添付する前に、ファイルを保護する必要があります。 それからファイルに必要な特定の使用権限を割り当てることができます。

または、[Exchange Online PowerShell](/powershell/exchange/exchange-online/connect-to-exchange-online-powershell/connect-to-exchange-online-powershell?view=exchange-ps) で `Set-IRMConfiguration -DecryptAttachmentForEncryptOnly $true` を指定して、このドキュメントの保護継承を変更することができます。 ユーザーの認証後にドキュメントの元の保護を保持する必要がない場合は、この構成を使用します。 受信者が電子メール メッセージを開く際に、ドキュメントは保護されません。

元の保護を保持するために添付されたドキュメントが必要な場合は、「[Azure Information Protection を使用したセキュアなドキュメント コラボレーション](secure-collaboration-documents.md)」をご覧ください。

注: **DecryptAttachmentFromPortal**への参照が表示されている場合、このパラメーターは、 [Set irmconfiguration](/powershell/module/exchange/encryption-and-certificates/set-irmconfiguration?view=exchange-ps)では非推奨となりました。 このパラメーターを以前に設定したことがない場合は使用できません。 

## <a name="rights-management-issuer-and-rights-management-owner"></a>Rights Management 発行者と Rights Management 所有者

ドキュメントまたは電子メールが Azure Rights Management サービスで保護されているとき、そのコンテンツを保護するアカウントはそのコンテンツの Rights Management 発行者に自動的になります。 このアカウントは[利用状況ログ](log-analyze-usage.md#how-to-interpret-your-usage-logs)の**発行者**フィールドとして記録されます。 

Rights Management 発行者には常にドキュメントまたは電子メールのフル コントロール使用権限が与えられます。さらに、次の操作が可能です。

- 保護設定に有効期限が含まれる場合、Rights Management 発行者はその日付の後でもドキュメントまたは電子メールを開き、編集できます。

- Rights Management 発行者は常にドキュメントまたは電子メールにオフラインでアクセスできます。

- Rights Management 発行者は取り消した後もドキュメントを開くことができます。 

既定では、このアカウントはそのコンテンツの **Rights Management 所有者**でもあります。Rights Management 所有者であれば、ドキュメントまたは電子メールを作成したユーザーが保護を開始します。 ただし、管理者またはサービスがユーザーの代わりにコンテンツを保護できるシナリオもあります。 たとえば、次のようになります。

- 管理者がファイル共有のファイルを一括保護する: Azure AD の管理者アカウントでユーザーのドキュメントを保護します。

- Rights Management コネクタが Windows Server フォルダーの Office ドキュメントを保護する: RMS コネクタに作成された Azure AD のサービス プリンシパル アカウントでユーザーのドキュメントを保護します。

以上のシナリオでは、Rights Management 発行者は Azure Information Protection SDK または PowerShell を利用して Rights Management 所有者を別のアカウントに割り当てることができます。 たとえば、Azure Information Protection クライアントで [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) PowerShell コマンドレットを使用するとき、**OwnerEmail** パラメーターを指定し、Rights Management 所有者を別のアカウントに割り当てることができます。 

ユーザーの代わりに Rights Management 発行者が保護するとき、Rights Management 所有者を割り当てることで、元のドキュメントまたは電子メールの所有者に、保護コンテンツに対し、保護を自分で開始した場合と同じレベルのコントロールが与えられます。 

たとえば、印刷使用権限が含まれていないテンプレートで保護されていても、ドキュメントを作成したユーザーはそのドキュメントを印刷できます。 そのテンプレートで構成されているオフライン アクセス設定や有効期限に関係なく、同じユーザーは常に自分のドキュメントにアクセスできます。 さらに、Rights Management 所有者にはフル コントロール使用権限が与えられるため、このユーザーはドキュメントを再保護し、追加のユーザー アクセスを付与することもできます (その時点で、ユーザーは Rights Management 発行者と Rights Management 所有者になります)。このユーザーは保護を解除することもできます。 ただし、ドキュメントを追跡し、取り消すことができるのは Rights Management 発行者だけです。

ドキュメントまたは電子メールの Rights Management 所有者は[利用状況ログ](log-analyze-usage.md#how-to-interpret-your-usage-logs)で **owner-email** フィールドとして記録されます。

Rights Management 所有者と Windows ファイル システム所有者に依存関係はありません。 この 2 つは同じことが多いですが、異なる場合もあります (SDK または PowerShell を使用しない場合でも)。

## <a name="rights-management-use-license"></a>Rights Management の使用ライセンス

Azure Rights Management によって保護されたドキュメントまたは電子メールをユーザーが開くと、そのコンテンツに対する Rights Management の使用ライセンスがユーザーに付与されます。 この使用ライセンスは証明書であり、ドキュメントまたは電子メール メッセージに対するユーザーの使用権限、およびコンテンツを暗号化するのに使用された暗号化キーが含まれています。 使用ライセンスにはまた、有効期限 (設定されている場合) および使用ライセンスの有効期間も含まれます。

ユーザーはコンテンツを開くために、有効な使用ライセンスと権利アカウント証明書 (RAC) を持つ必要があります。この証明書は、[ユーザー環境が初期化され](how-does-it-work.md#initializing-the-user-environment)て 31 日ごとに更新されたときに付与されます。

使用ライセンスの期間中、ユーザーはコンテンツについて再認証も再承認も行われません。 これにより、ユーザーは、インターネットに接続しなくても、保護されたドキュメントまたは電子メールを引き続き開くことができます。 使用ライセンスの有効期限を過ぎると、次に保護されたドキュメントまたは電子メールにアクセスしたときに、ユーザーは再認証および再承認される必要があります。 

保護設定を定義したラベルまたはテンプレートによってドキュメントおよび電子メールメッセージが保護されている場合は、ラベルまたはテンプレート内でこれらの設定を変更することができ、コンテンツを再保護する必要はありません。 ユーザーが既にコンテンツにアクセスしている場合は、使用ライセンスの有効期限が過ぎた後で変更が有効になります。 ただし、ユーザーがカスタム アクセス許可 (アドホック権利ポリシーとも呼ばれる) を適用した場合、ドキュメントまたは電子メールが保護された後でこれらのアクセス許可を変更する必要があるときは、そのコンテンツを新しいアクセス許可で再度保護する必要があります。 電子メール メッセージのカスタム アクセス許可は、[転送不可] オプションで実装されます。

テナントの既定の使用ライセンス有効期間は30日です。この値を構成するには、PowerShell コマンドレット[AipServiceMaxUseLicenseValidityTime](/powershell/module/aipservice/set-aipservicemaxuselicensevaliditytime)を使用します。 ラベルまたはテンプレートを使用して保護を適用する場合は、より制限の厳しい設定を構成できます。

- Azure Portal で、ラベルまたはテンプレートを構成する場合は、使用ライセンスの有効期間として、 **[オフライン アクセスの許可]** 設定の値が使用されます。 
    
    Azure Portal でこの設定を構成するための詳細とガイダンスについては、Rights Management の保護用にラベルを構成する方法について説明した記事の、「[保護の設定に関する情報](configure-policy-protection.md#information-about-the-protection-settings)」の表をご覧ください。

- PowerShell を使用してテンプレートを構成する場合、使用ライセンスの有効期間は、 *LicenseValidityDuration*パラメーターの値を設定します。これは、 [Set AipServiceTemplateProperty](/powershell/module/aipservice/set-aipservicetemplateproperty)および[Add-aipservicetemplate](/powershell/module/aipservice/add-aipservicetemplate)コマンドレットです。
    
    PowerShell を使用してこの設定を構成するための詳細とガイダンスについては、各コマンドレットのヘルプを参照してください。

## <a name="see-also"></a>参照
[Azure Information Protection のテンプレートを構成して管理する](configure-policy-templates.md)

[Azure Information Protection および探索サービスまたはデータ回復用のスーパーユーザーの構成](configure-super-users.md)
