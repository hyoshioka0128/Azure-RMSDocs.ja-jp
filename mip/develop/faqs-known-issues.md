---
title: よくあるご質問と既知の問題 - Microsoft Information Protection SDK。
description: Microsoft Information Protection (MIP) SDK のよく寄せられる質問と、問題とエラーに関するトラブルシューティングのガイダンスです。
author: msmbaldwin
ms.service: information-protection
ms.topic: troubleshooting
ms.date: 03/05/2019
ms.author: mbaldwin
ms.openlocfilehash: 0fbb704024a87cbee30016a2f5130d788609cea3
ms.sourcegitcommit: 437057990372948c9435b620052a7398360264b9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2020
ms.locfileid: "97701562"
---
# <a name="microsoft-information-protection-mip-sdk-faqs-and-issues"></a>Microsoft Information Protection (MIP) SDK のよく寄せられる質問と問題

この記事では、よく寄せられる質問 (FAQ) に対する回答と、既知の問題と一般的なエラーに関するトラブルシューティングのガイダンスを示します。

## <a name="frequently-asked-questions"></a>よく寄せられる質問 

### <a name="file-parsing"></a>ファイルの解析

**質問**: 現在ファイル SDK で読み込んでいるのと同じファイルに書き込むことはできますか。

MIP SDK は、同じファイルの読み取りと書き込みを同時にサポートしていません。 ラベルが付けられたファイルは、ラベルアクションが適用された入力ファイルの *コピー* になります。 アプリケーションでは、元のファイルをラベル付きファイルに置き換える必要があります。 

### <a name="sdk-string-handling"></a>SDK 文字列の処理

**質問**: SDK はどのようにして文字列を処理しますか? また、コードで使用する文字列型はどのようなものですか。

