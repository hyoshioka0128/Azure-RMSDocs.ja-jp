---
title: 概念 - MIP SDK 内のポリシー ハンドラー。
description: この記事は、ポリシー API ハンドラーを作成し操作を呼び出すためにこれを使用する方法について理解するのに役立ちます。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/01/2018
ms.author: tommos
ms.openlocfilehash: c1e150de6096e070f46232e77a4749081fe0bb9f
ms.sourcegitcommit: 05fdaf43f74013eecb5886b95b09dd5e00670753
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2018
ms.locfileid: "51297851"
---
# <a name="microsoft-information-protection-sdk---policy-handler-concepts"></a>Microsoft Information Protection SDK - ポリシー ハンドラーの概念

ポリシー API では、ポリシー アクションの計算および監査イベントの送信を行うために使用できるさまざまな操作が `mip::PolicyHandler` によって公開されます。

## <a name="policy-handler-functions"></a>ポリシー ハンドラー関数

`mip::PolicyHandler` では、ラベルと保護情報の両方を読み取り、書き込み、および削除するためのメソッドが示されます。 完全な一覧については、[API リファレンス](reference/class_mip_PolicyHandler.md)を参照してください。

この記事では、次のメソッドについて説明します。

- `ComputeActions`
- `NotifyCommittedActions`

## <a name="requirements"></a>要件

`PolicyHandler` を作成するには、以下が必要です。

- `PolicyProfile`
- `PolicyProfile` に追加された `PolicyEngine`
- `mip::PolicyHandler::Observer` を継承するクラス

## <a name="create-a-policy-handler"></a>ポリシー ハンドラーの作成

ポリシー アクションを取得する際に必要な最初の手順は、`PolicyHandler` オブジェクトを作成することです。 このクラスでは、特定のラベルがとる必要があるアクションの一覧を取得するために必要な機能と、監査イベントをトリガーするための関数が実装されます。

`PolicyHandler` の作成は、promise/future パターンを使用して `PolicyEngine` の `CreatePolicyHandlerAsync` 関数を呼び出すのと同じくらい簡単です。

`CreatePolicyHandlerAsync` で受け入れられるパラメーターは **isAuditDiscoveryEnabled** が 1 つです。 監査ログにおいてアプリケーションでハートビート イベントを表示する必要がある場合は、この値を **true** に設定します。

> [!NOTE]
> `mip::PolicyHandler::Observer` クラスは派生クラスで実装する必要があります。これは、`CreatePolicyHandler` に `Observer` オブジェクトが必要であるためです。 

```cpp
auto createPolicyHandlerPromise = std::make_shared<std::promise<std::shared_ptr<mip::PolicyHandler>>>();
auto createPolicyHandlerFuture = createPolicyHandlerPromise->get_future();
PolicyEngine->CreatePolicyHandlerAsync(true);
auto handler = createPolicyHandlerFuture.get();
```

`PolicyHandler` オブジェクトが正常に作成されると、アクションを計算し、監査イベントを送信することができます。

# <a name="compute-an-action"></a>アクションを計算する

前に詳述したように、ポリシー API の主な関数では次のことが行われます。

- 使用できるラベルが一覧表示されます。
- 現在の目的とする状態に基づいて、実行すべき特定のアクション セットが返されます。 

このプロセスでの最後の手順は、ラベル識別子と既存のラベルに関するメタデータ (省略可能) を `ComputeActions()`関数に指定することです。

この記事のサンプル コードは、GitHub で確認できます。

* [mipsdk-policyapi-cpp-sample-basic](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic)

## <a name="compute-an-action-for-a-new-label"></a>新しいラベルに対するアクションを計算する

新しいラベルに対して `mip::Actions` を計算できるようにするには、[ExecutionState](concept-auditing-policy-executionstate-cpp.md) セクションに定義されている `ExecutionStateImpl` を使用します。

```cpp
// Replace with valid label ID.
string newLabelId = "d7b93a40-4df3-47e4-b2fd-7862fc6b095c"; 
sample::policy::ExecutionStateOptions options;

// Set desired newLabelId in ExecutionStateOptions.
options.newLabelId = newLabelId;

// Initialize ExecutionStateImpl with options, create handler, call ComputeActions.
std::unique_ptr<ExecutionStateImpl> state(new ExecutionStateImpl(options));
auto handler = mEngine->CreatePolicyHandler(false); // Don't generate audit event.
auto actions = handler->ComputeActions(*state);
```

