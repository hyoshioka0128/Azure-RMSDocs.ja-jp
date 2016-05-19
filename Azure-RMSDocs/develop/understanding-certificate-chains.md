---
# required metadata

title: 証明書チェーンについて | Azure RMS
description:
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 14694cb0-adc4-4c2f-aff5-22aa132777df

# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

﻿# 証明書チェーンについて

権限保護対応アプリケーションを開発するには、公開キーのペアと、信頼のルートにある Microsoft の証明書につながる証明書チェーンが必要です。

## 証明書の種類

すべてのライセンスと Rights Management Services (RMS) 環境で使用される証明書は、Microsoft 証明機関 (CA) 証明書につながる証明書のチェーンで構成されます。 Microsoft では、ライセンスまたは証明書を入れ子にできる、運用前証明書チェーンと運用チェーンの 2 つを提供しています。 アプリケーションを開発する際は、Microsoft の *Production License Agreement* にサインインせずに作業できるように、運用前の階層を使用することをお勧めします。 なお、RMS サーバーは運用前の構成に設定する必要もあります。

アプリケーションをリリースする前に、運用チェーンに切り替える必要があります。 運用前証明書で保護されたコンテンツは、運用証明書よりも安全性が低くなります。

公開キーおよび秘密キーと運用前証明書は、`%MsipcSDKDir%\Bin` フォルダー内の次のファイルにある SDK に含まれています。

- **ISVTier5AppSigningPrivKey.dat** には、アプリケーション開発時に使用するマニフェストへの署名で使われる秘密キーが含まれています。
- **ISVTier5AppSigningPubKey.dat** には、運用前証明書の階層で署名する公開キーが含まれています。
- **ISVTier5AppSignSDK_Client.xml** には、アプリケーション開発時に使用するマニフェストの生成で使われる運用前証明書が含まれています。

 

証明書および秘密キーは、アプリケーションのプロセス空間に読み込みが可能なファイル、読み込む必要があるファイル、読み込んではならないファイルを識別するマニフェストの作成と署名に使用されます。 その後、マニフェストはプラットフォームに読み込まれます。

アプリケーションの開発時に運用前証明書を使用したか否かに関係なく、アプリケーションをリリースする準備ができたら、新しいキー ペアを生成して Microsoft の運用証明書を取得し、新しい秘密キーと証明書を使用して、アプリケーション マニフェストを作成し署名する必要があります。

証明書チェーンの使用とアプリケーションの署名の詳細については、「[Switching to the production environment (運用環境への切り替え)](switching-to-the-production-environment.md)」をご覧ください。

### 関連項目

* [開発者の概念](ad-rms-concepts-nav.md)
* [Switching to the production environment (運用環境への切り替え)](switching-to-the-production-environment.md)
 

 


<!--HONumber=Apr16_HO3-->


