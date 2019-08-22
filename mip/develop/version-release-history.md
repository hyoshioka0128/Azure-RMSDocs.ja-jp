---
title: Microsoft Information Protection (MIP) SDK バージョンリリース履歴とサポートポリシー
description: Microsoft Information Protection (MIP) SDK クライアント アプリケーションの初期化ロジックを記述する方法を示すクイック スタートです。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 01/08/2019
ms.author: mbaldwin
manager: barbkess
ms.openlocfilehash: c2a5d89bf318d9e685d00033ba3ad53915659cdb
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69882666"
---
# <a name="microsoft-information-protection-mip-sdk-version-release-history-and-support-policy"></a>Microsoft Information Protection (MIP) SDK バージョンリリース履歴とサポートポリシー

## <a name="servicing"></a>サービス 

各一般公開 (GA) バージョンは、次の GA バージョンがリリースされると6か月間サポートされます。 ドキュメントには、サポートされていないバージョンに関する情報が含まれない場合があります。 修正プログラムと新機能は、最新の GA バージョンにのみ適用されます。

プレビューバージョンを運用環境にデプロイすることはできません。 代わりに、最新のプレビューバージョンを使用して、次の GA バージョンに含まれる新しい機能や修正をテストします。 最新のプレビューバージョンのみがサポートされています。

## <a name="release-history"></a>リリース履歴

サポートされているリリースの新機能と変更点については、次の情報を参照してください。 最新のリリースは一番上に表示されます。 

> [!NOTE]
> マイナー修正は記載されていないので、SDK に問題が発生した場合は、最新の GA リリースで修正されているかどうかを確認することをお勧めします。 問題が解決されていない場合は、最新のプレビュー バージョンを確認します。
>  
> テクニカルサポートについては、 [Stack Overflow Microsoft Information Protection フォーラム](https://stackoverflow.com/questions/tagged/microsoft-information-protection)を参照してください。 


## <a name="version-130"></a>バージョン1.3.0

**リリース日**:TBD

## <a name="version-120"></a>バージョン1.2.0

**リリース日**:2019年4月15日

## <a name="version-110"></a>バージョン1.1.0

**リリース日**:2019年1月15日

このバージョンでは、次のプラットフォームのサポートが導入されています。

  - .NET
  - iOS SDK (ポリシー API)
  - Android SDK (ポリシー API と保護 API)

**新機能:**

- ADRMS のサポート
- 保護 API の操作は (Win32 上で) 真の非同期であり、非ブロッキングの暗号化/復号化操作を同時に行うことができます。
  - バックグラウンドスレッドでアプリケーションコールバック (AuthDelegate、HTTPDelegate など) を呼び出すことができるようになりました
- IT 管理者によって設定されたカスタムラベルのプロパティを mip:: Label:: GetCustomSettings を使用して読み取ることができるようになりました。
- シリアル化された発行ライセンスをファイルから直接取得できるようになりました。 mip:: FileHandler:: GetSerializedPublishingLicense を使用して HTTP 操作を行う必要はありません。
- Mip:: Fileengine:: Observer:: OnAddPolicyEngineStarting/mip::P Olicyengine:: Observer:: OnAddEngineStarting を使用して mip:: FileEngine/mip::P olicyEngine の作成を完了するために HTTP 操作が必要かどうかがアプリケーションに通知されます。
- 保護されたコンテンツの有効期限が切れているかどうかを検出します。また、便宜的な方法 mip::P rotectionDescriptor::D oesContentExpire 切れ
- 分類
  - 秘密度の種類 (CC # の、passport # などの正規表現式) は、SCC サービスから取得できます。
    - Mip:: FileEngine:: Settings/mip::P olicyEngine:: Settings フラグを設定して機能を有効にします
    - Mip:: FileEngine:: ListSensitivityTypes/mip::P olicyEngine:: ListSensitivityTypes を使用した型の読み取り
  - 外部ドキュメントスキャナーユーティリティからの分類の結果を MIP に渡すことで、ドキュメントの内容に基づいて推奨されるラベルや必要なラベルを作成できます。
    - Mip:: FileExecutionState:: GetClassificationResults/mip:: ExecutionState:: GetClassificationResults を使用して結果を MIP に渡します
    - mip:: ApplyLabelAction および mip:: RecommendLabelAction は mip::P olicyEngine:: ComputeActions によって返されます。分類の結果が、必須ラベルまたは推奨ラベルを示すポリシールールと一致する場合に使用します。

- 新しい要件:
  - Mip:: FileProfile、mip::P olicyProfile、mip::P rotectionProfile を作成するときに、ID/名前/バージョンフィールド mip:: ApplicationInfo を強制的に作成します
  - Mip:: Fileハンドラを作成するときは、アプリケーションで新しい mip:: FileExecutionState インターフェイスを実装する必要があります
  
- 更新された例外:
  - mip:: NoAuthTokenError がスローされました (キャンセルにより、アプリケーションの AuthDelegate から空のトークンが返された場合)
    - 次の作成に適用されます:
      - mip:: FileEngine
      - mip:: FileHandler
      - mip::P olicyEngine
      - mip::P rotectionHandler
  - mip:: NoPolicyError が、テナントがラベルに対して構成されていない場合にスローされる
    - 次の作成に適用されます:
      - mip:: FileEngine
      - mip::P olicyEngine
  - 特定のユーザー/デバイス/プラットフォーム/テナントに対して RMS サービスが無効になっている場合、mip:: ServiceDisabledError がスローされる
    - 次の作成に適用されます:
      - mip:: FileHandler
      - mip::P rotectionHandler
  - mip:: NoPermissionsError は、ユーザーがドキュメントの暗号化を解除する権限を持っていないか、コンテンツの有効期限が切れている場合にスローされます。
    - 次の作成に適用されます:
      - mip:: FileHandler
      - mip::P rotectionHandler

**修正内容**:

TBD

## <a name="next-steps"></a>次の手順

- サポートされているプラットフォームなどの詳細については[、MIP SDK に関する faq と問題](faqs-known-issues.md)を参照してください。
- MIP SDK の使用を開始する方法については、「 [MIP sdk のセットアップと構成](setup-configure-mip.md)」を参照してください。
