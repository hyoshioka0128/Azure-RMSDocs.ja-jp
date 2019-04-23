---
title: 概念 - MIP SDK の主要な概念 - プロファイルとエンジン
description: この記事は、アプリケーションの初期化中に作成される、プロファイルおよびエンジンという主要な SDK の概念を理解するのに役立ちます。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: e815820fa9f3a6de95d5e37e350ed18df8513b21
ms.sourcegitcommit: 682dc48cbbcbee93b26ab3872231b3fa54d3f6eb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "60175107"
---
# <a name="microsoft-information-protection-sdk---profile-and-engine-object-concepts"></a>Microsoft Information Protection SDK - プロファイル オブジェクトとエンジン オブジェクトの概念

## <a name="profiles"></a>Profiles

プロファイルは、MIP SDK のすべての操作のルート クラスです。 3 つの Api を使用するのには、クライアント アプリケーションがプロファイルを作成する必要があります。 プロファイル、または他のオブジェクトでは、今後の操作は実行されます*追加*をプロファイルします。

MIP SDK には、次の 3 つの種類のプロファイルがあります。

- [`PolicyProfile`](reference/class_mip_policyprofile.md):MIP ポリシー API の profile クラス。
- [`ProtectionProfile`](reference/class_mip_protectionprofile.md):MIP 保護 API の profile クラス。
- [`FileProfile`](reference/class_mip_fileprofile.md):MIP ファイル API の profile クラス。

コンシューマー側アプリケーションで使用される API は、どのプロファイル クラスを使用する必要がありますを決定します。

プロファイル自体では次の機能が提供されます。

- SDK 状態の保存場所を定義します。 状態データには、ユーザーの詳細、ダウンロードされたユーザー ポリシー、ログ、およびテレメトリ データが含まれています。
- 状態をメモリに読み込むか、ディスクに保持する必要があるかを定義します。
- `mip::AuthDelegate` を受け入れることで、認証を処理します。
- SDK を利用しているアプリのアプリケーション ID とフレンドリ名を設定します。

### <a name="profile-settings"></a>プロファイル設定

