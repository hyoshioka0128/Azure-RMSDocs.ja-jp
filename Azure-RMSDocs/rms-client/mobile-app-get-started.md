---
title: はじめに - iOS用および Android 用の AIP アプリ
description: iOS および Android 用の Azure Information Protection アプリを使って電子メールやファイルを表示する
author: rkarlin
ms.author: mlottner
manager: rkarlin
ms.date: 11/30/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 3d5d18d8-7b2e-456c-bb45-48da4eb55544
ms.reviewer: esaggese
ms.suite: ems
ms.custom: user
ms.openlocfilehash: 9da7eaecac3e8eb5bff2e46bf46b3fe77b1f717f
ms.sourcegitcommit: 40693000ce86110e14ffce3b553e42149d6b7dc2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/22/2019
ms.locfileid: "75326262"
---
# <a name="get-started-with-the-microsoft-azure-information-protection-app-for-ios-and-android"></a>iOS 用および Android 用の Microsoft Azure Information Protection アプリの開始

*適用対象: Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

このページの手順を利用する前に、「[iOS 用および Android 用の Microsoft Azure Information Protection アプリに関する FAQ](mobile-app-faq.md)」をお読みください。 そのページでは、アプリの概要、サポートされているデバイス、アプリの使用方法に関する基本情報が説明されています。

保護された電子メールまたはファイルを開く必要がある場合、ほとんどのユーザーは通常、Azure Information Protection アプリを使用します。 ユーザーのアプリをテストするか、必要になる前に単に試用する管理者の場合は、次の手順に従ってください。

> [!NOTE]
> アプリを起動してから、表示するドキュメントや電子メールを選ぶのではなく、 ドキュメントや電子メールを開いてから、このアプリを選び、ドキュメントまたは電子メールを表示します。
>
> 同様に、サインインをうながされるまではアプリにサインインしないでください。

次の手順を使用するには、アプリでサポートされているファイルの 1 つにモバイル デバイスがアクセスできる必要があります。 たとえば次のようになります。

- **.rpmsg ファイル**: モバイル デバイスの電子メール アプリが Rights Management データ保護をネイティブにサポートしていない場合に、電子メール メッセージの添付ファイルとして表示する、権利が保護された電子メール メッセージ。 
    
    別のデバイスを使用して、モバイル デバイスからアクセスできる権利が保護された電子メール メッセージを自分自身に送信します。 たとえば、Windows コンピューターから Outlook を使用します。 Rights management をネイティブでサポートしている電子メールクライアントの一覧については、「 [Azure Rights Management データ保護をサポートするアプリケーション](../requirements-applications.md)」の最初の表の「 **email** 」列を参照してください。

- **権利が保護された pdf ファイル**: Windows コンピューターでは、Azure Information Protection クライアント ([クラシック](client-classify-protect.md)または統一された[ラベル付けクライアント](clientv2-classify-protect.md)) を使用して pdf ファイルを保護し、この権利で保護された pdf ファイルを電子メールの添付ファイルとして送信します。 または、自分の電子メール アドレスを使用し、SharePoint で保護されたライブラリに PDF ファイルをアップロードして共有します。

- **A. ptxt または ptxt または ppng**: Windows コンピューターから Azure Information Protection クライアントを使用してテキストまたはイメージファイルを保護し、この保護されたファイルを電子メールの添付ファイルとして送信します。 テストのために使用できるファイルの種類の全リストについては、Azure Information Protection クライアント管理ガイドの [「分類と保護がサポートされているファイルの種類」](client-admin-guide-file-types.md#supported-file-types-for-classification-and-protection) セクションの最初の表を参照してください。 

これらのファイルを Azure Information Protection ビューアー アプリで表示するには、電子メールの添付ファイルまたはリンクをタップします。 ファイルを開くアプリの選択を求められたら、 **[AIP Viewer]** (AIP ビューアー) アプリを選択します。 職場または学校アカウントでサインインするか、証明書を選択するように求められます。 これらの資格情報が認証されると、Azure Information Protection アプリで電子メールまたはファイルが表示されて読めるようになります。

## <a name="next-steps"></a>次の手順

[FAQ](mobile-app-faq.md) に記載されていない、このアプリに関する質問または意見があれば、[Yammer サイト](https://www.yammer.com/AskIPTeam)にアクセスしてください。
