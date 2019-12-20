---
title: よくあるご質問と既知の問題 - Microsoft Information Protection SDK。
description: Microsoft Information Protection (MIP) SDK のよく寄せられる質問と、問題とエラーに関するトラブルシューティングのガイダンスです。
author: msmbaldwin
ms.service: information-protection
ms.topic: troubleshooting
ms.collection: M365-security-compliance
ms.date: 03/05/2019
ms.author: mbaldwin
ms.openlocfilehash: 78dc655d8244378fcc37b22030d3060fd291ef16
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "60175470"
---
# <a name="microsoft-information-protection-mip-sdk-faqs-and-issues"></a>Microsoft Information Protection (MIP) SDK のよく寄せられる質問と問題

この記事では、よく寄せられる質問 (FAQ) に対する回答と、既知の問題と一般的なエラーに関するトラブルシューティングのガイダンスを示します。

## <a name="frequently-asked-questions"></a>AppLocker: Frequently Asked Questions (AppLocker: よく寄せられる質問) 

### <a name="sdk-string-handling"></a>SDK 文字列の処理

**質問**: SDK はどのようにして文字列を処理しますか? また、コードで使用する文字列型はどのようなものですか。

SDK はクロスプラットフォームでの使用を想定しています。文字列の処理には [UTF-8 (Unicode Transformation Format - 8 ビット)](https://wikipedia.org/wiki/UTF-8) が使用されます。 具体的なガイダンスは、使用するプラットフォームによって異なります。

| プラットフォーム | ガイダンス |
|-|-|
| Windows ネイティブ | C++ の SDK クライアントでは、API 関数との文字列のやり取りには C++ 標準ライブラリの型 [`std::string`](https://wikipedia.org/wiki/C%2B%2B_string_handling) が使用されます。 UTF-8 との間での変換は、MIP SDK によって内部的に管理されます。 API から `std::string` が返されるときは、UTF-8 エンコードを想定し、文字列を変換する場合はそれに応じて管理する必要があります。 場合によっては、文字列が `uint8_t` ベクター (発行ライセンス (PL) など) の一部として返されることがありますが、これは不透明な BLOB として扱う必要があります。<br><br>詳細および例については、次をご覧ください。<ul><li>ワイド文字の文字列を UTF-8 などの複数バイトに変換するのをサポートする [WideCharToMultiByte 関数](/windows/desktop/api/stringapiset/nf-stringapiset-widechartomultibyte)。<li>[SDK ダウンロード](setup-configure-mip.md#configure-your-client-workstation)に含まれる次のサンプル ファイル:<ul><li>ワイド UTF-8 文字列との間で変換するための、`file\samples\common\string_utils.cpp` の文字列ユーティリティ関数のサンプル。<li>前の文字列変換関数を使用する、`file\samples\file\main.cpp` の `wmain(int argc, wchar_t *argv[])` の実装。</li></ul></ul>|
| .NET | .NET SDK クライアントでは、すべての文字列で既定の UTF-16 エンコードが使用され、特別な変換は必要ありません。 UTF-16 との間での変換は、MIP SDK によって内部的に管理されます。 |
| その他のプラットフォーム | MIP SDK でサポートされているその他のすべてのプラットフォームでは、UTF-8 がネイティブでサポートされています。 |

## <a name="issues-and-errors-reference"></a>問題とエラーのリファレンス

### <a name="error-file-format-not-supported"></a>エラー: "ファイル形式がサポートされていません"  

**質問**: PDF ファイルを保護またはラベル付けしようとすると、次のエラーが表示されるのはなぜですか。

> ファイル形式はサポートされていません

この例外は、デジタル署名またはパスワードで保護されている PDF ファイルを保護またはラベル付けしようとした場合に発生します。 PDF ファイルの保護とラベル付けについて詳しくは、「[New support for PDF encryption with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/New-support-for-PDF-encryption-with-Microsoft-Information/ba-p/262757)」(Microsoft Information Protection での PDF の新しい暗号化のサポート) をご覧ください。

### <a name="error-failed-to-parse-the-acquired-compliance-policy"></a>エラー: "取得したコンプライアンス ポリシーを解析できませんでした"  

**質問**: MIP SDK をダウンロードし、ファイルのサンプルを使用してすべてのラベルを表示しようとした後に、次のエラーが表示されるのはなぜですか。

> 問題が発生しました: 取得したコンプライアンスポリシーを解析できませんでした。 で失敗しました: [クラス mip:: CompliancePolicyParserException] タグが見つかりません: ポリシー、NodeType:15、名前: 名前が見つかりません、値:、先祖: <SyncFile><Content>、correlationId: [34668a40-blll-4ef8-b2af-00005aa674z9]

これは、ラベルを Azure Information Protection から統合されたラベル付けエクスペリエンスに移行していないことを示しています。 「[Azure Information Protection ラベルを Office 365 セキュリティ/コンプライアンス センターに移行する方法](/azure/information-protection/configure-policy-migrate-labels)」に従ってラベルを移行した後、Office 365 セキュリティとコンプライアンス センターでラベル ポリシーを作成します。 

### <a name="error-systemcomponentmodelwin32exception-loadlibrary-failed"></a>エラー: "System.componentmodel. Win32Exception: LoadLibrary が失敗しました"

**質問**: MIP SDK .net ラッパーを使用すると、次のエラーが表示されるのはなぜですか。

> System.componentmodel: Win32Exception: MIP の呼び出し時に、: [sdk_wrapper_dotnet .dll] の LoadLibrary が失敗しました。Initialize ()。

アプリケーションに必要なランタイムがないか、またはリリースとしてビルドされていません。 詳細については、「[アプリに必要なランタイムがあることを確認](setup-configure-mip.md#ensure-your-app-has-the-required-runtime)する」を参照してください。 

### <a name="error-proxyautherror-exception"></a>エラー: "ProxyAuthError 例外"

**質問**: MIP SDK を使用すると、次のエラーが表示されるのはなぜですか。

> "Proxyauthentication Atonerror: プロキシ認証がサポートされていません"

MIP SDK は、認証されたプロキシの使用をサポートしていません。 このメッセージを修正するには、プロキシ管理者は、プロキシをバイパスするように Microsoft Information Protection サービスエンドポイントを設定する必要があります。 これらのエンドポイントの一覧については、「 [Office 365 の url と IP アドレス範囲](https://docs.microsoft.com/office365/enterprise/urls-and-ip-address-ranges)」ページを参照してください。 MIP SDK を使用するには、`*.protection.outlook.com` (行 9) と Azure Information Protection サービスエンドポイント (行 73) がプロキシ認証をバイパスする必要があります。
