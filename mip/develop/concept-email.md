---
title: MIP SDK を使用して電子メールメッセージを処理する方法
description: この記事では、MIP SDK file API を使用して、.msg および rpq メッセージファイルを処理する方法のシナリオについて説明します。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 04/08/2020
ms.author: mbaldwin
ms.openlocfilehash: 52526409b6d08efde1064063b9f36564baa6a378
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2021
ms.locfileid: "97864772"
---
# <a name="file-api-email-message-file-processing"></a>ファイル API の電子メールメッセージファイル処理

MIP SDK は、電子メールメッセージの復号化と暗号化をサポートしています。 Outlook または Exchange によって生成される .msg ファイルと、という2つのメッセージファイルは、SDK でサポートされています。ただし、このシナリオでは少し異なる方法で説明します。

このシナリオの一般的なユースケースの一部を次に示します。

- 電子情報開示のためにメッセージを復号化する
- DLP 検査のためにメールと添付ファイルの暗号化を解除する
- 基幹業務アプリケーションから保護されたメッセージを直接公開する
- 転送中のメッセージの暗号化解除、変更、再保護

## <a name="file-api-operations-for-msg-files"></a>.Msg ファイルのファイル API 操作

File API は、.msg ファイルの保護操作と、その他の種類のファイルと同じ方法でサポートされます。ただし、SDK では MSG 機能フラグを有効にする必要がある点が異なります。 

> [!IMPORTANT]
> .Msg ファイルのラベル付け操作は現在サポートされていません。

前に説明したとおり、`mip::FileEngine` のインスタンス化には、設定オブジェクト、`mip::FileEngineSettings` が必要です。 `mip::FileEngineSettings` を使用すると、特定のインスタンスに対してアプリケーションで設定する必要があるカスタム設定のパラメーターを渡すことができます。 FileEngineSettings の CustomSettings プロパティは、 `enable_msg_file_type` .msg ファイルの処理を有効にするためのフラグを設定するために使用されます。

Msg ファイル保護操作の擬似コードは、次のようになります。

- `enable_msg_file_type`にフラグを設定 `mip::FileEngineSettings` し、 `mip::FileEngine` をに追加し `mip::FileProfile` ます。
- 保護 API を使用して、ユーザーが使用できる保護テンプレートを一覧表示します。
- `mip::FileHandler`保護されるファイルを指すコンストラクト。
- 保護するテンプレートを選択し、の方法を使用して保護をファイルに設定し `mip::FileHandler` `SetProtection` ます。

保護テンプレートを一覧表示する方法については、「Protection API の [クイックスタート: テンプレートの一覧](quick-protection-list-templates-cpp.md) 」を参照してください。

## <a name="file-api-operations-for-rpmsg-files"></a>ファイル API 操作 (. rpq msg ファイル)

MIP SDK は、MIME に準拠している (通常は EML) メッセージをサポートしていません。 代わりに、SDK は、埋め込まれた **メッセージ** を復号化し、バイトストリームのセットを出力として表現できる検査関数を公開します。 メッセージを抽出して API に渡すのは、SDK のコンシューマーだけです。 Office メッセージの暗号化のシナリオでは、このファイル名のバリエーションが存在し、API は message_v2、v3、または v4 ファイルも受け入れます。

通常、メールゲートウェイとデータ損失防止 (DLP) サービスは、電子メールの転送中に MIME 準拠メッセージを処理します。 メールが保護されている場合、メッセージの内容は添付ファイル ( *メッセージ*) に格納されます。 この添付ファイルには、暗号化された電子メール本文と、元のメッセージの一部であった添付ファイルが含まれます。 *Rpq msg* ファイルは、プレーンテキストのラッパー電子メールに添付され、メールサービスに送信されます。 メッセージが Exchange または Exchange Online の境界内に出ると、そのメッセージは、送信先に送信できるように、MIME に準拠した形式になります。

ほとんどの場合、dlp パートナーは、DLP ポリシーを検査して評価するために、メッセージから添付ファイルとプレーンテキストバイトを取得できる必要があります。 検査 API は、メッセージを入力として受け取り、バイトストリームを出力として返します。 これらのバイトストリームには、メッセージのプレーンテキストバイトと添付ファイルが含まれています。 アプリケーション開発者は、これらのストリームを処理し、それらのストリームで役に立つもの (検査、再帰的な復号化など) を実行する必要があります。

API は、 `Inspect` `mip::FileInspector` サポートされているファイルの種類を検査する操作を公開するクラスによって実装されます。 `mip::MsgInspector` を拡張します。これにより `mip::FileInspector` 、は、rpq msg ファイル形式に固有の復号化操作を公開します。 MIP SDK は、 *メッセージの rpq* ファイルの発行シナリオをサポートしていません。

`mip::MsgInspector` クラスは以下のメンバーを公開します:

```cpp
public const std::vector<uint8_t>& GetBody()
public BodyType GetBodyType() const
public BodyType GetBodyType() const
public InspectorType GetInspectorType() const
public std::shared_ptr<Stream> GetFileStream() const
```

詳細については、 [API リファレンス](./reference/mip-sdk-reference.md)を参照してください。

## <a name="next-steps"></a>次の手順

- [FILE API-Process email. msg files (C++) クイックスタート](quick-email-msg-cpp.md)を確認する
- [ファイル API を確認する-電子メールファイルを処理する (C#) クイックスタート](quick-email-msg-csharp.md)