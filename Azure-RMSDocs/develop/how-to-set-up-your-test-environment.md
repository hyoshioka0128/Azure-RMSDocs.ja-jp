---
title: アプリケーションのテスト | Azure RMS
description: Azure RMS または Windows Server 上で実行されている RMS サーバーを使用して、アプリケーションテストを準備する方法について説明します。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: E480D8D6-F070-43D1-B2B0-6921459C3437
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.custom: dev, has-adal-ref
ms.openlocfilehash: 638a8ec54a850a051795c00b2b1aef4ef47866ff
ms.sourcegitcommit: dc50f9a6c2f66544893278a7fd16dff38eef88c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/18/2020
ms.locfileid: "88564071"
---
# <a name="testing-your-application"></a>アプリケーションのテスト

ここでは、アプリケーションのテストを準備する方法を説明します。

## <a name="instructions"></a>Instructions

Azure RMS または Windows Server で実行される RMS サーバーのいずれかからテストすることができます。  Azure RMS でテストを開始し、RMS Server を使用してテストを行います (展開で必要な場合)。

- Azure RMS でテストする方法については、「[方法: ADAL 認証の使用](how-to-use-adal-authentication.md)」を参照してください。
- RMS サーバーでテストする方法については、「[方法: RMS サーバーをインストールし、構成する](how-to-install-and-configure-an-rms-server.md)」を参照してください。
- 開発者向けランタイムをインストールするには:

   Rights Management Service Client 2.1 がアプリケーションのテストを実行するコンピューターにインストールされている必要があります。
  - 開発コンピューター以外のコンピューターでアプリケーションをテストする場合は、[AD RMS クライアント ダウンロード ページ](https://www.microsoft.com/download/details.aspx?id=38396)からそのコンピューターに RMS クライアント 2.1 をインストールします。
  - 開発用のコンピューターには、既に Rights Management サービス SDK 2.1 がインストールされている必要があります。

    RMS SDK 2.1 のインストールについては、「[SDK のインストール](install-the-rms-sdk.md)」を参照してください。

## <a name="remarks"></a>解説

これは、包括的なガイドではありません。 RMS クライアント 2.1 の構成方法については、「[RMS クライアント 2.1 のデプロイに関する注意事項](https://technet.microsoft.com/library/jj159267(WS.10).aspx)」を参照してください。

## <a name="related-topics"></a>関連トピック

* [RMS サーバーをインストールして構成する方法](how-to-install-and-configure-an-rms-server.md)
* [方法: ADAL 認証を使用する](how-to-use-adal-authentication.md)
* [SDK のインストール](install-the-rms-sdk.md)
* [RMS クライアント 2.1 のデプロイに関する注意事項](https://technet.microsoft.com/library/jj159267(WS.10).aspx)
