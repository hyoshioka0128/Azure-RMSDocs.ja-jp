---
title: クライアント | Azure RMS
description: AD RMS クライアント 2.1 は、情報へのアクセスと情報の使用を保護するために設計されたクライアント コンピューター向けのソフトウェアです
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: F7145090-C2EB-405A-A4CF-0240D57A36DA
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev
ms.openlocfilehash: 30a5dd75aece0afbbed67c9e7fb92c4169f0a1a8
ms.sourcegitcommit: d01580c266de1019de5f895d65c4732f2c98456b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "95570254"
---
# <a name="client"></a>Client

このトピックでは、Rights Management Service Client 2.1 の用途と機能について説明します。

RMS クライアント 2.1 は、(オンプレミスでインストールされるか、Microsoft のデータセンターにインストールされているかにかかわらず) RMS を使用するアプリケーション経由でやり取りされる情報のアクセスと使用を保護することを目的として、クライアント コンピューター向けに設計されたソフトウェアです。 このソフトウェアは、個別のダウンロードとして提供されています。使用許諾契約書を確認して承諾することで、サードパーティ製ソフトウェアと一緒に自由に配布できるため、クライアントは環境内の RMS サーバーを使用してデプロイすることで、権利保護されたコンテンツにアクセスできるようになります。

RMS クライアント 2.1 は、ユーザーが保護された (暗号化された) コンテンツを作成、発行、および利用できるようにする機能を公開します。 具体的には、RMS 対応のアプリケーションは、エンドユーザーのコンピューターにインストールされているクライアントを使用して、権限管理のコンテキストでの実行を想定して作成されたタスクを実行します。

Rights Management Service SDK 2.1 は、RMS クライアント 2.1 で動作します。 RMS SDK 2.1 上で構築された権限保護対応アプリケーションは、RMS クライアント 2.1 を使用する必要があります。

詳細については、[RMS クライアント 2.1 に関する TechNet のドキュメント](../rms-client/client-deployment-notes.md)を参照してください。

## <a name="related-topics"></a>関連トピック

* [概要](ad-rms-overview.md)
* [クラウド ベース RMS でのサービス アプリケーション使用の有効化](how-to-use-file-api-with-aadrm-cloud.md)
* [RMS クライアント 2.1 に関する TechNet のドキュメント](../rms-client/client-deployment-notes.md)