---
title: 概念 - MIP SDK 内のポリシー ハンドラー。
description: この記事は、ポリシー API ハンドラーを作成し操作を呼び出すためにこれを使用する方法について理解するのに役立ちます。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: 583e59832e40f87665232ebf39e1dddb462ba212
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75556182"
---
# <a name="microsoft-information-protection-sdk---policy-handler-concepts"></a>Microsoft Information Protection SDK - ポリシー ハンドラーの概念

ポリシー API では、`mip::PolicyHandler` は、ポリシーアクションを計算し、監査イベントを送信するために使用される操作を公開します。

## <a name="policy-handler-functions"></a>ポリシー ハンドラー関数

`mip::PolicyHandler` では、ラベルと保護情報の両方を読み取り、書き込み、および削除するためのメソッドが示されます。 完全な一覧については、[API リファレンス](reference/class_mip_PolicyHandler.md)を参照してください。

この記事では、次のメソッドについて説明します。

- `ComputeActions`
- `NotifyCommittedActions`

## <a name="requirements"></a>［要件］

`PolicyHandler` を作成するには、以下が必要です。

- `mip::MipContext`
- `mip::PolicyProfile`
- `mip::PolicyProfile` に追加された `mip::PolicyEngine`
- を実装するクラス `mip::PolicyHandler::Observer`

## <a name="create-a-policy-handler"></a>ポリシー ハンドラーの作成

ポリシー アクションを取得する際に必要な最初の手順は、`PolicyHandler` オブジェクトを作成することです。 このクラスは、特定のラベルが受け取る必要のあるアクションの一覧を取得するために必要な機能を実装します。 また、監査イベントをトリガーする関数も実装します。

`PolicyHandler` の作成は、promise/future パターンを使用して `PolicyEngine` の `CreatePolicyHandlerAsync` 関数を呼び出すのと同じくらい簡単です。

`CreatePolicyHandlerAsync` で受け入れられるパラメーターは **isAuditDiscoveryEnabled** が 1 つです。 アプリケーションでハートビートイベントと検出イベントを監査ログに記録する必要がある場合は、この値を**true**に設定します。

> [!NOTE]
> `mip::PolicyHandler::Observer` クラスは派生クラスで実装する必要があります。これは、`CreatePolicyHandler` に `Observer` オブジェクトが必要であるためです。 

```cpp
auto createPolicyHandlerPromise = std::make_shared<std::promise<std::shared_ptr<mip::PolicyHandler>>>();
auto createPolicyHandlerFuture = createPolicyHandlerPromise->get_future();
PolicyEngine->CreatePolicyHandlerAsync(true);
auto handler = createPolicyHandlerFuture.get();
```

`PolicyHandler` オブジェクトが正常に作成されると、アクションを計算し、監査イベントを送信することができます。

## <a name="next-steps"></a>次のステップ

これで、ポリシーハンドラーの作成について学習できました。

- [実行状態クラスを作成](concept-handler-policy-executionstate-cpp.md)する方法について説明します。このクラスは、コンピューティングアクションを決定するために使用されます。
- [GitHub からポリシー Api サンプルをダウンロードし、ポリシー api を試す](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)
