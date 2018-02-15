---
title: "Azure Rights Management の使用権限を構成する - AIP"
description: "Azure Information Protection から Azure Rights Management サービスを使用してファイルまたは電子メールを保護するときに使用される、特定の権限を確認します。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 97ddde38-b91b-42a5-8eb4-3ce6ce15393d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ceada043abfa1bee18c6407b3804815d95e89453
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2018
---
# <a name="configuring-usage-rights-for-azure-rights-management"></a>Azure Rights Management の使用権限を構成する

>*適用対象: Azure Information Protection、Office 365*

Azure Information Protection から Azure Rights Management サービスを使用してファイルまたは電子メールに対して保護を設定し、テンプレートは使用しない場合、使用権限を自分で構成する必要があります。 また、Azure Rights Management 保護用のテンプレートまたはラベルを構成する場合は、ユーザー、管理者、または構成済みのサービスによってテンプレートまたはラベルが選択されたときに自動的に適用される使用権限を選択します。 たとえば、Azure Portal では、使用権限の論理的なグループを構成するロールを選択することも、個別の権限を構成することもできます。

この記事では、使用しているアプリケーションに対して必要な使用権限を構成する際に役立つ情報を提供すると共に、それらの権限がアプリケーションによってどのように解釈されるかを説明します。

> [!NOTE] 
> 完全を期すため、この記事には 2018 年 1 月 8 日に廃止された Azure クラシック ポータルの値も含まれています。
>
> 新しいポータルへの移行については「[Azure クラシック ポータルで行っていたタスク](migrate-portal.md)」を参照してください。

## <a name="usage-rights-and-descriptions"></a>使用権限と説明
次の表は、Rights Management でサポートされている使用権限と説明の一覧です。それらの使用方法と解釈方法も示します。 一覧では**共通名**を示しています。これは、通常、使用権限が表示されたり参照されたりするときに使われる名前であり、コード内で使用される単一ワード値 (**ポリシーでのエンコード**値) よりもわかりやすい名前です。 

**API の定数または値**は、MSIPC API 呼び出しの SDK 名であり、使用権限があるかどうかを確認したり、ポリシーに使用権限を追加したりする RMS 対応アプリケーションを記述するときに使用されます。


