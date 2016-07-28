---
title: "Azure Information Protection クイック スタート チュートリアル手順 1 | Azure Rights Management"
description: "4 つの手順を実行して約 10 分で組織の Microsoft Azure Information Protection を簡単に試すことができる概要チュートリアルの手順 1 です。"
author: cabailey
manager: mbaldwin
ms.date: 07/11/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f6dbb143-96f7-4a9c-8208-be9280d69de9
translationtype: Human Translation
ms.sourcegitcommit: 78f0f07271414fb646f996e7273343f2abf8852b
ms.openlocfilehash: 633b24d0c23cbbee88a2647aaa9defe376ccb40e


---

# 手順 1.Rights Management サービスの有効化
 
*適用対象: Azure Information Protection プレビュー*

> [!NOTE]
>データの分類のみを行い、Azure Rights Management で保護しない場合、またはテナントで Azure Rights Management を既にアクティブ化してある場合は、このまま[次の手順](infoprotect-tutorial-step2.md)に進んでください。 

Azure Rights Management がアクティブ化されていると、分類した後で最も重要なドキュメントやファイルを保護できます。 Azure Rights Management をアクティブ化するには、Office 365 管理センターまたは Azure クラシック ポータルを使用します。

-   Azure Rights Management が含まれている Office 365 サブスクリプションを所有している場合、または所有している Office 365 サブスクリプションに Azure Rights Management が含まれていないものの、Azure RMS Premium 用のサブスクリプションを所有している場合: **Office 365 管理センターを使用します**。

-   Office 365 サブスクリプションを所有していない場合: **Azure クラシック ポータルを使用します**。

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

この時点では、[ **高度な機能**] をクリックしないでください。 クリックすると、Azure クラシック ポータルに移動し、カスタム テンプレートを構成できますが、今回のチュートリアルではその必要はありません。 このため、Office 365 管理センターを閉じてかまいません。

### Azure クラシック ポータルから Rights Management をアクティブ化するには

1.  [Azure クラシック ポータル](http://go.microsoft.com/fwlink/p/?LinkID=275081)に移動して、Azure Active Directory の全体管理者アカウントでサインインします。

2.  左ペインで、[ **ACTIVE DIRECTORY**] をクリックします。

3.  [ **Active Directory** ] ページで、[ **RIGHTS MANAGEMENT**] をクリックします。

4.  [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] で管理するディレクトリを選択し、**[アクティブ化]** をクリックして、操作を確定します。

これで、[ **Rights Management のステータス** ] に [ **アクティブ** ] と表示され、[ **アクティブ化** ] オプションが [ **非アクティブ化**] に置き換えられます。

ポータルでは Rights Management の他のオプションを構成できますが、このチュートリアルではその必要がないため、Azure クラシック ポータルを閉じてかまいません。

これで、この最初の手順に必要な操作は終わりました。 Azure Rights Management サービスがアクティブになったので、後で既定の Azure Rights Management テンプレートのいずれかを選択し、機密として分類されたドキュメントおよび電子メールを保護できます。

運用デプロイメントの場合は、2 つの既定の Azure Rights Management テンプレートに加えて、またはそれらに代えて、カスタム テンプレートの構成が通常は必要です。 ただし、このチュートリアルではカスタム テンプレートは必要ないので、手順 2 に進むことができます。

|必要な詳細情報|追加情報|
|--------------------------------|--------------------------|
|Rights Management のアクティブ化について|[Rights Management をアクティブにする](../deploy-use/activate-service.md)|
|既定のテンプレートの情報と、新しいカスタム テンプレートを作成する方法について|[Azure Rights Management のカスタム テンプレートを構成する](../deploy-use/configure-custom-templates.md)|

>[!div class="step-by-step"]
[&#171; 概要](infoprotect-quick-start-tutorial.md)
[手順 2 &#187;](infoprotect-tutorial-step2.md)



<!--HONumber=Jul16_HO3-->


