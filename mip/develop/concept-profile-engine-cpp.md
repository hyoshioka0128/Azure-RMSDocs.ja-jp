---
title: 概念 - MIP SDK の主要な概念 - プロファイルとエンジン
description: この記事は、アプリケーションの初期化中に作成される、プロファイルおよびエンジンという主要な SDK の概念を理解するのに役立ちます。
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 6f11944e7cceed39423af2a8104ce044d1f6eec6
ms.sourcegitcommit: 823a14784f4b34288f221e3b3cb41bbd1d5ef3a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453420"
---
# <a name="microsoft-information-protection-sdk---profile-and-engine-object-concepts"></a>Microsoft Information Protection SDK - プロファイル オブジェクトとエンジン オブジェクトの概念

## <a name="profiles"></a>Profiles

プロファイルは、MIP SDK のすべての操作のルート クラスです。 3 つの API のいずれかを使用する前に、クライアント アプリケーションでプロファイルを作成する必要があります。 今後のすべての操作は、プロファイルに*追加された* 他のオブジェクト、またはプロファイルによって実行されます。

MIP SDK には、次の 3 つの種類のプロファイルがあります。

- [`PolicyProfile`](reference/class_mip_policyprofile.md): MIP ポリシー API のプロファイル クラス。
- [`ProtectionProfile`](reference/class_mip_protectionprofile.md): MIP 保護 API のプロファイル クラス。
- [`FileProfile`](reference/class_mip_fileprofile.md): MIP ファイル API のプロファイル クラス。

利用する側のアプリケーションで使用される API では、使用する必要があるプロファイル クラスが判別されます。

プロファイル自体では次の機能が提供されます。

- SDK 状態の保存場所を定義します。 状態データには、ユーザーの詳細、ダウンロードされたユーザー ポリシー、ログ、およびテレメトリ データが含まれています。
- 状態をメモリに読み込むか、ディスクに保持する必要があるかを定義します。
- `mip::AuthDelegate` を受け入れることで、認証を処理します。
- SDK を利用しているアプリのアプリケーション ID とフレンドリ名を設定します。

### <a name="profile-settings"></a>プロファイル設定

- `Path`: ログ、テレメトリ、その他の継続状態が格納されるファイル パス。
- `useInMemoryStorage`: 状態をメモリ内に格納するか、ディスク上に格納する必要があるかを定義するブール値。
- `authDelegate`: クラス `mip::AuthDelegate` の共有ポインター。 
- `consentDelegate`: クラス `mip::ConsentDelegate` の共有ポインター。 
- `observer`: プロファイル `Observer` の実装 (`PolicyProfile`、`ProtectionProfile`、および `EngineProfile` 内) への共有ポインター。
- `applicationInfo`: `mip::ApplicationInfo` オブジェクト。 SDK を利用しているアプリケーションに関する情報。

## <a name="engines"></a>エンジン

ファイル、プロファイル、および保護の各 API では、エンジンによって、特定の ID に代わって実行される操作へのインターフェイスが提供されます。 アプリケーションにサインインする各ユーザーのために、1 つのエンジンがプロファイル オブジェクトに追加されます。 エンジンによるすべての操作は、その ID のコンテキストで行われます。

SDK には 3 つのエンジン クラス (API ごとに 1 つずつ) があります。 エンジン クラスとそれぞれに関連付けられているいくつかの関数を以下の一覧に示します。

- [`mip::ProtectionEngine`]
- [`mip::PolicyEngine`](reference/class_mip_policyengine.md)
  - `ListSensitivityLabels()`: 読み込まれたエンジンに対するラベルの一覧が取得されます。
  - `GetSensitivityLabel()`: 既存のコンテンツからラベルを取得します。
  - `ComputeActions()`: ラベル ID と省略可能なメタデータと共に指定され、特定の項目に対して行う必要があるアクションの一覧を返します。
- [`mip::FileEngine`](reference/class_mip_fileengine.md)
  - `ListSensitivityLabels()`: 読み込まれたエンジンに対するラベルの一覧が取得されます。
  - `CreateFileHandler()`: 特定のファイルまたはストリームに対する `mip::FileHandler` が作成されます。

