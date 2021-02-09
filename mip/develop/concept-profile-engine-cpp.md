---
title: 概念 - MIP SDK の主要な概念 - プロファイルとエンジン
description: この記事は、アプリケーションの初期化中に作成される、プロファイルおよびエンジンという主要な SDK の概念を理解するのに役立ちます。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/29/2019
ms.author: mbaldwin
ms.openlocfilehash: 8c414b5b66525169b1c55ae83f60e91e69188b53
ms.sourcegitcommit: 4815ab96e4596303af297ae4c13fb6d7083b21e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "95570839"
---
# <a name="microsoft-information-protection-sdk---profile-and-engine-object-concepts"></a>Microsoft Information Protection SDK - プロファイル オブジェクトとエンジン オブジェクトの概念

## <a name="profiles"></a>Profiles

は、 `MipContext` SDK 固有の設定を格納するためのクラスです。このプロファイルは、MIP SDK のすべての mipmap ラベル付け操作と保護固有の操作のルートクラスです。 3つの API セットのいずれかを使用する前に、クライアントアプリケーションでプロファイルを作成する必要があります。 今後の操作は、プロファイルまたはプロファイルに *追加された* 他のオブジェクトによって実行されます。 プロセスごとに1つのプロファイルオブジェクトのみをお勧めします。 複数のを作成すると、予期しない動作が発生する可能性があります。 

MIP SDK には、次の 3 つの種類のプロファイルがあります。

- [`PolicyProfile`](reference/class_mip_policyprofile.md): MIP ポリシー API のプロファイルクラス。
- [`ProtectionProfile`](reference/class_mip_protectionprofile.md): MIP 保護 API のプロファイルクラス。
- [`FileProfile`](reference/class_mip_fileprofile.md): MIP ファイル API のプロファイルクラス。

使用するアプリケーションで使用する API によって、使用するプロファイルクラスが決まります。

プロファイル自体では次の機能が提供されます。

- 状態をメモリに読み込むかディスクに保存するかを定義し、ディスクに保存されている場合は暗号化する必要があるかどうかを定義します。
- `mip::ConsentDelegate`同意操作に使用するを定義します。
- `mip::FileProfile::Observer`プロファイル操作の非同期コールバックに使用されるの実装を定義します。

### <a name="profile-settings"></a>プロファイル設定

