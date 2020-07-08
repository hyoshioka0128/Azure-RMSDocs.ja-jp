---
title: はじめに - iOS用および Android 用の AIP アプリ
description: iOS および Android 用の Azure Information Protection アプリを使って電子メールやファイルを表示する
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 07/07/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 3d5d18d8-7b2e-456c-bb45-48da4eb55544
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 4b50f89c9f8d0a965b630c82461f1190bb893938
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86048699"
---
# <a name="get-started-with-the-microsoft-azure-information-protection-app-for-ios-and-android"></a>iOS 用および Android 用の Microsoft Azure Information Protection アプリの開始

*適用対象: Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

このページでは、iOS または Android 用の Azure Information Protection アプリの実行をテストする方法について説明します。

保護された電子メールまたはファイルを開く必要がある場合、ほとんどのユーザーは通常、Azure Information Protection アプリを使用します。 ただし、管理者がユーザーのアプリをテストする場合、または必要なときに単に試してみる場合は、以下の手順に従って、デバイス上の保護されたファイルを表示してください。

> [!IMPORTANT]
> 開始する前に、 [iOS または Android 用の Azure Information Protection アプリ](mobile-app-faq.md)の要件と手順を確認してください。
> 

## <a name="access-a-protected-file-from-your-device"></a>デバイスから保護されたファイルにアクセスする

AIP モバイルアプリをテストするには、次のいずれかの種類の保護されたファイルにデバイスからアクセスできることを確認します。

|ファイルの種類  |Instructions  |
|---------|---------|
|**... メッセージファイル**     | 権利で保護された電子メールメッセージ。 モバイル電子メールアプリが rights management データ保護をネイティブでサポートしていない場合、保護された電子メールメッセージは電子メールの添付ファイルとして表示されます。 </br></br>Windows コンピューターの Outlook などの別のデバイスを使用して、権限で保護された電子メールメッセージを自分宛てに送信し、モバイルデバイスからアクセスできるようにします。 </br></br>**注:** Rights management をネイティブでサポートしている電子メールクライアントの一覧については、「 [RMS 対応 applications](../requirements-applications.md#rms-enlightened-applications)」の「 **email** 」列を参照してください。 |
|**権限で保護された PDF ファイル**     | 1. Windows コンピューターから、AIP[クラシック](client-classify-protect.md)または統合された[ラベル付けクライアント](clientv2-classify-protect.md)クライアントを使用して PDF ファイルを保護します。 </br>2. 保護された PDF を自分で送信するか、SharePoint で保護されたライブラリにアップロードして、自分の電子メールアドレスに共有します。        |
|**. Ptxt または ptxt または ppng**     | 1. Windows コンピューターから、AIP[クラシック](client-classify-protect.md)または統合された[ラベル付けクライアント](clientv2-classify-protect.md)クライアントを使用してテキストまたはイメージファイルを保護します。 </br></br>2. 保護されたファイルを自分で送信するか、SharePoint で保護されたライブラリにアップロードして、自分の電子メールアドレスに共有します。 </br></br>**注:** 詳細については、「[分類と保護のサポートされるファイルの種類](client-admin-guide-file-types.md#supported-file-types-for-classification-and-protection)」を参照してください。   |
| | |

### <a name="open-the-protected-file-on-your-mobile"></a>モバイルで保護されたファイルを開く

1. 電子メールの添付ファイルまたはリンクをタップして、保護されたコンテンツを開きます。

1. メッセージが表示されたら、 **AIP Viewer**アプリを選択して、保護されたコンテンツを表示します。

1. メッセージが表示されたら、職場または学校のアカウントでサインインするか、証明書を選択します。

認証が完了すると、AIP Viewer アプリに電子メールまたはファイルが表示されます。

> [!NOTE]
> 常に、保護されたコンテンツを開いて AIP アプリを開きます。 メッセージが表示されるまで、または AIP Viewer アプリ内から保護されたファイルを開くために、アプリへのサインインを試行しないでください。
> 

## <a name="next-steps"></a>次のステップ

AIP モバイルアプリに関するフィードバックを提供するには、次のいずれかの方法を使用します。

- [**設定**] [  >  **フィードバックの送信**] に移動
- [Yammer サイト](https://www.yammer.com/AskIPTeam)に質問を投稿する