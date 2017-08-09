---
title: "クイック スタート チュートリアルの手順 1 - AIP"
description: "Azure Information Protection を簡単に試すためのチュートリアルの手順 1 - Azure Rights Management サービスの有効化。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
ms.openlocfilehash: 1779eb6f2bcf31ce3515b58b6ed955208fafb237
ms.sourcegitcommit: 55a71f83947e7b178930aaa85a8716e993ffc063
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2017
---
# <a name="step-1-activate-the-rights-management-service"></a>手順 1.Rights Management サービスの有効化
 
>*適用対象: Azure Information Protection*

> [!NOTE]
>テナントの Azure Rights Management サービスを既にアクティブ化していることがわかっている場合は、直接、[次の手順](infoprotect-tutorial-step2.md)に進んでください。 
>
>このサービスがアクティブ化されているかどうかわからない場合は、この手順の指示に従って確認します。

Azure Rights Management サービスをアクティブ化すると、組織の最も機密性の高いドキュメントや電子メールを保護し、保護したドキュメントを他のユーザーと共有する際に使用する方法を追跡することができます。 Windows PowerShell の使用や、管理ポータルの使用など、このサービスをアクティブ化するにはさまざまな方法があります。

このチュートリアルでは、直接、Office 365 管理者向け管理ポータルのアクティブ化ページに移動します。 ただし、このページに直接移動せずに、Office 365 管理ポータルから移動する場合は、「[Rights Management をアクティブにする](../deploy-use/activate-service.md)」の詳しい手順をご覧ください。 Azure Portal にアクセスできるが、Office 365 管理ポータルにはアクセスできない場合にも、これらの詳しい手順を使用します。

## <a name="to-activate-the-rights-management-service"></a>Rights Management サービスをアクティブにするには

1. 新しいブラウザー ウィンドウを開き、Office 365 管理者用の [Rights Management アクティブ化ページ](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx)に直接移動します。
    
    サインインを求められたら、Office 365 のグローバル管理者であるアカウントを使用します。

2. **[RIGHTS MANAGEMENT]** ページで、 **[アクティブ化]**をクリックします。 このボタンに**非アクティブ化**と表示される場合、サービスは既にアクティブ化されています。[次の手順](infoprotect-tutorial-step2.md)に進んでください。 

    ![Azure Information Protection クイック スタート チュートリアル手順 1 - サービスのアクティブ化](../media/info-protect-activate.png)

3. **[Rights Management をアクティブ化しますか?]** というメッセージが表示されたら、**[アクティブ化]** をクリックして確認します。

    " **Rights Management はアクティブ化されています** " というテキストと、非アクティブ化するオプションが表示されます (このページの手動更新が必要になる場合があります)。

    この時点では、[ **高度な機能**] をクリックしないでください。 代わりに、このページを閉じることができます。

これで、このチュートリアルを完了するための最初の手順に必要な操作は終わりました。 これで手順 2 に進むことができます。

|必要な詳細情報|追加情報|
|--------------------------------|--------------------------|
|Rights Management のアクティブ化について|[Azure Rights Management をアクティブにする](../deploy-use/activate-service.md)|


>[!div class="step-by-step"]
[&#171; 概要](infoprotect-quick-start-tutorial.md)
[手順 2 &#187;](infoprotect-tutorial-step2.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
