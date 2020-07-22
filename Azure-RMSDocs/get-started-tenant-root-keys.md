---
title: テナントルートキーの使用と管理を開始する
description: テナントのルートキー管理を計画した後の次の手順について説明します。これには、Microsoft および BYOK 保護によって生成される既定のキーが含まれます。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/21/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.subservice: kms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: 0d0fe05fa31e14c583362183e28cc14835d78268
ms.sourcegitcommit: 6d10435c67434bdbbdd51b4a3535d0efaf8307da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86869667"
---
# <a name="getting-started-with-tenant-root-keys"></a>テナントルートキーの概要

>*適用対象: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

必要に応じてテナントキーの計画、作成、および構成が完了したら、次の手順に進みます。

- [テナントキーの使用を開始する](#start-using-your-tenant-key)
- [使用状況ログを考慮する](#consider-usage-logging)

テナントキーに対してサポートされているライフサイクル操作の詳細については、「 [Azure Information Protection テナントキーの操作](./operations-tenant-key.md)」を参照してください。

> [!TIP]
> 機密性の高いコンテンツに対してオンプレミスの保護を必要とする組織の場合は、 [HYOK protection](configure-adrms-restrictions.md) (クラシッククライアントのみ) または[dke 保護](plan-implement-tenant-key.md#double-key-encryption-dke-aip-unified-labeling-client-only)(統合ラベル付けクライアントのみ) を構成します。
> 

## <a name="start-using-your-tenant-key"></a>テナントキーの使用を開始する

Rights Management サービスがまだアクティブになっていない場合はアクティブ化し、組織で Azure Information Protection の使用を開始できるようにします。 ユーザーはすぐにテナントキーの使用を開始します。

詳細については、「[Activating the protection service from Azure Information Protection (Azure Information Protection の保護サービスのアクティブ化)](./activate-service.md)」をご覧ください。

> [!NOTE]
> Rights Management サービスがアクティブ化された後に独自のテナントキーを管理することにした場合、ユーザーは数週間後に古いキーから新しいキーに徐々に移行されます。
>
>この移行中、以前のテナントキーで保護されていたドキュメントやファイルは、承認されたユーザーに引き続きアクセスできます。

## <a name="consider-usage-logging"></a>使用状況ログを考慮する

使用状況ログは、Azure Rights Management サービスが実行するすべてのトランザクションをログに記録します。

キー管理方法によっては、テナントキーの詳細がログ情報に含まれる場合があります。 次の図は、Excel に表示されるログファイルの例を示しています。この例では、テナントキーが使用されていることを示す**KeyVaultDecryptRequest**および**KeyVaultSignRequest**要求の種類が示されています。
    
![Excel のログ ファイル、テナント キーが使用されていることがわかる](./media/RMS_Logging.png)
    
使用状況ログの詳細については、「 [Azure Information Protection からの保護の使用状況のログと分析](./log-analyze-usage.md)」を参照してください。
