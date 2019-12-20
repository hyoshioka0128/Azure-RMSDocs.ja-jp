---
title: 概念-MIP SDK でのメタデータのラベル付け
description: この記事は、Microsoft Information Protection SDK によって生成されるメタデータを理解するのに役立ちます。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 11/08/2018
ms.author: tommos
ms.openlocfilehash: 3ae27b1bf0b4f709e9621f00b1b3a16c2ba1882c
ms.sourcegitcommit: 474cd033de025bab280cb7a9721ac7ffc2d60b55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "69886142"
---
# <a name="microsoft-information-protection-sdk---metadata"></a>Microsoft Information Protection SDK-メタデータ

Microsoft Information Protection SDK は、ファイルに適用する必要があるメタデータのセットを生成します。 このメタデータは、ラベルの表現です。 このドキュメントでは、メール、ドキュメント、およびその他のレコードに適用するために SDK によって生成されるメタデータについて説明します。

## <a name="labels"></a>ラベル

Microsoft Information Protection SDK のラベルは、その情報の機密度を説明するために、情報に適用されます。 ラベルデータは、ラベルを説明するキーと値のペアのセット内のファイルまたはレコードに保存されます。 メタデータ名は、次の構造に基づいて構築されます。

`DefinedPrefix_ElementType_GlobalIdentifier_AttributeName`

Microsoft Information Protection でラベル付けされたデータに適用すると、結果は次のようになります。

`MSIP_Label_GUID_Enabled = true`

GUID は、組織内の各ラベルの一意の識別子です。

## <a name="microsoft-information-protection-sdk-metadata"></a>Microsoft Information Protection SDK メタデータ

MIP SDK は、次の一連のメタデータを適用します。

| 属性 | 型または値                 | [説明]                                                                                                                                                                                                                                        | [必須] |
|-----------|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|
| **Enabled**   | True または False                 | この属性は、このキーと値のペアのセットによって表される分類がデータ項目に対して有効になっているかどうかを示します。 DLP 製品は、通常、このキーが存在するかどうかを検証して分類ラベルを識別します。 | [はい]       |
| **SiteId**    | GUID                          | Azure Active Directory テナント ID                                                                                                                                                                                                                   | [はい]       |
| **ActionId**  | GUID                          | ActionID は、ラベルが設定されるたびに変更されます。 監査ログには、古い actionID と新しい actionID の両方が含まれます。これにより、データ項目にラベルアクティビティを連鎖させることができます。                                                                                 | [はい]       |
| **方法**    | 標準または特権        | [Mip::](reference/mip-enums-and-structs.md#assignmentmethod-enum)の設定メソッドを使用して設定します。 標準は、ラベルが既定で適用されるか、自動的に適用されることを意味します。 Privileged は、ラベルが手動で選択されたことを意味します。                                                                                                                                                                                                                 | [いいえ]        |
| **SetDate**   | 拡張 ISO 8601 日付形式 | ラベルが設定されたときのタイムスタンプ。                                                                                                                                                                                                              | [いいえ]        |
| **名前**      | string                        | テナント内の一意の名前をラベル付けします。 必ずしも表示名に対応しているわけではありません。                                                                                                                                                              | [いいえ]      |
| **ContentBits** | integer | ファイルに適用するコンテンツマークの種類を記述するビットマスク。 CONTENT_HEADER = 0X1、CONTENT_FOOTER = 0X2、透かし = 0X4、ENCRYPT = 0x8
 | [いいえ] |

ファイルに適用すると、結果は次の表のようになります。

| キー                                                         | 値                                |
|-------------------------------------------------------------|--------------------------------------|
| MSIP_Label_2096f6a2-d2f7-48be-b73aaa526e5d_Enabled     | true                                 |
| MSIP_Label_2096f6a2-d2f7-48be-b73aaa526e5d_SetDate     | 2018-11-08T21:13:16-0800             |
| MSIP_Label_2096f6a2-d2f7-48be-b73aaa526e5d_Method      | 特権付き                           |
| MSIP_Label_2096f6a2-d2f7-48be-b73aaa526e5d_Name        | 社外秘                         |
| MSIP_Label_2096f6a2-d2f7-48be-b73aaa526e5d_SiteId      | cb46c030-1825-4e81-a295-151c039dbf02 |
| MSIP_Label_2096f6a2-d2f7-48be-b73aaa526e5d_ContentBits | 2 で保護されたプロセスとして起動されました                                    |
| MSIP_Label_2096f6a2-d2f7-48be-b73aaa526e5d_ActionId    | 88124cf5-1340-457d-90e1-0000a9427c99 |

## <a name="extending-metadata-with-custom-attributes"></a>カスタム属性を使用したメタデータの拡張

カスタムメタデータは、ファイルおよびポリシー API を使用して追加できます。 カスタム属性では、基本 `MSIP_Label_GUID` プレフィックスを維持する必要があります。 

たとえば、Contoso Corporation によって作成されたアプリケーションは、ラベル付きファイルを生成したシステムを示すメタデータを適用する必要があります。 アプリケーションでは、`MSIP_Label_GUID`で始まる新しいラベルを作成できます。 カスタムメタデータを生成するために、ソフトウェアベンダー名とカスタム属性がプレフィックスに追加されます。

```
MSIP_Label_f048e7b8-f3aa-4857-bf32-a317f4bc3f29_ContosoCorp_GeneratedBy = HRReportingSystem
```

> [!Note]
> 共通のアプリケーション間での互換性を維持するために、キーと値の最大長は255文字です。

## <a name="versioning"></a>バージョン管理

時間の経過と共に、属性は導入、変更、または廃止されます。 企業全体で値を置き換えるには数年かかる場合があるため、アプリケーションはこれらの古い属性または廃止された属性を引き続き処理することが期待されます。

属性を新しいバージョンに置き換える場合は、バージョンサフィックスを属性に追加する必要があります。

`MSIP_Label_GUID_EnabledV2 = True | False | Condition`

## <a name="email"></a>電子メール

電子メールに適用されるメタデータは、ドキュメントの場合と同様に、キーと値のペアの形式を保持します。 主な違いは、すべての属性が**MSIP_Labels**と呼ばれる1つの電子メールヘッダーにシリアル化されることです。 キーと値のペアは、セミコロンと空白で区切られ、新しいヘッダーに配置されます。

上記のサンプルメタデータを使用します。

```
MSIP_Labels: MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Enabled=true; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SetDate=2018-11-08T21:13:16-0800; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Method=Privileged; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Name=Confidential; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SiteId=cb46c030-1825-4e81-a295-151c039dbf02; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ContentBits=2; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ActionId=88124cf5-1340-457d-90e1-0000a9427c99
```