- `MipContext`: `MipContext` アプリケーション情報や状態パスなどを格納するために初期化されたオブジェクト。
- `CacheStorageType`: 状態をメモリ内、ディスク上、またはディスク上に格納し、暗号化する方法を定義します。
- `consentDelegate`: クラスの共有ポインター [`mip::ConsentDelegate`](reference/class_mip_consentdelegate.md) 。
- `observer`: プロファイルの実装への共有ポインター `Observer` ( [`PolicyProfile`](reference/class_mip_policyprofile_observer.md) 、、 [`ProtectionProfile`](reference/class_mip_protectionprofile_observer.md) および [`FileProfile`](reference/class_mip_fileprofile_observer.md) )。
- `applicationInfo`: [`mip::ApplicationInfo`](reference/mip-enums-and-structs.md#structures) オブジェクト。 SDK を使用しているアプリケーションに関する情報。 Azure Active Directory アプリケーションの登録 ID と名前に一致します。

## <a name="engines"></a>エンジン

ファイル、プロファイル、および保護 API エンジンは、特定の id によって実行される操作に対するインターフェイスを提供します。 アプリケーションにサインインするユーザーまたはサービスプリンシパルごとに、1つのエンジンがプロファイルオブジェクトに追加されます。 およびファイルまたは保護ハンドラーを介して、委任された操作を実行することができ `mip::ProtectionSettings` ます。 詳細については、「FileHandler の概念」の「 [保護設定」セクション](concept-handler-file-cpp.md) を参照してください。

SDK には 3 つのエンジン クラス (API ごとに 1 つずつ) があります。 エンジン クラスとそれぞれに関連付けられているいくつかの関数を以下の一覧に示します。

- [`mip::ProtectionEngine`](reference/class_mip_protectionengine.md)
- [`mip::PolicyEngine`](reference/class_mip_policyengine.md)
  - `ListSensitivityLabels()`: 読み込まれたエンジンに対するラベルの一覧が取得されます。
  - `GetSensitivityLabel()`: 既存のコンテンツからラベルを取得します。
  - `ComputeActions()`: ラベル ID と省略可能なメタデータと共に指定され、特定の項目に対して行う必要があるアクションの一覧を返します。
- [`mip::FileEngine`](reference/class_mip_fileengine.md)
  - `ListSensitivityLabels()`: 読み込まれたエンジンに対するラベルの一覧が取得されます。
  - `CreateFileHandler()`: 特定のファイルまたはストリームに対する `mip::FileHandler` が作成されます。

エンジンを作成するには、作成するエンジンの種類の設定を含む特定のエンジン設定オブジェクトを渡す必要があります。 設定オブジェクトを使用すると、開発者は、エンジン識別子、 `mip::AuthDelegate` 実装、ロケール、およびカスタム設定の詳細や、API 固有のその他の詳細を指定できます。

### <a name="engine-states"></a>エンジンの状態

エンジンは、次の 2 つの状態のいずれかになる場合があります。

- `CREATED`: 必要なバックエンド サービスを呼び出した後に、SDK に十分なローカル状態情報があることを示します。
- `LOADED`: SDK で、エンジンが動作できるようにするために必要なデータ構造が構築されています。

エンジンはすべての操作を行うために作成され、また、読み込まれる必要があります。 `Profile` クラスでは、`AddEngineAsync`、`DeleteEngineAsync`、および `UnloadEngineAsync` というエンジン管理メソッドがいくつか示されます。

次の表では、使用可能なエンジンの状態とその状態を変更できる方法について説明します。

| エンジンの状態 | NONE              | CREATED           | LOADED         |
|--------------|-------------------|-------------------|----------------|
| NONE         |                   |                   | AddEngineAsync |
| CREATED      | DeleteEngineAsync |                   | AddEngineAsync |
| LOADED       | DeleteEngineAsync | UnloadEngineAsync |                |

### <a name="engine-id"></a>エンジン ID

各エンジンには一意識別子である `id` があり、すべてのエンジン管理操作で使用されます。 アプリケーションによってが提供される `id` 場合、またはアプリケーションによって提供されない場合は、SDK によって生成されることがあります。 その他のすべてのエンジン プロパティ (ID 情報のメール アドレスなど) は、SDK のための非透過のペイロードです。 SDK では、他のプロパティを一意にしておくため、または他の制約を適用するためのロジックは実行されません。

> [!IMPORTANT]
> ベストプラクティスとして、ユーザーに固有のエンジン Id を使用し、ユーザーが SDK で操作を実行するたびにその Id を使用することをお勧めします。 既存のエンジン Id を指定しないと、ポリシーのフェッチに余分なサービスラウンドトリップが発生し、既存のエンジンに対して既にキャッシュされている可能性があるライセンスがフェッチされます。

### <a name="engine-management-methods"></a>エンジン管理メソッド

前述のように、SDK には、、、およびの3つのエンジン管理メソッドがあり `AddEngineAsync` `DeleteEngineAsync` `UnloadEngineAsync` ます。

#### <a name="addengineasync"></a>AddEngineAsync

このメソッドは、既存のエンジンを読み込むか、またはローカル状態にまだ存在しない場合は作成します。

アプリケーションで `id` が提供されない場合、`AddEngineAsync` で新しい `id` が生成されます。 その後、その `id` を持つエンジンがローカル状態で既に存在するかどうかが確認されます。 存在しない場合は、そのエンジンが読み込まれます。 エンジンがローカル状態で存在 *しない* 場合、必要な API とバックエンド サービスを呼び出すことで、新しいエンジンが作成されます。

いずれの場合も、メソッドが成功したときに、エンジンが読み込まれ、使用できるようになります。

#### <a name="deleteengineasync"></a>DeleteEngineAsync

指定された `id` を持つエンジンを削除します。 エンジンのすべてのトレースは、ローカル状態から削除されます。

#### <a name="unloadengineasync"></a>UnloadEngineAsync

指定された `id` を持つエンジンのメモリ内データ構造をアップロードします。 このエンジンのローカル状態はそのままであり、`AddEngineAsync` で再度読み込むことができます。

このメソッドを使用すると、間もなく使用されることが想定されていないエンジンをアンロードすることにより、メモリ使用量についてアプリケーションを慎重に実行できます。

## <a name="next-steps"></a>次の手順

- 次は、[認証の概念](concept-authentication-cpp.md)と[オブザーバー](concept-async-observers.md)について確認します。 MIP では拡張可能な認証モデルが提供されますが、オブザーバーは、非同期イベントのイベント通知を提供するために使用されます。 両方とも基本的なものであり、すべての MIP API セットに適用されます。
- 次に、ファイル、ポリシーおよび保護の各 API のプロファイルとエンジンの概念を確認します
  - [ファイル API プロファイルの概念](concept-profile-engine-file-profile-cpp.md)
  - [ファイル API エンジンの概念](concept-profile-engine-file-engine-cpp.md)
  - [ポリシー API プロファイルの概念](concept-profile-engine-file-profile-cpp.md)
  - [ポリシー API エンジンの概念](concept-profile-engine-file-engine-cpp.md)
  - [保護 API プロファイルの概念](concept-profile-engine-file-profile-cpp.md)
  - [保護 API エンジンの概念](concept-profile-engine-file-engine-cpp.md)  
