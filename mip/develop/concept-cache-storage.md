---
title: 概念-キャッシュストレージ
description: この記事は、MIP SDK のキャッシュストレージに関する概念を理解するのに役立ちます。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/30/2019
ms.author: tommos
ms.openlocfilehash: 6e9e726c133f5796a2406a1cacb746fc561a6457
ms.sourcegitcommit: 6b159e050176a2cc1b308b1e4f19f52bb4ab1340
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "95570151"
---
# <a name="microsoft-information-protection-sdk---cache-storage"></a>Microsoft Information Protection SDK-キャッシュストレージ

MIP SDK は、SDK キャッシュストレージを維持するための SQLite3 データベースを実装します。 Microsoft Information Protection SDK のバージョン1.3 より前では、ディスクとメモリの2種類のキャッシュ状態ストレージのみがサポートされていました。 これらの型はいずれも、特定のデータ (特に保護されたコンテンツのライセンスとポリシー情報) をプレーンテキストで格納しています。

SDK のセキュリティ体制を向上させるために、プラットフォーム固有の暗号化 Api を使用してデータベースとその内容を保護する、2番目の種類のディスクキャッシュのサポートを追加しました。

アプリケーションは `FileProfileSettings` 、、 `PolicyProfileSettings` 、またはオブジェクトの一部としてプロファイルを読み込むときに、キャッシュの種類を定義し `ProtectionProfileSettings` ます。 キャッシュの種類は、プロファイルが有効な場合は静的です。 別の種類のキャッシュストレージ型に変更するには、既存のプロファイルを破棄して新しいプロファイルを作成する必要があります。

## <a name="cache-storage-types"></a>キャッシュストレージの種類

MIP SDK リリース1.3 以降では、次のストレージキャッシュの種類を使用できます。

| Type            | 目的                                                                                                                         |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| InMemory        | では、アプリケーションのメモリにストレージキャッシュを保持します。                                                                       |
| Ondisk です          | 設定オブジェクトで指定されたディレクトリに、ディスク上にデータベースを格納します。 データベースはプレーンテキストで格納されます。              |
| OnDiskEncrypted | 設定オブジェクトで指定されたディレクトリに、ディスク上にデータベースを格納します。 データベースは OS 固有の Api を使用して暗号化されます。 |

アプリケーションによって生成された各 **エンジン** は、新しい暗号化キーを生成します。

キャッシュストレージは、いずれかのプロファイル設定オブジェクトを使用して `mip::CacheStorageType` 列挙されます。

```cpp 
FileProfile::Settings profileSettings(mMipContext,
    mip::CacheStorageType::OnDiskEncrypted, // Define the storage type to use.
    mAuthDelegate,
    std::make_shared<sample::consent::ConsentDelegateImpl>(),
    std::make_shared<FileProfileObserver>());
```

## <a name="when-to-use-each-type"></a>各型を使用する場合

キャッシュストレージは、以前に暗号化が解除された情報へのオフラインアクセスを維持し、データが以前に使用されていたときの暗号化解除操作のパフォーマンスを確保するために重要です。

- **メモリストレージの** 場合: このストレージの種類は、サービスの再起動の間にポリシーまたはライセンスキャッシュ情報を保持する必要がない長期間のプロセスに使用します。
- **ディスク上**: プロセスの停止と開始が頻繁に行われるが、再起動の際にポリシー、ライセンス、およびサービス検出のキャッシュを保持する必要があるアプリケーションには、この種類のストレージを使用します。 このストレージキャッシュの種類はプレーンテキストであるため、ユーザーが状態ストレージにアクセスできないサーバーワークロードに適しています。 この例としては、サーバー上で実行されている Windows サービスまたは Linux デーモンや、サービス管理者のみが状態データにアクセスできる SaaS アプリケーションなどがあります。
- **ディスク上および暗号化** 済み: プロセスが頻繁に停止および起動する可能性がありますが、再起動の際にポリシー、ライセンス、およびサービス検索のキャッシュを保持する必要があるアプリケーションには、この種類のストレージを使用します。 このストレージキャッシュは暗号化されているため、ユーザーが状態データベースを参照して検出できるワークステーションアプリケーションに適しています。 暗号化を使用すると、ポリシーの内容または保護ライセンスの内容をプレーンテキストで使用して、ユーザーがアクセスできないようにすることができます。 すべてのケースで、ユーザーがアクセスできるキーを使用してデータが暗号化されることに注意してください。 熟練した敵対者は、最小限の労力でキャッシュの暗号化を解除できますが、改ざんや閲覧を防ぐことができます。

## <a name="supported-platforms-for-encryption"></a>暗号化に対してサポートされているプラットフォーム

