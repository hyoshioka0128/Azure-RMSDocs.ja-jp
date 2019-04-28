---
title: 概念 - MIP SDK 内のポリシー ハンドラー。
description: この記事は、ポリシー API ハンドラーを作成し操作を呼び出すためにこれを使用する方法について理解するのに役立ちます。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 11/16/2018
ms.author: tommos
ms.openlocfilehash: cc35475086de76b869428c62cfc35e73fc3060db
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60184928"
---
# <a name="microsoft-information-protection-sdk---policy-handler-concepts"></a>Microsoft Information Protection SDK - ポリシー ハンドラーの概念

API では、ポリシー、`mip::PolicyHandler`ポリシーのアクションを計算し、監査イベントを送信するために使用する操作を公開します。

## <a name="policy-handler-functions"></a>ポリシー ハンドラー関数

`mip::PolicyHandler` では、ラベルと保護情報の両方を読み取り、書き込み、および削除するためのメソッドが示されます。 完全な一覧については、[API リファレンス](reference/class_mip_PolicyHandler.md)を参照してください。

この記事では、次のメソッドについて説明します。

- `ComputeActions`
- `NotifyCommittedActions`

## <a name="requirements"></a>必要条件

`PolicyHandler` を作成するには、以下が必要です。

- `PolicyProfile`
- `PolicyProfile` に追加された `PolicyEngine`
- `mip::PolicyHandler::Observer` を継承するクラス

## <a name="create-a-policy-handler"></a>ポリシー ハンドラーの作成

ポリシー アクションを取得する際に必要な最初の手順は、`PolicyHandler` オブジェクトを作成することです。 このクラスは、特定のラベルを実行する必要がありますアクションの一覧を取得するために必要な機能を実装します。 監査イベントをトリガーする関数も実装します。

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

## <a name="next-steps"></a>次の手順

これで、ポリシーのハンドラーの作成について説明しました。

- について説明する方法[実行状態クラスを作成する](concept-handler-policy-executionstate-cpp.md)コンピューティングのアクションの決定に使用されます。
- ダウンロード、[ポリシー API のサンプルを GitHub ポリシー API を試すから](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)
