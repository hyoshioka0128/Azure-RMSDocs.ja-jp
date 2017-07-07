---
title: "サポートされるファイル形式 | Azure RMS"
description: "File API の現在のバージョンは、MS Office ファイルに対するネイティブ保護と、それ以外のすべてのファイル形式に対する PDF および PFile 保護をサポートしています。"
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: EC831494-7F2C-4C70-9063-B02CDDEA14EE
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 579a02755e4703e34914309475cf03d74c2758b4
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2017
---
# <a name="supported-file-formats"></a>サポートされるファイル形式

File API は、ネイティブ形式と Pfile 形式をサポートしています。

## <a name="supported-file-formats"></a>サポートされるファイル形式

File API の現在のバージョンは、Microsoft Office ファイルに対するネイティブ保護と、それ以外のすべてのファイル形式に対する Portable Document Files (PDF) および PFile 保護をサポートしています。 PDF ファイルには、オプションで PFile 保護を適用できます。

-   **ネイティブ保護**。 ネイティブ保護では、ファイルは MIME の種類 (ファイル名拡張子) に基づく AD RMS ファイル形式に暗号化されます。 File API を使ってネイティブに保護されるファイルは、ネイティブ保護を使用する AD RMS 対応アプリケーション (たとえば、Office 2013、Office 2010、FoxIt PDF リーダー) が対応する形式と一致します。 ネイティブ保護は、Office ファイル、PDF ファイル、および他のいくつかのファイルの種類でのみサポートされます。 ネイティブ保護がサポートされるファイルの種類の詳細については、「[File API configuration (File API の構成)](file-api-configuration.md)」を参照してください。
-   **PFile 保護**。 PFile 保護では、ファイルは、AD RMS 保護ファイル (PFile) 形式を使用して暗号化されます。 ファイルは、.pfile という拡張子のファイルに暗号化されます。 PFile 保護は、Office ファイルを除くすべてのファイル形式に対してサポートされます。

管理者は、レジストリ キーを設定して、ファイル名拡張子に基づいてファイルを保護するかどうか、およびその方法を構成することができます。 File API を使用してファイルの保護を構成する方法の詳細については、「[File API configuration (File API の構成)](file-api-configuration.md)」を参照してください。

## <a name="related-topics"></a>関連項目

* [開発者向け注意事項](developer-notes.md)
* [ファイル API の構成](file-api-configuration.md)
 
[!INCLUDE[Commenting house rules](../includes/houserules.md)]