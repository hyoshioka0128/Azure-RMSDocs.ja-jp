---
title: 概念 - Microsoft Information Protection SDK ポリシー API
description: この記事は、Microsoft Information Protection SDK を使用してポリシー API 監査イベントを Azure Information Protection Analytics に送信する方法を理解するのに役立ちます。
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 11/07/2018
ms.author: tommos
ms.openlocfilehash: 729570c902ad3175b65ddd8167005c0cb4e4078c
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60175226"
---
# <a name="auditing-in-the-mip-sdk"></a>MIP SDK での監査

Azure Information Protection の管理ポータルでは、管理者レポートにアクセスできます。 これらのレポートにより、MIP SDK が統合された任意のアプリケーションの間にユーザーが手動または自動で適用したラベルの可視性が提供されます。 SDK を利用している開発パートナーは、この機能を簡単に有効にして自分のアプリケーションからの情報が顧客レポートに表示されるようにすることができます。

## <a name="event-types"></a>イベントの種類

SDK を介して Azure Information Protection Analytics に送信できるイベントには 3 つの種類があります。 **ハートビート イベント**、**検出イベント**、および**変更イベント**です

### <a name="heartbeat-events"></a>ハートビート イベント

ハートビート イベントは、ポリシー API が統合された任意のアプリケーションに対して自動的に作成されます。 ハートビート イベントには、次のものが含まれます。

* TenantId
* 作成された時刻
* ユーザー プリンシパル名
* 監査が作成されたマシンの名前
* プロセス名
* プラットフォーム
* アプリケーション ID - Azure AD のアプリケーション ID に対応します。

これらのイベントは、Microsoft Information Protection SDK を使用しているアプリケーションを、会社全体にわたって検出する際に便利です。

### <a name="discovery-events"></a>検出イベント

検出イベントでは、ポリシー API によって読み取られたり使用されたりするラベル付き情報に関する情報が提供されます。 これらのイベントは、情報にアクセスしているデバイス、場所、およびユーザーを組織全体にわたって確認できるので便利です。

作成するときに、フラグを設定して、ポリシー API で検出イベントが生成されます、`mip::PolicyHandler`オブジェクト。 値は、次の例で**isAuditDiscoveryEnabled**に設定されている`true`します。 ときに`mip::ExecutionState`に渡される`ComputeActions()`または`GetSensitivityLabel()`(識別子を持つ既存のメタデータ情報およびコンテンツ)、探索情報を Azure 情報保護 Analytics に送信されます。

アプリケーションによって `ComputeActions()` または `GetSensitivityLabel()` が呼び出され、`mip::ExecutionState` が指定されると、検出監査が作成されます。 このイベントは、ハンドラーごとに 1 回だけ作成されます。

実行状態の詳細については、`mip::ExecutionState` の概念に関するドキュメントを参照してください。

```cpp
// Create PolicyHandler, passing in true for isAuditDiscoveryEnabled
auto handler = mEngine->CreatePolicyHandler(true);

// Returns vector of mip::Action and generates discovery event.
auto actions = handler->ComputeActions(*state);

//Or, get the label for a given state
auto label = handler->GetSensitivityLabel(*state);
```

実際には、`mip::PolicyHandler` の構築中に **isAuditDiscoveryEnabled** を `true` に設定して、ファイル アクセス情報が Azure Information Protection Analytics に送信されるようにしておく必要があります。

## <a name="change-event"></a>変更イベント

変更イベントでは、ファイル、適用または変更されたラベル、およびユーザーが示した理由について情報が提供されます。 変更イベントを生成するには、`mip::PolicyHandler` 上で `NotifyCommittedActions()` を呼び出します。 変更がファイルに正常にコミットされると呼び出しが行われ、アクションの計算に使用された `mip::ExecutionState` が渡されます。

> アプリケーションによるこの関数の呼び出しが失敗した場合、Azure Information Protection Analytics にイベントは届きません。

```cpp
handler->NotifyCommittedActions(*state);
```

## <a name="audit-dashboard"></a>監査ダッシュボード

Azure Information Protection 監査パイプラインに送信されたイベントは、 https://portal.azure.com にあるレポートに表示されます。 Azure 情報保護の Analytics はパブリック プレビューであり、機能/機能を変更することがあります。

## <a name="next-steps"></a>次の手順

- 詳細については、Azure Information Protection での監査操作は、次を参照してください。、[技術コミュニティでの発表に関するブログをプレビュー](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854)します。
- ダウンロード、[ポリシー API のサンプルを GitHub ポリシー API を試すから](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)

