---
title: 概念 - Microsoft Information Protection SDK への ExecutionState の実装
description: この記事は、Microsoft Information Protection SDK 内で ExecutionState を使用してアクションの計算を行い監査ログの詳細を提供する方法を理解するのに役立ちます。
services: information-protection
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 11/01/2018
ms.author: tommos
ms.openlocfilehash: dbe6db5fe54f9d26d072d3f6fcad1f2595d61040
ms.sourcegitcommit: ea76aade54134afaf5023145fcb755e40c7b84b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2019
ms.locfileid: "59574153"
---
# <a name="implement-executionstate"></a>ExecutionState を実装する

実行する必要があるアクションを現在の状態と目的とする状態に基づいて計算できるように MIP SDK に情報を渡す処理は、`mip::ExecutionState` クラスを介して実装されます。 SDK 内の他のクラスと同様に、`ExecutionState` は抽象クラスであり、開発者によって実装される必要があります。

> `ExecutionState` 実装の完全な例については、次のソース サンプルを参照してください。
>
> * [execution_state_impl.h](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic/blob/master/mipsdk-policyapi-cpp-sample-basic/execution_state_impl.h)
> * [execution_state_impl.cpp](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic/blob/master/mipsdk-policyapi-cpp-sample-basic/execution_state_impl.cpp)

## <a name="mipexecutionstate-members"></a>mip::ExecutionState のメンバー

`ExecutionState` では、次の仮想メンバーが公開されます。 各メンバーからポリシー エンジンに何らかのコンテキストが渡されると、アプリケーションによって実行される必要があるアクションに関する情報が返されます。 さらに、この情報は、Azure Information Protection レポート機能に監査情報を提供するために、使用される場合もあります。


| Member                                                                           | 戻り値                                                                                                              |
|----------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| `std::string GetNewLabelId()`                                                      | オブジェクトに適用するラベル ID が返されます。                                                                    |
| `mip::DataState GetDataState()`                                              | オブジェクトの mip::DataState を返します。                                                                         |
| `std::pair<bool, std::string> IsDowngradeJustified()`                              | ダウングレードの正当性と理由を表す std::pair が返されます。                                 |
| `std::string GetContentIdentifier()`                                               | コンテンツの識別子が返されます。 オブジェクトの位置を示していて人間が判読できる識別子である必要があります。   |
| `mip::ActionSource GetNewLabelActionSource()`                                      | ラベルの mip::ActionSource が返されます。                                                                          |
| `mip::AssignmentMethod GetNewLabelAssignmentMethod()`                              | ラベルの mip::AssignmentMethod が返されます。                                                                        |
| `std::vector<std::pair<std::string, std::string>> GetNewLabelExtendedProperties()` | ドキュメントに適用されるカスタム メタデータを含む文字列の std::pairs の std::vector が返されます。 |
| `std::vector<std::pair<std::string, std::string>> GetContentMetadata()`            | 現在のコンテンツのメタデータを含む文字列の std::pairs の std::vector が返されます。                               |
| `std::shared_ptr<mip::ProtectionDescriptor> GetProtectionDescriptor()`           | mip::ProtectionDescriptor にポインターが返されます。                                                                     |
| `mip::ContentFormat GetContentFormat()`                                            | mip::ContentFormat が返されます。                                                                                           |
| `mip::ActionType GetSupportedActions()`                                           | ラベルの mip::ActionTypes が返されます。                                                                              |

`mip::ExecutionState` から派生したクラスの実装内で、それぞれをオーバーライドする必要があります。 上記のリンクされたサンプル アプリケーションにおいて、このプロセスは `ExecutionStateOptions` と呼ばれる構造体を実装しそれを派生クラスのコンストラクターに渡すことにより達成されます。

[例](https://github.com/Azure-Samples/mipsdk-policyapi-cpp-sample-basic/blob/master/mipsdk-policyapi-cpp-sample-basic/execution_state_impl.h)で、`ExecutionStateOptions` と呼ばれる構造体は次のように定義されています。

```cpp
struct ExecutionStateOptions {
    std::unordered_map<std::string, std::string> metadata;
    std::string newLabelId;
    std::string contentIdentifier;
    mip::ActionSource actionSource = mip::ActionSource::MANUAL;
    mip::DataState dataState = mip::DataState::USE;
    mip::AssignmentMethod assignmentMethod = mip::AssignmentMethod::STANDARD;
    bool isDowngradeJustified = false;
    std::string downgradeJustification;
    std::string templateId;
    mip::ContentFormat contentFormat = mip::ContentFormat::DEFAULT;
};
```

アプリケーションによって各プロパティが設定され、次に、`mip::ExecutionState` から派生したクラスのコンストラクターに `ExecutionStateOptions` が渡されます。 この情報は、実行するアクションを決定するために使用されます。 `mip::ExecutionState` 内に指定されたデータは、Azure Information Protection Analytics にも表示されます。

### <a name="next-steps"></a>次の手順

- 確認する方法について[新規または既存のラベルの操作をコンピューティング](concept-handler-policy-computeactions-cpp.md)現在と目的の状態に基づいて、します。
- ダウンロード、[ポリシー API のサンプルを GitHub ポリシー API を試すから](https://azure.microsoft.com/resources/samples/?sort=0&term=mipsdk+policyapi)
