---
title: 概念 - Microsoft Information Protection SDK ファイル API での監査
description: この記事は、Microsoft Information Protection SDK を使用してファイル API 監査イベントを Azure Information Protection Analytics に送信する方法を理解するのに役立ちます。
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: df67886f53d697e47f6e812cdcbbac394acaa98d
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "69884744"
---
# <a name="auditing-in-the-mip-sdk-file-api"></a>MIP SDK ファイル API での監査

Azure Information Protection の管理ポータルでは、管理者レポートにアクセスできます。 これらのレポートでは、MIP SDK を統合しているアプリケーションまたはサービス全体で、ユーザーがどのラベルを手動または自動で適用しているかが表示されます。 SDK を使用する開発パートナーは、この機能を有効にすることで、アプリケーションからの情報を顧客レポートに表示できます。

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
fileEngine->CreateFileHandlerAsync(inputFilePath, actualFilePath, true /*AuditDiscoveryEnabled*/, make_shared<FileHandlerObserver>(), createFileHandlerPromise);
auto handler = handlerFuture.get();

// Read label. This generates the discovery audit.
auto label = handler->GetLabel();
```

### <a name="change-events"></a>変更イベント

変更イベントでは、ファイル、適用または変更されたラベル、およびユーザーが示した理由について情報が提供されます。 変更がファイルに正常にコミットされた後、`mip::FileHandler` 上で `NotifyCommitSuccessful()` を呼び出すことで、変更イベントが作成されます。

```cpp
// Create labeling options, set label
string contentId = "C:\users\myuser\Documents\MyPlan.docx";
mip::LabelingOptions labelingOptions(mip::AssignmentMethod::PRIVILEGED);
handler->SetLabel(labelId, labelingOptions, mip::ProtectionSettings());
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

Azure Information Protection 監査パイプラインに送信されたイベントは、 https://portal.azure.com にあるレポートに表示されます。 

## <a name="next-steps"></a>次のステップ

Azure Information Protection の監査エクスペリエンスの詳細については、 [Tech Community のプレビュー発表のブログ](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854)を参照してください。
