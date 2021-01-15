---
title: よくあるご質問と既知の問題 - Microsoft Information Protection SDK。
description: Microsoft Information Protection (MIP) SDK のよく寄せられる質問と、問題とエラーに関するトラブルシューティングのガイダンスです。
author: msmbaldwin
ms.service: information-protection
ms.topic: troubleshooting
ms.date: 03/05/2019
ms.author: mbaldwin
ms.openlocfilehash: da1e3f26ca4c2a0326b6ae8dfee7a13a1855044a
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98212605"
---
# <a name="microsoft-information-protection-mip-sdk-faqs-and-issues"></a>Microsoft Information Protection (MIP) SDK のよく寄せられる質問と問題

この記事では、よく寄せられる質問 (FAQ) に対する回答と、既知の問題と一般的なエラーに関するトラブルシューティングのガイダンスを示します。

## <a name="frequently-asked-questions"></a>よく寄せられる質問

### <a name="metadata-storage-changes"></a>メタデータストレージの変更

Office 365、SharePoint Online、およびその他のサービスの新機能をサポートするために、Office ファイル (Word、Excel、PowerPoint) のラベルメタデータストレージの場所を変更していることが [最近発表](https://aka.ms/mipsdkmetadata) されました。

#### <a name="metadata-faq"></a>メタデータに関する FAQ

**質問**: この新しいストレージの場所を必要とする最初の機能が利用可能になるのはいつですか。

- 最初の機能は、2021年の第2四半期に利用可能になる予定です。 お客様は、前にプライベートプレビューまたはパブリックプレビューを選択できます。  

**質問**: PDF など、他の形式に影響がありますか。

- Office ファイル、特に Word、Excel、PowerPoint ファイルのみ。

**質問**: 特定のバージョンの MIP SDK が必要ですか?

- MIP SDK 1.7 以降には完全に互換性があります。

**質問**: Office クライアントの特定のバージョンが必要になるか、このストアを使用しますか?

- 機能が発表されると、新しい記憶域の場所を利用するように Office クライアントが更新されます。 新しいストレージの場所は、テナント管理者が機能を有効にするまでは使用されません。

**質問**: のカスタムプロパティとして格納されている既存のメタデータを最新の状態に保つことが *custom.xml* ますか?

- いいえ。 新しいストレージの場所を有効にした後でドキュメントを初めて保存すると、ラベルのメタデータが新しい場所に移動されます。 によって書き込まれたメタデータ [`LabelingOptions.ExtendedProperties`](https://docs.microsoft.com/dotnet/api/microsoft.informationprotection.file.labelingoptions.extendedproperties?view=mipsdk-dotnet-1.7#Microsoft_InformationProtection_File_LabelingOptions_ExtendedProperties) は *custom.xml* に残ります。

**質問**: MIP SDK を使用せずにラベルメタデータを読み取ることはできますか? 

- はい。ただし、ファイルを解析して情報を抽出するには、独自のコードを実装する必要があります。

**質問**: 現時点では、ファイルからキー/値ペアの文字列を抽出することで、ラベルを簡単に "読み取る" ことができます。 このようにしても読み取りは可能ですか。 

- はい。メタデータは、Office ファイル XML で読み取ることができます。 ただし、アプリケーションでは、新しい機能セットが有効になっているかどうかを把握しておく必要があることに注意してください (custom.xml と labelinfo.xml)。 [MS-OFFCRYPTO の確認: LabelInfo とカスタムドキュメントプロパティ |Microsoft Docs。](https://docs.microsoft.com/openspecs/office_file_formats/ms-offcrypto/13939de6-c833-44ab-b213-e0088bf02341)実装の詳細。
  
**質問**: 新機能が有効になっているかどうかを確認するにはどうすればよいですか。 

- この情報は、機能のリリース日に近づくにつれて共有される予定です。 

**質問**: ラベルはどのように移行されますか。

- 次のロジックを使用して、ラベルデータの読み取りまたは書き込みに使用するセクションを決定します。

| 操作                                                                                                | 機能が有効になっていません                                                                    | 機能の有効化                                              |
| ----------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| 読み取り                                                                                                  | custom.xml (保護されていない) または Doc の概要情報 (保護されている) のラベル。                      | ラベルが labelinfo.xml に存在する場合は、有効なラベルです。<br> labelinfo.xml にラベルがない場合は、custom.xml または Doc の概要情報のラベルが有効なラベルになります。 |
| Write                                                                                                 | 新しいラベルはすべて custom.xml (保護されていない) または Doc の概要情報 (保護) に書き込まれます。 | 新しいラベルはすべて labelinfo.xml に書き込まれます。                 |


<br>
<br>

### <a name="file-parsing"></a>ファイルの解析

**質問**: 現在ファイル SDK で読み込んでいるのと同じファイルに書き込むことはできますか。

MIP SDK は、同じファイルの読み取りと書き込みを同時にサポートしていません。 ラベルが付けられたファイルは、ラベルアクションが適用された入力ファイルの *コピー* になります。 アプリケーションでは、元のファイルをラベル付きファイルに置き換える必要があります。

### <a name="sdk-string-handling"></a>SDK 文字列の処理

**質問**: SDK はどのようにして文字列を処理しますか? また、コードで使用する文字列型はどのようなものですか。

SDK はクロスプラットフォームでの使用を想定しています。文字列の処理には [UTF-8 (Unicode Transformation Format - 8 ビット)](https://wikipedia.org/wiki/UTF-8) が使用されます。 具体的なガイダンスは、使用するプラットフォームによって異なります。

| プラットフォーム        | ガイダンス                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Windows ネイティブ  | C++ SDK クライアントの場合、 [`std::string`](https://wikipedia.org/wiki/C%2B%2B_string_handling) API 関数との間で文字列を渡すために C++ 標準ライブラリの型が使用されます。 UTF-8 との間での変換は、MIP SDK によって内部的に管理されます。 API から `std::string` が返されるときは、UTF-8 エンコードを想定し、文字列を変換する場合はそれに応じて管理する必要があります。 場合によっては、文字列が `uint8_t` ベクター (発行ライセンス (PL) など) の一部として返されることがありますが、これは不透明な BLOB として扱う必要があります。<br><br>詳細および例については、次をご覧ください。<ul><li>ワイド文字の文字列を UTF-8 などの複数バイトに変換するのをサポートする [WideCharToMultiByte 関数](/windows/desktop/api/stringapiset/nf-stringapiset-widechartomultibyte)。<li>[SDK ダウンロード](setup-configure-mip.md#configure-your-client-workstation)に含まれる次のサンプル ファイル:<ul><li>ワイド UTF-8 文字列との間で変換するための、`file\samples\common\string_utils.cpp` の文字列ユーティリティ関数のサンプル。<li>前の文字列変換関数を使用する、`file\samples\file\main.cpp` の `wmain(int argc, wchar_t *argv[])` の実装。</li></ul></ul> |
| .NET            | .NET SDK クライアントでは、すべての文字列で既定の UTF-16 エンコードが使用され、特別な変換は必要ありません。 UTF-16 との間での変換は、MIP SDK によって内部的に管理されます。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| その他のプラットフォーム | MIP SDK でサポートされているその他のすべてのプラットフォームでは、UTF-8 がネイティブでサポートされています。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

## <a name="issues-and-errors-reference"></a>問題とエラーのリファレンス

### <a name="error-file-format-not-supported"></a>エラー: "ファイル形式がサポートされていません"  

**質問**: PDF ファイルを保護またはラベル付けしようとすると、次のエラーが表示されるのはなぜですか。

> ファイル形式がサポートされていません

この例外は、デジタル署名またはパスワードで保護されている PDF ファイルを保護またはラベル付けしようとした場合に発生します。 PDF ファイルの保護とラベル付けについて詳しくは、「[New support for PDF encryption with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/New-support-for-PDF-encryption-with-Microsoft-Information/ba-p/262757)」(Microsoft Information Protection での PDF の新しい暗号化のサポート) をご覧ください。

### <a name="error-failed-to-parse-the-acquired-compliance-policy"></a>エラー: "取得したコンプライアンス ポリシーを解析できませんでした"  

**質問**: MIP SDK をダウンロードし、ファイルのサンプルを使用してすべてのラベルを表示しようとした後に、次のエラーが表示されるのはなぜですか。

> エラーが発生しました: 取得したコンプライアンス ポリシーを解析できませんでした。 Failed with: [class mip::CompliancePolicyParserException] Tag not found: policy, NodeType: 15, Name: No Name Found, Value: , Ancestors: <SyncFile><Content>, correlationId:[34668a40-blll-4ef8-b2af-00005aa674z9]

このエラーは、ラベルを Azure Information Protection から統合されたラベル付けエクスペリエンスに移行していないことを示しています。 「[Azure Information Protection ラベルを Office 365 セキュリティ/コンプライアンス センターに移行する方法](/azure/information-protection/configure-policy-migrate-labels)」に従ってラベルを移行した後、Office 365 セキュリティとコンプライアンス センターでラベル ポリシーを作成します。 

### <a name="error-nopolicyexception-label-policy-did-not-contain-data"></a>エラー: "NoPolicyException: ラベルポリシーにデータが含まれていません"

**質問**: MIP SDK を使用してラベルを読み取り、ラベルを一覧表示しようとすると、次のエラーが表示されるのはなぜですか。

> NoPolicyException: ラベルポリシーにデータが含まれていませんでした。 CorrelationId = GUID, CorrelationId. Description = PolicyProfile, Nopolicyexception. Category = SyncFile, Nopolicyexception. Category = SyncFile

このエラーは、ラベルポリシーが Microsoft のセキュリティとコンプライアンスセンターで公開されていないことを示します。 ラベル付けポリシーを構成するには、「 [秘密度ラベルとそのポリシーを作成して構成](/microsoft-365/compliance/create-sensitivity-labels) する」に従ってください。

### <a name="error-systemcomponentmodelwin32exception-loadlibrary-failed"></a>エラー: "System.componentmodel. Win32Exception: LoadLibrary が失敗しました"

**質問**: MIP SDK .net ラッパーを使用すると、次のエラーが表示されるのはなぜですか。

> MIP.Initialize () を呼び出すときに、: [sdk_wrapper_dotnet.dll] の System.componentmodel: LoadLibrary が失敗しました。

アプリケーションに必要なランタイムがないか、またはリリースとしてビルドされていません。 詳細については、「 [アプリに必要なランタイムがあることを確認](setup-configure-mip.md#ensure-your-app-has-the-required-runtime) する」を参照してください。 

### <a name="error-proxyautherror-exception"></a>エラー: "ProxyAuthError 例外"

**質問**: MIP SDK を使用すると、次のエラーが表示されるのはなぜですか。

> "Proxyauthentication Atonerror: プロキシ認証がサポートされていません"

MIP SDK は、認証されたプロキシの使用をサポートしていません。 このメッセージを修正するには、プロキシ管理者は、プロキシをバイパスするように Microsoft Information Protection サービスエンドポイントを設定する必要があります。 これらのエンドポイントの一覧については、「 [Office 365 の url と IP アドレス範囲](/office365/enterprise/urls-and-ip-address-ranges) 」ページを参照してください。 MIP SDK で `*.protection.outlook.com` は、(行 9) と Azure Information Protection サービスエンドポイント (行 73) がプロキシ認証をバイパスする必要があります。
