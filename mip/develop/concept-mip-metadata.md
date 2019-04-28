---
title: MIP SDK 内のラベルのメタデータの概念
description: この記事では、Microsoft Information Protection SDK によって生成されるメタデータを理解できます。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 11/08/2018
ms.author: tommos
ms.openlocfilehash: 990f729edaa0a2e212812f84fc5a4c63f82e37fb
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60175362"
---
# <a name="microsoft-information-protection-sdk---metadata"></a>Microsoft Information Protection SDK - メタデータ

Microsoft の Information Protection SDK には、ファイルに適用されるメタデータのセットが生成されます。 このメタデータは、ラベルを表したものです。 このドキュメントでは、メール、ドキュメント、およびその他のレコードに適用する SDK を生成するメタデータについて説明します。

## <a name="labels"></a>ラベル

Microsoft の Information Protection SDK 内のラベルは、その情報の機密性を説明する情報に適用されます。 データのラベルは、ファイルまたはラベルを表すキー/値ペアのセット内のレコードに保存されます。 メタデータ名は、次の構造にビルドされます。

`DefinedPrefix_ElementType_GlobalIdentifier_AttributeName`

Microsoft Information Protection ラベルが付いたデータに適用すると、結果は。

`MSIP_Label_GUID_Enabled = true`

GUID は、組織の各ラベルの一意の識別子です。

## <a name="microsoft-information-protection-sdk-metadata"></a>Microsoft の情報保護 SDK メタデータ

MIP SDK には、次の一連のメタデータが適用されます。

| 属性 | 型または値                 | 説明                                                                                                                                                                                                                                        | 必須 |
|-----------|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|
| **有効**   | True または False                 | この属性は、データ項目のこのキー値のペアのセットによって表される分類が有効になっているかどうかを示します。 通常、DLP 製品は、分類ラベルを識別するためにこのキーの存在を検証します。 | はい       |
| **SiteId**    | GUID                          | Azure Active Directory テナント ID                                                                                                                                                                                                                   | はい       |
| **ActionId**  | GUID                          | ActionID は、ラベルを設定するたびに変更されます。 監査ログには、新旧両方の actionID アクティビティ データ項目にラベル付けのチェーンを許可するのには含まれます。                                                                                 | はい       |
| **方法**    | Standard、Privileged、または自動        | :Assignmentmethod を使用して設定します。                                                                                                                                                                                                                 | いいえ        |
| **SetDate**   | 拡張の ISO 8601 の日付形式 | ラベルが設定されたときのタイムスタンプ。                                                                                                                                                                                                              | いいえ        |
| **名前**      | string                        | ラベル、テナント内で一意の名前。 必ずしも、表示名に対応していません。                                                                                                                                                              | いいえ      |
| **ContentBits** | 整数 (integer) | マークするコンテンツの種類を記述するビットマスクは、ファイルに適用する必要があります。 CONTENT_HEADER = 0X1、CONTENT_FOOTER = 0X2、透かし = 0X4
 | いいえ |

ファイルに適用する場合、結果は次の表に似ています。

| キー                                                         | [値]                                |
|-------------------------------------------------------------|--------------------------------------|
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Enabled     | true                                 |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SetDate     | 2018-11-08T21:13:16-0800             |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Method      | 特権                           |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Name        | 社外秘                         |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SiteId      | cb46c030-1825-4e81-a295-151c039dbf02 |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ContentBits | 2                                    |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ActionId    | 88124cf5-1340-457d-90e1-0000a9427c99 |

## <a name="extending-metadata-with-custom-attributes"></a>カスタム属性を持つメタデータの拡張

ファイルとポリシーの API を使用してカスタム メタデータを追加できます。 カスタム属性は、ベースを維持する必要があります`MSIP_Label_GUID`プレフィックス。 

たとえば、Contoso Corporation によって記述されたアプリケーションは、どのシステムにはラベルの付いたファイルが生成されたことを示すメタデータを適用する必要があります。 アプリケーションが付いた、新しいラベルを作成できます`MSIP_Label_GUID`します。 カスタム メタデータを生成するプレフィックスには、ソフトウェア ベンダーの名前とカスタム属性が追加されます。

```
MSIP_Label_f048e7b8-f3aa-4857-bf32-a317f4bc3f29_ContosoCorp_GeneratedBy = HRReportingSystem
```

> [!Note]
> 一般的なアプリケーション、それぞれの最大長の間で互換性を維持するために、キーと値は、255 文字です。

## <a name="versioning"></a>バージョン管理

時間の経過と共に属性導入された、変更、または廃止します。 これらの古いを処理するアプリケーションは引き続きまたは企業全体の値の置換としての提供終了になった属性が年にかかる場合がありますのことが期待されます。

属性を新しいバージョンに置き換えることがある場合は、属性にバージョン サフィックスを追加してください。

`MSIP_Label_GUID_EnabledV2 = True | False | Condition`

## <a name="email"></a>Email

電子メールに適用されるメタデータは保持キー/値ペアの形式のドキュメントに似ています。 主な違いは、という名前の 1 つの電子メール ヘッダーをですべての属性をシリアル化する**MSIP_Labels**します。 キー/値ペアは、セミコロンと空白文字で区切られ、新しいヘッダーに配置します。

上記のサンプル メタデータを使用するには。

```
MSIP_Labels: MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Enabled=true; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SetDate=2018-11-08T21:13:16-0800; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Method=Privileged; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Name=Confidential; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SiteId=cb46c030-1825-4e81-a295-151c039dbf02; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ContentBits=2; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ActionId=88124cf5-1340-457d-90e1-0000a9427c99
```
