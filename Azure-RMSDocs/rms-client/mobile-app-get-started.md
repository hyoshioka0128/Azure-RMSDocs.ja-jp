---
title: "iOS 用および Android 用の Azure Information Protection アプリの開始 | Azure Information Protection"
description: 
keywords: "iOS 用および Android 用の Azure Information Protection アプリで電子メールやファイルを表示する方法"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: azure
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3d5d18d8-7b2e-456c-bb45-48da4eb55544
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 47de236f07996eed3f1ceb51309c6315d4625128
ms.openlocfilehash: 32e0315a8a4e6515b0b89b85afefa1bb17591e0b


---

# <a name="get-started-with-the-microsoft-azure-information-protection-app-for-ios-and-android"></a>iOS 用および Android 用の Microsoft Azure Information Protection アプリの開始

*適用対象: Active Directory Rights Management サービス、Azure Information Protection*

保護された電子メールまたはファイルを開く必要がある場合、ほとんどのユーザーは通常、Azure Information Protection アプリを自動的に使用します。 ユーザーのアプリをテストするか、必要になる前に単に試用する管理者の場合は、次の手順に従ってください。

モバイル デバイスで、アプリがビューアーでの表示をサポートするファイルのいずれかにアクセスする必要があります。 次に例を示します。

- **.rpmsg ファイル**: モバイル デバイスの電子メール アプリが Rights Management データ保護をネイティブにサポートしていない場合に、電子メール メッセージの添付ファイルとして表示する、権利が保護された電子メール メッセージ。 
    
    別のデバイスを使用して、モバイル デバイスからアクセスできる権利が保護された電子メール メッセージを自分自身に送信します。 たとえば、Windows コンピューターから Outlook を使用します。 Rights Management をネイティブにサポートする電子メール クライアントの一覧については、「[Azure Rights Management データ保護をサポートするアプリケーション](../get-started/requirements-applications.md)」ページの「電子メール」列を参照してください。

- **権利が保護された PDF ファイル**: Windows コンピューターから Azure Information Protection クライアントを使用して、[PDF ファイルを保護](client-classify-protect.md)し、この権利が保護された PDF ファイルを電子メールの添付ファイルとして自分自身に送信します。 または、自分の電子メール アドレスを使用し、SharePoint で保護されたライブラリに PDF ファイルをアップロードして共有します。

- **.ptxt、.pjpg、.ppng**: Windows コンピューターから Azure Information Protection クライアントを使用して、テキストまたはイメージ ファイルを保護し、この保護されたファイルを電子メールの添付ファイルとして自分自身に送信します。 テストのために使用できるファイルの種類の全リストについては、Azure Information Protection クライアント管理ガイドの「[保護に対してサポートされるファイルの種類と、そのファイル名拡張子](client-admin-guide-file-types.md#supported-file-types-for-protection-and-their-file-name-extensions)」セクションを参照してください。 

これらのファイルを Azure Information Protection ビューアー アプリで表示するには、電子メールの添付ファイルまたはリンクをタップします。 ファイルを開くアプリの選択を求められたら、**[AIP Viewer]** (AIP ビューアー) アプリを選択します。 職場または学校アカウントでサインインするように求められます。 正常に認証されると、Azure Information Protection アプリで電子メールまたはファイルが表示されて読めるようになります。

## <a name="next-steps"></a>次のステップ

このアプリについてその他の質問がある場合は、「[iOS 用および Android 用の Azure Information Protection アプリに関する FAQ](mobile-app-faq.md)」で解決するかどうかを確認してください。 

その他の質問については、[Yammer サイト](https://www.yammer.com/AskIPTeam) にアクセスするか、または[情報保護チームに電子メールを送信](mailto:askIPteam@microsoft.com?subject=Question%20about%20Azure%20Information%20Protection%20app)してください。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Feb17_HO2-->


