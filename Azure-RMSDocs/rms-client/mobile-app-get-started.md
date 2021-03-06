---
title: はじめに - iOS用および Android 用の AIP アプリ
description: iOS および Android 用の Azure Information Protection アプリを使って電子メールやファイルを表示する
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 05/01/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 3d5d18d8-7b2e-456c-bb45-48da4eb55544
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 07391252e55f1b75df4d0fb57d167748d6d69853
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "60180943"
---
# <a name="get-started-with-the-microsoft-azure-information-protection-app-for-ios-and-android"></a>iOS 用および Android 用の Microsoft Azure Information Protection アプリの開始

*適用対象:Active Directory Rights Management サービス、[Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

このページの手順を利用する前に、「[iOS 用および Android 用の Microsoft Azure Information Protection アプリに関する FAQ](mobile-app-faq.md)」をお読みください。 そのページでは、アプリの概要、サポートされているデバイス、アプリの使用方法に関する基本情報が説明されています。

保護された電子メールまたはファイルを開く必要がある場合、ほとんどのユーザーは通常、Azure Information Protection アプリを使用します。 ユーザーのアプリをテストするか、必要になる前に単に試用する管理者の場合は、次の手順に従ってください。

> [!NOTE]
> アプリを起動してから、表示するドキュメントや電子メールを選ぶのではなく、 ドキュメントや電子メールを開いてから、このアプリを選び、ドキュメントまたは電子メールを表示します。
>
> 同様に、サインインをうながされるまではアプリにサインインしないでください。

次の手順を使用するには、アプリでサポートされているファイルの 1 つにモバイル デバイスがアクセスできる必要があります。 以下に例を示します。

- **.rpmsg ファイル**:モバイル デバイスの電子メール アプリが Rights Management データ保護をネイティブにサポートしていない場合に、電子メール メッセージの添付ファイルとして表示する、権利が保護された電子メール メッセージ。 
    
    別のデバイスを使用して、モバイル デバイスからアクセスできる権利が保護された電子メール メッセージを自分自身に送信します。 たとえば、Windows コンピューターから Outlook を使用します。 Rights Management をネイティブにサポートする電子メール クライアントの一覧については、「[Azure Rights Management データ保護をサポートするアプリケーション](../requirements-applications.md)」ページの「電子メール」列を参照してください。

- **権利が保護された PDF ファイル**:Windows コンピューターから Azure Information Protection クライアントを使用して、[PDF ファイルを保護](client-classify-protect.md)し、この権利が保護された PDF ファイルを電子メールの添付ファイルとして自分自身に送信します。 または、自分の電子メール アドレスを使用し、SharePoint で保護されたライブラリに PDF ファイルをアップロードして共有します。

- **.ptxt、.pjpg、.ppng**:Windows コンピューターから Azure Information Protection クライアントを使用して、テキストまたは画像ファイルを保護し、この保護されたファイルを電子メールの添付ファイルとして自分自身に送信します。 テストのために使用できるファイルの種類の全リストについては、Azure Information Protection クライアント管理ガイドの [「分類と保護がサポートされているファイルの種類」](client-admin-guide-file-types.md#supported-file-types-for-classification-and-protection) セクションの最初の表を参照してください。 

これらのファイルを Azure Information Protection ビューアー アプリで表示するには、電子メールの添付ファイルまたはリンクをタップします。 ファイルを開くアプリの選択を求められたら、**[AIP Viewer]** (AIP ビューアー) アプリを選択します。 職場または学校アカウントでサインインするか、証明書を選択するように求められます。 これらの資格情報が認証されると、Azure Information Protection アプリで電子メールまたはファイルが表示されて読めるようになります。

## <a name="next-steps"></a>次の手順

[FAQ](mobile-app-faq.md) に記載されていない、このアプリに関する質問または意見があれば、[Yammer サイト](https://www.yammer.com/AskIPTeam)にアクセスしてください。
