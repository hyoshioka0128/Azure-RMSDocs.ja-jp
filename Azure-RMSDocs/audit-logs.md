---
title: Azure Information Protection によって生成される監査ログ-AIP
description: AIP Azure Information Protection によって生成される監査ログについて説明します。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 11/09/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: e48c3a32527ea214d952725a4935c566a60d208f
ms.sourcegitcommit: 8a141858e494dd1d3e48831e6cd5a5be48ac00d2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2020
ms.locfileid: "97383943"
---
# <a name="azure-information-protection-audit-log-reference-public-preview"></a>Azure Information Protection 監査ログの参照 (パブリックプレビュー)

>***適用対象**: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*
>
>***関連**: [AIP のラベル付けクライアントと従来のクライアント](faqs.md#whats-the-difference-between-the-azure-information-protection-classic-and-unified-labeling-clients)*

>[!NOTE] 
> 統一された効率的なカスタマーエクスペリエンスを提供するために、 **Azure Information Protection クラシッククライアント** および Azure Portal での **ラベル管理** は **、2021年3月31日** に **非推奨** となっています。 このタイムフレームにより、現在のすべての Azure Information Protection のお客様は、Microsoft Information Protection 統合ラベル付けプラットフォームを使用する統一されたラベル付けソリューションに移行できます。 詳細については、公式な[非推奨の通知](https://aka.ms/aipclassicsunset)をご覧ください。

監査ログの Azure Information Protection 機能は、現在プレビューの段階です。 [Azure プレビューの追加使用条件](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)には、ベータ版、プレビュー版、またはまだ一般提供されていない Azure 機能に適用される追加の法律条項が含まれています。 

Microsoft Azure Information Protection は、次のアクティビティイベントで監査ログを生成します。

* [Access (アクセス)](#access-audit-logs)
* [アクセスが拒否されました](#access-denied-audit-logs)
* [保護の変更](#change-protection-audit-logs)
* [発見](#discover-audit-logs)
* [ダウングレードラベル](#downgrade-label-audit-logs)
* [削除されたファイル](#file-removed-audit-logs)
* [新しいラベル](#new-label-audit-logs)
* [新しい保護](#new-protection-audit-logs)
* [ラベルの削除](#remove-label-audit-logs)
* [保護の削除](#remove-protection-audit-logs)
* [アップグレードラベル](#upgrade-label-audit-logs)

> [!NOTE]
> [AIP ビューアー](rms-client/clientv2-view-use-files.md)は、監査ログを送信しません。 
>
## <a name="access-audit-logs"></a>監査ログにアクセスする

**アクセス** 監査ログは、次のアクティビティに対して生成されます。

|報告者  |プラットフォーム  |Application  |アクション/説明  |
|---------|---------|---------|---------|
|Azure Information Protection: クラシッククライアントのみ | Windows        | Office        |ラベル付けまたは保護されたファイルが保存される各セッションで、最初に生成されます。<br>ログには、すべての情報の種類の一致が含まれます。      |
|Azure Information Protection: クラシッククライアントのみ     |Windows         |Office         |ラベル付きまたは保護されたファイルが作成されるたびに生成されます。       |
|Azure Information Protection:<br />-クラシッククライアント<br />-統一されたラベル付けクライアント     | Windows、SharePoint、OneDrive        | Office        | ラベル付きまたは保護されたファイルが開かれるたびに生成されます。 <br /><br />**注**: 保護されたファイルの場合、アクセス監査ログが生成されるのは、ファイルが開かれており、コンテンツが正常に復号化され、ユーザーに公開された場合のみです。 <br />Outlook の保護された電子メールについては、アクセス許可がないことが原因で暗号化解除がブロックされた場合でも、ユーザーが暗号化された電子メールを開こうとするたびに、アクセス監査ログが生成されます。         |
|Microsoft Information Protection (MIP) SDK     | 任意        | サードパーティ アプリケーション        | ラベル付きまたは保護されたファイルが、それをサポートするサードパーティ製アプリケーションによってアクセスされるたびに生成されます。       |
|RMS サービス     | Windows        | Office         |ラベル付きまたは保護されたドキュメントがアクセスされるたびに生成されます。       |
| | | | |


## <a name="access-denied-audit-logs"></a>アクセス拒否監査ログ

**アクセス拒否** 監査ログは、次のアクティビティに対して生成されます。

|報告者  |プラットフォーム  |Application  |アクション/説明   |
|---------|---------|---------|---------|
|RMS サービス     | Windows        | Office         |アクセス許可のない保護されたドキュメントにユーザーがアクセスを試みるたびに生成されます。
| | | | |

## <a name="change-protection-audit-logs"></a>保護監査ログの変更

**変更防止** の監査ログは、次のアクティビティに対して生成されます。

|報告者  |プラットフォーム  |Application  |アクション/説明   |
|---------|---------|---------|---------|
|Azure Information Protection:<br />-クラシッククライアント<br />-統一されたラベル付けクライアント     | Windows、SharePoint、OneDrive        | Office        | ラベルのないドキュメントの保護が手動で変更されるたびに生成されます。         |
|Microsoft Information Protection (MIP) SDK     | 任意        | サードパーティ アプリケーション        | ラベルのないドキュメントの保護が手動で変更されるたびに生成されます。<br>サードパーティのアプリケーションでサポートされている場合にのみ生成されます。       |
| | | | |

## <a name="discover-audit-logs"></a>監査ログの検出

次のアクティビティについて、**検出** 監査ログが生成されます。

|報告者  |プラットフォーム  |Application  |アクション/説明   |
|---------|---------|---------|---------|
|Azure Information Protection: <br />-クラシックスキャナー <br />-統一されたラベル付けスキャナー | Windows        | Office        |AIP スキャナーによってファイルがスキャンされるたびに生成されます。<br>ログには、次の詳細が含まれます。<br>-一致する情報の種類<br>-ラベル |
|Microsoft Information Protection (MIP) SDK | 任意 | サードパーティ アプリケーション | ファイルがサポートされているサードパーティアプリケーションによってスキャンされるたびに生成されます。 <br />ログには、次の詳細が含まれます。<br />-一致する情報の種類<br />-ラベル|
| | | | |

## <a name="downgrade-label-audit-logs"></a>ラベル監査ログのダウングレード

**ダウングレードラベル** 監査ログは、次のアクティビティに対して生成されます。

| 報告者      | プラットフォーム                       | Application              | アクション/説明      |
| ---------------- | ------------------------------ | ------------------------ | --------------- |
|Azure Information Protection:<br />-従来のスキャナーとクライアント<br />-スキャナーとクライアントの統一されたラベル付け | Windows、SharePoint、1台のドライブ | Office                   | 重要度の低いラベルでドキュメントラベルが更新されるたびに生成されます。|
| Microsoft Defender ATP            | Windows                        | OS                       | 重要度の低いラベルでドキュメントラベルが更新されるたびに生成されます。 |
| Microsoft Information Protection (MIP) SDK          | 任意                            | サードパーティ アプリケーション | 重要度の低いラベルでドキュメントラベルが更新されるたびに生成されます。<br>サードパーティのアプリケーションでサポートされている場合にのみ生成されます。 |
| | | | |

## <a name="file-removed-audit-logs"></a>ファイルが削除された監査ログ

> [!NOTE]
> 削除されたファイルの監査ログは、Azure Information Protection スキャナーバージョン [2.7.96.0](rms-client/unifiedlabelingclient-version-release-history.md#version-27960) 以降でのみサポートされます。

**削除さ** れたファイルの監査ログは、次のアクティビティに対して生成されます。

| 報告者                                                                              | プラットフォーム | Application                     | アクション/説明                                                          |
| ---------------------------------------------------------------------------------------- | -------- | ------------------------------- | ------------------------------------------------------------------------------ |
| Azure Information Protection スキャナー、統一されたラベル付けクライアント | Windows  | Office およびサポートされているファイルの種類 | 以前にスキャンされたファイルが削除されたことを AIP スキャナーが検出するたびに生成されます。 |
| | | | |

## <a name="new-label-audit-logs"></a>新しいラベルの監査ログ

**新しいラベル** の監査ログは、次のアクティビティに対して生成されます。

| 報告者                                                                      | プラットフォーム                       | Application              | アクション/説明                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure Information Protection:<br />-従来のスキャナーとクライアント<br />-スキャナーとクライアントの統一されたラベル付け | Windows、SharePoint、1台のドライブ | Office                   | 新しいラベルが適用されるたびに生成されます。                                                                  |
| Microsoft Defender ATP                                                                            | Windows                        | OS                       | 新しいドキュメントラベルが適用されるたびに生成されます。                                                                  |
| Microsoft Information Protection (MIP) SDK                                                                          | 任意                            | サードパーティ アプリケーション | 新しいドキュメントラベルが適用されるたびに生成されます。<br>サードパーティのアプリケーションでサポートされている場合にのみ生成されます。 |
| | | | |

## <a name="new-protection-audit-logs"></a>新しい保護監査ログ

次のアクティビティについて、**新しい保護** 監査ログが生成されます。

| 報告者                                                                      | プラットフォーム                       | Application              | アクション/説明                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure Information Protection:<br />-クラシッククライアント<br />-統一されたラベル付けクライアント | Windows、SharePoint、1台のドライブ | Office                   | ラベルなしで保護が新たに手動で追加されるたびに生成されます。                                                                  |
| Microsoft Information Protection (MIP) SDK                                                                          | 任意                            | サードパーティ アプリケーション | ラベルなしで保護が新たに手動で追加されるたびに生成されます。<br>サードパーティのアプリケーションでサポートされている場合にのみ生成されます。 |
| | | | |

## <a name="remove-label-audit-logs"></a>ラベル監査ログの削除

**削除ラベル** 監査ログは、次のアクティビティに対して生成されます。

| 報告者                                                                      | プラットフォーム                       | Application              | アクション/説明                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure Information Protection:<br />-従来のスキャナーとクライアント<br />-スキャナーとクライアントの統一されたラベル付け | Windows、SharePoint、1台のドライブ | Office                   | ラベルが削除されるたびに生成されます。                                                                  |
| Microsoft Defender ATP                                                                            | Windows                        | OS                       | ラベルが削除されるたびに生成されます。                                                                  |
| Microsoft Information Protection (MIP) SDK                                                                          | 任意                            | サードパーティ アプリケーション | ラベルが削除されるたびに生成されます。<br>サードパーティのアプリケーションでサポートされている場合にのみ生成されます。 |
| | | | |

## <a name="remove-protection-audit-logs"></a>保護監査ログの削除

**保護の削除** の監査ログは、次のアクティビティに対して生成されます。

| 報告者                                                                      | プラットフォーム                       | Application              | アクション/説明                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure Information Protection:<br />-クラシッククライアント<br />-統一されたラベル付けクライアント | Windows、SharePoint、1台のドライブ | Office                   | ラベルなしで保護が手動で削除されるたびに生成されます。                                                                  |
| Microsoft Information Protection (MIP) SDK                                                                          | 任意                            | サードパーティ アプリケーション | ラベルなしで保護が手動で削除されるたびに生成されます。<br>サードパーティのアプリケーションでサポートされている場合にのみ生成されます。 |
| | | | |

## <a name="upgrade-label-audit-logs"></a>アップグレードラベルの監査ログ

**アップグレードラベル** 監査ログは、次のアクティビティに対して生成されます。

| 報告者                                                                      | プラットフォーム                       | Application              | アクション/説明                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure Information Protection:<br />-従来のスキャナーとクライアント<br />-スキャナーとクライアントの統一されたラベル付け | Windows、SharePoint、1台のドライブ | Office                   | より機密性の高いラベルでドキュメントラベルが更新されるたびに生成されます。                                                                   |
| Microsoft Defender ATP                                                                            | Windows                        | OS                       | より機密性の高いラベルでドキュメントラベルが更新されるたびに生成されます。                                                                   |
| Microsoft Information Protection (MIP) SDK                                                                          | 任意                            | サードパーティ アプリケーション | より機密性の高いラベルでドキュメントラベルが更新されるたびに生成されます。<br>サードパーティのアプリケーションでサポートされている場合にのみ生成されます。 |
| | | | |

## <a name="next-steps"></a>次のステップ

監査ログの詳細については、「 [Azure Information Protection の中央レポート (パブリックプレビュー)](reports-aip.md)」を参照してください。
