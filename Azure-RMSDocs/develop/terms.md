---
title: AIP 開発者向け用語集 |Microsoft Docs
description: Rights Management サービスに固有の開発者用語定義のコレクション。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 01/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: adb1f868-0da7-431b-83d1-86f41c2da4ae
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: a636b58b1ac60beed54492ac74240080ed4ce95e
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57330306"
---
# <a name="terms"></a>利用規約

Azure Information Protection に固有の開発者用語定義のコレクション。

**非推奨のアルゴリズム**  
以前のコンテンツ保護スキーム、具体的には電子コードブック暗号モード (ECB) を実装するモーダル設定。 この SDK では、この設定を使用して、[AD Rights Management サービス SDK](https://msdn.microsoft.com/library/windows/desktop/cc530379.aspx) で使用される MSDRM ライブラリと互換性のあるライセンスを生成できます。

この設定を使用すると、顧客のコンテンツ保護の標準に準拠しない方法で、アプリケーションがコンテンツを保護する可能性があります。

この設定を使用すると、アプリケーションでは Microsoft Rights Management SDK 3.0 以降で追加される暗号化の機能強化のベネフィットを得られなくなります。

**Microsoft 保護されたファイル形式**

PFile 形式とも呼ばれる AD RMS の既定のファイル形式で、RMS 対応アプリケーション全体で標準として機能します。

PFile 形式は Microsoft Rights Management SDK 4.2 の設計方法で埋め込まれているため、アプリケーション開発者が意識することはほとんどありません。