- `Path`:ファイルのパスをログ、テレメトリ、およびその他の永続的な状態が格納されます。
- `useInMemoryStorage`:状態をメモリに格納する必要があるかどうかを定義するブール値またはディスクにします。
- `authDelegate`:クラスの共有ポインター`mip::AuthDelegate`します。 
- `consentDelegate`:クラスの共有ポインター [ `mip::ConsentDelegate`](reference/class_mip_consentdelegate.md)します。 
- `observer`:プロファイルへの共有ポインター`Observer`実装 (で[ `PolicyProfile` ](reference/class_mip_policyprofile_observer.md)、 [ `ProtectionProfile` ](reference/class_mip_protectionprofile_observer.md)、および[ `FileProfile` ](reference/class_mip_fileprofile_observer.md))。
- `applicationInfo`:A [ `mip::ApplicationInfo` ](reference/mip-enums-and-structs.md#structures)オブジェクト。 Azure Active Directory アプリケーションの登録 ID、名前に一致すると、SDK を利用するアプリケーションについて説明します。

## <a name="engines"></a>エンジン

ファイル、プロファイル、および保護 API のエンジンは、特定のユーザーに代わって実行される操作へのインターフェイスを提供します。 1 つのエンジンは、アプリケーションにサインインするユーザーごと、プロファイル オブジェクトに追加されます。 エンジンによって実行されるすべての操作では、その id のコンテキストでします。

SDK には 3 つのエンジン クラス (API ごとに 1 つずつ) があります。 エンジン クラスとそれぞれに関連付けられているいくつかの関数を以下の一覧に示します。

- [`mip::ProtectionEngine`](reference/class_mip_protectionengine.md)
- [`mip::PolicyEngine`](reference/class_mip_policyengine.md)
  - `ListSensitivityLabels()`:読み込まれたエンジンのラベルの一覧を取得します。
  - `GetSensitivityLabel()`:既存のコンテンツからラベルを取得します。
  - `ComputeActions()`:ラベル ID を持つと省略可能なメタデータが特定の項目を実行するアクションの一覧を返します。
- [`mip::FileEngine`](reference/class_mip_fileengine.md)
  - `ListSensitivityLabels()`:読み込まれたエンジンのラベルの一覧を取得します。
  - `CreateFileHandler()`:作成、`mip::FileHandler`特定のファイルまたはストリームにします。

### <a name="engine-states"></a>エンジンの状態

エンジンは、次の 2 つの状態のいずれかになる場合があります。

- `CREATED`:作成された SDK が必要なバックエンド サービスを呼び出した後に、十分なローカルの状態情報を持っていることを示します。
- `LOADED`:SDK が機能する、エンジンの必要なデータ構造を作成しました。

エンジンはすべての操作を行うために作成され、また、読み込まれる必要があります。 `Profile` クラスでは、`AddEngineAsync`、`RemoveEngineAsync`、および `UnloadEngineAsync` というエンジン管理メソッドがいくつか示されます。

次の表に、可能なエンジンの状態と、メソッドがその状態を変更できます。

|         | なし              | CREATED           | LOADED         |
|---------|-------------------|-------------------|----------------|
| なし    |                   |                   | AddEngineAsync |
| CREATED | DeleteEngineAsync |                   | AddEngineAsync |
| LOADED  | DeleteEngineAsync | UnloadEngineAsync |                |

### <a name="engine-id"></a>エンジン ID

各エンジンには一意識別子である `id` があり、すべてのエンジン管理操作で使用されます。 アプリケーションを提供できる、 `id`SDK で生成、1 つが、アプリケーションで指定されていない場合またはします。 その他のすべてのエンジン プロパティ (ID 情報のメール アドレスなど) は、SDK のための非透過のペイロードです。 SDK では、他のプロパティを一意にしておくため、または他の制約を適用するためのロジックは実行されません。

### <a name="engine-management-methods"></a>エンジン管理メソッド

SDK の 3 つのエンジン管理メソッドがある前述のように、: `AddEngineAsync`、 `DeleteEngineAsync`、および`UnloadEngineAsync`します。

#### <a name="addengineasync"></a>AddEngineAsync

このメソッドは、既存のエンジンの読み込みまたはローカル状態に既に存在していない場合は、1 つ作成します。

アプリケーションで `id` が提供されない場合、`AddEngineAsync` で新しい `id` が生成されます。 その後、その `id` を持つエンジンがローカル状態で既に存在するかどうかが確認されます。 存在しない場合は、そのエンジンが読み込まれます。 エンジンがローカル状態で存在*しない* 場合、必要な API とバックエンド サービスを呼び出すことで、新しいエンジンが作成されます。

いずれの場合も、メソッドが成功したときに、エンジンが読み込まれ、使用できるようになります。

#### <a name="deleteengineasync"></a>DeleteEngineAsync

指定された `id` を持つエンジンを削除します。 エンジンのすべてのトレースは、ローカル状態から削除されます。

#### <a name="unloadengineasync"></a>UnloadEngineAsync

指定された `id` を持つエンジンのメモリ内データ構造をアップロードします。 このエンジンのローカル状態はそのままであり、`AddEngineAsync` で再度読み込むことができます。

このメソッドは、すぐに使用することを期待されませんアンロードのエンジンによって、メモリ使用量について注意するアプリケーションを使用します。

## <a name="next-steps"></a>次の手順

- 次は、[認証の概念](concept-authentication-cpp.md)と[オブザーバー](concept-async-observers.md)について確認します。 MIP では拡張可能な認証モデルが提供されますが、オブザーバーは、非同期イベントのイベント通知を提供するために使用されます。 両方とも基本的なものであり、すべての MIP API セットに適用されます。
- 次に、ファイル、ポリシーおよび保護の各 API のプロファイルとエンジンの概念を確認します
  - [ファイル API プロファイルの概念](concept-profile-engine-file-profile-cpp.md)
  - [ファイル API エンジンの概念](concept-profile-engine-file-engine-cpp.md)
  - [ポリシー API プロファイルの概念](concept-profile-engine-file-profile-cpp.md)
  - [ポリシー API エンジンの概念](concept-profile-engine-file-engine-cpp.md)
  - [保護 API プロファイルの概念](concept-profile-engine-file-profile-cpp.md)
  - [保護 API エンジンの概念](concept-profile-engine-file-engine-cpp.md)  
