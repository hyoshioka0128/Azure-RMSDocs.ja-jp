---
title: 概念 - Microsoft Information Protection SDK を使用した監査イベントの作成
description: この記事は、Microsoft Information Protection SDK を使用して計算する方法を理解するのに役立ちます。
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: 8ade287531ee9f1c18678d42ef5e51a4c70ee13f
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "69886195"
---
# <a name="compute-an-action"></a>アクションを計算する

前に詳述したように、ポリシー API の主な関数では次のことが行われます。

- 使用可能なラベルが一覧表示されます
- 現在の状態と目的の状態に基づいて実行する必要がある一連のアクションを返します。

このプロセスでの最後の手順は、ラベル識別子と既存のラベルに関するメタデータ (省略可能) を `ComputeActions()`関数に指定することです。

この記事のサンプル コードは、GitHub で確認できます。

- [mipsdk-policyapi-cpp-sample-basic](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic)

## <a name="compute-an-action-for-a-new-label"></a>新しいラベルに対するアクションを計算する

を新しいラベル`ExecutionStateImpl` に対して計算するには、[ExecutionState](concept-handler-policy-executionstate-cpp.md) に定義されているを使用します`mip::Actions` 。

```cpp
// Replace with valid label ID.
string newLabelId = "d7b93a40-4df3-47e4-b2fd-7862fc6b095c"; 
sample::policy::ExecutionStateOptions options;

// Resolve desired label id to mip::Label and set in ExecutionStateOptions.
options.newLabel = mEngine->GetLabelById(newLabelId);

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

ポリシー API を使用する場合は、コンテンツからメタデータを読み取るアプリケーションである必要があります。 このメタデータは `mip::ExecutionState` の一部として API に渡されます。 `ComputeActions()` を使用すると、ラベルの付いていないドキュメントに新しいラベルを適用する操作よりもっと複雑な操作を処理することができます。 次の例では、より機密性の高いラベルから、より重要度の低いラベルにラベルをダウングレードする方法を示します。 このプロセスをシミュレートするには、メタデータのコンマ区切りの文字列を読み取り、`mip::ExecutionState`を使用して API に渡します。

> [!NOTE]
> サンプルでは、`SplitString()` と呼ばれるユーティリティ関数が使用されています。 例については、[こちら](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic/blob/master/mipsdk-policyapi-cpp-sample-basic/utils.cpp)を参照してください。

```cpp
// Replace with valid label ID.
string newLabelId = "d7b93a40-4df3-47e4-b2fd-7862fc6b095c";

// Comma and Pipe Delimited Metadata.
string metadata = "MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Enabled|true,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SetDate|2018-10-23T21:53:31-0800,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Method|Standard,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_Name|Contoso FTEs (C),MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_SiteId|94f6984e-8d31-4794-bdeb-3ac89ad2b660,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ActionId|b56491d9-155f-40ff-866f-0000acd85c31,MSIP_Label_d7b93a40-4df3-47e4-b2fd-7862fc6b095c_ContentBits|7";

// Create ExecutionStateOptions and resolve newLabelId to mip::Label
sample::policy::ExecutionStateOptions options;
options.newLabel = mEngine->GetLabelById(newLabelId);

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

## <a name="next-steps"></a>次のステップ

- [監査イベントを Azure Information Protection Analytics に渡す](concept-handler-policy-auditing-cpp.md)方法について説明します
- [GitHub からポリシー Api サンプルをダウンロードし、ポリシー api を試す](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)