| プラットフォーム          | バージョン                | ノート                                                                                                                               |
| ----------------- | ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Microsoft Windows | Windows 8 以降    | Windows 7 でサポートされるのは CacheStorageType:: OnDisk のみです                                                                                    |
| macOS             | High Sierra 以降  |                                                                                                                                     |
| Ubuntu Linux      | 16.04 以降        | [SecretService](https://developer.gnome.org/libsecret/unstable/SecretService.html)と `LinuxEncryptedCache` 機能フラグが必要です。 |
| Android           | Android 7.0 以降   |                                                                                                                                     |
| iOS               | サポートされているすべてのバージョン |                                                                                                                                     |

MIP SDK では他の Linux ディストリビューションがサポートされていますが、Red Hat Enterprise Linux、CentOS、Debian のキャッシュ暗号化はテストしていません。

> [!NOTE]
> Linux でキャッシュストレージを有効にする機能フラグは、 `mip::MipContext::CreateWithCustomFeatureSettings()`

## <a name="cache-storage-database-tables"></a>キャッシュストレージデータベーステーブル

MIP SDK はキャッシュ用に2つのデータベースを保持します。 1つは、保護 Api 用であり、保護の状態の詳細を維持することです。 もう1つは、ポリシー Api と、ポリシーの詳細とサービス情報の管理です。 どちらも、settings オブジェクトで定義されたパスに格納されます。 **mip\mip.policies.sqlite3** と **mip\mip.protection.sqlite3** の下にあります。

### <a name="protection-database"></a>保護データベース

| テーブル         | 目的                                                        | 暗号化 |
| ------------- | -------------------------------------------------------------- | --------- |
| AuthInfoStore | 認証チャレンジの詳細を格納します。                       | いいえ        |
| Conのストア  | 各エンジンの同意結果を格納します。                        | いいえ        |
| DnsInfoStore  | SDK 保護操作の DNS 参照結果を格納します        | いいえ        |
| EngineStore   | エンジンの詳細、関連付けられたユーザー、およびカスタムクライアントデータを格納します。 | いいえ        |
| KeyStore      | 各エンジンの対称暗号化キーを格納します。              | はい       |
| LicenseStore  | 以前に暗号化解除されたデータの使用ライセンス情報を格納します。  | はい       |
| SdInfoStore   | サービス検出の結果を格納します。                              | いいえ        |

### <a name="policy-database"></a>ポリシーデータベース

| テーブル           | 目的                                                          | 暗号化 |
| --------------- | ---------------------------------------------------------------- | --------- |
| KeyStore        | 各エンジンの対称暗号化キーを格納します。                | はい       |
| ポリシー        | 各ユーザーのラベルポリシー情報を格納します。                   | はい       |
| この Url     | 特定のユーザーのバックエンドポリシーサービスの URL を格納します。             | いいえ        |
| 感度     | 特定のユーザーポリシーの分類規則を格納します。          | はい       |
| SensitivityUrls | 特定のユーザーのバックエンド感度ポリシーサービスの URL を格納します。 | いいえ        |

## <a name="database-size-considerations"></a>データベースサイズに関する考慮事項

データベースサイズは、キャッシュに追加されているエンジンの数とキャッシュされている保護ライセンスの数という2つの要因によって異なります。 MIP SDK 1.3 では、有効期限が切れたときにライセンスキャッシュをクリーンアップするメカニズムはありません。 必要以上に大きくなったときにキャッシュを削除するには、外部プロセスが必要です。

データベースの拡張に関する最も重要な貢献者は、保護ライセンスキャッシュです。 サービスのラウンドトリップがアプリケーションのパフォーマンスに影響を与えない場合、またはキャッシュのサイズが大きすぎる場合は、ライセンスキャッシュを無効にすることができます。 これを実現するには `CanCacheLicenses` 、 `FileProfile::Settings` オブジェクトのを false に設定します。

```cpp
FileProfile::Settings profileSettings(mMipContext,
    mip::CacheStorageType::OnDiskEncrypted,
    mAuthDelegate,
    std::make_shared<sample::consent::ConsentDelegateImpl>(),
    std::make_shared<FileProfileObserver>());

profileSettings.SetCanCacheLicenses(false);
```

### <a name="caching-api-engines"></a>API エンジンのキャッシュ

通常、MIP SDK では、api 操作を実行するユーザーごとに API エンジンが作成され、認証済み id の代わりに実行されるすべての操作へのインターフェイスが提供されます。 「 [プロファイルとエンジンの概念](concept-profile-engine-cpp.md)」で説明したように、Fileengine、policyengine、または protectionengine にはそれぞれ、との2つの状態があり `CREATED` `LOADED` ます。 SDK 操作を実行できるようにするには、エンジンを作成して読み込む必要があります。 エンジンが使用されていない場合、API はエンジンをキャッシュし、 `CREATED` 使用可能なリソースに応じて、可能な限り状態のままにします。 各 API のプロファイルクラスには、 `UnloadEngineAsync` これを明示的に実現するメソッドも用意されています。

各エンジンには、 `id` すべてのエンジン管理操作で使用される一意の識別子があります。 クライアントアプリケーションは、id を明示的に提供することも、アプリケーションによって提供されない場合は SDK を生成することもできます。 エンジンの作成時にエンジン設定オブジェクトを使用して一意の識別子を指定し、前に説明したように API プロファイルでキャッシュを有効にすると、ユーザーが SDK で操作を実行するたびに同じエンジンを使用できます。 コードスニペットに従って、、を作成し `[mip::FileEngine](./concept-profile-engine-file-engine-cpp.md#create-file-engine-settings)` `[mip::PolicyEngine](./concept-profile-engine-policy-engine-cpp.md#implementation-create-policy-engine-settings)` ます。

既存のエンジン Id を指定しないと、ポリシーのフェッチに余分なサービスラウンドトリップが発生し、既存のエンジンに対して既にキャッシュされている可能性があるライセンスがフェッチされます。 エンジン ID をキャッシュすることで、以前に暗号化が解除された情報と一般的なパフォーマンスの向上に、SDK のオフラインアクセスを alllows ことができます。