### <a name="engine-states"></a>エンジンの状態

エンジンは、次の 2 つの状態のいずれかになる場合があります。

- `CREATED`: 必要なバックエンド サービスを呼び出した後に、SDK に十分なローカル状態情報があることを示します。
- `LOADED`: SDK で、エンジンが動作できるようにするために必要なデータ構造が構築されています。

エンジンはすべての操作を行うために作成され、また、読み込まれる必要があります。 `Profile` クラスでは、`AddEngineAsync`、`RemoveEngineAsync`、および `UnloadEngineAsync` というエンジン管理メソッドがいくつか示されます。

次の表で、考えられるエンジンの状態とその状態を変更できるメソッドについて説明します。

|         | なし              | CREATED           | LOADED         |
|---------|-------------------|-------------------|----------------|
| なし    |                   |                   | AddEngineAsync |
| CREATED | DeleteEngineAsync |                   | AddEngineAsync |
| LOADED  | DeleteEngineAsync | UnloadEngineAsync |                |

### <a name="engine-id"></a>エンジン ID

各エンジンには一意識別子である `id` があり、すべてのエンジン管理操作で使用されます。 アプリケーションで `id` を提供できます。あるいは、アプリケーションによって提供されない場合は、SDK によって新しい一意識別子が生成されます。 その他のすべてのエンジン プロパティ (ID 情報のメール アドレスなど) は、SDK のための非透過のペイロードです。 SDK では、他のプロパティを一意にしておくため、または他の制約を適用するためのロジックは実行されません。

### <a name="engine-management-methods"></a>エンジン管理メソッド

前述のとおり、SDK には、`AddEngineAsync`、`DeleteEngineAsync`、`UnloadEngineAsync` という 3 つのエンジン管理メソッドがあります。

#### <a name="addengineasync"></a>AddEngineAsync

このメソッドでは既存のエンジンを読み込みます。あるいは、ローカル状態でまだ存在しない場合は、新しいエンジンを作成します。

アプリケーションで `id` が提供されない場合、`AddEngineAsync` で新しい `id` が生成されます。 その後、その `id` を持つエンジンがローカル状態で既に存在するかどうかが確認されます。 存在しない場合は、そのエンジンが読み込まれます。 エンジンがローカル状態で存在*しない* 場合、必要な API とバックエンド サービスを呼び出すことで、新しいエンジンが作成されます。

いずれの場合も、メソッドが成功したときに、エンジンが読み込まれ、使用できるようになります。

#### <a name="deleteengineasync"></a>DeleteEngineAsync

指定された `id` を持つエンジンを削除します。 エンジンのすべてのトレースは、ローカル状態から削除されます。

#### <a name="unloadengineasync"></a>UnloadEngineAsync

指定された `id` を持つエンジンのメモリ内データ構造をアップロードします。 このエンジンのローカル状態はそのままであり、`AddEngineAsync` で再度読み込むことができます。

このメソッドでは、すぐに使用する見込みのないエンジンをアンロードすることで、アプリケーションでメモリ使用率について適切に判断できます。

## <a name="next-steps"></a>次の手順

- 次は、[認証の概念](concept-authentication-cpp.md)と[オブザーバー](concept-async-observers.md)について確認します。 MIP では拡張可能な認証モデルが提供されますが、オブザーバーは、非同期イベントのイベント通知を提供するために使用されます。 両方とも基本的なものであり、すべての MIP API セットに適用されます。
- 次に、ファイル、ポリシーおよび保護の各 API のプロファイルとエンジンの概念を確認します
  - [ファイル API プロファイルの概念](concept-profile-engine-file-profile-cpp.md)
  - [ファイル API エンジンの概念](concept-profile-engine-file-engine-cpp.md)
  - [ポリシー API プロファイルの概念](concept-profile-engine-file-profile-cpp.md)
  - [ポリシー API エンジンの概念](concept-profile-engine-file-engine-cpp.md)
  - [保護 API プロファイルの概念](concept-profile-engine-file-profile-cpp.md)
  - [保護 API エンジンの概念](concept-profile-engine-file-engine-cpp.md)  