SDK はクロスプラットフォームでの使用を想定しています。文字列の処理には [UTF-8 (Unicode Transformation Format - 8 ビット)](https://wikipedia.org/wiki/UTF-8) が使用されます。 具体的なガイダンスは、使用するプラットフォームによって異なります。

| プラットフォーム | ガイダンス |
|-|-|
| Windows ネイティブ | C++ SDK クライアントの場合、 [`std::string`](https://wikipedia.org/wiki/C%2B%2B_string_handling) API 関数との間で文字列を渡すために C++ 標準ライブラリの型が使用されます。 UTF-8 との間での変換は、MIP SDK によって内部的に管理されます。 API から `std::string` が返されるときは、UTF-8 エンコードを想定し、文字列を変換する場合はそれに応じて管理する必要があります。 場合によっては、文字列が `uint8_t` ベクター (発行ライセンス (PL) など) の一部として返されることがありますが、これは不透明な BLOB として扱う必要があります。<br><br>詳細および例については、次をご覧ください。<ul><li>ワイド文字の文字列を UTF-8 などの複数バイトに変換するのをサポートする [WideCharToMultiByte 関数](/windows/desktop/api/stringapiset/nf-stringapiset-widechartomultibyte)。<li>[SDK ダウンロード](setup-configure-mip.md#configure-your-client-workstation)に含まれる次のサンプル ファイル:<ul><li>ワイド UTF-8 文字列との間で変換するための、`file\samples\common\string_utils.cpp` の文字列ユーティリティ関数のサンプル。<li>前の文字列変換関数を使用する、`file\samples\file\main.cpp` の `wmain(int argc, wchar_t *argv[])` の実装。</li></ul></ul>|
| .NET | .NET SDK クライアントでは、すべての文字列で既定の UTF-16 エンコードが使用され、特別な変換は必要ありません。 UTF-16 との間での変換は、MIP SDK によって内部的に管理されます。 |
| その他のプラットフォーム | MIP SDK でサポートされているその他のすべてのプラットフォームでは、UTF-8 がネイティブでサポートされています。 |

## <a name="issues-and-errors-reference"></a>問題とエラーのリファレンス

### <a name="error-file-format-not-supported"></a>エラー: "ファイル形式がサポートされていません"  

**質問**: PDF ファイルを保護またはラベル付けしようとすると、次のエラーが表示されるのはなぜですか。

> ファイル形式がサポートされていません

この例外は、デジタル署名またはパスワードで保護されている PDF ファイルを保護またはラベル付けしようとした場合に発生します。 PDF ファイルの保護とラベル付けについて詳しくは、「[New support for PDF encryption with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/New-support-for-PDF-encryption-with-Microsoft-Information/ba-p/262757)」(Microsoft Information Protection での PDF の新しい暗号化のサポート) をご覧ください。

### <a name="error-failed-to-parse-the-acquired-compliance-policy"></a>エラー: "取得したコンプライアンス ポリシーを解析できませんでした"  

**質問**: MIP SDK をダウンロードし、ファイルのサンプルを使用してすべてのラベルを表示しようとした後に、次のエラーが表示されるのはなぜですか。

> エラーが発生しました: 取得したコンプライアンス ポリシーを解析できませんでした。 Failed with: [class mip::CompliancePolicyParserException] Tag not found: policy, NodeType: 15, Name: No Name Found, Value: , Ancestors: <SyncFile><Content>, correlationId:[34668a40-blll-4ef8-b2af-00005aa674z9]

これは、ラベルを Azure Information Protection から統合されたラベル付けエクスペリエンスに移行していないことを示しています。 「[Azure Information Protection ラベルを Office 365 セキュリティ/コンプライアンス センターに移行する方法](/azure/information-protection/configure-policy-migrate-labels)」に従ってラベルを移行した後、Office 365 セキュリティとコンプライアンス センターでラベル ポリシーを作成します。 

### <a name="error-nopolicyexception-label-policy-did-not-contain-data"></a>エラー: "NoPolicyException: ラベルポリシーにデータが含まれていません"

**質問**: MIP SDK を使用してラベルを読み取り、ラベルを一覧表示しようとすると、次のエラーが表示されるのはなぜですか。

> NoPolicyException: ラベルポリシーにデータが含まれていませんでした。 CorrelationId = GUID, CorrelationId. Description = PolicyProfile, Nopolicyexception. Category = SyncFile, Nopolicyexception. Category = SyncFile

これは、Microsoft のセキュリティとコンプライアンスセンターで、ラベル付けポリシーが発行されていないことを示します。 ラベル付けポリシーを構成するには、「 [秘密度ラベルとそのポリシーを作成して構成](/microsoft-365/compliance/create-sensitivity-labels) する」に従ってください。

### <a name="error-systemcomponentmodelwin32exception-loadlibrary-failed"></a>エラー: "System.componentmodel. Win32Exception: LoadLibrary が失敗しました"

**質問**: MIP SDK .net ラッパーを使用すると、次のエラーが表示されるのはなぜですか。

> MIP.Initialize () を呼び出すときに、: [sdk_wrapper_dotnet.dll] の System.componentmodel: LoadLibrary が失敗しました。

アプリケーションに必要なランタイムがないか、またはリリースとしてビルドされていません。 詳細については、「 [アプリに必要なランタイムがあることを確認](setup-configure-mip.md#ensure-your-app-has-the-required-runtime) する」を参照してください。 

### <a name="error-proxyautherror-exception"></a>エラー: "ProxyAuthError 例外"

**質問**: MIP SDK を使用すると、次のエラーが表示されるのはなぜですか。

> "Proxyauthentication Atonerror: プロキシ認証がサポートされていません"

MIP SDK は、認証されたプロキシの使用をサポートしていません。 このメッセージを修正するには、プロキシ管理者は、プロキシをバイパスするように Microsoft Information Protection サービスエンドポイントを設定する必要があります。 これらのエンドポイントの一覧については、「 [Office 365 の url と IP アドレス範囲](/office365/enterprise/urls-and-ip-address-ranges) 」ページを参照してください。 MIP SDK で `*.protection.outlook.com` は、(行 9) と Azure Information Protection サービスエンドポイント (行 73) がプロキシ認証をバイパスする必要があります。
