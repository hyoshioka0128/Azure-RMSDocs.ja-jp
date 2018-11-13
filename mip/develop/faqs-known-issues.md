---
title: よくあるご質問と既知の問題 - Microsoft Information Protection SDK。
description: Microsoft Information Protection (MIP) SDK のよく寄せられる質問と、問題とエラーに関するトラブルシューティングのガイダンスです。
author: BryanLa
ms.service: information-protection
ms.topic: troubleshooting
ms.date: 10/19/2018
ms.author: bryanla
ms.openlocfilehash: f213b31d9b0e41ea9c1e076055a90e9f62b31b3a
ms.sourcegitcommit: fa0be701b85b1fba5e75428714bb4525dd739a93
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2018
ms.locfileid: "51223927"
---
# <a name="microsoft-information-protection-mip-sdk-faqs-and-issues"></a>Microsoft Information Protection (MIP) SDK のよく寄せられる質問と問題

この記事では、よく寄せられる質問 (FAQ) に対する回答と、既知の問題と一般的なエラーに関するトラブルシューティングのガイダンスを示します。

## <a name="frequently-asked-questions"></a>よく寄せられる質問 

### <a name="question-which-platforms-are-supported-by-the-mip-sdk"></a>質問: MIP SDK ではどのプラットフォームがサポートされますか?

MIP SDK は、次のプラットフォームで使用できます。

[!INCLUDE [MIP SDK platform support](../include/mip-sdk-platform-support.md)]

### <a name="question-how-does-the-sdk-handle-strings-and-what-string-type-should-i-be-using-in-my-code"></a>質問: SDK ではどのように文字列が処理されますか? また、コードではどの文字列型を使用すればよいですか?

SDK はクロスプラットフォームでの使用を想定しています。文字列の処理には [UTF-8 (Unicode Transformation Format - 8 ビット)](https://wikipedia.org/wiki/UTF-8) が使用されます。 具体的なガイダンスは、使用するプラットフォームによって異なります。

| プラットフォーム | ガイダンス |
|-|-|
| Windows ネイティブ | C++ の SDK クライアントでは、API 関数との文字列のやり取りには C++ 標準ライブラリの型 [`std::string`](https://wikipedia.org/wiki/C%2B%2B_string_handling) が使用されます。 UTF-8 との間での変換は、MIP SDK によって内部的に管理されます。 API から `std::string` が返されるときは、UTF-8 エンコードを想定し、文字列を変換する場合はそれに応じて管理する必要があります。 場合によっては、文字列が `uint8_t` ベクター (発行ライセンス (PL) など) の一部として返されることがありますが、これは不透明な BLOB として扱う必要があります。<br><br>詳細および例については、次をご覧ください。<ul><li>ワイド文字の文字列を UTF-8 などの複数バイトに変換するのをサポートする [WideCharToMultiByte 関数](/windows/desktop/api/stringapiset/nf-stringapiset-widechartomultibyte)。<li>[SDK ダウンロード](setup-configure-mip.md#configure-your-client-workstation)に含まれる次のサンプル ファイル:<ul><li>ワイド UTF-8 文字列との間で変換するための、`file\samples\common\string_utils.cpp` の文字列ユーティリティ関数のサンプル。<li>前の文字列変換関数を使用する、`file\samples\file\main.cpp` の `wmain(int argc, wchar_t *argv[])` の実装。</li></ul></ul>|
| .NET | .NET SDK クライアントでは、すべての文字列で既定の UTF-16 エンコードが使用され、特別な変換は必要ありません。 UTF-16 との間での変換は、MIP SDK によって内部的に管理されます。 |
| その他のプラットフォーム | MIP SDK でサポートされているその他のすべてのプラットフォームでは、UTF-8 がネイティブでサポートされています。 |

## <a name="issues-and-errors-reference"></a>問題とエラーのリファレンス

### <a name="error-file-format-not-supported"></a>エラー: "ファイル形式がサポートされていません"  

| エラー | 解決方法 |
|-|-|
|*ファイル形式がサポートされていません*| この例外は、デジタル署名されているかパスワードで保護されている PDF ファイルを保護またはラベル付けしようとすると発生します。 PDF ファイルの保護とラベル付けについて詳しくは、「[New support for PDF encryption with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/New-support-for-PDF-encryption-with-Microsoft-Information/ba-p/262757)」(Microsoft Information Protection での PDF の新しい暗号化のサポート) をご覧ください。|

### <a name="error-failed-to-parse-the-acquired-compliance-policy"></a>エラー: "取得したコンプライアンス ポリシーを解析できませんでした"  

MIP SDK をダウンロードして、サンプル アプリケーションを実行したとします。 ファイルのサンプルを使用してすべてのラベルを一覧表示しようとすると、次のエラーが発生します。

| エラー | 解決方法 |
|-|-|
|*エラーが発生しました: 取得したコンプライアンス ポリシーを解析できませんでした。Failed with: [class mip::CompliancePolicyParserException] Tag not found: policy, NodeType: 15, Name: No Name Found, Value: , Ancestors: <SyncFile><Content>, correlationId:[34668a40-blll-4ef8-b2af-00005aa674z9]*| これは、ラベルを Azure Information Protection から統合ラベル付けエクスペリエンスに移行していないことを示しています。 「[Azure Information Protection ラベルを Office 365 セキュリティ/コンプライアンス センターに移行する方法](/azure/information-protection/configure-policy-migrate-labels)」に従ってラベルを移行した後、Office 365 セキュリティとコンプライアンス センターでラベル ポリシーを作成します。 完了すると、サンプルが正常に実行されます。|
