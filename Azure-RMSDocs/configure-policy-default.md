---
title: Azure Information Protection の既定のポリシー
description: Azure Information Protection の既定のポリシーの構成方法について説明します。 既定のポリシーを変更した場合、これらの値を参照して、ポリシーを既定値に戻すことができます。
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/09/2018
ms.topic: article
ms.service: information-protection
ms.assetid: 671281c8-f0d1-42b6-aae3-681d1821e2cf
ms.openlocfilehash: ada4e4b2b7f8ef4bcf95307184d9c262a930c9f0
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2018
ms.locfileid: "42807324"
---
# <a name="the-default-azure-information-protection-policy"></a>Azure Information Protection の既定のポリシー

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

以下では、Azure Information Protection の既定のポリシーの構成方法を説明します。

管理者が Azure Portal を使用して最初に Azure Information Protection サービスに接続したときに、そのテナントの既定のポリシーが作成されます。 Microsoft は、時折、既定のポリシーに変更を加えることがありますが、既定のポリシーが改訂される前に、既にサービスを使用していた場合、以前のバージョンの既定のポリシーは更新されません。これは、ユーザーが既定のポリシーを構成し、運用環境に展開している可能性があるためです。

次の値を参照してポリシーを既定値に戻したり、ポリシーを最新の値に更新したりすることができます。

## <a name="current-default-policy"></a>最新の既定のポリシー

このバージョンの既定のポリシーは、2017 年 7 月 31 日付けのものです。

