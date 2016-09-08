---
title: "Azure RMS のクイック スタート チュートリアル - 手順 1. | Azure RMS"
description: "5 つの手順を実行するだけで 15 分もかからずに組織の Microsoft Azure Rights Management を簡単に試すことができるチュートリアルの最初の手順。"
keywords: 
author: Cabailey
manager: mbaldwin
ms.date: 06/29/2016
ms.topic: get-started-article
ms.prod: 
ms.service: rights-management
ms.assetid: 7c4798e6-34a0-4c3f-a47f-505764ddf322
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: c00264e6c8b99d95e8eedf9b91781484611880c3


---



# Azure RMS のクイック スタート: 手順 1. Rights Management サービスのアクティブ化

>*適用対象: Azure Rights Management、Office 365*


移動: 
> [!div class="op_single_selector"]
- [概要](quick-start-tutorial.md)
- [手順 1. Azure RMS をアクティブ化する](tutorial-step1.md)
- [手順 2. RMS 共有アプリをインストールする](tutorial-step2.md)
- [手順 3. 機密ドキュメントを電子メールで送信する](tutorial-step3.md)
- [手順 4. 受信者がドキュメントを閲覧する](tutorial-step4.md)
- [手順 5. ドキュメントを追跡する](tutorial-step5.md)


![Azure RMS のクイック スタート チュートリアルの手順 1](../media/AzRMS_QuickStartSteps1.PNG)

Azure Rights Management をサポートするサブスクリプションを所有している場合でも、既定はサービスが無効になっています。 アクティブ化するには、Office 365 管理センターまたは Azure クラシック ポータルを使用します。

-   Azure Rights Management が含まれている Office 365 サブスクリプションを所有している場合、または所有している Office 365 サブスクリプションに Azure Rights Management が含まれていないものの、Azure RMS Premium 用のサブスクリプションを所有している場合: **Office 365 管理センターを使用します**。

-   Office 365 サブスクリプションを所有していない場合: **Azure クラシック ポータルを使用します**。

![チュートリアルの手順 1 のスクリーンショット](../media/AzRMS_Tutorial_1_Screenshots.png)

### Office 365 クラシック管理センターから Rights Management をアクティブ化するには

> [!NOTE]
> Office 365 クラシック管理センターではなく **Office 365 管理センター プレビュー**を使用している場合、「[Office 365 管理センター プレビューから Azure Rights Management をアクティブ化する方法](../deploy-use/activate-office365-preview.md)」の指示に従うか、この指示を使用するためにクラシック バージョンに切り替えます。 切り替えを行うには、サインインした後に、[**ホーム**] ページの [**古い管理センターに移動**] をクリックします。

1.  [Office 365 ポータル](https://portal.office.com/) に移動して、Office 365 の全体管理者アカウントでサインインします。

2.  Office 365 管理センターが自動的に表示されない場合は、左上のアプリ ランチャー アイコンを選択し、**[管理]** を選択します。 [ **管理** ] タイルは、Office 365 管理者に対してのみ表示されます。

    > [!TIP]
    > 管理センターのヘルプについては、「 [Office 365 管理センターについて - 管理者向けヘルプ](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547)」を参照してください。

3.  左ペインで、 **[サービス設定]**を展開します。

4.  [ **Rights Management**] をクリックします。

5.  [ **RIGHTS MANAGEMENT** ] ページで、[ **管理**] をクリックします。

6.  **[RIGHTS MANAGEMENT]** ページで、 **[アクティブ化]**をクリックします。

7.  **[Rights Management をアクティブ化しますか?]**というメッセージが表示されたら、 **[アクティブ化]**をクリックします。

" **Rights Management はアクティブ化されています** " というテキストと、非アクティブ化するオプションが表示されます (このページの手動更新が必要になる場合があります)。

この時点では、[**高度な機能**] をクリックしないでください。 クリックすると、Azure クラシック ポータルに移動し、テンプレートを構成できますが、今回のチュートリアルではその必要はありません。 このため、Office 365 管理センターを閉じてかまいません。

### Azure クラシック ポータルから Rights Management をアクティブ化するには

1.  [Azure クラシック ポータル](http://go.microsoft.com/fwlink/p/?LinkID=275081)に移動して、Azure Active Directory の全体管理者アカウントでサインインします。

2.  左ペインで、[ **ACTIVE DIRECTORY**] をクリックします。

3.  [ **Active Directory** ] ページで、[ **RIGHTS MANAGEMENT**] をクリックします。

4.  [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] で管理するディレクトリを選択し、**[アクティブ化]** をクリックして、操作を確定します。

これで、[ **Rights Management のステータス** ] に [ **アクティブ** ] と表示され、[ **アクティブ化** ] オプションが [ **非アクティブ化**] に置き換えられます。

ポータルでは Rights Management の他のオプションを構成できますが、このチュートリアルではその必要がないため、Azure クラシック ポータルを閉じてかまいません。

これで、この最初の手順に必要な操作は終わりました。 サービスがアクティブ化されたので、組織内のすべてのユーザーは、機密性の高い重要なドキュメントを保護できるようになりました。 運用環境では、初めのうちはこの機能を実行できるユーザーを制限しておき、段階的にロールアウトしていくこともできます。 ただし、このチュートリアルではその必要はありません。

このチュートリアルでは扱いませんが、運用環境のデプロイでは、カスタム テンプレートを構成することもできます。 テンプレートを使用すると、ファイルの保護が必要なときに、適切な設定をより簡単かつすばやく適用できるようになります。 Rights Management をアクティブ化すると、2 つの既定のテンプレートを自動的に取得します。独自のカスタム テンプレートを使えば、運用環境で既定のテンプレートを補完することができます。 ただ、このチュートリアルにはテンプレートは必要ありませんので、次の手順に進みます。

|必要な詳細情報|追加情報|
|--------------------------------|--------------------------|
|Rights Management をアクティブ化する方法と、サービスがアクティブ化された際にファイルの保護や電子メールの送信が可能なユーザーを制御する方法について|[Rights Management をアクティブにする](../deploy-use/activate-service.md)|
|既定のテンプレートの情報と、新しいカスタム テンプレートを作成する方法について|[Azure Rights Management のカスタム テンプレートを構成する](../deploy-use/configure-custom-templates.md)|


>[!div class="step-by-step"]
[« 概要](quick-start-tutorial.md)
[手順 2 »](tutorial-step2.md)


<!--HONumber=Aug16_HO4-->


