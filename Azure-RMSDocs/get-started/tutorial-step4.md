---
title: "Azure RMS のクイック スタート チュートリアル - 手順 4. | Azure RMS"
description: "5 つの手順を実行するだけで 15 分もかからずに組織の Microsoft Azure Rights Management を簡単に試すことができるチュートリアルの 4 番目の手順。"
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 07/13/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: 
ms.assetid: f8340056-87a1-4daa-8b63-3d95fc381b9c
ROBOTS: 
audience: 
ms.devlang: 
ms.reviewer: esaggese
ms.suite: ems
ms.tgt_pltfrm: 
ms.custom: 
translationtype: Human Translation
ms.sourcegitcommit: 67129d6cdac124947fc07aa4d42523686227752e
ms.openlocfilehash: 07c71de207fc7af019dfeea37ca194cf85cc1760


---


# Azure RMS のクイック スタート: 手順 4. 電子メールで送信したドキュメントを開くよう受信者に依頼する

*適用対象: Azure Rights Management、Office 365*


移動: 
> [!div class="op_single_selector"]
- [概要](quick-start-tutorial.md)
- [手順 1. Azure RMS をアクティブ化する](tutorial-step1.md)
- [手順 2. RMS 共有アプリをインストールする](tutorial-step2.md)
- [手順 3. 機密ドキュメントを電子メールで送信する](tutorial-step3.md)
- [手順 4. 受信者がドキュメントを閲覧する](tutorial-step4.md)
- [手順 5. ドキュメントを追跡する](tutorial-step5.md)


![Azure RMS のクイック スタート チュートリアルの手順 4](../media/AzRMS_QuickStartSteps4.PNG)

受信者は、電子メールの添付ファイルとして送信された保護対象のドキュメントを読むために、多くのデバイスを使用できます。 これらのデバイスには、iPad、iPhone、Android タブレットや携帯電話、Mac コンピューター、Windows コンピューターが含まれます。

送信した電子メール メッセージを読むよう受信者に依頼します。 受信者には電子メールのメッセージが表示されますが、その前に次のテキストが表示されます。

**送信者が Microsoft RMS で添付ファイルを保護しました。それらを開くには、**[サインイン](http://aka.ms/rms)
      **する必要があります。**

リンクをクリックすると、手順に移動し、RMS 共有アプリケーションをインストールして、必要に応じて無料アカウントにサインアップするよう指示されます。 無料アカウントでは、受信者に個人用 RMS のサブスクリプションが付与されます。これにより、組織が Azure RMS を所有していない場合でも、承認されたユーザーが、保護されたドキュメントを必ず読むことができます。 受信者は、これから説明する手順を使用して、保護された添付ファイルを読むことができます。

![チュートリアルの手順 4 のスクリーンショット](../media/AzRMS_Tutorial_4_Screenshots.png)

### 保護されたドキュメントの添付ファイルを表示するには

1.  Azure Rights Management により Word 文書が保護されているため、電子メール メッセージには、2 つの添付ファイルがあります。 これらは、実際には 2 つのバージョンの同じファイルですが、ファイル名拡張子は異なります。 ファイル名拡張子 **.ppdf** が付いているバージョン (**Confidential.ppdf**) を開きます。

    デバイスに [Rights Management をサポートしているバージョンの Office](https://technet.microsoft.com/library/dn655136.aspx) がある場合、もう 1 つのバージョンのファイル (**Confidential.docx**) を開くことができます。そのため、このファイルは Word で開きます。

2.  ユーザー名とパスワードの入力を求められたら、電子メールと添付ファイルの送信に使われた電子メール アドレスと同じ形式で自分のユーザー名を入力します。 たとえば、**janetm@contoso.com** や **p.dover@fabrikam.com** です。 パスワードには、個人用 RMS にサインアップするときに指定したパスワードを入力します。 または、組織が Azure RMS を所有している場合は、通常の仕事用のパスワードを入力します。

ドキュメントが開いて、内容を読むことができます。 たとえば、"**電子メールの添付ファイルからこのテキストを読み取ることができた場合には、送信者が Azure RMS で保護したファイルを正常に共有できたことになります。**" のような内容です。 このテキストは、読み取り専用であるため、内容を変更することはできません。

場合によっては、元の電子メールの宛先に含まれていなかった他のユーザーに電子メールを転送するよう、受信者に依頼してみてもよいでしょう。 その他のユーザーが Azure Rights Management を所有する組織で作業していても、または独自に個人用 RMS サブスクリプションを適用していても、添付ファイルを開くことはできません。 これらのユーザーがユーザー名の入力を求められた時点で、ドキュメントへのアクセスが拒否されます。

これで、受信者が添付ファイルを開き、必要に応じて、他のユーザーに転送したので、このアクティビティを報告する電子メール通知を受け取ることができます。 ただし、電子メール メッセージは時間の経過と共に失われやすくなるため、ドキュメントにアクセスしたユーザーを追跡する優れた方法として、ドキュメント追跡サイトを使用できます。ドキュメント追跡サイトについては、最後の手順で説明しています。

|必要な詳細情報|追加情報|
|--------------------------------|--------------------------|
|Azure Rights Management によって保護されたファイルを表示するすべての手順|[Rights Management によって保護されたファイルを表示して使用する](../rms-client/sharing-app-view-use-files.md)|
|無料のサブスクリプション、個人用 RMS について|[個人用 RMS と Azure Rights Management](../understand-explore/rms-for-individuals.md)|
|電子メール メッセージに添付されている 2 つのバージョンのファイルについて|[自動的に作成される .ppdf ファイルとは](../rms-client/sharing-app-dialog-box.md#what-s-the-ppdf-file-that-s-automatically-created)|


>[!div class="step-by-step"]
[« 手順 3](tutorial-step3.md)
[手順 5 »](tutorial-step5.md)


<!--HONumber=Jul16_HO3-->