`actions` の一部として返される `mip::MetadataActions` を記述するだけで、次の内容が表示されます。

```cpp
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Enabled : true
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SetDate : 2018-10-23T20:39:06-0800
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Method : Standard
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Name : Contoso FTEs (C)
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SiteId : 94f6984e-8d31-4794-bdeb-3ac89ad2b660
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ActionId : 2266fbe8-a0d9-44e8-bad8-00008f2a0915
Add: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ContentBits : 3
```

`PolicyHandler` ではアクションが計算され、`mip::Action` の `std::vector` が返されます。 このメタデータをファイルまたはデータに適用するのは、アプリケーション開発者の責任です。

> [!NOTE]
> 上記の例には、`mip::MetadataAction` の出力のみが表示されます。 追加のアクションの種類を表示する例については、[API ポリシーのダウンロード](https://aka.ms/mipsdkbins)に関するページにアクセスしてバンドルのサンプルを確認してください。

## <a name="compute-actions-with-an-existing-label"></a>既存のラベルに対してアクションを計算する

ポリシー API を使用する場合、コンテンツからメタデータを読み取るのはアプリケーションの役割です。 このメタデータは `mip::ExecutionState` の一部として API に渡されます。 `ComputeActions()` を使用すると、ラベルの付いていないドキュメントに新しいラベルを適用する操作よりもっと複雑な操作を処理することができます。 次の例では、ラベルを秘密度のより高いラベルから秘密度のより低いラベルにダウングレードする方法を示します。この場合、ラベルはすでに存在しています。 メタデータのコンマ区切り文字列を読み込み、それを `mip::ExecutionState` を介して API に渡すことで、このプロセスがシミュレートされます。

> [!NOTE]
> サンプルでは、`SplitString()` と呼ばれるユーティリティ関数が使用されています。 例については、[こちら](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-advanced/blob/master/mipsdk-policyapi-cpp-sample-advanced/utils.cpp)を参照してください。

```cpp
// Replace with valid label ID.
string newLabelId = "d7b93a40-4df3-47e4-b2fd-7862fc6b095c";

// Comma and Pipe Delimited Metadata.
string metadata = "MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Enabled|true,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SetDate|2018-10-23T21:53:31-0800,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Method|Standard,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Name|Contoso FTEs (C),MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SiteId|94f6984e-8d31-4794-bdeb-3ac89ad2b660,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ActionId|b56491d9-155f-40ff-866f-0000acd85c31,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ContentBits|7";

// Create ExecutionStateOptions and set newLabelId.
sample::policy::ExecutionStateOptions options;
options.newLabelId = newLabelId;

// Split metadata string by commas, store in vector.
vector<string> metadataPairs = sample::utils::SplitString(metadata, ','); 

// Iterate through each string, splitting by the pipe.
// Add each key/value pair to ExecutionStateOptions metadata.
for (const string& metadataPair : metadataPairs) {
    vector<string> keyValue = sample::utils::SplitString(metadataPair, '|');
    options.metadata[keyValue[0]] = keyValue[1];
}

// Initialize ExecutionStateImpl with options, create handler, call ComputeActions
std::unique_ptr<ExecutionStateImpl> state(new ExecutionStateImpl(options));
auto handler = mEngine->CreatePolicyHandler(false); // Don't generate audit event.
auto actions = handler->ComputeActions(*state);
```

上記の例では、結果としてアクションが複数になることがあります。 それらのアクションは、入力およびラベル構成として指定されたラベルによって異なります。 少なくとも、`GetMetadataToRemove()` を介して削除するデータおよび `GetMetadataToAdd()` を介して追加するデータを含む `mip::MetadataAction` が 1 つという結果になります。

```
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_Enabled : true
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_SetDate : 2018-10-23T23:59:41-0800
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_Method : Standard
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_Name : General
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_SiteId : 94f6984e-8d31-4794-bdeb-3ac89ad2b660
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_ActionId : 447a996b-28ea-482c-b0b5-000075bd4bb3
Add: MSIP_Label_d48d0e60-c766-40d6-96d3-53b2857fe775_ContentBits : 7
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Name
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Enabled
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SiteId
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SetDate
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Method
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ContentBits
Remove: MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ActionId
```

## <a name="next-steps"></a>次の手順

* 次に、[ポリシー API のサンプルを GitHub からダウンロードしてポリシー API を試みる](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)
* [Azure Information Protection Analytics に監査イベントを渡す](concept-auditing-policy-cpp.md)方法を参照する