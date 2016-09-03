---
title: "用語 | Azure RMS"
description: "Rights Management サービスに固有の用語定義のコレクション。"
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: adb1f868-0da7-431b-83d1-86f41c2da4ae
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 024a29d7c7db2e4c0578a95c93e22f8e7a5b173e
ms.openlocfilehash: 5340673beb2a6f2dd4acd96fd599c0b90b9991dd


---

# 利用規約

Rights Management サービスに固有の用語定義のコレクション。

**非推奨のアルゴリズム**  
以前のコンテンツ保護スキーム、具体的には電子クックブック暗号モード (ECB) を参照するものを実装するモーダル設定。 この SDK では、この設定を使用して、[AD Rights Management サービス SDK](https://msdn.microsoft.com/library/windows/desktop/cc530379.aspx) で使用される MSDRM ライブラリと互換性のあるライセンスを生成できます。

この設定を使用すると、顧客のコンテンツ保護の標準に準拠しない方法で、アプリケーションがコンテンツを保護する可能性があります。

この設定を使用すると、アプリケーションは Microsoft Rights Management SDK 3.0 以降で追加される暗号化の機能強化の恩恵を受けられなくなります。

**Microsoft 保護されたファイル形式**

PFile 形式とも呼ばれる AD RMS の既定のファイル形式で、RMS 対応アプリケーション全体で標準として機能します。

PFile 形式は Microsoft Rights Management SDK 4.2 の設計方法で埋め込まれているため、アプリケーション開発者が意識することはほとんどありません。

 

 






<!--HONumber=Aug16_HO4-->


