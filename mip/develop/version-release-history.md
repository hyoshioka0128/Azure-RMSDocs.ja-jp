---
title: Microsoft Information Protection (MIP) SDK のバージョン リリース履歴とサポート ポリシー
description: Microsoft Information Protection (MIP) SDK クライアント アプリケーションの初期化ロジックを記述する方法を示すクイック スタートです。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 01/08/2019
ms.author: mbaldwin
manager: barbkess
ms.openlocfilehash: 9f02d682164dac8ee28ed023dd7b21b53937f4bb
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333638"
---
# <a name="microsoft-information-protection-mip-sdk-version-release-history-and-support-policy"></a>Microsoft Information Protection (MIP) SDK のバージョン リリース履歴とサポート ポリシー

## <a name="servicing"></a>サービス 

各一般 (公開 GA) バージョンは、次の GA バージョンがリリース後 6 か月間でサポートされています。 ドキュメントは、サポートされていないバージョンに関する情報を含まない場合があります。 修正プログラムおよび新しい機能は最新の GA バージョンにのみ適用されます。

プレビュー バージョンは、運用環境にデプロイしないでください。 代わりに、最新のプレビュー バージョンを使用して、新しい機能や、次の GA バージョンで予定されている修正プログラムをテストします。 最新のプレビュー バージョンのみがサポートされています。

## <a name="release-history"></a>リリース履歴

次の情報を使用すると、新機能やサポートされているリリースの変更を参照してください。 最新のリリースは一番上に表示されます。 

> [!NOTE]
> 細かい修正点は記載されていないので修正のかどうかを確認することをお勧め、SDK に問題が発生した場合、最新の GA リリースでします。 問題が解決されていない場合は、最新のプレビュー バージョンを確認します。
>  
> テクニカル サポートは、次を参照してください、 [Stack Overflow Microsoft Information Protection のフォーラム](https://stackoverflow.com/questions/tagged/microsoft-information-protection)します。 

## <a name="version-110"></a>バージョン 1.1.0

**リリース日**:未定

このバージョンには、次のプラットフォームのサポートが導入されています。

  - .NET
  - iOS SDK (API のポリシー)
  - Android SDK (API と API の保護のポリシー)

**新機能:**

- ADRMS サポート
- 保護 API 操作が (Win32)、真に非同期で同時に非ブロッキング暗号化/暗号解除の操作のことができます
  - アプリケーションのコールバック (authdelegate:、HTTPDelegate など) を呼び出すようになりましたが*任意*バック グラウンド スレッド
- Mip::Label::GetCustomSettings で、IT 管理者によって設定されるカスタム ラベルのプロパティを読み取るようになりましたことができます。
- シリアル化された発行ライセンスを mip::FileHandler::GetSerializedPublishingLicense 経由で任意の HTTP 操作なしのファイルから直接取得できるようになりました
- アプリケーションは、mip::FileEngine/mip::PolicyEngine mip::FileProfile::Observer::OnAddPolicyEngineStarting 経由での作成を完了する HTTP 操作が必要かどうかが通知/mip::PolicyProfile::Observer::OnAddEngineStarting
- 便利なメソッド mip::ProtectionDescriptor::DoesContentExpire で保護されたコンテンツが有効期限の日付にするかどうかどうかの検出が簡略化されました
- 分類:
  - 機密の種類 (正規表現の式の CC # の passport # など) SCC サービスから取得できます
    - Mip::FileEngine::Settings を設定して機能を有効にする::settings フラグ/
    - Mip::FileEngine::ListSensitivityTypes を使用して型を読み取る/mip::PolicyEngine::ListSensitivityTypes
  - ドキュメントの外部スキャナー ユーティリティから分類結果は、ドキュメントの内容を基に推奨される必要なラベルをドライブに MIP に取り込むことができます。
    - MIP に mip::FileExecutionState::GetClassificationResults を使用して結果を渡す/mip::ExecutionState::GetClassificationResults
    - 分類の結果に必要な推奨ラベルを示すポリシー ルールが一致する場合、mip::ApplyLabelAction と mip::RecommendLabelAction を mip::PolicyEngine::ComputeActions によって返されることができます。

- 新しい要件:
  - ID/名前/バージョン フィールド mip::ApplicationInfo mip::FileProfile、mip::PolicyProfile、および mip::ProtectionProfile を作成するときの強制の作成
  - Mip::FileHandlers を作成するときに、アプリケーションは新しい mip::FileExecutionState インターフェイスを実装する必要があります。
  
- 更新された例外処理:
  - アプリケーションの authdelegate: (キャンセル) により空のトークンを返す場合にスローされる mip::NoAuthTokenError
    - 作成に適用されます。
      - mip::FileEngine
      - mip::FileHandler
      - mip::PolicyEngine
      - mip::ProtectionHandler
  - mip::NoPolicyError ラベルのテナントが構成されていない場合にスローされます。
    - 作成に適用されます。
      - mip::FileEngine
      - mip::PolicyEngine
  - mip::ServiceDisabledError RMS サービスが特定のユーザー/デバイス/プラットフォーム/テナントで無効になっている場合にスローされます。
    - 作成に適用されます。
      - mip::FileHandler
      - mip::ProtectionHandler
  - ユーザーがドキュメントまたはコンテンツを復号化する権限を持っていない場合にスロー mip::NoPermissionsError の期限が切れています
    - 作成に適用されます。
      - mip::FileHandler
      - mip::ProtectionHandler

**修正内容**:

未定

## <a name="next-steps"></a>次の手順

- 参照してください[MIP SDK よく寄せられる質問と問題](faqs-known-issues.md)サポートされているプラットフォームと詳細について。
- 参照してください[MIP SDK のセットアップと構成](setup-configure-mip.md)MIP SDK を使用する方法について。
