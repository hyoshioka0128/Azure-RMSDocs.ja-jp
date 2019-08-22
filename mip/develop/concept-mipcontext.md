---
title: 概念-MIP SDK の主要な概念-MipContext
description: この記事では、アプリケーションの初期化を行う MipContext と呼ばれる主要な SDK の概念を理解するのに役立ちます。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: aac40c5ba5f06e705aaf5c6d42c6963d851d2764
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69893737"
---
# <a name="microsoft-information-protection-sdk---mipcontext-object-concepts"></a>Microsoft Information Protection SDK-MipContext オブジェクトの概念

## <a name="mipcontext"></a>MipContext

`MipContext`は、SDK の最上位レベルのオブジェクトです。 アプリケーションまたはサービスの一部として作成できるすべてのプロファイルの状態を管理する責任があります。 さらに、MipContext オブジェクトが破棄されると、MIP SDK リソースの解放を処理します。

具体的に`MipContext`は、は次のように設定します。

- `mip::ApplicationInfo`SDK では、アプリケーション ID、バージョン、アプリケーション名に使用されます。
- MIP 状態情報を格納するパス (有効な場合)。
- ログ記録レベル。
- 必要に応じてカスタムロガーデリゲート。
- テレメトリ構成のオーバーライド。
- 機能フラグの背後にある SDK のプレビュー機能を有効にします。

`mip::MipContext`のオブジェクトが作成されたら`PolicyProfile` `MipContext` 、オブジェクトを使用してオブジェクト ( `mip::FileProfile`または/ `ProtectionProfile`) を作成できます。

### <a name="mipcontext-functions"></a>MipContext 関数

`mip::MipContext`オブジェクトの作成と破棄`MipContext`に使用される3つの重要な静的関数を公開します。

#### `mip::MipContext::Create()`

プロファイルを初期化するときに使用する新しい MipContext インスタンスを作成します。 この関数は、次のものを受け入れます。

- `mip::ApplicationInfo`
- MIP ストレージキャッシュのパス。
- `mip::LogLevel`
- (省略可能) `mip::LoggerDelegate`
- (省略可能) `mip::TelemetryConfiguration`

#### `mip::MipContext::CreateWithCustomFeatureSettings()`

カスタム機能設定が有効になっているプロファイルを初期化するときに使用する新しい MipContext インスタンスを作成します。

- `mip::ApplicationInfo`
- MIP ストレージキャッシュのパス。
- `mip::LogLevel`
- (省略可能) `mip::LoggerDelegate`
- (省略可能) `mip::TelemetryConfiguration`
- `mip::FlightingFeature`

#### `mip::mipContext::Shutdown()`

すべての MIP リソースを解放します。 アプリをシャットダウンする前に、を呼び出す必要があります。 `MipContext`また、 `MipContext`デストラクターは、オブジェクトが破棄されるときにこれを呼び出します。

## <a name="next-steps"></a>次の手順

- 次は、[認証の概念](concept-authentication-cpp.md)と[オブザーバー](concept-async-observers.md)について確認します。 MIP では拡張可能な認証モデルが提供されますが、オブザーバーは、非同期イベントのイベント通知を提供するために使用されます。 両方とも基本的なものであり、すべての MIP API セットに適用されます。
- 次に、ファイル、ポリシーおよび保護の各 API のプロファイルとエンジンの概念を確認します
  - [ファイル API プロファイルの概念](concept-profile-engine-file-profile-cpp.md)
  - [ファイル API エンジンの概念](concept-profile-engine-file-engine-cpp.md)
  - [ポリシー API プロファイルの概念](concept-profile-engine-file-profile-cpp.md)
  - [ポリシー API エンジンの概念](concept-profile-engine-file-engine-cpp.md)
  - [保護 API プロファイルの概念](concept-profile-engine-file-profile-cpp.md)
  - [保護 API エンジンの概念](concept-profile-engine-file-engine-cpp.md)