|使用権限|Description|実装|
|-------------------------------|---------------------------|-----------------|
|共通名: **コンテンツの編集、編集** <br /><br />ポリシーでのエンコード: **DOCEDIT**|アプリケーション内のコンテンツの変更、並べ替え、書式設定、またはフィルター処理をユーザーに許可します。 編集済みのコピーを保存する権限は付与されません。|Office カスタム権限: **変更**と**フル コントロール** オプションの一部。 <br /><br />Azure クラシック ポータルでの名前: **コンテンツの編集**<br /><br />Azure Portal での名前: **コンテンツの編集、編集 (DOCEDIT)**<br /><br />AD RMS テンプレートでの名前: **編集** <br /><br />API の定数または値: 該当なし。|
|共通名: **保存** <br /><br />ポリシーでのエンコード: **EDIT**|ドキュメントを現在の場所に保存することをユーザーに許可します。<br /><br />Office アプリケーションでは、この権限はドキュメントを変更することもユーザーに許可します。|Office カスタム権限: **変更**と**フル コントロール** オプションの一部。 <br /><br />Azure クラシック ポータルでの名前: **ファイルの保存**<br /><br />Azure Portal での名前: **保存 (EDIT)**<br /><br />AD RMS テンプレートでの名前: **保存** <br /><br />API の定数または値: `IPC_GENERIC_WRITE L"EDIT"`|
|共通名: **コメント** <br /><br />ポリシーでのエンコード: **COMMENT**|コンテンツに注釈やコメントを追加するオプションを有効にします。<br /><br />この権限は SDK で使用でき、Azure Information Protection と Windows PowerShell の RMS 保護モジュールでアドホック ポリシーとして使用できます。また、いくつかのソフトウェア ベンダーのアプリケーションに実装されています。 ただし広く使用されてはおらず、Office アプリケーションでは現在のところサポートされていません。|Office カスタム権限: 実装されていません。 <br /><br />Azure クラシック ポータルでの名前: 実装されていません。<br /><br />Azure Portal での名前: 実装されていません。<br /><br />AD RMS テンプレートでの名前: 実装されていません。 <br /><br />API の定数または値: `IPC_GENERIC_COMMENT L"COMMENT`|
|共通名: **名前を付けて保存、エクスポート** <br /><br />ポリシーでのエンコード: **EXPORT**|別のファイル名でコンテンツを保存するオプション (名前を付けて保存) を有効にします。 Office ドキュメントと Azure Information Protection クライアントについては、ファイルを保護なしで保存できます。<br /><br />この権限は、アプリケーションでその他のエクスポート オプション (**[OneNote に送る]** など) を実行することもユーザーに許可します。<br /><br /> 注: この権限が与えられていない場合、ユーザーが選択したファイル形式が Rights Management 保護をネイティブにサポートしていれば、Office アプリケーションは新しい名前でドキュメントを保存することをユーザーに許可します。|Office カスタム権限: **変更**と**フル コントロール** オプションの一部。 <br /><br />Azure クラシック ポータルでの名前: **コンテンツのエクスポート (名前を付けて保存)** <br /><br />Azure Portal での名前: **名前を付けて保存、エクスポート (EXPORT)**<br /><br />AD RMS テンプレートでの名前: **エクスポート (名前を付けて保存)** <br /><br />API の定数または値: `IPC_GENERIC_EXPORT L"EXPORT"`|
|共通名: **転送** <br /><br />ポリシーでのエンコード: **FORWARD**|電子メール メッセージの転送と、**[宛先]** および **[CC]** 行への受信者の追加を行うオプションを有効にします。 この権限は、ドキュメントには適用されません。メール メッセージだけに適用されます。<br /><br />転送操作の一部として転送者が他のユーザーに権限を付与することは許可しません。 <br /><br />この権限を付与するときは、元の電子メールが添付ファイルではなく、転送される電子メール メッセージの一部になるように、**コンテンツの編集、編集**権限 (共通名) も付与します。 この権限は、Outlook クライアントまたは Outlook Web アプリを利用する別の組織に電子メールを送信するときにも必要になります。 または、[オンボーディング コントロール](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy)を実装したために、Azure Rights Management サービスの使用対象から除外されている組織内のユーザーにも必要です。|Office カスタム権限: **転送不可**標準ポリシーを使用すると拒否されます。<br /><br />Azure クラシック ポータルでの名前: **転送**<br /><br />Azure Portal での名前: **転送 (FORWARD)**<br /><br />AD RMS テンプレートでの名前: **転送** <br /><br />API の定数または値: `IPC_EMAIL_FORWARD L"FORWARD"`|
|共通名: **フル コントロール** <br /><br />ポリシーでのエンコード: **OWNER**|ドキュメントに対するすべての権限を付与します。利用可能なすべての操作を実行できます。<br /><br />ドキュメントの保護解除と再保護の能力も含まれます。 <br /><br />この使用権限は、[Rights Management 所有者](#rights-management-issuer-and-rights-management-owner)と同じではないことに注意してください。|Office カスタム権限: **フル コントロール** カスタム オプション。<br /><br />Azure クラシック ポータルでの名前: **フル コントロール**<br /><br />Azure Portal での名前: **フル コントロール (OWNER)**<br /><br />AD RMS テンプレートでの名前: **フル コントロール** <br /><br />API の定数または値: `IPC_GENERIC_ALL L"OWNER"`|
|共通名: **印刷** <br /><br />ポリシーでのエンコード: **PRINT**|コンテンツを印刷するオプションを有効にします。|Office カスタム権限: カスタム アクセス許可の**コンテンツの印刷**オプション。 受信者単位の設定ではありません。<br /><br />Azure クラシック ポータルでの名前: **印刷**<br /><br />Azure Portal での名前: **印刷 (PRINT)**<br /><br />AD RMS テンプレートでの名前: **印刷** <br /><br />API の定数または値: `IPC_GENERIC_PRINT L"PRINT"`|
|共通名: **返信** <br /><br />ポリシーでのエンコード: **REPLY**|メール クライアントの **[返信]** オプションを有効にします。ただし、**[宛先]** または **[CC]** 行に対する変更は許可しません。<br /><br />この権限を付与するときは、元の電子メールが添付ファイルではなく、転送される電子メール メッセージの一部になるように、**コンテンツの編集、編集**権限 (共通名) も付与します。 この権限は、Outlook クライアントまたは Outlook Web アプリを利用する別の組織に電子メールを送信するときにも必要になります。 または、[オンボーディング コントロール](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy)を実装したために、Azure Rights Management サービスの使用対象から除外されている組織内のユーザーにも必要です。|Office カスタム権限: 該当なし。<br /><br />Azure クラシック ポータルでの名前: **返信**<br /><br />Azure Portal での名前: **返信 (REPLY)**<br /><br />AD RMS テンプレートでの名前: **返信** <br /><br />API の定数または値: `IPC_EMAIL_REPLY`|
|共通名: **全員に返信** <br /><br />ポリシーでのエンコード: **REPLYALL**|メール クライアントの **[全員に返信]** オプションを有効にします。ただし、**[宛先]** または **[CC]** 行への受信者の追加はユーザーに許可しません。<br /><br />この権限を付与するときは、元の電子メールが添付ファイルではなく、転送される電子メール メッセージの一部になるように、**コンテンツの編集、編集**権限 (共通名) も付与します。 この権限は、Outlook クライアントまたは Outlook Web アプリを利用する別の組織に電子メールを送信するときにも必要になります。 または、[オンボーディング コントロール](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy)を実装したために、Azure Rights Management サービスの使用対象から除外されている組織内のユーザーにも必要です。|Office カスタム権限: 該当なし。<br /><br />Azure クラシック ポータルでの名前: **全員に返信**<br /><br />Azure Portal での名前: **全員に返信 (REPLY ALL)**<br /><br />AD RMS テンプレートでの名前: **全員に返信** <br /><br />API の定数または値: `IPC_EMAIL_REPLYALL L"REPLYALL"`|
|共通名: **表示、開く、読み取り** <br /><br />ポリシーでのエンコード: **VIEW**|ドキュメントを開き、内容を表示することをユーザーに許可します。|Office カスタム権限: **読み取り**カスタム ポリシー、**表示**オプション。<br /><br />Azure クラシック ポータルでの名前: **表示**<br /><br />Azure Portal での名前: **表示、開く、読み取り (VIEW)**<br /><br />AD RMS テンプレートでの名前: **全員に返信** <br /><br />API の定数または値: `IPC_GENERIC_READ L"VIEW"`|
|共通名: **コピー** <br /><br />ポリシーでのエンコード: **EXTRACT**|ドキュメントのデータを同じドキュメントまたは別のドキュメントにコピーする (画面キャプチャを含む) オプションを有効にします。<br /><br />一部のアプリケーションでは、ドキュメント全体を保護されていない形式で保存することも許可されます。|Office カスタム権限: **[閲覧の権限を持つユーザーが、コンテンツをコピーすることを許可する]** カスタム ポリシー オプション。<br /><br />Azure クラシック ポータルでの名前: **コンテンツのコピーと抽出**<br /><br />Azure Portal での名前: **コピー (EXTRACT)**<br /><br />AD RMS テンプレートでの名前: **抽出** <br /><br />API の定数または値: `IPC_GENERIC_EXTRACT L"EXTRACT"`|
|共通名: **権利の表示** <br /><br />ポリシーでのエンコード: **VIEWRIGHTSDATA**|ドキュメントに適用されるポリシーの表示をユーザーに許可します。|Office カスタム権限: 実装されていません。<br /><br />Azure クラシック ポータルでの名前: **割り当てられた権利の表示**<br /><br />Azure Portal での名前: **権利の表示 (VIEWRIGHTSDATA)**<br /><br />AD RMS テンプレートでの名前: **権利の表示** <br /><br />API の定数または値: `IPC_READ_RIGHTS L"VIEWRIGHTSDATA"`|
|共通名: **権利の変更** <br /><br />ポリシーでのエンコード: **EDITRIGHTSDATA**|ドキュメントに適用されるポリシーの変更をユーザーに許可します。 保護の解除が含まれます。|Office カスタム権限: 実装されていません。<br /><br />Azure クラシック ポータルでの名前: **権利の変更**<br /><br />Azure Portal での名前: **権利の編集 (EDITRIGHTSDATA)**<br /><br />AD RMS テンプレートでの名前: **権利の編集** <br /><br />API の定数または値: `PC_WRITE_RIGHTS L"EDITRIGHTSDATA"`|
|共通名: **マクロの許可** <br /><br />ポリシーでのエンコード: **OBJMODEL**|マクロを実行したり、その他のプログラムまたはリモートからドキュメントのコンテンツにアクセスしたりするオプションを有効にします。|Office カスタム権限: **[プログラムによるアクセスを許可]** カスタム ポリシー オプション。 受信者単位の設定ではありません。<br /><br />Azure クラシック ポータルでの名前: **マクロの許可**<br /><br />Azure Portal での名前: **マクロの許可 (OBJMODEL)**<br /><br />AD RMS テンプレートでの名前: **マクロの許可** <br /><br />API の定数または値: 実装されていません。|

## <a name="rights-included-in-permissions-levels"></a>アクセス許可レベルに含まれる権限

一部のアプリケーションは、通常は一緒に使用される使用権限を選択しやすくするために、使用権限をまとめてアクセス許可レベルにグループ化します。 これらのアクセス許可レベルによって、複雑なレベルがユーザーからは見えなくなるため、役割ベースでオプションを選択できるようになります。  たとえば、**レビュー担当者**や**共同作成者**などがあります。 多くの場合、これらのオプションではユーザーに対して権限の概要が表示されますが、前の表に記載されているすべての権限が含まれるとは限りません。

これらのアクセス許可レベルの一覧、および含まれる使用権限の完全な一覧については、次の表を参照してください。 使用権限は、[共通名](#usage-rights-and-descriptions)で表示されています。

|アクセス許可レベル|[アプリケーション]|含まれる使用権限|
|---------------------|----------------|---------------------------------|
|[ビューアー]|Azure クラシック ポータル <br /><br />Azure ポータル<br /><br /> Windows 用 Rights Management 共有アプリケーション<br /><br />Windows 用 Azure Information Protection クライアント|表示、開く、読み取り、権利の表示、返信 [[1]](#footnote-1)、全員に返信 [[1]](#footnote-1)、マクロの許可 [[2]](#footnote-2)<br /><br />注: 電子メールの場合、電子メールの返信が添付ファイルではなく電子メール メッセージとして受信されるように、このアクセス許可レベルではなく、レビュー担当者を利用します。 レビュー担当者は、Outlook クライアントまたは Outlook Web アプリを利用する別の組織に電子メールを送信するときにも必要になります。 または、[オンボーディング コントロール](/powershell/module/aadrm/set-aadrmonboardingcontrolpolicy)を実装したために、Azure Rights Management サービスの使用対象から除外されている組織内のユーザーにも必要です。|
|レビュー担当者|Azure クラシック ポータル <br /><br />Azure ポータル<br /><br />Windows 用 Rights Management 共有アプリケーション<br /><br />Windows 用 Azure Information Protection クライアント|表示、開く、読み取り、保存、コンテンツの編集、編集、権利の表示、返信、全員に返信 [[3]](#footnote-3)、転送 [[3]](#footnote-3)、マクロの許可 [[2]](#footnote-2)|
|共同作成者|Azure クラシック ポータル <br /><br />Azure ポータル<br /><br />Windows 用 Rights Management 共有アプリケーション<br /><br />Windows 用 Azure Information Protection クライアント|表示、開く、読み取り、保存、コンテンツの編集、編集、コピー、権利の表示、マクロの許可、名前を付けて保存、エクスポート [[4]](#footnote-4)、印刷、返信 [[3]](#footnote-3)、全員に返信 [[3]](#footnote-3)、転送 [[3]](#footnote-3)|
|共同所有者|Azure クラシック ポータル <br /><br />Azure ポータル<br /><br />Windows 用 Rights Management 共有アプリケーション<br /><br />Windows 用 Azure Information Protection クライアント|表示、開く、読み取り、保存、コンテンツの編集、編集、コピー、権利の表示、権利の変更、マクロの許可、名前を付けて保存、エクスポート、印刷、返信 [[3]](#footnote-3)、全員に返信 [[3]](#footnote-3)、転送 [[3]](#footnote-3)、フル コントロール|

----

###### <a name="footnote-1"></a>脚注 1

Azure Portal には含まれていません。

###### <a name="footnote-2"></a>脚注 2

Windows 用 Azure Information Protection クライアントの場合、この権限は、Office アプリケーションの Information Protection バーで現在必要です。

###### <a name="footnote-3"></a>脚注 3
Windows 用 Azure Information Protection クライアントまたは Windows 用 Rights Management 共有アプリケーションには適用されません。

###### <a name="footnote-4"></a>脚注 4
Azure Portal または Windows 用 Azure Information Protection クライアントには含まれていません。

## <a name="rights-included-in-the-default-templates"></a>既定のテンプレートに含まれる権限
次の表は、既定のテンプレートを作成したときに含まれる使用権限の一覧です。 使用権限は、[共通名](#usage-rights-and-descriptions)で表示されています。

これらの既定のテンプレートは、サブスクリプションを購入すると作成されます。Azure Portal で、名前と使用権限を[変更](configure-policy-templates.md)することができます。 

|テンプレートの表示名|使用権限 (2017 年 10 月 6 日から現在)|使用権限 (2017 年 10 月 6 日より前)|
|----------------|--------------------|----------|
|\<*組織名> - 社外秘、表示のみ* <br /><br />内の複数の<br /><br /> *非常に機密性の高い社外秘 \ すべての従業員*|表示、開く、読み取り、コピー、権利の表示、マクロの許可、印刷、転送、返信、全員に返信、保存、コンテンツの編集、編集|表示、開く、読み取り|
|\<*組織名> - 社外秘* <br /><br />内の複数の <br /><br />*社外秘 \ すべての従業員*|表示、開く、読み取り、名前を付けて保存、エクスポート、コピー、権利の表示、権利の変更、マクロの許可、印刷、転送、返信、全員に返信、保存、コンテンツの編集、編集、フル コントロール|表示、開く、読み取り、名前を付けて保存、エクスポート、コンテンツの編集、編集、権利の表示、マクロの許可、転送、返信、全員に返信|

## <a name="do-not-forward-option-for-emails"></a>電子メールの [転送不可] オプション

Exchange のクライアントとサービス (Outlook クライアント、Outlook Web Access アプリ、Exchange トランスポート ルールなど) には、電子メール用に **[転送不可]** という 1 つの追加の情報権限保護オプションがあります。 

このオプションは、ユーザー (および Exchange 管理者) には選択可能な既定の Rights Management テンプレートのように見えますが、**[転送不可]** はテンプレートではありません。 そのため、Azure Rights Management のテンプレートを表示したり管理したりするときに、Azure Portal に表示されません。 **[転送不可]** オプションは権限の集合であり、ユーザーが電子メール受信者に動的に適用します。

**[転送不可]** オプションが電子メールに適用されると、受信者は電子メールの転送、印刷、コピー、添付ファイルの保存、または別名での保存を行うことができません。 たとえば、Outlook クライアントでは、[転送] ボタンが利用できなくなり、**[名前を付けて保存]**、**[添付ファイルの保存]**、**[印刷]** メニュー オプションが利用できなくなり、**[宛先]**、**[Ccc]**、**[Bcc]** ボックスの受信者を追加したり、変更したりできなくなります。

**[転送不可]** オプションの適用と電子メールに転送権限を与えないテンプレートの適用には重要な違いがあります。**[転送不可]** オプションの場合は、元の電子メールでユーザーが選択した受信者に基づいて、許可されるユーザーの動的なリストが使用されます。テンプレートの権限の場合は、管理者が前もって指定した許可されるユーザーの静的なリストが使用されます。 どのような違いがあるでしょうか。 例を見てみましょう。 

あるユーザーがいくつかの情報をマーケティング部署の一部の人たちに電子メールで送信します。それ以外の人とこの情報を共有することは許されません。 権限 (表示、返信、保存) をマーケティング部署に限定するテンプレートで電子メールを保護するべきでしょうか。  それとも、**[転送不可]** オプションを選択するべきでしょうか。 いずれの場合でも、受信者は電子メールを転送できません。 

- テンプレートを適用した場合、受信者はマーケティング部署の他の人と情報を共有できる可能性があります。 たとえば、エクスプローラーを利用し、電子メールを共有の場所や USB ドライブにドラッグ アンド ドロップできます。 マーケティング部署の人で共有の場所や USB ドライブにアクセスできる人であれば、だれでも電子メールの情報を見ることができます。
 
- **[転送不可]** オプションを適用した場合、受信者は電子メールを別の場所に移すことができず、マーケティング部署の他の人と情報を共有することができません。 この場合、元の受信者 (と電子メールの作成者) だけが電子メールの情報を見ることができます。

> [!NOTE] 
> 送信者が選択した受信者だけに電子メールの情報の閲覧を許可することが重要である場合は、**[転送不可]** を使用してください。 送信者が選択した受信者に関係なく、管理者が前もって指定したユーザー グループに権限を制限する場合は、電子メールのテンプレートを使用します。

## <a name="rights-management-issuer-and-rights-management-owner"></a>Rights Management 発行者と Rights Management 所有者

ドキュメントまたは電子メールが Azure Rights Management サービスを使用して保護されている場合、そのコンテンツを保護するアカウントは自動的にそのコンテンツの Rights Management 発行者になります。 このアカウントは、[利用状況ログ](log-analyze-usage.md#how-to-interpret-your-azure-rights-management-usage-logs)の**発行者**フィールドに記録されます。 

Rights Management 発行者には、常にドキュメントまたは電子メールのフル コントロール使用権限が与えられます。さらに、次の操作が可能です。

- 保護設定に有効期限が含まれる場合、Rights Management 発行者はその日付の後でもドキュメントまたは電子メールを開き、編集できます。

- Rights Management 発行者は常にドキュメントまたは電子メールにオフラインでアクセスできます。

- Rights Management 発行者は取り消されたドキュメントも開くことができます。 

既定では、このアカウントはそのコンテンツの **Rights Management 所有者**でもあります。これは、ドキュメントまたは電子メールを作成したユーザーが保護を開始した場合です。 ただし、管理者またはサービスがユーザーの代わりにコンテンツを保護できるシナリオもあります。 例 :

- 管理者がファイル共有のファイルを一括保護する: Azure AD の管理者アカウントがユーザーのためにドキュメントを保護します。

- Rights Management コネクタが Windows Server フォルダーの Office ドキュメントを保護する: RMS コネクタ用に作成された Azure AD のサービス プリンシパル アカウントがユーザーのためにドキュメントを保護します。

以上のシナリオでは、Rights Management 発行者は Azure Information Protection SDK または PowerShell を利用して Rights Management 所有者を別のアカウントに割り当てることができます。 たとえば、Azure Information Protection クライアントで [Protect-RMSFile](/powershell/module/azureinformationprotection/protect-rmsfile) PowerShell コマンドレットを使用するとき、**OwnerEmail** パラメーターを指定し、Rights Management 所有者を別のアカウントに割り当てることができます。 

ユーザーの代わりに Rights Management 発行者が保護を行う場合、元のドキュメントまたは電子メールの所有者に Rights Management 所有者を割り当てることで、保護コンテンツに対し、保護を自分で開始した場合と同じレベルのコントロールを与えることができます。 

たとえば、印刷使用権限が含まれていないテンプレートで保護されていても、ドキュメントを作成したユーザーはそのドキュメントを印刷できます。 そのテンプレートで構成されているオフライン アクセス設定や有効期限に関係なく、このユーザーは常に自分のドキュメントにアクセスできます。 さらに、Rights Management 所有者にはフル コントロール使用権限が与えられるため、このユーザーはドキュメントを再保護し、追加のユーザー アクセスを付与することもできます (その時点で、ユーザーは Rights Management 発行者と Rights Management 所有者になります)。このユーザーは保護を解除することもできます。 ただし、ドキュメントを追跡し、取り消すことができるのは、Rights Management 発行者だけです。

ドキュメントまたは電子メールの Rights Management 所有者は、[利用状況ログ](log-analyze-usage.md#how-to-interpret-your-azure-rights-management-usage-logs)で **owner-email** フィールドに記録されます。

Rights Management 所有者と Windows ファイル システム所有者に依存関係はありません。 この 2 つは多くの場合は同じですが、別々にすることもできます (SDK または PowerShell を使用しなくても)。

## <a name="rights-management-use-license"></a>Rights Management の使用ライセンス

Azure Rights Management によって保護されたドキュメントまたは電子メールをユーザーが開くと、そのコンテンツに対する Rights Management の使用ライセンスがユーザーに付与されます。 この使用ライセンスは証明書であり、ドキュメントまたは電子メール メッセージに対するユーザーの使用権限、およびコンテンツを暗号化するために使用された暗号化キーが含まれています。 また、使用ライセンスには有効期日 (設定されている場合) および使用ライセンスの有効期間も含まれます。

使用ライセンスの期間中、ユーザーは再認証も再承認も行われません。 そのため、ユーザーはインターネットに接続しなくても、保護されたドキュメントまたは電子メールを引き続き開くことができます。 使用ライセンスの有効期限を過ぎると、ユーザーは次回の保護されたドキュメントまたは電子メールへのアクセス時に、再認証および再承認される必要があります。 

保護設定を定義したラベルまたはテンプレートによってドキュメントおよび電子メール メッセージが保護されている場合は、ラベルまたはテンプレート内でこれらの設定を変更することができ、コンテンツを再保護する必要はありません。 ユーザーが既にコンテンツにアクセスしている場合は、使用ライセンスの有効期限が過ぎた後で変更が有効になります。 ただし、ユーザーがカスタム アクセス許可 (ad hoc 権利ポリシーとも呼ばれる) を適用した場合、ドキュメントまたは電子メールが保護された後でこれらのアクセス許可を変更する必要があるときは、そのコンテンツを新しいアクセス許可で再度保護する必要があります。 電子メール メッセージのカスタム アクセス許可は、[転送不可] オプションで実装されます。

テナントの既定の使用ライセンス有効期間は 30 日間であり、この値は PowerShell のコマンドレット [Set-AadrmMaxUseLicenseValidityTime](/powershell/module/aadrm/set-aadrmmaxuselicensevaliditytime) を使用して構成することができます。 ラベルまたはテンプレートを使用して保護を適用する場合は、より制限の厳しい設定を構成できます。

- Azure Portal で、ラベルまたはテンプレートを構成する場合は、使用ライセンスの有効期間として、**[オフライン アクセスの許可]** 設定の値が使用されます。 
    
    Azure Portal でこの設定を構成するための詳細とガイダンスについては、「[Rights Management による保護でラベルを構成する方法](configure-policy-protection.md)」の手順 9. の表を参照してください。

- PowerShell を使用してテンプレートを構成する場合、使用ライセンスの有効期間としては、[Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty) および [Add-AadrmTemplate](/powershell/module/aadrm/add-aadrmtemplate) コマンドレットの *LicenseValidityDuration* パラメーターの値が使用されます。
    
    PowerShell を使用してこの設定を構成するための詳細とガイダンスについては、各コマンドレットのヘルプを参照してください。


## <a name="see-also"></a>参照
[Azure Information Protection のテンプレートを構成して管理する](configure-policy-templates.md)

[Azure Rights Management および探索サービスまたはデータの回復用のスーパー ユーザーの構成](configure-super-users.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

