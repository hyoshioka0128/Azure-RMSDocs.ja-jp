---
title: "クイック スタート チュートリアル手順 1 | Azure Information Protection"
description: "約 30 分で組織の Microsoft Azure Information Protection を簡単に試すことができる概要チュートリアルの手順 1 です。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
translationtype: Human Translation
ms.sourcegitcommit: 9d8354f2d68f211d349226970fd2f83dd0ce810b
ms.openlocfilehash: edb98a61d247b51319a1eb172f9978e3d64d0e1b


---

# <a name="step-1-activate-the-rights-management-service"></a>手順 1.Rights Management サービスの有効化
 
>*適用対象: Azure Information Protection*

> [!NOTE]
>テナントの Azure Rights Management サービスを既にアクティブ化している場合は、直接、[次の手順](infoprotect-tutorial-step2.md)に進んでください。 

Azure Rights Management サービスをアクティブ化すると、組織の最も機密性の高いドキュメントや電子メールを保護し、他のユーザーと共有する際に使用する方法を追跡することができます。 Windows PowerShell の使用や、管理ポータル間の移動を含め、このサービスをアクティブ化するさまざまな方法があります。

このチュートリアルでは、Office 365 管理者用のアクティブ化ページに直接移動します。このページは、Office 365 クラシック ポータルと Office 365 管理センター プレビューの場合と同じです。 

このページに直接移動せずに、Office 365 管理ポータルから移動する場合は、「[Rights Management をアクティブにする](../deploy-use/activate-service.md)」の詳しい手順を参照してください。 Azure ポータルにアクセスできるが、Office 365 管理ポータルにはアクセスできない場合にも、これらの詳しい手順を使用します。

## <a name="to-activate-the-rights-management-service"></a>Rights Management サービスをアクティブにするには

1. 新しいブラウザー ウィンドウを開き、Office 365 管理者用の [Rights Management アクティブ化ページ](https://account.activedirectory.windowsazure.com/RmsOnline/Manage.aspx)に直接移動します。
    
    サインインを求められたら、Office 365 のグローバル管理者であるアカウントを使用します。

2. **[RIGHTS MANAGEMENT]** ページで、 **[アクティブ化]**をクリックします。

3. **[Rights Management をアクティブ化しますか?]**というメッセージが表示されたら、 **[アクティブ化]**をクリックします。

    " **Rights Management はアクティブ化されています** " というテキストと、非アクティブ化するオプションが表示されます (このページの手動更新が必要になる場合があります)。

    この時点では、[ **高度な機能**] をクリックしないでください。 クリックすると、Azure クラシック ポータルに移動し、カスタム テンプレートを構成できますが、今回のチュートリアルではその必要はありません。 代わりに、このページを閉じることができます。

これで、このチュートリアルを完了するための最初の手順に必要な操作は終わりました。 運用デプロイメントの場合は、2 つの既定の Azure Rights Management テンプレートに加えて、またはそれらに代えて、カスタム テンプレートの構成が通常は必要です。 ただし、このチュートリアルではカスタム テンプレートは必要ないので、手順 2 に進むことができます。

|必要な詳細情報|追加情報|
|--------------------------------|--------------------------|
|Rights Management のアクティブ化について|[Azure Rights Management をアクティブにする](../deploy-use/activate-service.md)|
|既定のテンプレートの情報と、新しいカスタム テンプレートを作成する方法について|[Azure Rights Management サービスのカスタム テンプレートを構成する](../deploy-use/configure-custom-templates.md)|

>[!div class="step-by-step"]
[&#171; 概要](infoprotect-quick-start-tutorial.md)
[手順 2 &#187;](infoprotect-tutorial-step2.md)



<!--HONumber=Nov16_HO2-->