この既定のポリシーは、Azure Rights Management サービスがアクティブ化される場合 (2018 年 2 月以降の新しいテナントの場合) に作成されます。 詳細については、ブログ投稿のお知らせ「[Improvements to the protection stack in Azure Information Protection (Azure Information Protection の保護スタックの向上)](https://cloudblogs.microsoft.com/enterprisemobility/2018/03/08/improvements-to-the-protection-stack-in-azure-information-protection)」を参照してください。

この既定のポリシーは、ポリシーの作成前に手動で[サービスをアクティブ化](activate-service.md)した場合にも作成されます。 

サービスがアクティブ化しなかった場合、既定のポリシーは次のサブラベルの保護を構成しません。

- **社外秘 \ すべての従業員**

- **社外秘 \ 受信者のみ**

- **非常に機密性の高い社外秘 \ すべての従業員** 

- **非常に機密性の高い社外秘 \ 受信者のみ** 

保護に対してこれらのサブラベルが自動的に構成されないとき、既定のポリシーは[前の既定のポリシー](#default-policy-before-july-31-2017)と同じになります。

保護が **[すべての従業員]** サブラベルに適用されるとき、Azure Portal で自動的にラベルに変換される既定のテンプレートを利用し、保護が構成されます。 これらのテンプレートの詳細については、「[Azure Information Protection のテンプレートを構成して管理する](configure-policy-templates.md)」を参照してください。

2017 年 8 月 30 日以降、既定ポリシーのこのバージョンには、ラベルの名前と説明の多言語版が含まれるようになりました。 

#### <a name="more-information-about-the-recipients-only-sublabel"></a>[受信者のみ] サブラベルに関する詳細

ユーザーには Outlook のみでこのラベルが表示されます。 このラベルは Word、Excel、PowerPoint には表示されず、エクスプローラーからも表示されません。 

ユーザーがこのラベルを選択すると、Outlook の [転送不可] オプションがメールに自動的に適用されます。 ユーザーが指定した受信者はメールを転送したり、コンテンツをコピーまたは印刷したり、添付ファイルを保存したりできません。


### <a name="labels"></a>ラベル

|Label|ツールヒント|Settings|
|-------------------------------|---------------------------|-----------------|
|個人用|ビジネス以外のデータ、個人用としてのみ使用します。|**有効**: オン <br /><br />**色**: 明るい緑<br /><br />**視覚的なマーキング**: オフ <br /><br />**条件**: なし<br /><br />**保護**: なし|
|パブリック|パブリックで使用するために、特別に準備され、承認されたビジネス データ。|**有効**: オン <br /><br />**色**: 緑<br /><br />**視覚的なマーキング**: オフ<br /><br />**条件**: なし<br /><br />**保護**: なし|
|全般|パブリックでの使用を目的としないビジネス データ。 ただし、これは必要に応じて、外部のパートナーと共有できます。 たとえば、会社の内部電話帳、組織図、社内基準、内部通信の大部分が含まれます。|**有効**: オン <br /><br />**色**: 青 <br /><br />**視覚的なマーキング**: オフ<br /><br />**条件**: なし<br /><br />**保護**: なし|
|社外秘|承認されていない人と共有した場合、ビジネスに損害を与える可能性のある機密性の高いビジネス データ。 例としては、契約書、セキュリティ レポート、予測の概要、および販売取引データなどがあります。|**有効**: オン <br /><br />**色**: オレンジ<br /><br />**視覚的なマーキング**: オフ<br /><br />**条件**: なし<br /><br />**保護**: なし|
|非常に機密性の高い社外秘|承認されていない人と共有した場合、ビジネスに損害を与える可能性のある非常に機密性の高いビジネス データ。 例としては、従業員と顧客の情報、パスワード、ソース コード、および発表前の財務レポートなどがあります。|**有効**: オン <br /><br />**色**: 赤<br /><br />**視覚的なマーキング**: オフ<br /><br />**条件**: なし<br /><br />**保護**: なし|


### <a name="sublabels"></a>サブラベル

|Label|ツールヒント|Settings|
|-------------------------------|---------------------------|-----------------|
|社外秘 \ すべての従業員|保護を必要とする機密データ。すべての従業員に完全なアクセス許可を付与します。 データ所有者は、コンテンツの追跡や取り消しを実行できます。|**有効**: オン <br /><br />**視覚的なマーキング**: フッター (ドキュメントや電子メール)<br /><br />社外秘として分類<br /><br />**条件**: なし<br /><br />**保護**: Azure (クラウド キー) [[1]](#footnote-1)|
|社外秘 \ (保護されていない) すべてのユーザー|保護を必要としないデータ。 このオプションは、適切な業務の理由がある場合に、注意して使用します。|**有効**: オン <br /><br />**視覚的なマーキング**: フッター (ドキュメントや電子メール)<br /><br />社外秘として分類 <br /><br />**条件**: なし<br /><br />**保護**: なし|
|社外秘 \ 受信者のみ|保護を必要とし、受信者だけが閲覧できる機密データ。|**有効**: オン <br /><br />**視覚的なマーキング**: フッター (電子メール)<br /><br />社外秘として分類 <br /><br />**条件**: なし<br /><br />**保護**: ユーザー定義のアクセス許可を設定します (プレビュー)。Outlook では転送不可を適用します|
|非常に機密性の高い社外秘 \ すべての従業員|すべての従業員に対して、このコンテンツの表示、編集、返信のアクセス許可を付与する非常に機密性の高い社外秘データ。 データ所有者は、コンテンツの追跡や取り消しを実行できます。|**有効**: オン <br /><br />**視覚的なマーキング**: フッター (ドキュメントや電子メール)<br /><br />非常に機密性の高い社外秘として分類<br /><br />**条件**: なし<br /><br />**保護**: Azure (クラウド キー) [[2]](#footnote-2)|
|非常に機密性の高い社外秘 \ (保護されていない) すべてのユーザー|保護を必要としないデータ。 このオプションは、適切な業務の理由がある場合に、注意して使用します。|**有効**: オン <br /><br />**視覚的なマーキング**: フッター (ドキュメントや電子メール)<br /><br />非常に機密性の高い社外秘として分類<br /><br />**条件**: なし<br /><br />**保護**: なし|
|非常に機密性の高い社外秘 \ 受信者のみ|保護を必要とし、受信者だけが閲覧できる非常に機密性の高いデータ。|**有効**: オン <br /><br />**視覚的なマーキング**: フッター (電子メール)<br /><br />非常に機密性の高い社外秘として分類 <br /><br />**条件**: なし<br /><br />**保護**: ユーザー定義のアクセス許可を設定します (プレビュー)。Outlook では転送不可を適用します|

###### <a name="footnote-1"></a>脚注 1:
保護のアクセス許可は、[既定のテンプレート](configure-policy-templates.md#default-templates)である**社外秘 \ すべての従業員**でこれらと一致します。

###### <a name="footnote-2"></a>脚注 2: 
保護のアクセス許可は、[既定のテンプレート](configure-policy-templates.md#default-templates)である**非常に機密性の高い社外秘 \ すべての従業員**でこれらと一致します。


### <a name="information-protection-bar"></a>Information Protection バー

|Setting|値|
|-------------------------------|---------------------------|
|タイトル|検出感度|
|ツールヒント|このコンテンツの現在のラベル。 このコンテンツが組織内外の承認されていないユーザーと共有されている場合、この設定はビジネスのリスクを識別します。|


### <a name="settings"></a>Settings

|Setting|値|
|-------------------------------|---------------------------|
|All documents and emails must have a label (applied automatically or by users) (すべてのドキュメントと電子メールにラベルを設定する必要があります (自動設定またはユーザーが設定))|オフ|
|Select the default label (既定のラベルを選択する)|なし|
|Users must provide justification to set a lower classification label, remove a label, or remove protection (ユーザーは分類ラベルの秘密度を下げる、ラベルを削除する、または保護を解除するときにその理由を示す必要があります)|オフ|
|添付ファイル付きの電子メール メッセージの場合、添付ファイルの最上位の分類に一致するラベルを適用します|オフ|
|Azure Information Protection クライアントの "詳細" Web ページのカスタム URL を指定します|新規|


## <a name="default-policy-before-july-31-2017"></a>2017 年 7 月 31 日より前の既定のポリシー

このポリシーの説明では、保護を必要とするデータおよびデータの追跡や取り消しについて言及しています。 ポリシーでは、これらのラベルについてこの保護を構成するわけではないため、この説明を満たすためには追加の手順を実行する必要があります。 たとえば、保護を適用したり、データ損失防止 (DLP) ソリューションを使用したりするようにラベルを構成します。 ドキュメント追跡サイトを使用してドキュメントの追跡や取り消しを行うには、Azure Rights Management サービスでドキュメントを保護し、ドキュメントを保護したユーザーがドキュメントを追跡記録する必要があります。 


### <a name="labels"></a>ラベル

|Label|ツールヒント|Settings|
|-------------------------------|---------------------------|-----------------|
|個人用|ビジネス以外のデータ、個人用としてのみ使用します。|**有効**: オン <br /><br />**色**: 明るい緑<br /><br />**視覚的なマーキング**: オフ <br /><br />**条件**: なし<br /><br />**保護**: なし|
|パブリック|パブリックで使用するために、特別に準備され、承認されたビジネス データ。|**有効**: オン <br /><br />**色**: 緑<br /><br />**視覚的なマーキング**: オフ<br /><br />**条件**: なし<br /><br />**保護**: なし|
|全般|パブリックでの使用を目的としないビジネス データ。 ただし、これは必要に応じて、外部のパートナーと共有できます。 たとえば、会社の内部電話帳、組織図、社内基準、内部通信の大部分が含まれます。|**有効**: オン <br /><br />**色**: 青 <br /><br />**視覚的なマーキング**: オフ<br /><br />**条件**: なし<br /><br />**保護**: なし|
|社外秘|承認されていない人と共有した場合、ビジネスに損害を与える可能性のある機密性の高いビジネス データ。 例としては、契約書、セキュリティ レポート、予測の概要、および販売取引データなどがあります。|**有効**: オン <br /><br />**色**: オレンジ<br /><br />**視覚的なマーキング**: オフ<br /><br />**条件**: なし<br /><br />**保護**: なし|
|非常に機密性の高い社外秘|承認されていない人と共有した場合、ビジネスに損害を与える可能性のある非常に機密性の高いビジネス データ。 例としては、従業員と顧客の情報、パスワード、ソース コード、および発表前の財務レポートなどがあります。|**有効**: オン <br /><br />**色**: 赤<br /><br />**視覚的なマーキング**: オフ<br /><br />**条件**: なし<br /><br />**保護**: なし|


### <a name="sublabels"></a>サブラベル

|Label|ツールヒント|Settings|
|-------------------------------|---------------------------|-----------------|
|社外秘 \ すべての従業員|保護を必要とする機密データ。すべての従業員に完全なアクセス許可を付与します。 データ所有者は、コンテンツの追跡や取り消しを実行できます。|**有効**: オン <br /><br />**視覚的なマーキング**: フッター (ドキュメントや電子メール)<br /><br />社外秘として分類<br /><br />**条件**: なし<br /><br />**保護**: なし|
|社外秘 \ (保護されていない) すべてのユーザー|保護を必要としないデータ。 このオプションは、適切な業務の理由がある場合に、注意して使用します。|**有効**: オン <br /><br />**視覚的なマーキング**: フッター (ドキュメントや電子メール)<br /><br />社外秘として分類 <br /><br />**条件**: なし<br /><br />**保護**: なし|
|非常に機密性の高い社外秘 \ すべての従業員|すべての従業員に対して、このコンテンツの表示、編集、返信のアクセス許可を付与する非常に機密性の高い社外秘データ。 データ所有者は、コンテンツの追跡や取り消しを実行できます。|**有効**: オン <br /><br />**視覚的なマーキング**: フッター (ドキュメントや電子メール)<br /><br />非常に機密性の高い社外秘として分類<br /><br />**条件**: なし<br /><br />**保護**: なし|
|非常に機密性の高い社外秘 \ (保護されていない) すべてのユーザー|保護を必要としないデータ。 このオプションは、適切な業務の理由がある場合に、注意して使用します。|**有効**: オン <br /><br />**視覚的なマーキング**: フッター (ドキュメントや電子メール)<br /><br />非常に機密性の高い社外秘として分類<br /><br />**条件**: なし<br /><br />**保護**: なし|

### <a name="information-protection-bar"></a>Information Protection バー

|Setting|値|
|-------------------------------|---------------------------|
|タイトル|検出感度|
|ツールヒント|このコンテンツの現在のラベル。 このコンテンツが組織内外の承認されていないユーザーと共有されている場合、この設定はビジネスのリスクを識別します。|


### <a name="settings"></a>Settings

|Setting|値|
|-------------------------------|---------------------------|
|All documents and emails must have a label (applied automatically or by users) (すべてのドキュメントと電子メールにラベルを設定する必要があります (自動設定またはユーザーが設定))|オフ|
|Select the default label (既定のラベルを選択する)|なし|
|Users must provide justification to set a lower classification label, remove a label, or remove protection (ユーザーは分類ラベルの秘密度を下げる、ラベルを削除する、または保護を解除するときにその理由を示す必要があります)|オフ|
|添付ファイル付きの電子メール メッセージの場合、添付ファイルの最上位の分類に一致するラベルを適用します|オフ|
|Azure Information Protection クライアントの "詳細" Web ページのカスタム URL を指定します|新規|

## <a name="default-policy-before-march-21-2017"></a>2017 年 3 月 21 日より前の既定のポリシー

### <a name="labels"></a>ラベル

|Label|ツールヒント|Settings|
|-------------------------------|---------------------------|-----------------|
|個人用|個人用としてのみ使用します。 このデータは組織によって監視されることはありません。 個人用の情報にビジネスに関連するデータを含めないでください。|**有効**: オン <br /><br />**色**: 明るい緑<br /><br />**視覚的なマーキング**: オフ <br /><br />**条件**: なし<br /><br />**保護**: なし|
|パブリック|これは内部情報であり、社内および社外のだれもが使用できます。|**有効**: オン <br /><br />**色**: 緑<br /><br />**視覚的なマーキング**: オフ<br /><br />**条件**: なし<br /><br />**保護**: なし|
|内部|この情報には、すべての従業員が使用でき、承認された顧客およびビジネス パートナーと共有できる、幅広い内部ビジネス データが含まれます。 内部情報の例として、会社のポリシーや、ほとんどの内部通信が挙げられます。|**有効**: オン <br /><br />**色**: 青 <br /><br />**視覚的なマーキング**: フッター (ドキュメントや電子メール): <br /><br />検出感度: 内部<br /><br />**条件**: なし<br /><br />**保護**: なし|
|社外秘|このデータには機密性の高いビジネス情報が含まれます。 承認されていないユーザーにこのデータを公開すると、組織に損害が生じる可能性があります。 機密情報の例には、従業員情報、個々の顧客のプロジェクトまたは契約書、販売取引データなどがあります。|**有効**: オン <br /><br />**色**: オレンジ<br /><br />**視覚的なマーキング**: フッター (ドキュメントや電子メール):<br /><br /> 検出感度: 社外秘<br /><br />**条件**: なし<br /><br />**保護**: なし|
|秘密|このデータには、保護する必要がある機密性の高いビジネス情報が含まれます。 承認されていないユーザーに秘密データを公開すると、組織に深刻な損害が生じる可能性があります。 秘密情報の例には、個人識別情報、顧客レコード、ソース コード、発表前の財務レポートなどがあります。|**有効**: オン <br /><br />**色**: 赤<br /><br />**視覚的なマーキング**: フッター (ドキュメントや電子メール):<br /><br /> 検出感度: 秘密<br /><br />**条件**: なし<br /><br />**保護**: なし|


### <a name="sublabels"></a>サブラベル

|Label|ツールヒント|Settings|
|-------------------------------|---------------------------|-----------------|
|秘密 \ 会社全体|このデータには、すべての会社の従業員に対して許可される機密性のあるビジネス情報が含まれます。|**有効**: オン <br /><br />**視覚的なマーキング**: オフ<br /><br />**条件**: なし<br /><br />**保護**: なし|
|秘密 \ マイ グループ|このデータには、従業員グループに対してのみ許可される機密性のあるビジネス情報が含まれます。|**有効**: オン <br /><br />**視覚的なマーキング**: オフ<br /><br />**条件**: なし<br /><br />**保護**: なし|

### <a name="information-protection-bar"></a>Information Protection バー

|Setting|値|
|-------------------------------|---------------------------|
|タイトル|検出感度|
|ツールヒント|情報の秘密度は 4 つの異なるレベル (パブリック、内部、機密、秘密) で構成され、これによってユーザーは、社内または社外の承認されていないユーザーに対する情報漏えいのリスクを識別できます。|


### <a name="settings"></a>Settings

|Setting|値|
|-------------------------------|---------------------------|
|All documents and emails must have a label (applied automatically or by users) (すべてのドキュメントと電子メールにラベルを設定する必要があります (自動設定またはユーザーが設定))|オフ|
|Select the default label (既定のラベルを選択する)|なし|
|Users must provide justification to set a lower classification label, remove a label, or remove protection (ユーザーは分類ラベルの秘密度を下げる、ラベルを削除する、または保護を解除するときにその理由を示す必要があります)|オフ|
|Azure Information Protection クライアントの "詳細" Web ページのカスタム URL を指定します|新規|


## <a name="next-steps"></a>次の手順

Azure Information Protection ポリシーの構成の詳細については、「[組織のポリシーの構成](configure-policy.md#configuring-your-organizations-policy)」セクションのリンクを使用してください。 