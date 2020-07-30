---
title: 概念-MIP SDK プロキシサポートの主要な概念
description: この記事では、MIP SDK でのプロキシのサポートについて説明します。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 07/29/2020
ms.author: tommos
ms.openlocfilehash: 54d675b44088550a07c549ff6c10621fa351fdf1
ms.sourcegitcommit: edd0614ef6f687ff2745f56e4171cd72e03edc9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2020
ms.locfileid: "87440652"
---
# <a name="microsoft-information-protection-sdk---proxy-support"></a>Microsoft Information Protection SDK-プロキシのサポート

## <a name="proxies-and-the-mip-sdk"></a>プロキシと MIP SDK

現在、MIP SDK では、非透過プロキシは Windows でのみサポートされています。

* **透過プロキシ**とは、明示的または自動検出された設定を含む、クライアント側の構成を必要としない任意の種類のプロキシを指します。
* **認証済みプロキシ**とは、呼び出し元が認証される必要がある任意の種類のプロキシを指します。
* **プロキシ自動検出**は、web プロキシ自動検出 (WPAD) を介して検出されたプロキシまたは設定を参照します。
* **明示的なプロキシ**とは、オペレーティングシステムまたはアプリケーションに直接提供されるプロキシを指します。
  
| プラットフォーム        | 透過プロキシ | 認証されたプロキシ | プロキシの自動検出 | 明示的なプロキシ |
| --------------- | ----------------- | --------------------- | -------------------- | -------------- |
| **Windows**     | サポートされています         | サポート非対象         | サポート            | サポートされています      |
| **Linux (すべて)** | サポートされています         | サポートされていません         | サポートされていません        | サポートされていません  |
| **MacOS**       | サポートされています         | サポートされていません         | サポートされていません        | サポートされていません  |
| **Android**     | サポートされています         | サポートされていません         | サポートされていません        | サポートされていません  |
| **iOS**         | サポートされています         | サポートされていません         | サポートされていません        | サポートされていません  |

## <a name="proxies-on-windows"></a>Windows 上のプロキシ

Windows で実行されている MIP SDK アプリケーションは、WinHTTP を使用してネットワークにアクセスします。 WinHTTP の構成設定は、Windows インターネット (WinINet) のインターネット参照プロキシ設定とは関係なく、次の探索方法を使用してのみ、プロキシサーバーを検出できます。

* 自動検出方法:
  * 透過的プロキシ
  * Web プロキシ自動検出プロトコル (WPAD)
* 手動による静的プロキシ構成:
  * netsh コマンドを使用して構成された WinHTTP

WinHTTP の構成の詳細については、 [winhttp のドキュメント](/windows/win32/winhttp/winhttp-start-page)を参照してください。

## <a name="proxies-on-other-platforms"></a>他のプラットフォームのプロキシ

MIP SDK は、Windows 以外のプラットフォーム上の任意の型の完全に透過的なプロキシをサポートしていません。 この機能が必要な場合、詳細については、「カスタム HTTP デリゲートと回避策」セクションを参照してください。

## <a name="custom-http-delegate"></a>カスタム HTTP デリゲート

Microsoft Information Protection SDK は、SDK の既定の HTTP スタックをオーバーライドできるカスタム HTTP デリゲートの実装をサポートしています。 機能が存在しない場合、または特定の HTTP 実装が必要な場合は、を継承する新しいクラスを追加することによって、このデリゲートを実装でき [`mip::HttpDelegate`](./reference/class_mip_httpdelegate.md) ます。

この `mip::HttpDelegate` 派生クラスは、次の方法で設定され `mip::FileProfile::Settings` ます。

```cpp
std::shared_ptr<MyHttpDelegate> httpDelegate = std::make_shared<MyHttpDelegate>();
            
FileProfile::Settings profileSettings(mMipContext,
    mip::CacheStorageType::OnDisk,
    std::make_shared<sample::consent::ConsentDelegateImpl>(),
    std::make_shared<FileProfileObserver>());

profileSettings.SetHttpDelegate(httpDelegate);
```

## <a name="other-workarounds"></a>その他の回避策

カスタム HTTP デリゲートがオプションでない場合は、プロキシをバイパスし、MIP ラベルと保護エンドポイントの直接ネットワーク接続を許可し、Azure Active Directory する必要があります。 [監査ログ](/azure/information-protection/reports-aip)が必要な場合は、監査ログのエンドポイントも必要です。

| エンドポイント           | hostname                                                                                                                                                                |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 保護サービス | https://api.aadrm.com                                                                                                                                                   |
| ポリシー             | https:// \* protection.outlook.com                                                                                                                                       |
| 監査ログ      | https:// \* events.data.microsoft.com、https:// \* (iOS のみ)                                                                                          |
| 認証     | [Azure AD のドキュメントを確認してください](/azure/active-directory/develop/authentication-national-cloud#azure-ad-authentication-endpoints) |
