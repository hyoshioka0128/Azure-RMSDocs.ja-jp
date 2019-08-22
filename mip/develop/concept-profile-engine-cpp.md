---
title: 概念 - MIP SDK の主要な概念 - プロファイルとエンジン
description: この記事は、アプリケーションの初期化中に作成される、プロファイルおよびエンジンという主要な SDK の概念を理解するのに役立ちます。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/29/2019
ms.author: mbaldwin
ms.openlocfilehash: a1112b3c35539654ac71b6c8c686f93e676ac5f3
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69886117"
---
# <a name="microsoft-information-protection-sdk---profile-and-engine-object-concepts"></a>Microsoft Information Protection SDK - プロファイル オブジェクトとエンジン オブジェクトの概念

## <a name="profiles"></a>プロファイル

は、 `MipContext` SDK 固有の設定を格納するためのクラスです。このプロファイルは、mip SDK のすべての mipmap ラベル付け操作と保護固有の操作のルートクラスです。 3つの API セットのいずれかを使用する前に、クライアントアプリケーションでプロファイルを作成する必要があります。 今後の操作は、プロファイルまたはプロファイルに*追加された*他のオブジェクトによって実行されます。

MIP SDK には、次の 3 つの種類のプロファイルがあります。

- [`PolicyProfile`](reference/class_mip_policyprofile.md):MIP ポリシー API のプロファイルクラス。
- [`ProtectionProfile`](reference/class_mip_protectionprofile.md):MIP 保護 API のプロファイルクラス。
- [`FileProfile`](reference/class_mip_fileprofile.md):MIP ファイル API のプロファイルクラス。

使用するアプリケーションで使用する API によって、使用するプロファイルクラスが決まります。

プロファイル自体では次の機能が提供されます。

- 状態をメモリに読み込むかディスクに保存するかを定義し、ディスクに保存されている場合は暗号化する必要があるかどうかを定義します。
- `mip::AuthDelegate` を受け入れることで、認証を処理します。
- 同意操作`mip::ConsentDelegate`に使用するを定義します。
- プロファイル操作`mip::FileProfile::Observer`の非同期コールバックに使用されるの実装を定義します。

### <a name="profile-settings"></a>プロファイル設定

- `MipContext` :アプリケーション情報や状態パスなどを格納するために初期化されたオブジェクト。`MipContext`
- `CacheStorageType`:状態を格納する方法を定義します。メモリ内、ディスク上、またはディスク上で暗号化されます。
- `authDelegate`:クラス`mip::AuthDelegate`の共有ポインター。
- `consentDelegate` :クラス[`mip::ConsentDelegate`](reference/class_mip_consentdelegate.md)の共有ポインター。
- `observer`:プロファイル`Observer`の実装[`PolicyProfile`](reference/class_mip_policyprofile_observer.md)(、 [`ProtectionProfile`](reference/class_mip_protectionprofile_observer.md)、および[`FileProfile`](reference/class_mip_fileprofile_observer.md)) への共有ポインター。
- `applicationInfo`:[`mip::ApplicationInfo`](reference/mip-enums-and-structs.md#structures)オブジェクト。 SDK を使用しているアプリケーションに関する情報。 Azure Active Directory アプリケーションの登録 ID と名前に一致します。

## <a name="engines"></a>エンジン

ファイル、プロファイル、および保護 API エンジンは、特定の id によって実行される操作に対するインターフェイスを提供します。 アプリケーションにサインインするユーザーまたはサービスプリンシパルごとに、1つのエンジンがプロファイルオブジェクトに追加されます。 およびファイルまたは保護ハンドラーを介し`mip::ProtectionSettings`て、委任された操作を実行することができます。 詳細については、「FileHandler の概念」の「[保護設定」セクション](concept-handler-file-cpp.md)を参照してください。

SDK には 3 つのエンジン クラス (API ごとに 1 つずつ) があります。 エンジン クラスとそれぞれに関連付けられているいくつかの関数を以下の一覧に示します。

- [`mip::ProtectionEngine`](reference/class_mip_protectionengine.md)
- [`mip::PolicyEngine`](reference/class_mip_policyengine.md)
  - `ListSensitivityLabels()`:読み込まれたエンジンのラベルの一覧を取得します。
  - `GetSensitivityLabel()`:既存のコンテンツからラベルを取得します。
  - `ComputeActions()`:ラベル ID とオプションのメタデータを使用して、特定の項目に対して実行するアクションの一覧を返します。
- [`mip::FileEngine`](reference/class_mip_fileengine.md)
  - `ListSensitivityLabels()` :読み込まれたエンジンのラベルの一覧を取得します。
  - `CreateFileHandler()`:特定の`mip::FileHandler`ファイルまたはストリームのを作成します。

### <a name="engine-states"></a>エンジンの状態

エンジンは、次の 2 つの状態のいずれかになる場合があります。

- `CREATED`:Created は、必要なバックエンドサービスを呼び出した後、SDK に十分なローカル状態情報があることを示します。
- `LOADED`:SDK は、エンジンが動作するために必要なデータ構造を構築しました。

エンジンはすべての操作を行うために作成され、また、読み込まれる必要があります。 `Profile` クラスでは、`AddEngineAsync`、`RemoveEngineAsync`、および `UnloadEngineAsync` というエンジン管理メソッドがいくつか示されます。

次の表では、使用可能なエンジンの状態とその状態を変更できる方法について説明します。

|         | なし              | CREATED           | LOADED         |
|---------|-------------------|-------------------|----------------|
| なし    |                   |                   | AddEngineAsync |
| CREATED | DeleteEngineAsync |                   | AddEngineAsync |
| LOADED  | DeleteEngineAsync | UnloadEngineAsync |                |

### <a name="engine-id"></a>エンジン ID

各エンジンには一意識別子である `id` があり、すべてのエンジン管理操作で使用されます。 アプリケーションによってが`id`提供される場合、またはアプリケーションによって提供されない場合は、SDK によって生成されることがあります。 その他のすべてのエンジン プロパティ (ID 情報のメール アドレスなど) は、SDK のための非透過のペイロードです。 SDK では、他のプロパティを一意にしておくため、または他の制約を適用するためのロジックは実行されません。

> [!IMPORTANT]
> ベストプラクティスとして、ユーザーに固有のエンジン Id を使用し、ユーザーが SDK で操作を実行するたびにその Id を使用することをお勧めします。 既存のエンジン Id を指定しないと、ポリシーのフェッチに余分なサービスラウンドトリップが発生し、既存のエンジンに対して既にキャッシュされている可能性があるライセンスがフェッチされます。

### <a name="engine-management-methods"></a>エンジン管理メソッド

前述のように、SDK `AddEngineAsync`には、 `DeleteEngineAsync`、、および`UnloadEngineAsync`の3つのエンジン管理メソッドがあります。

#### <a name="addengineasync"></a>AddEngineAsync

このメソッドは、既存のエンジンを読み込むか、またはローカル状態にまだ存在しない場合は作成します。

アプリケーションで `id` が提供されない場合、`AddEngineAsync` で新しい `id` が生成されます。 その後、その `id` を持つエンジンがローカル状態で既に存在するかどうかが確認されます。 存在しない場合は、そのエンジンが読み込まれます。 エンジンがローカル状態で存在*しない* 場合、必要な API とバックエンド サービスを呼び出すことで、新しいエンジンが作成されます。

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
