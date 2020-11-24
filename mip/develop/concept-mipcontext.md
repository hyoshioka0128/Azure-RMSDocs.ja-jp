---
title: 概念-MIP SDK の主要な概念-MipContext
description: この記事では、アプリケーションの初期化を行う MipContext と呼ばれる主要な SDK の概念を理解するのに役立ちます。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: mbaldwin
ms.openlocfilehash: ed5c960215c67d424a31f7293a94b42629251eb4
ms.sourcegitcommit: 4815ab96e4596303af297ae4c13fb6d7083b21e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "95570831"
---
# <a name="microsoft-information-protection-sdk---mipcontext-object-concepts"></a>Microsoft Information Protection SDK-MipContext オブジェクトの概念

## <a name="mipcontext"></a>MipContext

`MipContext` は、SDK の最上位レベルのオブジェクトです。 アプリケーションまたはサービスの一部として作成できるすべてのプロファイルの状態を管理する責任があります。 さらに、MipContext オブジェクトが破棄されると、MIP SDK リソースの解放を処理します。 1つのプロセスにつき1つの `MipContext` プロセスのみが許可されます。 複数のを作成すると、予期しない動作が発生する可能性があります。

具体的には、は `MipContext` 次のオプションの設定を提供します。

- `mip::ApplicationInfo` SDK では、アプリケーション ID、バージョン、アプリケーション名に使用されます。
- MIP 状態情報を格納するパス (有効な場合)。
- ログ記録レベル。
- 必要に応じてカスタムロガーデリゲート。
- テレメトリ構成のオーバーライド。
- 機能フラグの背後にある SDK のプレビュー機能を有効にします。

のオブジェクト `mip::MipContext` が作成されたら、オブジェクトを使用して `MipContext` `mip::FileProfile` オブジェクト (または) を作成でき `PolicyProfile` / `ProtectionProfile` ます。

### <a name="mipcontext-functions"></a>MipContext 関数

`mip::MipContext` オブジェクトの作成と破棄に使用される3つの重要な静的関数を公開し `MipContext` ます。

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

すべての MIP リソースを解放します。 アプリをシャットダウンする前に、を呼び出す必要があります。 デストラクターは、 `MipContext` オブジェクトが破棄されたときにもこの関数を呼び出し `MipContext` ます。

## <a name="next-steps"></a>次の手順

- 次は、[認証の概念](concept-authentication-cpp.md)と[オブザーバー](concept-async-observers.md)について確認します。 MIP では拡張可能な認証モデルが提供されますが、オブザーバーは、非同期イベントのイベント通知を提供するために使用されます。 両方とも基本的なものであり、すべての MIP API セットに適用されます。
- 次に、ファイル、ポリシーおよび保護の各 API のプロファイルとエンジンの概念を確認します
  - [ファイル API プロファイルの概念](concept-profile-engine-file-profile-cpp.md)
  - [ファイル API エンジンの概念](concept-profile-engine-file-engine-cpp.md)
  - [ポリシー API プロファイルの概念](concept-profile-engine-file-profile-cpp.md)
  - [ポリシー API エンジンの概念](concept-profile-engine-file-engine-cpp.md)
  - [保護 API プロファイルの概念](concept-profile-engine-file-profile-cpp.md)
  - [保護 API エンジンの概念](concept-profile-engine-file-engine-cpp.md)
