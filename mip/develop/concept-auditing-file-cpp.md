---
title: 概念 - Microsoft Information Protection SDK ファイル API での監査
description: この記事は、Microsoft Information Protection SDK を使用してファイル API 監査イベントを Azure Information Protection Analytics に送信する方法を理解するのに役立ちます。
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/01/2018
ms.author: tommos
ms.openlocfilehash: bd04d9aa2edd6be01ae9e912d7ddbf936d6dd4df
ms.sourcegitcommit: 05fdaf43f74013eecb5886b95b09dd5e00670753
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2018
ms.locfileid: "51297807"
---
# <a name="auditing-in-the-mip-sdk-file-api"></a>MIP SDK ファイル API での監査

Azure Information Protection の管理ポータルでは、管理者レポートにアクセスできます。 これらのレポートにより、MIP SDK が統合された任意のアプリケーションとサービスの間にユーザーが手動または自動で適用したラベルの可視性が提供されます。 SDK を使用している開発パートナーは、自分のアプリケーションからの情報が顧客レポートに表示されるように、この機能を簡単に有効にすることができます。

## <a name="event-types"></a>イベントの種類

SDK を介して Azure Information Protection Analytics に送信できるイベントには 3 つの種類があります。 **ハートビート イベント**、**検出イベント**、および**変更イベント**です

### <a name="heartbeat-events"></a>ハートビート イベント

ハートビート イベントは、ファイル API が統合された任意のアプリケーションに対して自動的に作成されます。 ハートビート イベントには、次のものが含まれます。

* TenantId
* 作成された時刻
* ユーザー プリンシパル名
* 監査が作成されたマシンの名前
* プロセス名
* プラットフォーム
* アプリケーション ID - Azure AD のアプリケーション ID に対応します。

これらのイベントは、Microsoft Information Protection SDK を使用しているアプリケーションを、会社全体にわたって検出する際に便利です。

### <a name="discovery-events"></a>検出イベント

検出イベントでは、ファイル API によって読み取られるまたは使用されるラベル付き情報に関する情報が提供されます。 これらのイベントは、情報にアクセスしているデバイス、場所、およびユーザーを組織全体にわたって確認できるので便利です。

これらのイベントを Azure Information Protection Analytics に送信するには、新しい `mip::FileHandler` を作成するときに `AuditDiscoveryEnabled` パラメーターを true に設定します。 さらに、人間が判読できるいずれかの形式のファイルを識別するコンテンツ識別子が提供されます。 この識別子にはファイル パスを使用することをお勧めします。

次の例では、監査検出を有効にして新しい `mip::FileHandler` が作成されます。 `mip::FileEngine` と true に設定された `AuditDiscoveryEnabled` に対して `CreateFileHandler()` メソッドが呼び出されます。 `FileHanlder` によってラベルが読み取られると、検出監査が作成されます。

```cpp
// Create FileHandler with discovery enabled
auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
auto handlerFuture = handlerPromise->get_future();
fileEngine->CreateFileHandlerAsync(filePath, contentId, mip::ContentState::REST, true /*AuditDiscoveryEnabled*/, make_shared<FileHandlerObserver>(), createFileHandlerPromise);
auto handler = handlerFuture.get();

// Read label. This generates the discovery audit.
auto label = handler->GetLabel();
```

### <a name="change-events"></a>変更イベント

変更イベントでは、ファイル、適用または変更されたラベル、およびユーザーが示した理由について情報が提供されます。 変更がファイルに正常にコミットされた後、`mip::FileHandler` 上で `NotifyCommitSuccessful()` を呼び出すことで、変更イベントが作成されます。

```cpp
// Create labeling options, set label
string contentId = "C:\users\myuser\Documents\MyPlan.docx";
mip::LabelingOptions labelingOptions(mip::AssignmentMethod::PRIVILEGED, mip::ActionSource::MANUAL);
handler->SetLabel(labelId, labelingOptions);
auto commitPromise = std::make_shared<std::promise<bool>>();
auto commitFuture = commitPromise->get_future();

// CommitAsync() returns a bool. If the change was successful, call NotifyCommitSuccessful().
fileHandler->CommitAsync(outputFile, commitPromise);
if(commitFuture.get()) {

    // Submit audit event.
    handler->NotifyCommitSuccessful(contentId);
}
```

## <a name="audit-dashboard"></a>監査ダッシュボード

Azure Information Protection 監査パイプラインに送信されたイベントは、 https://portal.azure.com にあるレポートに表示されます。 Azure Information Protection Analytics はパブリック プレビュー段階にあり、機能は変更される可能性があります。

## <a name="next-steps"></a>次の手順

Azure Information Protection の監査エクスペリエンスの詳細については、[Tech Community でのプレビューのお知らせ](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854)に関するブログ記事を参照してください。
